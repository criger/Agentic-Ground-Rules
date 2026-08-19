# ParcelFlow Platform deployment

> Fictional example. Real commands and environment controls must come from the actual repositories.

## Environments

```text
local -> test -> production
```

Test and production use separate databases, queues, identities and carrier credentials.

## Web

```text
feature branch
  -> lint + tests + build
  -> merge to main
  -> automatic static deployment
  -> smoke test deployed revision
```

A successful workflow is deployment evidence only when the expected revision is active and the smoke test passes.

## API

```text
feature branch
  -> test + publish
  -> merge to main
  -> version tag
  -> test deployment
  -> approval
  -> production rolling deployment
```

Apply backward-compatible migrations before code that requires them. Remove old columns or contracts only after old application revisions and consumers are gone.

## Infrastructure

```text
feature branch
  -> fmt + validate
  -> reviewed plan
  -> explicit environment approval
  -> apply
  -> resource and application verification
```

Never apply an unreviewed plan or infer infrastructure deployment from an application merge.

## Coordinated rollout

For additive API changes used by the web:

1. Deploy backward-compatible API support.
2. Verify it in the target environment.
3. Deploy the web consumer.
4. Observe errors and core flow.
5. Remove old API behaviour in a later delivery only when no consumer needs it.

## Rollback

- Web: redeploy the previous verified artifact.
- API: deploy the previous compatible image; avoid destructive migrations in the same step.
- Infrastructure: use a reviewed corrective plan, not an assumed automatic rollback.
- Messaging: preserve message compatibility or pause consumers before rollback.
