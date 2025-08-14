# reactions-based-pr-label

The reactions-based-pr-label workflow checks each open PR in a repository for the desired count of a specified reaction, and adds a label if the count is met.

## Functionality

If there are no open PRs in the repo, the job does nothing. If the reaction count is met on any PR, the job adds the label to that PR. If there are open PRs, but they do not have the desired reaction count, the job checks to see if the label was present already. If the reaction count is not met on a PR, but the label was present, it will remove the label from that PR (i.e., if reactions were removed). If the reaction count is not met on a PR and the label is not present, the job does nothing. 

## Prerequisites

None

## Usage

- This workflow should be triggered on a cron schedule, as it checks and manages all open PRs across the repository.

### Required Permissions

```yaml
permissions:
  pull-requests: read
  issues: write
```

**Note:** It is best practice to define least privilege permissions (read-all) at the top-level of a workflow file, and any greater permissions needed, at the individual job-level.

### Inputs

```yaml

# required, the reaction type to check for, see options at https://docs.github.com/en/rest/reactions/reactions?apiVersion=2022-11-28#about-reactions
reaction: "reaction"
# required, the minimum number of reactions required to add the label
reaction-count: 5
# required, the label to add / remove based on the reaction count
label: "your-label"
```

### Example Workflow Call

```yaml
name: check-pr-thumbs-up
on:
  schedule:
    - cron: '0 5 * * *'
    - cron: '0 13 * * *' 
    - cron: '0 19 * * *'
permissions: read-all

jobs:
  check-pr-thumbs-up:
    name: check-pr-thumbs-up
    permissions:
      pull-requests: read
      issues: write
    uses: mindbuttergold/github-actions-reusable-workflows/.github/workflows/reactions-based-pr-label.yaml@v2.0.0
    with:
      reaction: "+1"
      reaction-count: 5
      label: "community-approved"
```
