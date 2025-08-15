# check-conventional-commit-pr-title

The check-conventional-commit-pr-title workflow is just a wrapper over the [action-semantic-pull-request Github Action](https://github.com/amannn/action-semantic-pull-request/tree/v5/), which ensures PR titles meet conventional commit standards for use with squash merging to facilitate automated semantic releasing. It is turned into a workflow in the mindbuttergold org to centralize versioning, etc., across repos. For those outside the org, it makes more sense to just use the original action.

## Functionality

The workflow checks the title of a PR to make sure it is consistent with conventional commit formatting (e.g., `feat: some commit info`). This is done because the title of squash merges are what is used as the final, single commit message upon merging, for the semver-release workflow to then base release actions off. If the title does not meet the standard, the job fails. If it meets the standard, the job succeeds.

## Prerequisites

None

## Usage

- The workflow must be triggered on `pull_request_target` if the repository will have fork-based PRs. In this case, the workflow will only use the code that's on the main branch of the base repository, so it will not run until after it has been merged.
- If not doing fork-based PRs, the workflow can be triggered on `pull_request`.

### Required Permissions

```yaml
permissions:
  contents: read
  pull-requests: read
```

**Note:** It is best practice to define least privilege permissions (read-all) at the top-level of a workflow file, and any greater permissions needed, at the individual job-level.

### Inputs

None

### Outputs

None

### Example Workflow Call

```yaml
name: validate-pr-title
on:
  pull_request_target:
    types:
      - opened
      - synchronize
      - edited
      - reopened
permissions: read-all

jobs:
  validate-pr-title:
    name: validate-pr-title
    uses: ./.github/workflows/check-conventional-commit-pr-title.yaml
```
