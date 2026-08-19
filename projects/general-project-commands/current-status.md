# `<PROJECT>` current status

> Template: This is a dated snapshot. Verify branch, commit and environment before new work.

## Documented baseline

```text
Last updated:       <YYYY-MM-DD>
Source inspected:   <YYYY-MM-DD>
Repository:         <owner/repo>
Branch:             <branch>
Commit:             <SHA or not verified>
Environment:        <local/test/production/other>
```

For several repositories:

| Repository | Branch | Commit | Last inspected | Role |
| --- | --- | --- | --- | --- |
| `<owner/repo>` | `<branch>` | `<SHA>` | `<date>` | `<PLACEHOLDER>` |

## Status legend

```text
✅ Verified      Tested or observed with stated evidence
🟦 Implemented   Code exists; full verification or deployment is missing
🟡 In progress   Active work
⛔ Blocked       An explicit blocker exists
⬜ Planned       Not implemented
❓ Unknown       Requires investigation
```

## Production or release state

```text
<confirmed deployed state>
<merged but not deployment-verified state>
<manual publication or migration still required>
```

## Implemented and verified

- `✅ <feature>` — `<how and where it was verified>`

## Implemented but not fully verified

- `🟦 <feature>` — `<missing build/test/runtime/deployment evidence>`

## Active work

- `🟡 <work>` — `<branch, state and nearest milestone>`

## Blockers and known deviations

- `⛔ <blocker>` — `<owner, impact and safe alternative>`
- `❓ <unknown>` — `<smallest test that can resolve it>`

## Build and test state

| Check | Result | Date/environment | Notes |
| --- | --- | --- | --- |
| `<command or manual test>` | `<passed/failed/not run>` | `<PLACEHOLDER>` | `<PLACEHOLDER>` |

Do not write "all tests pass" without naming the tests that ran.

## Runtime and operational conditions

- `<third-party status, capacity, rate limit, scheduled/manual task or other>`

Move lasting lessons to `pitfalls.md`.

## Recent deliveries

| Date | Delivery | Repository/branch | Verification | Deployment |
| --- | --- | --- | --- | --- |
| `<date>` | `<short description>` | `<PLACEHOLDER>` | `<PLACEHOLDER>` | `<PLACEHOLDER>` |

Use `implementation-log.md` when the list grows.

## Not verified

- `<explicit limitation of the latest inspection>`

## Before the next change

1. Fetch and verify the actual branch/commit.
2. Read task-relevant specialized documents.
3. Reconfirm blockers and deployment state when relevant.
4. Follow `next-steps.md` or the first action in `handover.md`.

Update this document whenever new evidence changes the baseline or a delivery's implementation, test or deployment status.
