# Community Events Web API contract

> Fictional client-observed contract. Backend implementation is outside this example.

## Base behaviour

- Requests use relative `/api` paths through the hosting proxy.
- Authenticated requests include browser credentials.
- JSON errors use `{ "code": string, "message": string }` when the backend follows the published contract.
- Unknown error bodies are normalized to a safe generic UI error.

## Key endpoints

| Method/path | Purpose | Authentication |
| --- | --- | --- |
| `GET /api/events` | list published events | public |
| `GET /api/events/{id}` | event details | public or authorized private view |
| `POST /api/events` | create organizer event | required |
| `PUT /api/events/{id}` | edit owned event | required + ownership |
| `GET /api/me/favourites` | load favourites | required |
| `PUT /api/me/favourites/{eventId}` | save favourite | required |

## Compatibility rules

- Do not remove or rename response fields without coordinated backend rollout.
- Treat unknown additive fields as compatible.
- Never infer ownership from a user ID supplied by the browser.
- A `401` starts the existing sign-in flow; a `403` remains an authorization error.
- Do not automatically retry non-idempotent create/update requests.

## Verification when this contract changes

1. Update typed client models and mappers.
2. Update mock handlers and unit tests.
3. Verify the affected endpoint in a test environment.
4. Run the relevant Playwright flow.
5. Coordinate backend deployment order.
