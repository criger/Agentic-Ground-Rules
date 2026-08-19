# Community Events Web pitfalls

> Fictional example.

## Removing credentials breaks authenticated requests

The session is stored in an HTTP-only cookie. Preserve `credentials: 'include'` in the shared API client. A public list may still work without it, hiding the regression until an authenticated flow is tested.

## Route guards are not authorization

Hiding organizer routes is UX only. The API must verify session and event ownership on every protected operation.

## Effect-driven request loops

Do not place unstable option objects or functions in effects that trigger requests. Prefer TanStack Query keys derived from stable primitive values and explicit mutation handlers.

Test rapid filter changes and navigation for stale results.

## Storage-key migrations

`community-events.filters.v1` stores non-sensitive preferences. If its shape changes, either keep backward-compatible parsing or introduce a new versioned key. Do not let invalid persisted JSON prevent the app from starting.

## Query invalidation after mutation

Successful organizer edits must invalidate both the event detail and relevant list queries. Updating only local component state produces stale data after navigation.
