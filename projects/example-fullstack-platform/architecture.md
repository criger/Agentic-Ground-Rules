# ParcelFlow Platform architecture

> Fictional example.

## System overview

```text
React web
  -> ASP.NET Core API
      -> application services
          -> PostgreSQL
          -> transactional outbox
              -> Service Bus
                  -> carrier worker
                      -> carrier API

Carrier webhook
  -> API webhook endpoint
      -> signature verification + deduplication
          -> shipment domain update
```

## Components

| Component | Owns | Does not own |
| --- | --- | --- |
| Web | presentation, user input, remote-state coordination | authorization, carrier rules |
| API controllers | HTTP boundary and DTO mapping | domain workflow and EF queries |
| Application services | shipment use cases and transaction boundaries | carrier HTTP transport |
| Domain | shipment state transitions and invariants | ASP.NET/EF details |
| Repositories | tenant-scoped persistence | identity or UI flow |
| Outbox publisher | reliable publication of committed intent | shipment policy |
| Carrier client | transport, authentication and response mapping | tenant authorization |
| Infrastructure | cloud resources and environment wiring | application business rules |

## API dependency direction

```text
Controller
  -> application use case
      -> domain model
      -> repository/carrier contracts
          -> EF and HTTP implementations
```

Concrete EF, Service Bus and carrier clients stay outside the domain.

## Transactional outbox invariant

Shipment state and the outbound carrier intent are written in the same database transaction.

The publisher may deliver more than once. Consumers therefore use stable message IDs and idempotent handlers. Do not replace the outbox with "save, then publish" without accepting the lost-message failure window.

## Tenant boundary

Every tenant-owned repository query receives the authoritative tenant ID from the authenticated request context. Entity IDs are never sufficient on their own.

```text
authenticated claims
  -> validated tenant context
      -> application service
          -> repository query constrained by tenant ID + entity ID
```

## Carrier boundary

Carrier-specific statuses and payloads are mapped into a small internal model. Carrier transport DTOs must not become the public API or persistence domain by accident.

## Compatibility

- Web and API changes may require an additive API rollout before the web deploy.
- Database migrations must be backward-compatible with the currently deployed API during rolling deployment.
- Infrastructure changes require a reviewed plan and must not be inferred from application merge state.

## Architecture verification

- Unit-test domain transitions and idempotency.
- Integration-test tenant-scoped repositories against PostgreSQL.
- Contract-test carrier mapping and webhook signatures.
- Verify outbox publish/retry with an isolated queue.
- Run web build and critical user flows against the candidate API.
