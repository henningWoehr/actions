# poetry-run-tests
GitHub Action for Python projects using poetry

## Getting started

### Description
With this action you can easily test your code using poetry and pytest with the right dependencies based of the pyproject.toml

### Create your workflow
```yaml
name: Install poetry
on: pull_request

jobs:
  install-poetry:
    runs-on: ${{ matrix.os }}
    steps:
      - uses: actions/checkout@v2

      - name: Test code
        id: test-code
        uses: henningwoehr/actions/poetry-run-tests@main
        with:
            python-version: "3.10"      # optional (default: 3.10)
            poetry-version: "1.1.14"    # optional (default: 1.1.14)

      - name: Project Version
        run: echo ${{ steps.test-code.outputs.project-version }}
```