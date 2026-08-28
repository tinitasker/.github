# TiniTasker Organization Documentation — Agent Instructions

Read the [organization engineering handbook](https://github.com/tinitasker/.github/blob/main/docs/README.md) before making a change. It is the source of truth for the cross-repository development flow, product language, tenancy, money, time, and API-contract rules.

## Scope of this repository

This repository owns organization-wide documentation and GitHub community-health defaults. It does not own application runtime code, service deployment configuration, or repository-specific build instructions.

- Put cross-repository policy and business/domain decisions in `docs/`.
- Keep `profile/README.md` a concise public organization profile; do not duplicate operational detail there.
- Use `PULL_REQUEST_TEMPLATE.md` for the default pull-request checklist.
- Keep repository-specific technology, tests, deployment details, and operational contracts in that repository's `AGENTS.md` and existing local documentation.

Apply the shared `feature/<short-meaningful-description>` branch and draft-PR flow to documentation changes too. Do not edit or push directly to `main`.
