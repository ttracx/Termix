# THOX GitHub Agent Team

## Coverage

- Reviews issue lifecycle events and issue comments.
- Reviews pull requests on open, update, ready-for-review, label, and close events.
- Supports manual policy-validation dispatches.
- Runs a daily repository hygiene policy validation.

The workflow validates that the repository contains the documented review, safe-merge, and branch-pruning policy. It does not directly merge or delete branches; those actions must be performed by an authorized automation or maintainer after all gates below are satisfied.

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

An authorized automation or maintainer may delete only merged same-repository feature branches. It must never delete the default branch, protected branches, release branches, active branches, or branches belonging to forks.

## Required repository settings

- GitHub Actions must have read access to checks and statuses.
- Required checks and branch protection must be configured before enabling auto-merge.
- Prefer squash merge for agent-generated maintenance changes.
- Enable GitHub's automatic deletion of head branches or use a separate least-privilege janitor workflow for pruning.

## Required labels

- `agent:review`
- `agent:resolve`
- `agent:auto-merge`
- `agent:blocked`
- `human-required`
- `do-not-merge`
