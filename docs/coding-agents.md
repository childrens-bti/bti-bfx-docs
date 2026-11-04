---
icon: material/robot-outline
---

# Coding Agents

---

## What Data Can Go Into AI Tools

We have access to three AI tools, and they have different rules about which data you can use with them.

<div class="ai-data-rules" markdown>

| | Children's National Codex | Children's National Microsoft Copilot | Rokita Lab Claude Team |
|---|---|---|---|
| HIPAA-compliant | Yes, **only** with Children's National SSO login | Yes, **only** with Children's National SSO login | **No** |
| Sign in with | Children's National SSO login | Children's National SSO login | Children's National email address only |
| Protected health information (PHI) | Yes | Yes | **No** |
| Germline variant data | Yes | Yes | Only pathogenic/likely pathogenic (P/LP) variants that we would release with a manuscript |
| Raw data files (e.g., FASTQ, BAM/CRAM, germline VCF) | Do not upload; use Codex to write code that runs on the files in AWS, the HPC, or CAVATICA | **No**; do not upload. Raw files stay in AWS, the HPC, or CAVATICA | **No** (except creating MD5 checksums); have Claude write code that you run yourself |
| Code, de-identified summary data, documentation | Yes | Yes | Yes |

</div>

!!! danger "Codex and Copilot are only HIPAA-compliant when you sign in with your Children's National SSO login"
    The "Yes" answers in the Codex and Copilot columns apply **only** when you sign in with your Children's National single sign-on (SSO) account.
    Codex or Copilot used with a personal account, or without signing in, is **not** HIPAA-compliant; never enter PHI or germline variant data there.
    See [Running Codex Locally](#running-codex-locally) and [Children's National Microsoft Copilot](#childrens-national-microsoft-copilot) for how to sign in correctly.

!!! warning "When in doubt, use Codex"
    The Rokita Lab Claude Team is not approved for PHI, full germline variant data, or raw files.
    If your work touches any of these, use Children's National Codex, which the Children's National AI/ML team maintains for this purpose. See [Running Codex Locally](#running-codex-locally) or [Running Codex CLI on an Ubuntu EC2 Instance](#running-codex-cli-on-an-ubuntu-ec2-instance) for setup.

!!! note "Raw data stays in secure environments"
    Raw data files should only be stored and processed in our secure environments: [AWS](aws.md) (a HIPAA-compliant environment), the [HPC](access.md#high-performance-cluster-hpc), or [CAVATICA](cavatica.md).
    Do not upload raw files to any AI tool.
    Instead, ask the coding agent to write code (for example, a script or workflow), and then run that code on the raw files in one of these environments.

!!! tip "Run bulk deletes yourself"
    Coding agents may refuse, or ask for confirmation, before running bulk cloud deletes such as `aws s3 rm --recursive`.
    Expect to review and run these commands yourself.

---

## Using Claude Code

The Rokita Lab Claude Team includes Claude Code, which can be run from the terminal or through the VS Code extension.
The steps below cover installation; see the [Claude Code documentation](https://code.claude.com/docs/en/overview) for everything else.

- Sign in with your Children's National email address. Do not use a personal Claude account.
- You must be added to the lab's Claude Team access group before you can sign in. Contact Jo Lynne Rokita to request access.
- Follow the data rules in [What Data Can Go Into AI Tools](#what-data-can-go-into-ai-tools).

!!! danger "Do not let Claude work on raw data files"
    Claude must not read or process raw data files, such as CRAM, BAM, FASTQ, or germline VCF files.
    Somatic VCF files are OK, since we release them openly.
    The only exception is creating MD5 checksums (`md5sum`).
    This also applies when Claude Code runs on an EC2 instance or the HPC, where it can open files directly.
    Instead, ask Claude to write the code, and then run that code yourself outside of Claude.

### Installing Claude Code (Local or EC2)

The installation steps are the same on your local Mac and on an Ubuntu EC2 instance.
Node.js is not required.

```bash
# Install Claude Code (macOS or Linux)
curl -fsSL https://claude.ai/install.sh | bash

# Check the installation
claude --version
```

On a Mac, you can install with Homebrew instead (`brew install --cask claude-code`), but Homebrew installs do not update automatically.
Run `brew upgrade claude-code` to update.

To start Claude Code, change to your project directory and run `claude`:

```bash
cd /path/to/your/project
claude
```

The first time you run `claude`, it asks you to sign in through your browser.
Sign in with your Children's National email address.
On an EC2 instance with no browser, Claude Code prints a sign-in link instead. Open the link in the browser on your local computer, sign in, then copy the code it shows and paste it back into the Claude Code prompt on the instance.
To switch accounts later, type `/login` in a Claude Code session.

Run `claude doctor` if the installation is not working.

### VS Code Extension

Install the [Claude Code extension](https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code) from the VS Code Marketplace, or search for "Claude Code" in the Extensions view (`Cmd+Shift+X`).
To open it, open the Command Palette (`Cmd+Shift+P`), type "Claude Code", and select **Open in New Tab**.
If you use VS Code Remote-SSH to work on an EC2 instance, install the extension on the remote host when VS Code asks.

---

## Children's National Microsoft Copilot

Full-time staff can request a Microsoft 365 Copilot license by submitting a ServiceNow ticket.
Once you have a license, open Copilot from Outlook in your web browser.

!!! danger "Use only the Children's National SSO version"
    Only Children's National Copilot opened with your Children's National SSO login is HIPAA-compliant.
    Before entering PHI or germline variant data, check that you are signed in with your Children's National email address.
    Copilot with a personal Microsoft account, or without signing in, is not HIPAA-compliant.

---

## Running Codex Locally

The AI/ML team at Children's National maintains internal coding agents for our use. 
Follow the guide at [Children's National Codex CLI setup guide](https://aiml-apim-dev.azure-api.net/developer-docs/code-assistants/codex-cli-setup/) for the supported-user requirements, Codex installation, the `cnh-token.py` authentication script, and the Azure/APIM configuration. 

### Prerequisites

- Codex CLI version 0.146.0 is installed on your computer. (version 0.147 does not work with our Azure models.)
- Python 3.12 or later.
- The `cnh-token.py` script has been downloaded from the Children's National setup guide.
- You are in an approved user group for the Children's National coding-assistant endpoint.
- Optional: VS Code Codex extension

```bash
# Make yourself an admin and install the codex CLI
brew install node
brew install nvm
npm install -g @openai/codex@0.146.0
```

---

## Running Codex CLI on an Ubuntu EC2 Instance

This guide explains how to authenticate and run Codex CLI on a headless Ubuntu EC2 instance. 
The instance does not need a browser: the browser on your local computer completes the Microsoft sign-in through an SSH port-forwarding tunnel.
The steps below address the EC2-specific authentication flow.


### Prerequisites

- Codex CLI version 0.146.0 is installed on the EC2 instance. (version 0.147 does not work with our Azure models.)
- Python 3.12 or later is available on the instance.
- The `cnh-token.py` script has been downloaded from the Children's National setup guide.
- You can connect to the instance over SSH from your local computer.
- You are in an approved user group for the Children's National coding-assistant endpoint.

### Steps

#### 1. Create a Python virtual environment

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

#### 2. Start authentication on the EC2 instance

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

#### 3. Forward the current callback port over SSH

Open a second terminal on your local computer. Fill in the port number shown in the current authentication attempt's published-port message. Then ssh forwards that same port to the EC2 instance. `<user>@<ec2-host>` is your host name for the ssh profile that you set up for your EC2 instance e.g. `ubuntu@bti-ec2`

```bash
ssh -N -o ExitOnForwardFailure=yes \
  -L "${PORT}:127.0.0.1:${PORT}" \
  <user>@<ec2-host>
```

Do not replace `PORT` with a port from a previous run. The `-L` option maps the local port to the same callback port on the EC2 instance, and `-N` keeps this terminal dedicated to forwarding. Leave the SSH command running.

If you use an SSH host alias, substitute that alias for `<user>@<ec2-host>`.

#### 4. Sign in from your local browser

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

#### 5. Run Codex CLI

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

### Future authentication

`msal-extensions` caches the token on the EC2 instance. Future Codex launches
can reuse or refresh it without opening a browser or creating an SSH tunnel.
Repeat the authentication steps if the refresh token expires or is revoked, or
if the token cache is removed when the instance is rebuilt.

Persist `~/.codex` on storage that survives instance replacement if you want to
retain the configuration and token cache. Treat the cache as sensitive and do
not commit it to a repository.

### Known endpoint compatibility issue

!!! warning
    On the Children's National APIM endpoint, newer Codex CLI version 0.147 may fail with `gpt-5.6-*`
    models and report an error like:

    ```text
    Invalid 'input[0].tools[0].description': empty string ...
    ```

    This appears to be fixed in version 0.148.

If this occurs on every prompt, upgrade your codex to the latest version:

```bash
sudo npm install -g @openai/codex
codex --version
```

Restart Codex after changing the CLI version. If rolling back is not possible,
use `gpt-5.5-aiml` in the top-level `model` setting and in any profile that you
use in `~/.codex/config.toml`:

```toml
model = "gpt-5.5-aiml"
```

### Troubleshooting

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