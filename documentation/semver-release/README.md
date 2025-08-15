# semver-release

The semver-release workflow uses the [semantic-release](https://github.com/semantic-release/semantic-release) package to automate versioned Github releases, based on [Conventional Commit standards](https://www.conventionalcommits.org/en/v1.0.0/). It includes the [Conventional Changelog plugin](https://github.com/conventional-changelog/conventional-changelog) for release notes, and the [semantic-release-major-tag plugin](https://github.com/doteric/semantic-release-major-tag) for major version alias tagging.

## Functionality

The first time this workflow runs on a non-versioned repository, it will release `v1.0.0`, if the commit message prefix meets the standard for release (`fix:`, `feat:`, or `<prefix>!:`). A major version alias tag will be added for `v1` as well, pointed to the same commit. Once the repository is versioned (or if already versioned), if the message is prefixed with `fix:`, a new patch version will be released. If prefixed with `feat:`, a new minor version will be released. If a `!` is included, such as `feat!:`, a new major version will be released. After a release is completed, a comment will be added to the originating PR. The major version alias tag will also be updated to point to the latest commit of that major version. Release notes are shown in the Github Release section.

## Prerequisites

- The consuming repository must include a `.releaserc.yaml` file with the following config:

  ```yaml
  {
    "preset": "conventionalcommits",
    "plugins":
      [
        "@semantic-release/commit-analyzer",
        "@semantic-release/release-notes-generator",
        "@semantic-release/github",
        "semantic-release-major-tag",
      ],
  }
  ```

## Usage

- The workflow must be triggered on `push` to the default branch
- It is strongly recommended to only use squash merging, and to use this workflow in conjunction with a conventional commit PR title check.

### Required Permissions

```yaml
permissions:
  contents: write
  issues: write
  pull-requests: write
  id-token: write
```

**Note:** It is best practice to define least privilege permissions (read-all) at the top-level of a workflow file, and any greater permissions needed, at the individual job-level.

### Inputs

None

### Outputs

None

### Example Workflow Call

```yaml
name: semver-release
on:
  push:
    branches:
      - main
permissions: read-all

jobs:
  semver-release:
    name: semver-release
    permissions:
      contents: write
      issues: write
      pull-requests: write
      id-token: write
    uses: mindbuttergold/github-actions-reusable-workflows/.github/workflows/semver-release.yaml@v2
```
