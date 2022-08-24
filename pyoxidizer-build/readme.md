# pyoxidizer-build
This action will use a python poetry project and build executables/installer for either linux, windows or mac

## Action Inputs
| Input name | Description | Required | Default Value |
| --- | --- | --- | --- |
| target-system | Select one of the following system to build on: [linux_gnu_x64, windows_x32, windows_x64, macos_x64] | true | None |
| app-name | The name of the app. This name can later be used in the command line to call the app | true | None |
| run-command | The command to run at the start of the app. (eg. \"from package/main import main; main()\" | true | None |
| display-name | The name, which appears in the name of the msi-installer and in the program files folder | true | None |
| app-author | The name of the author or the manufacturer, which is displayed when installing the app per msi-installer | true | None |
| artifact-name | Name of the artifact, where the built file should be uploaded | true | None |
| use-own-pyoxidizer-config | Use own pyoxidizer.bzl, given in the project folder if true, otherwise use standard config provided by this action | false | false |

## Action Outputs
| Output name | Description                                   |
|-------------|-----------------------------------------------|
| -           | The identifier of the created release.        |
## Examples
### Linux GNU x64
This example will build an executable for linux (gnu) and download it via the artifact-name.
Important: If the linux executable is build on ubuntu-22.04, the executable can't be used on lower ubuntu versions. Therefore, to be most compatible, you have to use ubuntu-20.04.

```yml
name: Build Linux GNU x64

on: 
  push:
    tags:
    - '*'

jobs:

  build:
    runs-on: ubuntu-20.04
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v2
    
    - name: build executable
      uses: henningwoehr/actions/pyoxidizer-build@main
      with:
        target-system: linux_gnu_x64
        app-name: example_app
        run-command: "from package.main import main; main()"
        artifact-name: example_artifact
        display-name: "Example App"
        app-author: "Your Name"

  download_files:
    runs-on: ubuntu-latest
    needs: build

    steps:
      - name: Download files
        uses: actions/download-artifact@v2
        with:
          name: example_artifact
          path: built_files

      - name: List files
        run: ls built_files

```

#### Notes
- You must provide a tag either via the action input or the git ref (i.e push / create a tag). If you do not provide a tag the action will fail.
- If the tag of the release you are creating does not yet exist, you should set both the `tag` and `commit` action inputs. `commit` can point to a commit hash or a branch name (ex - `main`).
- In the example above only required permissions for the action specified (which is `contents: write`). If you add other actions to the same workflow you should expand `permissions` block accordingly.