# Example: ParcelFlow Platform

> **Fictional example.** This directory demonstrates instruction context for a production-like system spanning several repositories.

## Repositories

| Repository | Responsibility |
| --- | --- |
| `example-org/parcelflow-web` | React operations portal |
| `example-org/parcelflow-api` | .NET API, domain workflows and persistence |
| `example-org/parcelflow-infrastructure` | Terraform and environment configuration |

All names are fictional.

## Purpose

ParcelFlow helps small logistics companies create shipments, purchase carrier labels and track delivery events in one tenant-isolated workspace.

## Stack

```text
Web:             React 19, TypeScript, Vite
API:             .NET 9, ASP.NET Core, EF Core
Database:        PostgreSQL
Messaging:       Azure Service Bus
Infrastructure:  Terraform
```

## Main flow

```text
Operator creates shipment
  -> API validates tenant and request
  -> shipment + outbox message commit together
  -> background publisher sends carrier request
  -> carrier webhook updates tracking state idempotently
  -> web refreshes shipment timeline
```

## Reading order

1. `context.md`
2. `architecture.md`
3. `current-status.md`
4. `security.md` for identity/data work
5. `deployment.md` for release work
6. `handover.md` and `next-steps.md` for the active delivery
7. Actual source in every affected repository

## Repository checks

```text
parcelflow-web:             npm run lint && npm run test && npm run build
parcelflow-api:             dotnet test && dotnet publish -c Release
parcelflow-infrastructure:  terraform fmt -check && terraform validate && terraform plan
```

These commands are illustrative. Real projects must verify commands and environment prerequisites from source.

## Project-specific rules

- Tenant identity comes from the authenticated server-side context, never a client-supplied authority field.
- Shipment creation is idempotent for a stable client request ID.
- Database state and outbound intent commit through the outbox pattern.
- Web, API and infrastructure have different deployment evidence and must be reported separately.
- Carrier payloads are external transport data and are mapped before entering the domain model.
