---
icon: material/file-document-multiple-outline
---

# How to update documentation

This site is built with [Zensical](https://zensical.org), the Material for MkDocs team's successor to MkDocs. It reads the same `mkdocs.yml` configuration and Markdown content that MkDocs does, so nothing about writing pages changes - only the build tool.

To update, please submit a PR to [GitHub](https://github.com/childrens-bti/bti-bfx-docs).

---

## Commands (automated through GitHub Actions)

* `pip install zensical` - Install the Zensical CLI.
* `zensical serve` - Start the live-reloading docs server.
* `zensical build` - Build the documentation site.
* `zensical --help` - Print help message and exit.

!!! note
    `zensical` replaces `mkdocs` on the command line, but does not support `mkdocs gh-deploy`. The [deploy workflow](https://github.com/childrens-bti/bti-bfx-docs/blob/main/.github/workflows/deploy.yaml) instead runs `zensical build` followed by `ghp-import` directly to publish to `gh-pages`.

---

## Project layout

    mkdocs.yml    # The configuration file, read by Zensical.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.
