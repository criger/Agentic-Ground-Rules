# Security instructions

Security boundaries must be enforced by an authoritative server-side or infrastructure layer, not only by client-side visibility or agent instructions.

## Secrets

Never expose or commit:

- API keys, tokens or passwords
- database or OAuth credentials
- session secrets
- private keys or certificates
- production connection strings

Use configuration names and examples without real values.

### Signing and publish credentials

Release signing keys, store passwords, company keystores and store-publishing
credentials (Google Play, Apple App Store and similar) form a special secret
class that often lives in local, git-ignored files or CI secrets instead of a
server. They matter differently from ordinary credentials:

- A lost or corrupted signing key can permanently block updates to an already
  published client app or desktop package. Treat it as a backup-critical asset,
  not a rotatable password.
- Never commit keystores, signing certificates, `keystore.properties` or their
  equivalent local credential files.
- Keep store passwords and signing keys out of source, build logs, test output
  and generated artifacts.
- Document where release credentials are stored and who can recover them, with
  example variable names and no real values.

## User and business data

- Minimize access to personal, financial and confidential data.
- Do not copy production data into examples, logs or tests without an approved process.
- Verify resource ownership and authorization server-side.
- Do not trust client-provided user IDs, roles, prices or permissions.
- Preserve auditability for sensitive state changes.

## Transactions and asynchronous work

- Make retry and idempotency behaviour explicit.
- Prevent duplicate charges, grants, messages and writes.
- Define what happens when only part of an operation succeeds.
- Avoid hidden fail-open behaviour.

## AI-generated content

- Do not fabricate facts, experience, credentials, sources or test results.
- Preserve user review and control for consequential content.
- Treat model output as untrusted input until it is validated for its use case.
