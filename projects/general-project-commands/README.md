# General project instruction template

## Purpose

This directory is a working template for project-specific context under:

```text
projects/<project-name>/
```

Use it as inspiration and a checklist, not a rigid schema. A small library, a frontend with a separate backend, a learning project and a production platform do not need identical documentation.

Read `global/` first. The project folder describes concrete facts and specializes global rules only when necessary.

## Most important principle

Create the smallest document package that gives a new agent session enough correct context to work safely.

That means:

- do not create empty files to satisfy the template
- do not copy global rules into every project
- do not invent unverified facts
- distinguish source code, documentation, runtime observations and stakeholder statements
- state precisely what is implemented, built, tested, deployed, blocked or unknown
- use specialized files when one area needs substantially more detail than the rest

## Before writing the project folder

Use `project-intake.md` to identify:

1. source repositories, branches and relationships
2. what the project actually does and does not do
3. architecture, data, security and integration boundaries
4. available build, test and deployment workflows
5. current status and latest verified baseline
6. known pitfalls, failed attempts and decisions that must be preserved
7. which documents the project genuinely needs

If source is available, inspect it before documenting project facts. Existing READMEs and chat history are useful leads, not automatic truth.

## Recommended core

| File | Responsibility | Create when |
| --- | --- | --- |
| `README.md` | entrypoint, repositories, purpose, reading order and local rules | normally always |
| `context.md` | product/domain context, scope, actors and critical concerns | the README cannot stay concise |
| `architecture.md` | components, data flow, system boundaries and lasting contracts | architecture affects how changes must be made |
| `current-status.md` | dated evidence for implementation, tests, deployment and deviations | the project is active or has several deliverables |
| `next-steps.md` | selected goal, safe sequence and completion criteria | work is planned or active |
| `pitfalls.md` | concrete regressions, failed approaches and invariants | important knowledge would otherwise be forgotten |
| `handover.md` | short operational transfer from the latest work session | work continues across sessions or people |

A small stable project may use only `README.md`, `current-status.md` and `pitfalls.md`. A complex project may use all core documents plus specialized ones.

See `optional-files.md` before adding another document type.

## Adapt to project shape

| Project shape | Typical emphasis |
| --- | --- |
| One small repository | short README, status and pitfalls may be enough |
| Frontend and backend | repository ownership, API contracts and separate deploy flows |
| Native mobile app | package/signing release flow, platform SDK versions, accessibility and privacy as product constraints, single source for network/config |
| Library and consumer | public API, peer dependencies and testing in a real consumer |
| Monorepo or project family | shared root context with nested context for genuine differences |
| Learning/content project | sources, factual baseline, originality and practical verification |
| Production data system | ownership, access, migrations, observability, rollback and deploy boundaries |
| Integration project | external contracts, rate limits, retry, idempotency and fallback |

## Keep document responsibilities separate

```text
README.md
  Where do I start, what must I read, and which repositories are involved?

context.md
  Why does the project exist, who uses it, and what are its boundaries?

architecture.md
  How does the system fit together, and which contracts must survive?

current-status.md
  What is true now, and what evidence supports it?

next-steps.md
  What work is selected, in which order, and what means complete?

pitfalls.md
  What has failed or may regress, and why?

handover.md
  Where did the latest work stop, what was verified, and what happens first next?
```

Lasting decisions normally belong in `architecture.md`, `pitfalls.md` or `decisions.md`. Chronological deliveries may use `implementation-log.md`. Do not turn `handover.md` into an unlimited historical archive.

## Source priority

Define a project-specific evidence order. A useful default is:

```text
1. Recent, reproducible runtime or production observation
2. Current source, migrations and configuration on a verified branch/commit
3. Official external specifications or vendor documentation
4. Maintained project documentation with a known baseline
5. Old READMEs, work logs and chat memory
```

The order is not universal. A generated schema may be authoritative when it was just regenerated, but only a snapshot when its origin is unknown.

When sources conflict, document the conflict. Do not silently choose the convenient answer.

## Precise status language

```text
Implemented
  The code or content exists.

Build-verified
  The relevant build was actually run with the stated result.

Tested
  The named automated or manual tests were actually run.

Runtime-verified
  The behaviour was observed in the relevant environment.

Deployed
  The change is confirmed published to the named environment.

Blocked
  A stated dependency or defect prevents completion.

Not verified
  Evidence is currently insufficient.
```

Do not use "done" when files were only written. A merge is not always a deployment.

## Recommended reading order

```text
1. global/
2. projects/<project>/README.md
3. context.md and architecture.md when present
4. current-status.md
5. only task-relevant specialized files
6. pitfalls.md
7. handover.md and next-steps.md when continuing work
8. actual source on a verified branch/commit
```

The project README may define a different order when its architecture requires it.

## Creating a new project folder

1. Copy only relevant template files.
2. Replace every `<PLACEHOLDER>` value.
3. Remove template guidance from the finished documents.
4. Add project-specific context, not new global standards.
5. Verify repository URLs, branches, commits, paths and commands.
6. Match status words to real evidence.
7. Give each fact one natural home and link to it elsewhere.
8. Read the result as a new agent session with no chat history.

## Update the project folder when

- repository, branch or deployment models change
- public APIs, data formats or integration contracts change
- authentication, ownership, privacy or another security boundary changes
- an important architectural decision or evidence priority changes
- runtime behaviour, fallback or third-party limitations become known
- the selected delivery or blocker changes
- evidence moves a feature from implemented to tested or deployed
- a reproducible mistake would otherwise be repeated

Small cosmetic changes do not automatically require documentation updates.
