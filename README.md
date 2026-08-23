# BTI Bioinformatics Docs

[![Deploy Website](https://github.com/childrens-bti/bti-bfx-docs/actions/workflows/deploy.yaml/badge.svg)](https://github.com/childrens-bti/bti-bfx-docs/actions/workflows/deploy.yaml)
[![Build PR Preview](https://github.com/childrens-bti/bti-bfx-docs/actions/workflows/preview.yaml/badge.svg)](https://github.com/childrens-bti/bti-bfx-docs/actions/workflows/preview.yaml)

Documentation for the **Rokita Lab and BTI Bioinformatics Core** at Children's National Hospital — onboarding, compute access (AWS, CAVATICA, HPC), GitHub workflow guidelines, and general lab practices.

📖 **Live site:** https://childrens-bti.github.io/bti-bfx-docs/

## What's here

Built with [MkDocs](https://www.mkdocs.org/). Pages live under [`docs/`](docs/) and the site navigation is defined in [`mkdocs.yml`](mkdocs.yml). Topics include:

- Onboarding and technology access requests
- AWS and CAVATICA compute usage
- GitHub repository, PR, and code review guidelines
- Project management and sprint planning
- Lab literature and general resources

## Local development

```bash
pip install mkdocs mkdocs-material
mkdocs serve
```

Then open http://127.0.0.1:8000 to preview the site with live reload.

To build the static site into `site/`:

```bash
mkdocs build --clean
```

## Contributing a page

1. Add a new Markdown file under [`docs/`](docs/).
2. Add it to the `nav` section of [`mkdocs.yml`](mkdocs.yml) so it appears in the site sidebar.
3. Open a pull request — a preview build is automatically posted as a comment on the PR (see [`preview.yaml`](.github/workflows/preview.yaml)).
4. Once merged to `main`, the site is automatically rebuilt and deployed to GitHub Pages (see [`deploy.yaml`](.github/workflows/deploy.yaml)).

To file an issue or suggest a change, use the [issue tracker](https://github.com/childrens-bti/bti-bfx-docs/issues).
