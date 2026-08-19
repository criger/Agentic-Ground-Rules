# `<PROJECT>` pitfalls

> Template: Include only project-specific traps with a real cause or history. General rules belong in `global/`.

## Recommended format

```text
Symptom or tempting change
  -> why it happens
  -> what must be preserved
  -> smallest safe test
  -> evidence/as-of date when time-sensitive
```

## Security and ownership

### `<Short pitfall name>`

**Risk:** `<PLACEHOLDER>`

**Cause:** `<PLACEHOLDER>`

**Preserve:**

- `<server-side ownership, credential model, validation or other>`

**Verify first:**

- `<concrete test>`

## External integrations

### `<Rate limit, proxy, fallback or contract>`

**Failed approach:** `<previous attempt>`

**Why:** `<verified or clearly labelled suspected cause>`

**Current safe model:** `<PLACEHOLDER>`

**Do not:** `<aggressive retry, direct browser call, shape change or other>`

## State, lifecycle and concurrency

### `<Effect loop, polling, idempotency, cleanup or race>`

- Failure mode: `<PLACEHOLDER>`
- Existing protection: `<guard, debounce, signature, lock or rollback>`
- Test matrix: `<reload, multiple tabs, hidden tab, retry, error response>`

## Build, packages and runtime

### `<Dependency or build trap>`

- Critical configuration: `<peer dependency, import order, base path or other>`
- Typical symptom: `<PLACEHOLDER>`
- Before changing source: `<rebuild/reinstall/clear cache/verify environment>`

## UI, export or presentation

### `<Visual or document trap>`

- Why simple cleanup may break it: `<PLACEHOLDER>`
- Roles, devices or formats to test: `<PLACEHOLDER>`
- Rejected approach: `<PLACEHOLDER>`

## Domain logic

### `<Calculation, scoring or domain rule>`

- Authoritative source: `<PLACEHOLDER>`
- Invariant: `<PLACEHOLDER>`
- Common misinterpretation: `<PLACEHOLDER>`
- Regression test: `<PLACEHOLDER>`

## Legacy and technical debt

For code that appears unused, document:

```text
what still calls it
what remains unverified
which consumers must be checked
when deletion is actually safe
```

Do not turn this file into a general cleanup backlog.

## Keeping pitfalls current

When a pitfall is permanently resolved:

1. retain a short historical decision only if the lesson remains useful
2. remove rules that no longer apply
3. update references to the old limitation

`pitfalls.md` protects the current system; it is not a museum of every past defect.
