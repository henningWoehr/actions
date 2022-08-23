# linux-gnu-x64
GitHub Action for Python projects using poetry

## Getting started

### Description
With this action you can easily build an executable for linux(gnu) with pyoxidizer.
The used ubuntu version is important, because on newer ubuntu versions (22.04) a newer GNU lib is used. This can cause a problem, if the app is run on an older linux system.

Per default, a standard pyoxidizer config file (pyoxidizer.bzl) is used. To use an own config, the config has to be inside the project folder and the input 'use-own-pyoxidizer-config' has to be on 'true'.

### Create your workflow
```yaml
name: Build linux executable
on: pull_request

env:
  ARTIFACT_NAME: built_files

jobs:
  install-poetry:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2

      - name: Build linux_gnu_x64 app
          uses: henningwoehr/actions/pyoxidizer-build/linux-gnu-x64@main
          with:
            app-name: encryptioncli                                     # required
            run-command: "from encryptioncli.main import main; main()"  # required
            artifact-name: ${{ env.ARTIFACT_NAME }}                     # requried
            use-own-pyoxidizer-config: false                            # optional (default: false)

      - name: Download built file
        uses: actions/download-artifact@v2
        with:
          name: ${{ env.ARTIFACT_NAME }}
          path: built_files

      - run: ls built_files
```