# Git workflow

## Default model

- Do not commit directly to a protected or production branch unless the repository explicitly allows it for the current task.
- Use a focused feature branch for changes that require review or validation.
- Inspect the diff before committing.
- Commit only files that belong to the requested change.
- Use clear, terse commit messages that describe the outcome.
- Do not force-push or rewrite shared history without explicit approval.

## Recommended workflow

1. Verify the default branch and deployment consequences.
2. Create or use the agreed feature branch.
3. Make a focused change.
4. Run relevant tests, lint and build checks.
5. Review the complete diff.
6. Commit and push the feature branch.
7. Open or update a review request.
8. Merge only when the change is ready for the target environment.
9. Verify deployment separately when merge does not prove runtime state.

## Status language

Keep these states distinct:

```text
Committed  The change exists in Git history.
Pushed     The commit exists on the remote branch.
Merged     The target branch contains the change.
Deployed   The intended environment is confirmed to run it.
Verified   The expected behaviour was observed or tested.
```

Repository-specific deployment rules belong in the relevant project folder.
