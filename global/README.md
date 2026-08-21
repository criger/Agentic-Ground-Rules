# Global instructions

This directory contains project-independent working agreements.

They apply to every project unless a project file explicitly explains how the rule is specialized for that project's real architecture or constraints.

## Recommended reading order

1. `assistant-contract.md`
2. `response-style.md`
3. `workflow.md`
4. `architecture.md`
5. `coding-style.md`
6. `security.md`
7. `native-mobile.md`
8. `git-workflow.md`

## Mental model

Think of `global/` as an interface or abstract base class:

```text
global/
  Shared engineering contract

projects/<project>/
  Project-specific implementation and context
```

Project instructions may adapt names and folders to a language or framework. They should not silently weaken clear responsibility boundaries, MVC, DRY, security or evidence requirements.
