# Agent entrypoint

This repository is the canonical source for a public, model-agnostic agent instruction framework. Treat the Markdown files as operational instructions and reusable examples, not as product source code.

## Startup sequence

1. Read `global/README.md`.
2. Read the files in `global/` in the order listed there.
3. For project work, read `projects/AGENTS.md`, then the selected project's `AGENTS.md` and `README.md`.
4. Read only the project files relevant to the task. Do not load unrelated examples without a concrete reason.
5. When applying the framework to a real project, inspect the actual source, tests, configuration and runtime evidence before making technical claims.

## Instruction hierarchy

- Within repository defaults, an explicit current user instruction takes precedence unless it conflicts with higher-level platform instructions.
- Project instructions specialize the global rules for one project.
- Project instructions must not silently weaken global quality, security or verification requirements.
- Current source code, tests and reproducible runtime observations determine actual system behaviour.

## Public repository rules

- Keep `global/` project-independent.
- Keep the template generic and placeholder-based.
- Keep every `example-*` project clearly fictional.
- Never copy employer, customer, private repository or personal data into examples.
- Never include secrets, credentials, tokens or production connection details.
- Keep adapter files short. Rules belong in one authoritative location and are referenced rather than duplicated.
- Preserve the repository's CC BY 4.0 licensing and attribution notices.
