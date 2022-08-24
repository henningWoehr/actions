# poetry/lint-flake8
GitHub Action for python projects using poetry

## Description
With this action you can easily lint your code using poetry and pytest.

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
name: Lint code

on:
  pull_request:
    branches: 
      - master

jobs:
  lint_flake8:
    runs-on: ubuntu-latest

    steps:
      - name: Test code
        uses: henningwoehr/actions/poetry/lint-flake8@main
```