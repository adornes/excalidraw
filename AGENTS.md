# AGENTS.md

## Cursor Cloud specific instructions

### Overview

Excalidraw is a Yarn 1 monorepo (Node >= 18). The Vite dev server runs at `localhost:3001`. All external services (Firebase, collab WebSocket, AI backend) are optional and point to remote dev instances by default — the core drawing experience works fully standalone.

### Key commands

See `CLAUDE.md` and root `package.json` scripts for the full list. Highlights:

- **Dev server**: `yarn start` (Vite, port 3001)
- **Lint**: `yarn test:code` (ESLint) and `yarn test:other` (Prettier)
- **Typecheck**: `yarn test:typecheck`
- **Tests**: `yarn test:update` (Vitest, updates snapshots, runs ~1400 tests)
- **Auto-fix**: `yarn fix` (Prettier + ESLint)

### Gotchas

- The pre-commit hook in `.husky/pre-commit` is commented out (lint-staged is disabled). You still need to run `yarn fix` and `yarn test:code` manually before committing.
- `yarn test:update` runs all tests with `--update --watch=false`; use this instead of `yarn test:app` when you want a single non-interactive pass.
- Firebase config warnings (`Error JSON parsing firebase config`) appear in test stderr for `excalidraw-app` tests — these are expected and harmless in CI/local without a real Firebase config.
- ESLint emits a benign `MetaProperty` warning from `jsx-ast-utils`; it does not fail the lint pass.
- The `--frozen-lockfile` flag should be used with `yarn install` to avoid unintended lockfile changes.
