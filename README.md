# multiplatform.workflows
Repository hosting the Github Actions workflows used for building Multiplatform libraries.

## Notes

### Build and Publish workflow
#### Secrets that need to be defined

- `GH_PUBLISH_TOKEN`
- `GH_PUBLISH_USERNAME`
- `NPM_TOKEN`

#### Inputs that needs to be passed in

  - `IOS_LIBRARY_NAME`
  - `REPO_NAME`
  - `SWIFT_PACKAGE_REPO_OWNER`
  - `SWIFT_PACKAGE_REPO`
  - `XCFRAMEWORK_BUILD_TASK`
  - `ANDROID_PUBLISH_TASK`

#### Example usage

```yaml
name: Build and publish

on:
  push:
    branches:
      - master

jobs:
  invoke:
    uses: superbet-group/multiplatform.workflows/.github/workflows/build.yml@v1
    with:
        REPO_NAME: multiplatform.build-test
        IOS_LIBRARY_NAME: buildTestLib
        SWIFT_PACKAGE_REPO: multiplatform.ios.build-test
        XCFRAMEWORK_BUILD_TASK: assembleBuildTestLibXCFramework
        ANDROID_PUBLISH_TASK: publishAndroidReleasePublicationToMavenRepository
    **secrets**: inherit
```

### Test workflow
#### Secrets that need to be defined

none

#### Optional secrets

  - `SLACK_WEBHOOK_URL`

#### Inputs that needs to be passed in

  - `IOS_LIBRARY_NAME`
  - `REPO_NAME`

#### Optional inputs

  - `SLACK_NOTIFY` (boolean)
  - `SLACK_TOPIC` 

#### Example usage

```yaml
name: Nightly verification

on:
  schedule:
    - cron: '0 0 * * *' # Midnight UTC

jobs:
  invoke:
    uses: superbet-group/multiplatform.workflows/.github/workflows/test.yml
    with:
      REPO_NAME: multiplatform.lib
      IOS_LIBRARY_NAME: MultiplatformLib
      SLACK_NOTIFY: true
      SLACK_TOPIC: "Nightly Verification of `master` branch"
    secrets: inherit
```