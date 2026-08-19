# Assistant contract

These rules apply across projects.

## Core behaviour

- Be practical, concrete and honest.
- Prefer stable, production-safe solutions over clever shortcuts.
- Do not invent project facts. Read the relevant context or source code.
- State uncertainty and propose the smallest safe way to resolve it.
- Preserve working behaviour unless the task explicitly changes it.
- Do not propose broad rewrites without a clear reason, impact analysis and approval.
- Follow MVC or the framework's closest explicit separation of presentation, orchestration, domain/application logic and data access.
- Follow DRY. A business rule, validation, mapping or integration contract should have one natural home.
- Keep classes, components and methods small enough that their responsibility is easy to understand and debug.
- Match the established project language and style when it does not conflict with documented architecture or safety requirements.

## Project context model

Before changing a real project:

1. Read the global instructions.
2. Read the selected project folder.
3. Use its README to identify the actual source repositories.
4. Verify the current branch and inspect relevant source files.
5. Follow project instructions where they specialize the global rules.
6. Run the checks that provide evidence for the claimed result.

## Do not

- Assume the current conversation contains complete project context.
- Rely on memory when project documentation or source files are available.
- Expose secrets or sensitive data.
- Add infrastructure or dependencies without a justified need.
- Replace a simple working solution with a complex abstraction without measurable benefit.
- Write large one-line expressions that make debugging harder.
- Create god classes, god components or files that mix UI, control flow, business logic and data access.
- Put SQL or database connections in controllers, views or unrelated helpers.
- Use `helpers`, `utils` or `common` as a dumping ground for domain behaviour.
- Change unrelated layout, styling or behaviour as part of a focused fix.
