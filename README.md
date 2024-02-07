# multiplatform.workflows
Repository hosting the Github Actions workflows used for building Multiplatform libraries.

## Notes
### Secrets that need to be defined

- `GH_PUBLISH_TOKEN`
- `GH_PUBLISH_USERNAME`
- `NPM_TOKEN`

### Inputs that needs to be passed in

  - `IOS_LIBRARY_NAME`
  - `REPO_NAME`
  - `SWIFT_PACKAGE_REPO_OWNER`
  - `SWIFT_PACKAGE_REPO`
  - `XCFRAMEWORK_BUILD_TASK`
  - `ANDROID_PUBLISH_TASK`

### Example usage

#### Build and publish

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
    secrets: inherit
```

#### Test

**TODO**