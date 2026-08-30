# Development Flow

TiniTasker uses one long-lived branch: `main`. It does not use `develop`, release, or hotfix branches. Every change, including documentation, infrastructure, configuration, and dependency work, follows this short-lived feature-branch flow.

## Main-branch protection

Every current organization repository has an active `Require pull requests for main` ruleset for `refs/heads/main`:

- direct changes must be associated with an open pull request;
- force pushes and branch deletion are blocked;
- no user, team, or integration has a bypass; and
- review conversations must be resolved before merge.

The rule intentionally requires zero GitHub approvals. The repository owner manually reviews and merges each PR, and is not blocked from merging a PR created with the same account. Do not add a repository without applying the equivalent protection first.

## 1. Determine the affected repositories

Before editing, inspect the organization and the relevant repositories. Identify:

- which repository owns the behavior, data, API contract, migration, workflow, or deployment concern;
- every client or service that consumes a changed contract;
- whether a shared domain rule in this handbook must change; and
- a safe implementation and merge order when changes span repositories.

Do not make a speculative change in every repository. Change every repository that is genuinely affected, and record the relationship in the draft PRs.

## 2. Create matching feature branches

Create one short, meaningful branch name in every affected repository:

```sh
git fetch origin --prune
git switch -c feature/<short-meaningful-description> origin/main
```

For one logical cross-repository change, the branch name must be identical everywhere. Start from the current `origin/main`; never develop directly on local or remote `main`.

## Operational tags

Release and operational tags are immutable references, not development branches. They may record a reviewed `main` commit or release metadata, but must never be used to land code outside a feature-branch PR. Repository-local instructions define any approved release-tag pattern and protection.

Repositories with tag-driven releases use `vX.Y.Z-staging` for staging and
`vX.Y.Z` for production, with no leading zeroes. A release tag must be a new,
non-forced tag whose commit is reachable from `main`; a repository may impose a
stricter requirement when its deployment platform resolves `main` at deploy
time. Workflows consume the shared `tinitasker/actions/release/read-tag` action
pinned to a reviewed full commit SHA so format, immutability, ancestry, and
release metadata are enforced consistently. Protect the corresponding tag
patterns and GitHub Environment deployment-tag patterns before enabling a new
tag-triggered workflow.

## 3. Implement and verify

- Follow the local `AGENTS.md` and existing repository documentation for stack, tests, deployment, migrations, and secrets.
- Keep backward compatibility while rolling out shared contracts. Update consumers, producers, and this handbook together when the change is cross-repository.
- Run the relevant local checks before pushing. Never put secrets, credentials, Terraform state, or customer data in commits, logs, fixtures, or PR descriptions.
- Keep a change focused. Separate unrelated cleanup, reformatting, and dependency upgrades into their own work.

## 4. Commit and push

Commit messages state the action taken, not a vague result or ticket outcome. Use concise past-tense action descriptions, for example:

- `Added staging configuration`
- `Updated invoice status contract`
- `Removed unused migration helper`

Push only the feature branch:

```sh
git push -u origin feature/<short-meaningful-description>
```

Never push, merge, force-push, or commit directly to `main`.

## 5. Open draft pull requests

Create a draft pull request from each affected `feature/<short-meaningful-description>` branch to `main`. Use the organization pull-request template and include:

- a clear action-focused summary;
- validation performed and results;
- every related repository/PR and the required merge order;
- changed contract, migration, rollout, compatibility, or rollback considerations; and
- a link to the handbook update when a shared rule changed.

Keep PRs in draft until the requested implementation is complete. Do not enable auto-merge. The repository owner reviews and merges manually when appropriate.

## New repositories

An entirely empty repository needs a one-time seed default branch before a pull-request flow can exist. Create it with an initial README/default `main` branch during repository provisioning, then immediately apply the same `main` ruleset and add a root `AGENTS.md` that links to this handbook. All subsequent work begins on `feature/<short-meaningful-description>`, not `main`.
