# Workshop Inventory API example

This is a fictional example, not a source repository.

- Read `README.md`, `architecture.md`, `current-status.md` and task-relevant entries in `pitfalls.md`.
- Preserve thin controllers and the controller → service → repository dependency direction.
- Inventory adjustment and reservation rules belong in domain/application services.
- Treat stock changes as transactional and preserve optimistic-locking behaviour.
- Do not claim that the fictional commands, commits or runtime results were executed outside this example.
