# ParcelFlow Platform handover

> Fictional operational snapshot.

```text
Date:                 2026-08-19
Active task:          Webhook idempotency hardening
Source repository:    example-org/parcelflow-api
Working branch:       feature/webhook-idempotency
Latest relevant SHA:  c3d4e5f (fictional)
Environment:          local integration test
```

## Goal

Prevent repeated carrier webhook deliveries from applying the same shipment transition more than once.

## Completed

- `✅ Existing flow mapped` — signature verification occurs before the application handler.
- `✅ Identity selected` — carrier account + external event ID is the deduplication key.
- `✅ Migration drafted` — fictional unique constraint added.
- `✅ Sequential duplicate test` — first event updates once; second is a successful no-op.

## In progress

- `🟡 Concurrent duplicate test` — test exists but currently exposes a unique-constraint exception instead of mapping it to the successful duplicate result.

## Decision

Catch the repository's explicit duplicate result at the application boundary. Do not catch every database exception as a duplicate, because unrelated persistence failures must still fail.

## Central files

```text
src/ParcelFlow.Application/Tracking/ProcessTrackingEvent.cs
src/ParcelFlow.Infrastructure/Tracking/TrackingEventRepository.cs
src/ParcelFlow.Infrastructure/Migrations/<fictional-migration>.cs
tests/ParcelFlow.IntegrationTests/TrackingWebhookTests.cs
```

## Verification run

| Check | Result | Notes |
| --- | --- | --- |
| Tracking unit tests | Passed | Fictional result |
| Sequential duplicate integration test | Passed | Fictional result |
| Concurrent duplicate integration test | Failed | Expected mapping not implemented |
| Full `dotnet test` | Not run | Wait until the focused test passes |

## Blocker

Carrier sandbox callbacks remain unavailable, but they do not block local idempotency implementation and contract tests.

## First next action

1. Map the unique-key race to the explicit duplicate repository result.
2. Re-run the concurrent test, then full `dotnet test`.

## Preserve

- Signature verification remains before domain processing.
- Only the documented unique key is treated as a duplicate.
- Tenant/carrier scope remains part of the key.
- Do not mark the feature runtime-verified until a real signed callback is observed.
