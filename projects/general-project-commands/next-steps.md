# `<PROJECT>` recommended next steps

> Template: This is not automatically a product roadmap. Record selected work and its safe sequence.

## Active goal

```text
<one clear outcome for the next delivery>
```

Why this is next:

- `<user need, defect, risk or dependency>`

If no task is selected, state that explicitly and list only real candidates under deferred work.

## Preconditions

1. `<verify branch/commit>`
2. `<read relevant evidence>`
3. `<establish build/test baseline>`
4. `<resolve backend, data, design or external dependency>`

## P0: safe baseline

```text
<install/build/test/backup/feature flag/access>
```

Complete when:

- `<measurable control>`

## P1: smallest complete delivery

### Scope

- `<concrete change>`

### Affected areas

```text
<repository/path>
<API/database/integration>
```

### Completion criteria

- `<observable functional behaviour>`
- `<security/ownership requirement>`
- `<backward compatibility>`
- `<documentation update>`

### Verification

```text
<automated commands>
<manual scenarios>
<environments/roles/devices>
```

## P2: follow-up

- `<polish, expanded testing, cleanup or observability>`

Do not pull P2 into P1 when it makes the first delivery unnecessarily large.

## Dependencies and decisions

| Topic | Needs | Owner/source | Status |
| --- | --- | --- | --- |
| `<PLACEHOLDER>` | `<decision/data/access>` | `<PLACEHOLDER>` | `<open/resolved/blocked>` |

## Deferred or not selected

- `<idea>` — `<why it is not active>`

Do not present deferred ideas as an agreed roadmap.

## Out of scope

- `<explicit non-goal for this delivery>`

## Documentation updated on completion

- `current-status.md`
- `handover.md`
- `<architecture/api/pitfalls/feature log when contracts changed>`
