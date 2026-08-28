# TiniTasker Engineering Handbook

This directory is the source of truth for rules that span TiniTasker's repositories. Repository-local instructions belong in the root `AGENTS.md` and existing operational documentation of the relevant repository.

## Read in this order

1. [Architecture overview](architecture.md) — runtime components, communication paths, data boundaries, and delivery infrastructure.
2. [Development flow](development-flow.md) — required branch, commit, push, and draft-PR process.
3. [Product and domain](product-and-domain.md) — product vocabulary, ownership, and tenant boundaries.
4. [Cross-repository contracts](cross-repository-contracts.md) — money, tax, time, enum, locale, and API compatibility rules.

The root [organization README](../README.md) provides the high-level architecture. The public [organization profile](../profile/README.md) provides a product overview and service directory. Neither is a substitute for the policies in this handbook.

## Documentation ownership

- Update this handbook whenever a rule affects more than one repository.
- Keep service APIs, deployment steps, schemas, and developer commands in their owning repositories.
- Link to the relevant handbook page from each repository's `AGENTS.md`; do not copy cross-repository policy into local instructions.
