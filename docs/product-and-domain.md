# Product and Domain

TiniTasker is a Canadian B2B SaaS product for service businesses. It helps business owners and technicians keep operational and financial data clear and organized.

## Canonical ownership

| Repository | Owns |
| --- | --- |
| `api` | Product business behavior, product APIs, domain calculations, and the `public` PostgreSQL schema. |
| `identity` | Authentication, OpenID Connect, tokens, and the `identity` schema. |
| `storage` | Private organization-scoped attachment access and object-storage integration. |
| `messaging` | Email and push delivery, notification templates, and delivery audit behavior. |
| `app` | Mobile experience for business owners and technicians. |
| `web-portal` | Internal browser dashboard for business owners and managers. |
| `web-public` | Public marketing site plus public estimate and invoice experiences. |
| `infrastructure` | Terraform and DigitalOcean infrastructure definitions. |
| `migrations-runner` | Validated, digest-pinned PostgreSQL migration packaging and execution image. |
| `actions` | Shared versioned composite GitHub Actions. |
| `.github` | Organization-wide documentation and GitHub community-health defaults. |

The service that owns a domain rule remains its source of truth. Other services and clients consume an explicit contract rather than reimplementing the rule.

## Product vocabulary

- **User** — a person who uses TiniTasker, typically a business owner or technician.
- **Organization** — the tenant boundary that groups business entities and users.
- **Item** — a product or service provided by an organization.
- **Expense** — a business-related expense.
- **Customer** — a client of an organization.
- **Estimate** — approximate charges for products or services.
- **Invoice** — charges and payments for products or services.
- **Job** — work performed or scheduled by an organization.

Use these terms consistently in interfaces, APIs, data models, documentation, and notifications. Do not overload them with unrelated meanings.

## Tenant and data boundaries

TiniTasker uses pooled multi-tenancy: services share databases and schemas while data is segregated by `organization_id` (or the owning service's equivalent tenant boundary).

- Every data read, write, cache key, file lookup, message, and external side effect must be scoped and authorized for the organization.
- Never infer access from a client-supplied identifier alone. Authorization belongs at the owning service boundary.
- Storage access and cached file content must remain organization-scoped. Notification content must not cross tenant boundaries.

## Shared product policy

Business policy that changes the meaning of data across repositories belongs here or in [cross-repository contracts](cross-repository-contracts.md), not in a client-only workaround. Examples include tax treatment, invoice status semantics, organization timezones, and shared enum values.

Service-specific behavior, such as notification template placeholders or storage cache controls, remains documented in the owning repository.
