# ParcelFlow Platform next steps

> Fictional active plan.

## Active goal

Make carrier tracking webhook processing safely idempotent when the carrier retries the same event.

## Preconditions

1. Verify the API branch and current webhook tests.
2. Preserve raw-body signature verification.
3. Confirm the database unique key for carrier account + external event ID.
4. Keep the change inside the API repository; no web or infrastructure change is selected.

## P0: baseline

- Run existing webhook unit and integration tests.
- Capture current duplicate-event behaviour.
- Verify that the test database migration baseline succeeds.

## P1: smallest complete delivery

- Store the external event identity with a unique constraint.
- Treat a verified duplicate as a successful no-op.
- Keep invalid signatures as rejection, not deduplication.
- Add concurrent duplicate integration coverage.
- Add structured non-sensitive duplicate metrics/logging.

Complete when:

- the first valid event updates the shipment once
- sequential and concurrent duplicates return success without another transition
- a different tenant/carrier account cannot collide with the event ID
- signature failures remain rejected
- `current-status.md` and `handover.md` reflect actual verification

## P2: deferred follow-up

- Dashboard metric for repeated carrier callbacks.
- Carrier-specific retry timing analysis after real sandbox access returns.

## Out of scope

- Web timeline redesign
- Infrastructure queue changes
- New carrier integrations
