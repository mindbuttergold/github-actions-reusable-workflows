# github-actions-reusable-workflows

[![CodeQL](https://github.com/mindbuttergold/github-actions-reusable-workflows/actions/workflows/github-code-scanning/codeql/badge.svg)](https://github.com/mindbuttergold/github-actions-reusable-workflows/actions/workflows/github-code-scanning/codeql) [![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/mindbuttergold/github-actions-reusable-workflows/badge)](https://scorecard.dev/viewer/?uri=github.com/mindbuttergold/github-actions-reusable-workflows) 

<!-- TODO: Update after first merge -->
<!-- [!
[OpenSSF Best Practices](https://www.bestpractices.dev/projects/10740/badge?cache-control=no-cache)](https://www.bestpractices.dev/projects/10740) -->

Centralized repository for reusable Github actions workflows that can be consumed in other repositories.

## Usage

Reusable workflows are consumed via a workflow file in the calling repo. Reusable workflows are called at the job level.

**Note:** Reusable workflows only have only the permissions passed by the consuming repo, so any required permissions must be passed in the caller's workflow.

See the [documentation](./documentation/) for each workflow with info on required permissions and any other setup requirements.
