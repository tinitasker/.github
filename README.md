# TiniTasker

TiniTasker is a Canadian B2B SaaS platform for service businesses. It gives owners, managers, and technicians a shared system for customers, jobs, estimates, invoices, payments, attachments, and operational communication.

## Architecture at a glance

TiniTasker has three client experiences: the Flutter mobile app, the internal web portal, and the server-rendered public web application. Identity provides OpenID Connect authentication; the API owns product-domain behavior; Storage owns authorized attachments; and Messaging delivers email and push notifications. All backend services share a managed PostgreSQL cluster while retaining separate service schemas.

The [architecture overview](docs/architecture.md) describes components, communication paths, data boundaries, and delivery infrastructure. The [engineering handbook](docs/README.md) is the source of truth for organization-wide development and domain rules.

## Components

| Component           | Role                                                                  |
|---------------------|-----------------------------------------------------------------------|
| `app`               | Mobile experience for business owners and technicians.                |
| `web-portal`        | Internal web dashboard for business owners and managers.              |
| `web-public`        | Marketing site plus public estimate and invoice experiences.          |
| `api`               | Product-domain API and canonical business calculations.               |
| `identity`          | OpenID Connect authentication and token issuance.                     |
| `storage`           | Private, organization-scoped attachment operations.                   |
| `messaging`         | Email and push notification validation, delivery, and auditing.       |
| `actions`           | Shared GitHub Actions primitives, consumed from `main`.               |
| `migrations-runner` | Validated PostgreSQL migration packaging and execution image.         |
| `infrastructure`    | DigitalOcean Terraform definitions and delivery prerequisites.        |
| `.github`           | Organization documentation, community-health defaults, and templates. |

## Communication model

- The mobile app and web portal authenticate through Identity, use the API for
  product behavior, and use authorized Storage attachment operations.
- The public web app obtains client credentials from Identity and makes
  server-only calls to the API; its browser code never receives service
  credentials.
- API and Identity request email and push delivery from Messaging with service
  credentials. Messaging uses Resend and Firebase Cloud Messaging.
- API, Identity, Storage, and Messaging share managed PostgreSQL while keeping
  separate service schemas. Storage persists file bytes in DigitalOcean Spaces;
  the API integrates with Stripe, Helcim, and Google Places.
- Infrastructure provisions the DigitalOcean estate. Service workflows consume
  shared Actions and the digest-pinned migrations runner during delivery.

## Start here

- Read the [development flow](docs/development-flow.md) before creating or changing code.
- Read [product and domain](docs/product-and-domain.md) and [cross-repository contracts](docs/cross-repository-contracts.md) before changing shared behavior.
- Read the root `README.md`, `AGENTS.md`, and local deployment documentation in the repository you are changing.
