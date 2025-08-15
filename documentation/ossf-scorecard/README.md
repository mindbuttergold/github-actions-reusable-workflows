# semver-release

The ossf-scorecard workflow is a thin, configured wrapper over the Open Source Security Foundation's [scorecard-action Github Action](https://github.com/ossf/scorecard-action/tree/v2.4.2/). It rates a repository's adherence to Open Source Software security best practices.

## Functionality

The workflow analyzes the repository's adherence to a variety of security best practices, and generates a score for various areas. The results can be viewed via the Scorecard Badge added to the repository's README, the repo's Security > Code Scanning tab, or the workflow run in the repo's Actions tab.

## Prerequisites

- To display the scorecard badge, add the following to the repository's README.md, replacing instances of `{owner}` and `{repo}` with your values:  

  ```
  [![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/{owner}/{repo}/badge)](https://scorecard.dev/viewer/?uri=github.com/{owner}/{repo})
  ```

## Usage

- This workflow can only be used by public repositories, or private repositories that have [GitHub Advanced Security](https://docs.github.com/en/get-started/learning-about-github/about-github-advanced-security). It cannot be used on Github Enterprise repositories.
- The workflow must be triggered either on `push` from the default branch or `schedule`.

### Required Permissions

```yaml
permissions:
  contents: read
  security-events: write
  id-token: write
```

**Note:** It is best practice to define least privilege permissions (read-all) at the top-level of a workflow file, and any greater permissions needed, at the individual job-level.

### Inputs

None

### Outputs

None

### Example Workflow Call

```yaml
name: ossf-scorecard
on:
  push:
    branches: [ "main" ]
permissions: read-all

jobs:
  ossf-scorecard:
    name: ossf-scorecard
    permissions:
      security-events: write
      id-token: write
    uses: mindbuttergold/github-actions-reusable-workflows/.github/workflows/ossf-scorecard.yaml@v2
```
