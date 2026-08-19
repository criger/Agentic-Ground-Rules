# `<PROJECT>` context

> Template: Keep only relevant sections and replace every placeholder.

## What the project is

`<PROJECT>` is `<short, concrete description>`.

It is used by:

- `<user group or consumer>`
- `<another actor when relevant>`

The primary problem it solves is:

```text
<PLACEHOLDER>
```

## Repositories and responsibilities

| Repository | Responsibility | Active baseline |
| --- | --- | --- |
| `<owner/repo>` | `<frontend/backend/library/...>` | `<branch + commit/as-of>` |
| `<owner/repo>` | `<optional>` | `<branch + commit/as-of>` |

Describe the relationship when repositories must change, build or deploy together.

## Current lifecycle phase

```text
<prototype | active development | pilot | production | maintenance | learning>
```

Explain what the phase means operationally. Do not mix desired direction into existing functionality.

## Main user or system flows

### `<Flow 1>`

```text
<start>
  -> <step>
  -> <result>
```

### `<Flow 2>`

```text
<start>
  -> <step>
  -> <result>
```

## Ownership and scope boundaries

The project owns:

- `<PLACEHOLDER>`

The project does not own:

- `<backend, authentication, external source, consumer policy or other>`

Treat a change crossing this boundary as an explicit contract change.

## Data, state and persistence

| Data/state | Location | Owner/authority | Important contract |
| --- | --- | --- | --- |
| `<PLACEHOLDER>` | `<browser/API/database/file/...>` | `<PLACEHOLDER>` | `<PLACEHOLDER>` |

Include stable storage keys, cache formats, TTL, migrations or server-side ownership only when they affect future work.

## Critical concerns

### Security and privacy

- `<project-specific rule>`
- `<authoritative enforcement point>`
- `<anything not verified>`

### Business or domain-critical logic

- `<transaction, calculation, source of truth, access level or other>`

### Operations and hosting

- `<runtime, hosting, subfolder, manual deployment or other>`

## Important source files

```text
<path>  <responsibility>
<path>  <responsibility>
```

Keep this a useful starting map, not a complete file inventory.

## Evidence priority for project facts

```text
1. <primary evidence>
2. <secondary evidence>
3. <snapshot or documentation with caveat>
```

Explain how conflicts are handled and when generated or external material is considered current.

## Known unknowns

- `<question that must be verified before relevant work>`

## Project-specific agent rules

1. Read `global/` first.
2. Read `<project-specific order>`.
3. Inspect actual source on a verified branch before changing it.
4. `<rule that genuinely specializes the global standard>`.

Do not repeat the full global contract here.
