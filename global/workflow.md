# Global workflow

## Starting work on a project

1. Read the relevant files in `global/`.
2. Read the selected project folder under `projects/`.
3. Use the project README to identify the actual source repositories.
4. Verify the current source branch and baseline.
5. Inspect the owning source files before proposing a code change.
6. Apply project-specific instructions where they specialize the global standards.

## Typical project documentation

A project may use:

```text
README.md
context.md
architecture.md
current-status.md
next-steps.md
pitfalls.md
handover.md
```

Optional documents include:

```text
api.md
data-model.md
decisions.md
deployment.md
operations.md
security.md
testing.md
<feature>.md
```

Use `projects/general-project-commands/` as a flexible template. Do not create empty documents merely to match the list.

## Before changing code

1. Identify the exact behaviour and owning architectural layer.
2. Find existing services, interfaces, repositories, clients, validators or components that already own part of the responsibility.
3. Confirm how the change follows the project's MVC structure and dependency direction.
4. Check whether the change would make a class, component, hook or module too broad.
5. Reuse existing semantic rules without creating an artificial abstraction.
6. Assess production, data, security and compatibility impact.
7. Establish a relevant build and test baseline when possible.
8. Prefer the smallest complete change with clear responsibility boundaries.

For new functionality, make ownership explicit:

```text
View / component
Controller / handler
Service / use case
Model / DTO
Interface / contract
Repository / client
Database / external integration
```

Create only the layers the feature needs, but do not mix responsibilities merely to reduce file count.

## Architecture check after a change

Before considering work complete:

1. Confirm that views and controllers did not gain database access or heavy business logic.
2. Confirm that one rule was not implemented differently in several places.
3. Confirm that new files have clear names and live in the correct area.
4. Confirm that interfaces and implementations point in the intended direction.
5. Confirm that helper folders did not become a dumping ground.
6. Run checks for each affected layer and build the affected deliverable.
7. Update project architecture documentation when a lasting boundary changed.

## Debugging sequence

1. Reproduce or precisely describe the current behaviour.
2. Find the last known working state when available.
3. Determine what changed.
4. Inspect client console and network evidence for frontend failures.
5. Inspect API responses and server logs for backend failures.
6. Locate the architectural layer that owns the defect.
7. Change one verified cause at a time.
8. Re-run the smallest useful regression test, then the broader affected checks.

Do not place a workaround in a view or controller when the defect belongs to a service, repository or integration.

## Keeping context current

Update the relevant project documents when work changes:

- verified source baseline
- implementation, build, test or deployment status
- architecture or public contracts
- known regressions and disproved assumptions
- the selected next task or blocker
- the operational handover point

Do not update documentation for unrelated cosmetic edits.

## Default priority order

1. Production stability
2. Data and security correctness
3. Core user or system flow
4. Transaction and integration correctness
5. Maintainable architecture
6. User experience polish
7. Nice-to-have improvements
