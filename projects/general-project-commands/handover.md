# `<PROJECT>` handover

> Template: Keep this as a short operational transfer. Lasting facts belong elsewhere.

## Updated

```text
Date:                 <YYYY-MM-DD>
Active task:          <PLACEHOLDER>
Source repository:    <owner/repo>
Working branch:       <branch>
Latest relevant SHA:  <commit or not verified>
Environment:          <local/test/production>
```

For several repositories:

| Repository | Branch | SHA | Role in the task |
| --- | --- | --- | --- |
| `<owner/repo>` | `<branch>` | `<SHA>` | `<PLACEHOLDER>` |

## Session goal

```text
<short and concrete>
```

## Completed

- `✅ <change>` — `<verification>`

Do not mark a change deployed without explicit deployment evidence.

## In progress or incomplete

- `🟡 <work>` — `<exact stopping point>`

## Decisions

- `<decision>` — `<reason>`

Move lasting architecture decisions to `architecture.md` or `decisions.md` and link them here.

## Changed or central files

```text
<path>  <change or relevance>
```

## Verification actually run

| Check | Result | Notes |
| --- | --- | --- |
| `<build/test/manual scenario>` | `<passed/failed>` | `<PLACEHOLDER>` |

## Not verified

- `<build, test, runtime, deployment, migration or consumer>`

## Blockers

- `<blocker>` — `<impact and required resolution>`

If none: `No known blocker for the next action.`

## First next action

```text
1. <one concrete action>
2. <the next action if it succeeds>
```

Keep the longer backlog in `next-steps.md`.

## Contracts to preserve next session

- `<only rules directly relevant to the active task>`

## Documentation still requiring synchronization

- `<file and reason>`

If none: `No known documentation drift.`

## Handover hygiene

At the next significant work session:

1. replace this operational snapshot
2. do not retain a growing duplicate of `current-status.md`
3. move lasting lessons to `pitfalls.md`, `architecture.md` or a specialized document
4. verify branch and commit again before changing source
