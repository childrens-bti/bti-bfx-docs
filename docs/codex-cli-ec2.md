# Running Codex CLI on an Ubuntu EC2 Instance

This guide explains how to authenticate and run Codex CLI on a headless Ubuntu
EC2 instance. The instance does not need a browser: the browser on your local
computer completes the Microsoft sign-in through an SSH port-forwarding tunnel.

This guide extends the [CNH Codex CLI setup guide](https://aiml-apim-dev.azure-api.net/developer-docs/code-assistants/codex-cli-setup/).
Follow that guide for the supported-user requirements, Codex installation, the
`cnh-token.py` authentication script, and the Azure/APIM configuration. The
steps below address the EC2-specific authentication flow.

## Prerequisites

- Codex CLI is installed on the EC2 instance.
- Python 3.12 or later is available on the instance.
- The `cnh-token.py` script has been downloaded from the CNH setup guide.
- You can connect to the instance over SSH from your local computer.
- You are in an approved user group for the CNH coding-assistant endpoint.

## 1. Create a Python virtual environment

Ubuntu may prevent packages from being installed into its system Python
environment because of [PEP 668](https://peps.python.org/pep-0668/). Install the
authentication dependencies in an isolated virtual environment instead.

On the EC2 instance:

```bash
# Install Python 3.12 and venv support if needed.
sudo apt-get update
sudo apt-get install -y python3.12 python3.12-venv

# Create the virtual environment inside ~/.codex.
python3.12 -m venv ~/.codex/venv

# Install the authentication dependencies into the virtual environment.
~/.codex/venv/bin/python -m pip install --upgrade pip
~/.codex/venv/bin/python -m pip install msal msal-extensions

# Verify the dependencies.
~/.codex/venv/bin/python -c "import msal, msal_extensions; print('ok')"
```

Save `cnh-token.py` to `~/.codex/cnh-token.py`, or use another location and
update the path in `~/.codex/config.toml`. The authentication command must use
the virtual environment's Python:

```toml
[model_providers.azure.auth]
command = "/home/<user>/.codex/venv/bin/python"
args = ["/home/<user>/.codex/cnh-token.py"]
timeout_ms = 120000
```

Replace `<user>` with the EC2 instance user, such as `ubuntu` or `ec2-user`.

## 2. Start authentication on the EC2 instance

Open a terminal connected to the EC2 instance and run:

```bash
~/.codex/venv/bin/python ~/.codex/cnh-token.py
```

On a headless instance, the script reports that no browser was found, publishes
a randomly assigned callback port, prints an `Auth URI`, and waits for the
sign-in callback. Leave this command running.

The easiest way to find the port is the script's published-port message. The
output will look similar to this, where `<PORT>` is different for each
authentication attempt:

```text
Found no browser in current environment. ... published port <PORT> to host network ...
Auth URI: https://login.microsoftonline.com/...&redirect_uri=http%3A%2F%2Flocalhost%3A<PORT>&...
```

Use the number shown after `published port` as the value of `PORT` in the SSH
command below. The `redirect_uri` in the current `Auth URI` should contain the
same number and provides a confirmation:

```text
redirect_uri=http%3A%2F%2Flocalhost%3A<PORT>
```

Use the complete `Auth URI` from the current run. Do not reuse a port, `state`,
or `code_challenge` from an earlier attempt.

## 3. Forward the current callback port over SSH

Open a second terminal on your local computer. The command below prompts for
the port shown in the current authentication attempt's published-port message,
then forwards that same port to the EC2 instance:

```bash
printf 'Port published by the current auth run: '
read -r PORT
ssh -N -o ExitOnForwardFailure=yes \
  -L "${PORT}:127.0.0.1:${PORT}" \
  <user>@<ec2-host>
```

Replace `<user>@<ec2-host>` with your SSH destination. Do not replace `PORT`
with a port from a previous run. The `-L` option maps the local port to the
same callback port on the EC2 instance, and `-N` keeps this terminal dedicated
to forwarding. Leave the SSH command running.

If you use an SSH host alias, substitute that alias for `<user>@<ec2-host>`.

## 4. Sign in from your local browser

1. Copy the entire `Auth URI` printed in the EC2 terminal.
2. Paste it into a browser on your local computer and sign in with your
   Microsoft credentials.
3. The browser redirects to `http://localhost:<PORT>/?code=...`. The SSH tunnel
   sends that callback to the authentication script on the EC2 instance.
4. Wait for the script to exchange the code, cache the token on the instance,
   and exit successfully.

If the browser cannot connect to `localhost:<PORT>`, verify that the SSH
tunnel is still running and that its port came from the current `Auth URI`. If
you restart `cnh-token.py`, it may select a new port; use the new URI and
create the tunnel again with that new port.

After the authentication script exits, the tunnel terminal can be closed.

## 5. Run Codex CLI

Back on the EC2 instance, change to the project directory and start Codex:

```bash
cd /path/to/your/project
codex
```

The first time Codex runs in a directory, it asks whether you trust the
directory contents. Select **1. Yes, continue** for a directory you own.

Consider running Codex inside `tmux` or `screen` so it continues running after
an SSH disconnect:

```bash
tmux new -s codex
cd /path/to/your/project
codex
```

## Future authentication

`msal-extensions` caches the token on the EC2 instance. Future Codex launches
can reuse or refresh it without opening a browser or creating an SSH tunnel.
Repeat the authentication steps if the refresh token expires or is revoked, or
if the token cache is removed when the instance is rebuilt.

Persist `~/.codex` on storage that survives instance replacement if you want to
retain the configuration and token cache. Treat the cache as sensitive and do
not commit it to a repository.

## Known endpoint compatibility issue

On the CNH APIM endpoint, newer Codex CLI versions may fail with `gpt-5.6-*`
models and report an error like:

```text
Invalid 'input[0].tools[0].description': empty string ...
```

If this occurs on every prompt, install the compatible CLI version reported by
the current CNH setup instructions:

```bash
npm install -g @openai/codex@0.146
codex --version
```

Restart Codex after changing the CLI version. If rolling back is not possible,
use `gpt-5.5-aiml` in the top-level `model` setting and in any profile that you
use in `~/.codex/config.toml`:

```toml
model = "gpt-5.5-aiml"
```

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| `error: externally-managed-environment` | Packages are being installed into system Python. | Use the virtual environment; do not use `--break-system-packages`. |
| The script says no browser was found and waits | The EC2 instance is headless and is waiting for the callback. | Leave it running, read the published port, start the SSH tunnel, and complete sign-in. |
| The browser cannot reach `localhost:<PORT>` | The tunnel is not running or uses a stale/wrong port. | Use the port from the current published-port message, verify it against the `Auth URI`, and start the tunnel again. |
| Codex appears frozen on launch | The authentication command is waiting for the browser callback. | Complete the sign-in flow or inspect the authentication terminal for errors. |
| `tools[0].description: empty string` appears on every prompt | The CLI and `gpt-5.6-*` model are incompatible with this endpoint. | Install `@openai/codex@0.146` or use `gpt-5.5-aiml`. |
| Codex cannot find `msal` at authentication time | The auth command points to a different Python installation. | Set `command` to the full path `~/.codex/venv/bin/python`. |

Verify the authentication interpreter at any time:

```bash
~/.codex/venv/bin/python -c "import msal, msal_extensions; print('ok')"
```
