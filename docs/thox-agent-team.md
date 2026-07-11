# THOX GitHub Agent Team

## Coverage

- Reviews issue lifecycle events and issue comments.
- Reviews pull requests on open, update, ready-for-review, label, and close events.
- Supports manual review/prune/full dispatch modes.
- Runs a daily repository hygiene review.

## Safe merge gates

A pull request is eligible for automated merge only when all of these conditions are true:

1. The pull request is not a draft.
2. Required checks and status contexts completed successfully.
3. Branch protection permits the merge.
4. No blocking label is present, including `do-not-merge`, `human-required`, or `agent:blocked`.
5. The head branch belongs to this repository, not an external fork.
6. Changes to secrets, authentication, deployment credentials, or security controls received human review.
7. The expected head SHA still matches at merge time.

## Branch pruning policy

Automation may delete only merged same-repository feature branches. It must never delete the default branch, protected branches, release branches, active branches, or branches belonging to forks.

## Required repository settings

- GitHub Actions must have read access to checks and statuses.
- PR and issue write permissions must be enabled for the workflow.
- Required checks and branch protection must be configured before enabling auto-merge.
- Prefer squash merge for agent-generated maintenance changes.

## Required labels

- `agent:review`
- `agent:resolve`
- `agent:auto-merge`
- `agent:blocked`
- `human-required`
- `do-not-merge`
