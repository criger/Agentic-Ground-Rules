# `<PROJECT>` architecture

> Template: Document lasting boundaries and contracts. Put current delivery state in `current-status.md`.

## System overview

```text
<client or trigger>
  -> <component/service>
      -> <API, library or data store>
  -> <external integration>
```

## Components and responsibilities

| Component | Technology/repository | Owns | Does not own |
| --- | --- | --- | --- |
| `<PLACEHOLDER>` | `<PLACEHOLDER>` | `<PLACEHOLDER>` | `<PLACEHOLDER>` |

## Repository and dependency boundaries

Describe:

- included repositories
- dependency direction
- required build or directory order
- changes requiring coordinated commits or deployment
- public imports, interfaces, events or schemas

```text
<repository A>
  -> <dependency/API/event>
      -> <repository B>
```

## Runtime and data flow

### `<Main flow>`

```text
<input>
  -> <validation/normalization>
  -> <processing>
  -> <persistence or output>
```

Document alternative flows, retry, cache, polling and idempotency only when architecturally relevant.

## Contracts

### API, events and files

- `<request/response or event contract>`
- `<backward compatibility requirement>`
- `<consumers that must be verified together>`

Move extensive detail to `api.md` or another specialized document.

### State and persistence

- `<state owner>`
- `<database/local storage/cache/file>`
- `<format, TTL, migration or concurrency rule>`

### Authentication and authorization

```text
<login/session>
  -> <server-side identity>
  -> <ownership/role/entitlement check>
```

Mark client-side checks that are presentation only.

## Build, release and deployment

```text
<feature branch>
  -> <build/test>
  -> <merge>
  -> <automatic or manual deployment>
```

Document frontend, backend, database and shared package workflows separately when they differ.

## Architectural invariants

Do not change these as incidental cleanup:

- `<credential mode, peer dependency, relative base, ownership rule or other>`
- `<PLACEHOLDER>`

Explain why each invariant exists.

## Deliberate compromises and technical debt

| Area | Current choice | Why retained | Revisit when |
| --- | --- | --- | --- |
| `<PLACEHOLDER>` | `<PLACEHOLDER>` | `<PLACEHOLDER>` | `<PLACEHOLDER>` |

Include only conditions that affect real change decisions.

## Verification for architecture changes

```text
<build/test command>
<integration or consumer to test>
<roles/environments/devices to verify>
<rollback or compatibility check>
```

Update this document when component responsibilities, public contracts, data ownership, authorization boundaries, dependencies or deployment architecture change.
