# Project intake before writing instructions

## Purpose

Use this checklist when a new or existing codebase needs a project folder.

The goal is to gather enough evidence for useful context without guessing, over-documenting or accidentally treating an old README as current truth.

## 1. Clarify the assignment

```text
Project name:             <PLACEHOLDER>
Requested outcome:        <PLACEHOLDER>
Documentation scope:      <whole project | subsystem | feature | migration | other>
Current task:             <PLACEHOLDER>
```

Clarify whether the instructions cover:

- one repository or several
- the whole product or one bounded area
- production, prototype, learning or a library
- development, debugging, operations or documentation

## 2. Map repositories and relationships

For every repository:

| Field | Value |
| --- | --- |
| Repository | `<owner/repo>` |
| Role | `<frontend/backend/library/infrastructure/content/...>` |
| Default branch | `<PLACEHOLDER>` |
| Working branch | `<PLACEHOLDER or not selected>` |
| Verified commit | `<SHA or not verified>` |
| Last inspected | `<YYYY-MM-DD>` |
| Merge/deploy consequence | `<PLACEHOLDER>` |

Also check:

- whether repositories must be sibling directories
- whether a package is a local, workspace or registry dependency
- whether backend, migrations or infrastructure live elsewhere
- whether existing documentation links to outdated repositories
- whether subprojects need separate instruction folders

## 3. Inspect actual source and configuration

Inspect at least:

```text
README and existing agent/contribution instructions
package and build files
dependency manifests, lockfiles, configured registries and security tooling
entrypoints and routes
configuration and environment variable names
authentication and authorization boundaries
API clients or public interfaces
database and migration sources
deployment workflows
test and lint configuration
```

Record exact paths. Do not call a file important merely because its name looks plausible.

## 4. Describe the project without marketing language

Answer:

- Who uses it?
- Which problem does it solve?
- What are the main user or system flows?
- What is explicitly outside the project?
- Which lifecycle phase is it in?
- Which parts are critical to value or operation?

Separate desired direction from functionality that actually exists.

## 5. Map architecture and contracts

Identify:

- runtime components and responsibilities
- data flow and ownership
- API, event and file contracts
- state and persistence
- external integrations and data sources
- caching, polling, retry and idempotency
- authentication, session and ownership boundaries
- build, release and deployment flow
- observability, error handling and rollback
- runtime, framework and package compatibility constraints
- approved registries, dependency ownership and version policy

Look for implicit contracts that appear cosmetic: CSS import order, relative base paths, peer dependencies, cookie credentials or fixed storage keys.

## 6. Map security and data risk

Document only project-specific concerns:

- private or sensitive data
- where access is actually enforced
- resource and operation ownership
- client-side gates that are only presentation
- payment or transactional rules
- configuration that must not reach the client or repository
- deletion, migration and cleanup risk
- direct and transitive dependency risk, provenance and license constraints

If the implementation was not inspected, write `not verified`.

## 7. Verify workflows

Find real commands for:

```text
installation
local startup
build
lint
automated tests
manual verification
deployment
cleanup or rollback
```

For testing, identify which realistic user and system scenarios are covered at unit, integration, contract, component and end-to-end level. Record important gaps instead of treating the existence of test files or a coverage percentage as proof.

For dependencies, identify the approved package sources, audit/scanning commands, supported runtime matrix and who must approve uncertain packages or versions.

Keep these statements distinct:

- a command exists
- it was run
- it succeeded
- the feature was runtime-tested
- the change was deployed

An unavailable build environment is not the same as a failed build.

## 8. Preserve relevant history

Look for:

- previous defects and regressions
- approaches that were tried and rejected
- external limitations or rate limits
- decisions that look strange without context
- manual operational steps
- legacy paths that cannot be deleted blindly
- deliberately deferred or excluded work

Document the reason, not only the rule.

## 9. Select the document package

Start with the README and create only useful files.

Create a specialized document when at least one is true:

- the topic has its own contract or test matrix
- it changes at a different pace
- several documents need to reference it without duplication
- only certain tasks need the detail
- the information is chronological and should remain outside current status

Do not create a special file for two paragraphs that belong naturally in a core document.

## 10. Write with evidence

For time-sensitive claims, include:

```text
as-of date
repository
branch and commit when relevant
environment
verification method
```

Use explicit wording:

```text
Observed in source at ...
Runtime-verified in ...
Reported by the project owner; not verified in source
Implemented, but the build was not run in this environment
Documentation conflicts with source and requires clarification
```

## 11. Final check

- repository URLs and paths exist
- branch and commit status is precise
- no secrets, private data or unauthorized material was copied
- global content is referenced rather than duplicated
- documents do not contradict one another
- implemented, tested and deployed are used correctly
- unverified assumptions are visible
- the reading order is task-oriented
- next steps have completion criteria
- handover identifies one concrete first action
