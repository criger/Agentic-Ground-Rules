# ParcelFlow Platform security

> Fictional project-specific security context. Global security rules still apply.

## Trust boundaries

```text
Browser input              untrusted
Authenticated API claims   trusted only after issuer/audience/signature validation
Carrier webhook            untrusted until signature and account mapping succeed
Database records           authoritative within tenant and transaction rules
Queue message              authenticated transport, still validated by handler
```

## Tenant isolation

- Tenant ID is derived from validated claims.
- Client-supplied tenant IDs are ignored as authority.
- Repository methods require tenant scope for every tenant-owned entity.
- Support access uses a separate audited role and explicit tenant selection.
- Logs must not combine sensitive payloads across tenants.

## Carrier credentials and labels

- Carrier credentials are server-side secrets referenced through environment configuration.
- Credentials and raw authorization headers are never logged.
- Labels are private documents and require shipment ownership/role authorization.
- Temporary label URLs must be short-lived and tenant-bound.

## Webhook verification

1. Read the raw request bytes required by the carrier signature scheme.
2. Resolve the expected carrier account without trusting payload ownership fields.
3. Verify timestamp and signature using constant-time comparison where applicable.
4. Reject stale or invalid requests before deserialization drives domain actions.
5. Deduplicate by carrier account and external event ID.

## Abuse and failure cases to test

- valid entity ID from another tenant
- replayed webhook event
- valid signature for the wrong carrier account
- expired label URL
- duplicate create request during a timeout
- support role without explicit tenant context

Security-relevant failures should be observable without logging secrets or full private payloads.
