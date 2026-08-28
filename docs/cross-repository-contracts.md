# Cross-Repository Contracts

These rules keep the API, mobile app, web clients, services, and infrastructure consistent. A change to any rule requires coordinated feature branches, draft PRs, and an explicit rollout plan.

## Locale and language

- Product-facing English uses `en-CA`.
- Canadian dollars use the ISO currency code `CAD` whenever a currency needs to be explicit.
- Keep machine-readable values separate from localized labels. Format values for display at the presentation boundary.

## Money and tax

- The API is the canonical owner of financial calculation and summary behavior. The existing mobile and portal transaction-summary calculators are compatibility mirrors, not independent sources of truth. Change those mirrors only in a coordinated API/app/portal change with shared fixtures and a rollout plan; do not add another client-side calculator. Moving a summary fully server-side is separate migration work.
- Use fixed-point decimal semantics for money. Backend code uses `decimal` and database money columns use exact numeric types. Existing client mirrors must reproduce the documented contract and rounding behavior; do not use binary floating point for a new accounting calculation.
- Monetary values round to two decimal places using midpoint-away-from-zero behavior where rounding is required. Preserve the unrounded inputs and the calculated result appropriate to the domain operation.
- Store and preserve the tax components recorded with an issued financial document. Do not silently recompute historical documents from a later rate change.
- The canonical `GST` fields represent **GST/HST** (the entire HST amount in HST provinces). The canonical `PST` fields represent **PST/QST** where applicable. Province/rate policy belongs in the API and must not be independently duplicated in clients.

## Time and dates

- Store instants as timezone-aware UTC values and exchange them as ISO 8601 values with `Z` where the contract represents an instant.
- Store a business date separately when the domain means a calendar date rather than an instant. Use the organization's timezone when interpreting scheduling and business-day rules.
- The currently supported product timezone codes and IANA zone identifiers are:

  | Code | IANA zone |
  | --- | --- |
  | `NST` | `Canada/Newfoundland` |
  | `AST` | `Canada/Atlantic` |
  | `EST` | `Canada/Eastern` |
  | `CST` | `Canada/Central` |
  | `MST` | `Canada/Mountain` |
  | `PST` | `Canada/Pacific` |

- Do not derive a business timezone from a fixed UTC offset or a display abbreviation. Daylight-saving rules apply through the stored zone identifier.
- Do not introduce a new timezone string representation without a coordinated API, app, and web migration.

## Enums and statuses

- API enum and status values are stable string contract values, not ordinal integers or display labels.
- Adding a value is a contract change: update the producer, every affected consumer, tests, docs, and rollout plan together.
- Do not rename, repurpose, or remove an existing value without a compatibility migration. Consumers should handle an unexpected future value safely rather than crash or silently reinterpret it.

## API and event evolution

- The owning service documents and validates its contract. Client-only assumptions are not a substitute for an API change.
- Additive changes are preferred. Make breaking changes explicit, coordinate dependent repositories, and record required merge/deploy order in all related draft PRs.
- Keep identifiers opaque. Do not parse their representation in a consumer or use them to bypass authorization.
- Never expose server-only credentials, bearer tokens, private file URLs, or internal-only APIs to a browser or mobile client.
