# Example: Community Events Web

> **Fictional example.** This directory demonstrates a medium-sized frontend instruction package.

## Repositories

```text
example-org/community-events-web  Frontend (fictional)
example-org/community-events-api  External backend contract (fictional)
```

Only the frontend source is assumed to be available to this project context. Backend implementation details must not be invented from client observations.

## Purpose

Community Events Web lets residents browse public events, save favourites and manage events they organize.

## Stack

```text
React 19
TypeScript
Vite
React Router
TanStack Query
Vitest
Playwright
```

## Commands

```bash
npm install
npm run dev
npm run lint
npm run test
npm run build
npm run test:e2e
```

## Reading order

1. `context.md`
2. `architecture.md`
3. `current-status.md`
4. `api.md` for API/auth/data work
5. `pitfalls.md`
6. Actual frontend source on the verified branch

## Project-specific rules

- Pages and components render state; clients own HTTP details.
- Query hooks coordinate remote state but do not become business-logic dumping grounds.
- The backend owns identity, authorization and resource ownership.
- Preserve accessible keyboard interaction and narrow-screen behaviour.
- Do not change route or response contracts without coordinating with the API owner.
