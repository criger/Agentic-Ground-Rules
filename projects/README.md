# Project instruction folders

This directory shows how shared engineering rules become concrete project context.

## Contents

| Directory | Purpose |
| --- | --- |
| `general-project-commands/` | Flexible intake checklist and document templates. |
| `example-java-api/` | Compact instructions for a small backend service. |
| `example-react-frontend/` | Frontend context with API and browser-state boundaries. |
| `example-fullstack-platform/` | Multi-repository context with deployment, security and handover. |

All `example-*` projects are fictional. Their repository names, commits, users and operational state exist only to demonstrate precise writing.

## Adding a real project

1. Complete `general-project-commands/project-intake.md` from source evidence.
2. Create `projects/<project-name>/`.
3. Start with `README.md` and add only the documents the project needs.
4. Add a small `AGENTS.md` that routes the agent to the relevant files and project-specific constraints.
5. Remove all template guidance and placeholders.
6. Keep global rules in `global/`; do not copy them into the project.

A small project may need four files. A production platform may need ten. Document risk and complexity, not symmetry.
