# poetry/run-pytest
GitHub Action for python projects using poetry

## Description
With this action you can easily test your code using poetry and pytest with the right dependencies based of the pyproject.toml

## Action Inputs
| Input name | Description | Required | Default Value |
| --- | --- | --- | --- |
| python-version | Version of python to install | false | "3.10" |
| poetry-version | Version of poetry to install | false | "1.1.14" |

## Action Outputs
| Output name | Description |
| --- | --- |
| project-version | Current project version of pyproject.toml |

## Example

#### Notes
- No code checkout is needed

```yml
name: Test code

on:
  pull_request:
    branches: 
      - master

jobs:
  run_tests_poetry:
    runs-on: ubuntu-20.04

    steps:
      - name: Test code
        id: test-code
        uses: henningwoehr/actions/poetry/run-pytest@main
        with:
          python-version: "3.10"
          poetry-version: "1.1.14"

      - name: Project Version
        run: echo ${{ steps.setup-poetry.outputs.project-version }}
```