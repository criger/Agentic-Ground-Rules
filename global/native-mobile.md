# Native mobile (Android and iOS)

Native mobile apps add packaging, lifecycle, platform SDK and accessibility
constraints that differ from a web frontend. The same responsibility
boundaries apply, but the framework vocabulary changes.

## Architecture vocabulary

| Architectural role | Android (Jetpack Compose) | iOS (SwiftUI) |
| --- | --- | --- |
| View | `Composable` functions; `Screen`/`Modal` state and rendering | `View` structs and `ViewModifier` helpers |
| Controller / coordinator | `ViewModel` (StateFlow/state hoisting), navigation or screen coordinator | `@Observable`/`ObservableObject` view-model or coordinator |
| Model | domain objects and sealed-state types | `struct`/`enum` value types and result models |
| Service / use case | repository-facing use cases and feature workflows | use cases and application services |
| Repository / client | data-source wrappers for remote API and local storage | data-source protocols and client services |
| Persistence | Room/DataStore and DAOs behind a repository | SwiftData/CoreData or a repository protocol |
| Integration / mapper | OkHttp/Retrofit clients, JSON mappers | URLSession client, `Codable` mapping |
| Config | centralized constants and typed config objects | typed config/environment values |

## Mobile-specific rules

- Keep state and logic out of composable/view bodies. Hoist state into a
  view-model and let the platform bind it; a screen that calls APIs, maps data
  and owns domain state is a god screen.
- Treat the platform SDK version split (`minSdk`/`targetSdk`, iOS deployment
  target) as a contract that affects the installed base. Do not bump it
  casually.
- Keep composables and views focused on rendering, semantics and input
  delegation. Put data loading, parsing and business rules in the
  view-model/repository/client layers.
- Declare UI state from a single hoisted source. Prefer unidirectional state
  flow (state down, events up); avoid mutating shared globals from inside
  composables.
- Use a single real `OkHttpClient` (or equivalent) and reuse it. Register
  interceptors once, avoid double registration across modules/build variants,
  and document interceptor order.
- Keep external services (network clients, location, storage) behind one
  authoritative source. Do not duplicate endpoint URLs, headers or credentials
  across screens.
- Prefer Kotlin `Result` or `sealed` result types and explicit failure handling
  over bare exceptions or hidden nulls where a rule or result needs to be
  surfaced.
- Keep suspend functions on the `Dispatchers` appropriate to their work; do not
  block the main thread with network or disk I/O.
- Guard against async response races and cancelled scopes when UI state can
  change or the composable leaves composition.
- Keep user-visible strings in a central localization source, not inline.
  Accessibility labels and semantics are content, not styling.
- Preserve the app's privacy and accessibility posture. These are product
  constraints a refactor must not silently remove.
- Preserve existing `applicationId`/namespace mismatch and platform-version
  choices unless the task explicitly changes them.

## Release/signing considerations

See `security.md` for the signing and publishing credentials subsection. Release
signing keys, store passwords and company keystores are a distinct secret class
that is backup-critical and not rotatable. Never commit keystores,
`keystore.properties` or equivalent local credential files.