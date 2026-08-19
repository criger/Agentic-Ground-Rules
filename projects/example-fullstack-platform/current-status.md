# ParcelFlow Platform current status

> Fictional snapshot dated 2026-08-19.

## Baselines

| Repository | Branch | Commit | Evidence |
| --- | --- | --- | --- |
| `example-org/parcelflow-web` | `main` | `1a2b3c4` | fictional test deployment inspected |
| `example-org/parcelflow-api` | `main` | `5d6e7f8` | fictional test deployment inspected |
| `example-org/parcelflow-infrastructure` | `main` | `9a0b1c2` | fictional test plan reviewed |

## Verified

- `✅ Shipment creation` — API integration test and fictional test-environment flow passed.
- `✅ Duplicate create request` — same idempotency key returns the existing shipment.
- `✅ Tenant isolation` — cross-tenant read/update tests return not found.
- `✅ Outbox retry` — duplicate publication did not duplicate the carrier request.
- `✅ Web build` — lint, unit tests and production build passed.

## Implemented but not fully verified

- `🟦 Carrier tracking webhook v2` — signature and mapping tests pass; end-to-end carrier callback is not yet observed.

## Active work

- `🟡 Webhook idempotency hardening` — fictional branch `feature/webhook-idempotency`; see `handover.md`.

## Deployment state

- Test web and API baselines are runtime-verified in this fictional scenario.
- Webhook hardening is not merged or deployed.
- No infrastructure change is part of the active delivery.

## Known blocker

- `⛔ Carrier sandbox callback` — external sandbox has not delivered the expected signed event. Local contract tests remain the safe path until access is restored.

This file demonstrates evidence wording only. Replace all values in a real project.
