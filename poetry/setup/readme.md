# poetry/setup
GitHub Action for python projects using poetry

## Description
With this action you can easily install python, poetry and optionally the dependencies for the project

## Action Inputs
| Input name | Description | Required | Default Value |
| --- | --- | --- | --- |
| python-version | Version of python to install | false | "3.10" |
| poetry-version | Version of poetry to install | false | "1.1.14" |
| install-dependencies | Install project dependencies | false | false |

## Action Outputs
| Output name | Description |
| --- | --- |
| project-version | Current project version of pyproject.toml |

## Example

```yaml
name: Install poetry

on:
  pull_request:
    branches: 
      - master

jobs:
  install-poetry:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Setup poetry
          id: setup-poetry
          uses: henningwoehr/actions/setup-poetry@main
          with:
            python-version: "3.10"
            poetry-version: "1.1.14"
            install-dependencies: true

      - name: Project Version
        run: echo ${{ steps.setup-poetry.outputs.project-version }}

      - name: View poetry --help
        run: poetry --help
```