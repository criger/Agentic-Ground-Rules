# Optional project files

Create an additional document when it makes reading more targeted or prevents the same contract from being copied elsewhere.

Do not create every file in this list by default.

## Common options

| File | Use when | Typical contents |
| --- | --- | --- |
| `api.md` | API, event or component contracts are central | authentication, shapes, errors, polling, compatibility |
| `deployment.md` | deployment is multi-step, risky or different per repository | environments, branch rules, migrations, rollback |
| `testing.md` | the project has a substantial test strategy or manual matrix | commands, fixtures, roles, devices, E2E scenarios |
| `decisions.md` | lasting choices need rationale | date, options, consequences, revisit criteria |
| `data-model.md` | ownership and relationships are complex | schema source, entities, relationships, migrations |
| `security.md` | the project has material rules beyond `global/security.md` | trust boundaries, roles, ownership, abuse cases |
| `operations.md` | operation needs manual or scheduled actions | jobs, observability, alerts, backup, recovery |
| `prompts.md` | AI prompts are a versioned product contract | inputs, outputs, guardrails, evaluation, model requirements |
| `reusable-blueprint.md` | the project produces repeated subprojects | creation process, variation points, validation |
| `implementation-log.md` | chronological deliveries must be retained | date, change, branch/PR, tests, deployment |
| `<feature>.md` | one feature has its own data, API or test contract | bounded implementation and maintenance context |
| `<topic>-YYYY-MM-DD.md` | a milestone or investigation must remain a snapshot | evidence, decisions and outcome from that date |

## When to create a subdirectory

Use a subdirectory when an area:

- is maintained independently
- has its own evidence or domain baseline
- has a separate build/test/deploy flow
- has local rules that would make root project files unclear

```text
projects/<project>/
├─ README.md
├─ context.md
├─ architecture.md
└─ <subproject>/
   ├─ AGENTS.md
   ├─ README.md
   ├─ implementation.md
   └─ testing.md
```

Keep only genuinely shared context at the project root.

## Decisions format

```text
## YYYY-MM-DD — <decision>

Context:
<why a choice was required>

Decision:
<what was selected>

Alternatives:
- <alternative and reason rejected>

Consequences:
- <benefit>
- <cost or risk>

Revisit when:
- <concrete criterion>
```

## File naming and linking

- use short, descriptive kebab-case names
- use dates only for intentional historical snapshots
- link each specialized file from the project README and say when to read it
- identify the source of truth when several documents touch one topic
- remove or clearly mark outdated documents

## Questions before creating another file

```text
Will it reduce duplication?
Will only certain tasks need the detail?
Does the topic have its own lifecycle or contract?
Do we know which existing file will stop owning this information?
Will the project README explain when to read it?
```

If most answers are no, use an existing document.
