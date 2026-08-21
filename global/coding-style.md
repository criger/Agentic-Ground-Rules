# Coding style

## General rules

- Prefer readable code over clever code.
- Follow the project's documented MVC structure and dependency direction.
- Follow DRY and give shared semantics one natural home.
- Use names that describe role and domain intent.
- Preserve established formatting and idioms when they do not violate documented architecture or safety constraints.
- Avoid new dependencies unless they clearly solve the problem.
- Keep changes focused and easy to review.
- Optimize for the next developer who must understand and debug the code without knowing its history.

Detailed layer responsibilities are defined in `architecture.md`.

## Classes, components and modules

Each class, component or module should have one primary responsibility.

Names such as `Manager`, `Processor`, `Common`, `Utils` and `Helper` are warning signs when the contents span several domains.

Split responsibilities deliberately:

- business rules into a service or use case
- persistence into a repository
- external communication into a client or integration
- mapping into a mapper
- validation into a validator or domain model
- rendering into focused views or components
- connection lifecycle into the data layer

Do not create files merely to reduce line counts. Every extracted unit needs a coherent role.

## Methods and functions

A method should normally do one thing at one abstraction level.

Consider splitting when it:

- has several distinct phases
- mixes validation, data access, calculation and presentation
- contains deep nesting or early side effects
- needs comments to label every block
- takes many primitives that represent one concept
- returns or mutates several unrelated results

Prefer:

- guard clauses over deep conditional pyramids
- small named operations over long inline expressions
- immutable data when it makes flow safer and clearer
- explicit errors over hidden fallbacks
- dependency injection over constructing heavy dependencies inside domain logic

## DRY in practice

Do not duplicate:

- business rules
- equivalent validation or ownership checks
- mapping and normalization
- queries with the same purpose
- API request/response handling
- constants, URLs and configuration
- complex UI behaviour

When one change must be repeated across files, find the shared semantic source.

Avoid over-generalization. Do not build a framework for one case or force unrelated use cases into a function with many boolean flags.

## Naming

- Use domain language instead of generic technical buckets.
- Name interfaces after the capability they provide.
- Name repositories after the domain data they persist.
- Name controllers after the request or feature area they coordinate.
- Name services and use cases after an action or business responsibility.
- Use `Dto`, `Request`, `Response`, `Entity`, `Model` and `ViewModel` consistently when the project distinguishes them.
- Boolean names should read like state or capability: `isActive`, `hasAccess`, `canRetry`.

## Comments and code documentation

- Let names and structure explain what the code does.
- Use comments for why, external constraints and non-obvious historical context.
- Do not retain comments that only restate the next line.
- Document surprising fallback, rate-limit, security or framework workarounds.
- Update or remove comments when behaviour changes.

## Java and C#

- Keep controllers thin.
- Put business logic in services/use cases.
- Keep persistence in repositories/data access.
- Place interfaces at meaningful boundaries.
- Use dependency injection for services, repositories and integration clients.
- Separate entities/domain models from API DTOs when their needs differ.
- Do not move all controller logic into one equally broad service.
- Prefer centralized exception/error handling over repeated controller `try/catch` blocks.

## Kotlin and Android

- Keep composables and views focused on rendering, semantics and input
  delegation. Put data loading, parsing and business rules in the
  view-model/repository/client layers.
- Declare UI state from a single hoisted source. Prefer unidirectional state
  flow (state down, events up); avoid mutating shared globals from inside
  composables.
- Use a single real `OkHttpClient` (or equivalent) and reuse it. Register
  interceptors once, avoid double registration across modules/build variants,
  and document interceptor order.
- Keep endpoint URLs, headers, timeouts and other integration constants in one
  centralized configuration object. Do not reinvent them across screens.
- Prefer Kotlin `Result` or `sealed` result types and explicit failure handling over bare
  exceptions or hidden nulls where a rule or result needs to be surfaced.
- Keep suspend functions on the `Dispatchers` appropriate to their work; do not
  block the main thread with network or disk I/O.
- Guard against async response races and cancelled scopes when UI state can
  change or the composable leaves composition.
- Keep user-visible strings in a localization source, not inline. Accessibility
  labels are content and belong beside the interactive element they describe.
- Preserve existing `applicationId`/namespace mismatch and platform-version
  choices unless the task explicitly changes them.

## JavaScript and React

- Prefer functional components when consistent with the project.
- Keep pages/components focused on rendering and delegation.
- Put API calls in clients, services or repositories.
- Put feature orchestration in focused controller hooks or use cases.
- Move models, schemas and normalization out of large component files.
- Split components by responsibility, not arbitrary line count.
- Keep state local unless sharing is required.
- Avoid unstable functions in effect dependency arrays.
- Guard against render loops, stale responses and unnecessary re-renders.
- Preserve existing UI behaviour unless the task changes it.

A hook also needs one responsibility. Moving a god component into one god hook does not solve the design problem.

## React effects

- Use effects only for synchronization with external systems.
- Keep dependencies correct and stable.
- Clean up intervals, subscriptions, observers and event listeners.
- Protect against stale async responses when selected state can change.
- Verify that effects triggering network calls cannot loop.
- Do not use an effect for data that can be derived during rendering or handled by an explicit event.

## PHP and Python

- Keep endpoints/routes thin and predictable.
- Validate and normalize transport input at the boundary.
- Move business logic to services/use cases or domain models.
- Isolate persistence and external clients behind focused modules or contracts.
- Use dedicated database infrastructure for connections and technical setup.
- Return errors consistently without leaking internal details.
- Log enough for diagnosis without logging secrets or personal data.
- Preserve existing endpoint contracts unless intentionally changed.

## SQL

- Use prepared statements or framework parameter binding.
- Never concatenate untrusted input into SQL.
- Keep queries in repository/data layers.
- Include ownership predicates where required.
- Make transaction boundaries explicit for operations that must succeed or fail together.
- Do not implement the same database/domain rule differently in several queries without a documented reason.

## CSS and layout

- Prefer stable layout over fragile visual tricks.
- Test desktop, narrow screens and relevant interaction modes.
- Avoid broad selectors that leak into unrelated views.
- Keep global, feature and component styling boundaries clear.
- Use absolute positioning only when the design genuinely requires it.
- Keep generated document/PDF layouts deterministic.

## Testing by layer

| Layer | Focus |
| --- | --- |
| Domain/services | rules, edge cases and failure behaviour |
| Repositories/data | queries, mapping and persistence integration |
| Controllers/API | contracts, validation, status codes and authorization |
| Views/components | rendering and user interaction |
| Integrations | transport mapping, failures, retry and fallback |

A refactoring that splits a god object should preserve behaviour with existing tests and targeted tests around the newly created boundaries.

## Documentation

- Update project architecture when responsibility or folder boundaries change.
- Record lasting decisions in the appropriate project document.
- Add reproducible regressions and failed approaches to `pitfalls.md`.
- Record actual implementation, test and deployment state with precise status language.
