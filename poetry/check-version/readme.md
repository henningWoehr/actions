# poetry/check-version
This action compares the current project version with the latest tag of the repository. Fails if the project version isn't newer than the newest tag.

## Action Inputs
| Input name | Description | Required | Default Value |
| --- | --- | --- | --- |
| token | Github token to make authed request to GH API | true | None |

## Action Outputs
| Output name | Description |
| --- | --- |
| - | - |

## Example
This example will compare your project version with the newest tag.

#### Notes
- No code checkout is needed

```yml
name: Check Version

on:
  pull_request:
    branches:
      - master

  workflow_dispatch:

jobs:
  check_version:
    runs-on: ubuntu-latest
    steps:
      - name: Check Version
        uses: henningwoehr/actions/poetry/check-version@main
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
```