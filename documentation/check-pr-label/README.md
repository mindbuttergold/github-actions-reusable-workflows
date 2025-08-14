# check-pr-label

The check-pr-label workflow checks for the presence of a specified label on a PR.

## Functionality

If the specified label is present, the job passes. If it is absent, the job fails. This workflow is intended to be used along with another workflow that automates label creation, but it can be used alone if manual labelling is desired.

## Prerequisites

None

## Usage

- The workflow must be triggered by a PR event

### Required Permissions

```yaml
permissions:
  contents: read
```

**Note:** It is best practice to define least privilege permissions (read-all) at the top-level of a workflow file, and any greater permissions needed, at the individual job-level.

### Inputs

```yaml
# required, the label to check for
label: "your-label"
# optional, default = true, whether to fail the job if the label is missing 
fail-if-missing: "false"
```

### Outputs

```yaml
# Whether the PR label check succeeded or failed, values = "success" or "fail"
- success-status
```

### Example Workflow Call

```yaml
name: check-community-approval-label
on:
  pull_request:
    types:
      - opened
      - synchronize
      - reopened
      - labeled
      - unlabeled
permissions:
  contents: read

jobs:
  check-community-approval-label:
    name: check-community-approval-label
    uses: mindbuttergold/github-actions-reusable-workflows/.github/workflows/check-pr-label.yaml@v2
    with:
      label: "community-approved"
```
