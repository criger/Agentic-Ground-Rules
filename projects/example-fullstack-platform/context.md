# ParcelFlow Platform context

> Fictional example.

## Actors

- Operators create shipments and review tracking.
- Tenant administrators manage users and carrier accounts.
- Carrier systems accept label requests and send tracking webhooks.
- Support staff diagnose failed integrations through audited operational tools.

## Scope

ParcelFlow owns:

- tenant-scoped shipment records
- orchestration of label requests
- normalized tracking history
- operator-facing workflow and audit trail

ParcelFlow does not own:

- carrier availability or delivery decisions
- the enterprise identity provider
- financial settlement with carriers

## Critical flows

### Shipment creation

```text
authenticated operator
  -> tenant/role authorization
  -> validate address and package
  -> create shipment under idempotency key
  -> persist outbox intent
  -> return pending shipment
```

### Tracking update

```text
carrier webhook
  -> verify signature and carrier account
  -> deduplicate external event ID
  -> map carrier status
  -> append tracking event
  -> update shipment summary
```

## Data authority

| Data | Authority | Notes |
| --- | --- | --- |
| Tenant/user identity | identity provider + API claims mapping | browser fields are not authoritative |
| Shipment | ParcelFlow API/database | always tenant-scoped |
| Carrier label | carrier response stored by API | access-controlled document |
| Tracking event | normalized carrier webhook | deduplicated by carrier + event ID |
| UI filters | browser | non-sensitive preferences only |

## Evidence priority

1. Reproducible runtime observations and database/message evidence in the named environment.
2. Current API/web/infrastructure source on verified commits.
3. Carrier specifications for the configured integration version.
4. Maintained project documentation.
5. Old support notes and chat history.

Conflicts must be recorded rather than silently resolved.
