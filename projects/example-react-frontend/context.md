# Community Events Web context

> Fictional example.

## Users and flows

Anonymous visitors can browse and filter published events. Signed-in users can save favourites. Organizers can create and edit events they own.

```text
Browse
  -> load published events
  -> filter locally and through query parameters
  -> open event details

Organizer edit
  -> load current event
  -> edit draft
  -> submit to API
  -> invalidate event queries
```

## Scope boundary

The frontend owns:

- presentation and interaction
- route-level coordination
- client-side form validation for usability
- remote-state caching
- safe persistence of non-sensitive UI preferences

The frontend does not own:

- authentication sessions
- authorization or organizer ownership
- canonical event status
- notification delivery

## Browser state

| State | Location | Authority |
| --- | --- | --- |
| Session | HTTP-only cookie | API |
| Events | Query cache | API response |
| Filter preferences | `community-events.filters.v1` | Browser/user |
| Unsaved event draft | Component state | Current browser tab |

No token or private event payload belongs in local storage.

## Evidence priority

1. Current frontend source and tests.
2. Observed API responses in the test environment.
3. Published API contract in `api.md`.
4. Older UI documentation.

When observed API behaviour conflicts with `api.md`, record the difference and coordinate with the API owner.
