# setup-poetry
GitHub Actions for Python projects using poetry

## Getting started

### Breaking changes for v2
With this action you can easily install 

### Create your workflow
```yaml
name: Install poetry
on: pull_request

jobs:
  install-poetry:
    runs-on: ${{ matrix.os }}
    steps:
      - uses: actions/checkout@v2

      - name: Setup poetry
          id: setup-poetry
          uses: henningwoehr/actions/setup-poetry@main
          with:
            python-version: "3.10"      # optional (default: 3.10)
            poetry-version: "1.1.14"    # optional (default: 1.1.14)

      - name: Project Version
        run: echo ${{ steps.setup-poetry.outputs.project-version }}

      - name: View poetry --help
        run: poetry --help
```