# Contributing

Contributions that make the framework clearer, safer or easier to adopt are welcome.

## Before contributing

- Do not submit employer, customer, private repository or personal information without authorization.
- Use fictional names and reserved/example values in sample projects.
- Never include secrets, tokens, credentials or working production endpoints.
- Put a rule in its one natural home instead of copying it between files.
- Keep the framework model-agnostic unless a file is explicitly a compatibility adapter.

## What makes a useful rule?

A useful instruction is:

- concrete enough that an agent can act on it
- understandable to a developer reviewing the change
- scoped to the smallest level where it consistently applies
- explicit about risk, evidence or the safe path
- free from tool-specific ceremony unless that tool genuinely requires it

Avoid vague persona statements such as "be a world-class developer". Describe the behaviour, boundary or verification that matters.

## Workflow

1. Create a feature branch.
2. Make one focused change.
3. Check links, placeholders and Markdown rendering.
4. Verify that examples remain fictional.
5. Open a pull request explaining what changed and why.

## Pull request checklist

- [ ] The change has one clear purpose.
- [ ] Global and project-specific rules are not duplicated.
- [ ] No private or sensitive information is included.
- [ ] New example facts are explicitly fictional.
- [ ] Links and referenced paths exist.
- [ ] The README or template index is updated when structure changes.

By contributing, you agree that your contribution may be distributed under the repository's CC BY 4.0 license.
