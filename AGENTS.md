# TiniTasker GitHub Defaults — Agent Instructions

Read the [organization engineering handbook](https://github.com/tinitasker/docs/blob/main/docs/README.md) before making a change. The `docs` repository is the source of truth for cross-repository development flow, product language, tenancy, money, time, and API-contract rules.

## Scope of this repository

This repository owns GitHub community-health defaults. It does not own organization documentation, application runtime code, service deployment configuration, or repository-specific build instructions.

- Put cross-repository policy, architecture, and business/domain decisions in [`tinitasker/docs`](https://github.com/tinitasker/docs).
- Keep `profile/README.md` a concise public organization profile; do not duplicate operational detail there.
- Use `PULL_REQUEST_TEMPLATE.md` for the default pull-request checklist.
- Keep repository-specific technology, tests, deployment details, and operational contracts in that repository's `AGENTS.md` and existing local documentation.

Apply the shared `feature/<short-meaningful-description>` branch and draft-PR flow to documentation changes too. Do not edit or push directly to `main`.
