# Testing strategy

Tests must provide evidence about real behaviour, not merely repeat the implementation in another file.

A useful test would fail when the relevant contract or user-visible behaviour is broken and pass when it is correct. A test that only confirms that the current lines of code execute is not enough.

## Test behaviour and contracts

- Describe the scenario, action and expected outcome in domain language.
- Test public behaviour, business rules and meaningful side effects rather than private implementation details.
- Do not make mock-call assertions the only evidence unless the interaction itself is the contract.
- Include negative paths and prove that forbidden outcomes do not occur.
- Keep assertions specific enough to detect a real regression.
- Treat code coverage as a diagnostic signal, not a quality target or proof of correctness.

## Model realistic scenarios

Use production-shaped but synthetic, anonymized or explicitly approved test data. Never copy sensitive production data into tests casually.

Cover the scenarios that are relevant to the feature:

- the normal user or system workflow
- boundary values, empty input, malformed input and large input
- authentication, authorization, ownership and tenant separation
- duplicate requests, retry, idempotency and partial failure
- timeouts, unavailable dependencies and degraded responses
- concurrency, ordering and race conditions
- time zones, locale, encoding and numerical precision
- serialization, schema compatibility and migrations
- restart, recovery and rollback behaviour

Do not add every category mechanically. Select cases from the real risks and contracts of the change.

## Use the right test level

| Level | Primary evidence |
| --- | --- |
| Unit/domain | isolated rules, calculations, validation and edge cases |
| Integration | real collaboration with database, filesystem, queue, framework or controlled service boundary |
| Contract | request, response, event, schema and compatibility expectations between components |
| Component/UI | rendering, state transitions, accessibility and user interaction |
| End-to-end | a small number of critical workflows through the assembled system |

Fast unit tests and realistic integration tests solve different problems. Neither replaces the other.

Use fakes or mocks to isolate a unit or an external system that cannot safely participate in the test. Do not use them to avoid testing the database mapping, framework configuration, serialization or other integration that the change actually depends on.

## Regression tests

For a defect:

1. Reproduce the failure precisely.
2. Add a test that fails for the verified defect when practical.
3. Apply the smallest complete fix.
4. Run the focused regression test.
5. Run the broader affected suite and build.

The regression test should express the broken behaviour, not freeze the internal structure that happened to contain the bug.

## Test quality

- Keep tests deterministic, independent and repeatable.
- Control clocks, randomness and asynchronous completion where relevant.
- Do not depend on test execution order or shared mutable state.
- Name tests so the scenario and expected behaviour are obvious.
- Keep setup readable and use builders or fixtures only when they clarify the scenario.
- Apply normal code-quality rules to test code without hiding intent behind excessive abstraction.
- Treat flaky tests as defects; do not mask them with blind retries.
- Make failures explain what contract broke.

## Verification and reporting

- Run the new or changed test and the relevant affected suites.
- Run integration, contract or end-to-end checks when the change crosses those boundaries.
- State the exact commands or checks that were run and their result.
- Distinguish tests that exist from tests that were actually executed.
- Never claim that tests passed when they were not run or their result was not observed.
- Report important scenarios that remain untested and why.

Project-specific test commands, environments, fixtures and critical workflow matrices belong in the relevant project documentation.
