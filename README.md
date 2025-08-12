# github-actions-reusable-workflows

[![CodeQL](https://github.com/mindbuttergold/github-actions-reusable-workflows/actions/workflows/github-code-scanning/codeql/badge.svg)](https://github.com/mindbuttergold/github-actions-reusable-workflows/actions/workflows/github-code-scanning/codeql) [![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/mindbuttergold/github-actions-reusable-workflows/badge)](https://scorecard.dev/viewer/?uri=github.com/mindbuttergold/github-actions-reusable-workflows) 

<!-- TODO: Update after first merge -->
<!-- [!
[OpenSSF Best Practices](https://www.bestpractices.dev/projects/10740/badge?cache-control=no-cache)](https://www.bestpractices.dev/projects/10740) -->

Centralized repository for reusable Github actions workflows that can be consumed by calling repositories.

## Usage

Reusable workflows are consumed via a workflow file in the repo where usage is desired, called at the job level.

**Note:** The reusable workflow will have only the permissions passed by the consumer repo, so any required permissions must be passed at the caller level. See the individual workflow files in this repo under `./.github/workflows/` for each workflow's required permissions.

Workflows prefixed with `z_local_` are not reusable, they are this repo's local usage.

**Example Workflow Call:**

```bash
name: "Validate PR Title"
on:
  pull_request_target:
    types:
      - opened
      - synchronize
      - edited
      - reopened

jobs:
  validate_pr_title:
    permissions:
      pull-requests: read
    uses: mindbuttergold/github-actions-reusable-workflows/.github/workflows/validate-pr-title.yaml@v1
    secrets: inherit
```
