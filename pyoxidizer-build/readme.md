# pyoxidizer-build
This action will use a python poetry project and build executables/installer for either linux, windows or mac

## Action Inputs
| Input name                 |                   Description                                                                               	                                                                                                                                       | Required 	 | Default Value        |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|----------------------|
| allowUpdates               | An optional flag which indicates if we should update a release if it already exists. Defaults to false.                                                                                                                                             | false      | ""                   |
| artifactErrorsFailBuild    | An optional flag which indicates if artifact read or upload errors should fail the build.                                                                                                                                                           | false      | ""                   |
| artifacts                  | An optional set of paths representing artifacts to upload to the release. This may be a single path or a comma delimited list of paths (or globs)                                                                                                   | false      | ""                   |
| artifactContentType        | The content type of the artifact. Defaults to raw                                                                                                                                                                                                   | false      | ""                   |
| body                       | An optional body for the release.                                                                                                                                                                                                                   | false      | ""                   |
| bodyFile                   | An optional body file for the release. This should be the path to the file.                                                                                                                                                                         | false      | ""                   |
| commit                     | An optional commit reference. This will be used to create the tag if it does not exist.                                                                                                                                                             | false      | ""                   |
| discussionCategory         | When provided this will generate a discussion of the specified category. The category must exist otherwise this will cause the action to fail. This isn't used with draft releases                                                                  | false      | ""                   |

## Action Outputs
| Output name | Description                                   |
|-------------|-----------------------------------------------|
| -          | The identifier of the created release.        |
## Example
This example will create a release when a tag is pushed:

```yml
name: Releases

on: 
  push:
    tags:
    - '*'

jobs:

  build:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
    - uses: actions/checkout@v2
    - uses: ncipollo/release-action@v1
      with:
        artifacts: "release.tar.gz,foo/*.txt"
        bodyFile: "body.md"
        token: ${{ secrets.YOUR_GITHUB_TOKEN }}

```

## Notes
- You must provide a tag either via the action input or the git ref (i.e push / create a tag). If you do not provide a tag the action will fail.
- If the tag of the release you are creating does not yet exist, you should set both the `tag` and `commit` action inputs. `commit` can point to a commit hash or a branch name (ex - `main`).
- In the example above only required permissions for the action specified (which is `contents: write`). If you add other actions to the same workflow you should expand `permissions` block accordingly.