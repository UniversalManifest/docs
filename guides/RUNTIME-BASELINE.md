# Runtime Baseline and Toolchain Policy

This document defines the canonical local/CI runtime baseline for Universal Manifest development and deployment tooling.

## Canonical Baseline

- Node.js: `22.x` (repository baseline)
- Wrangler CLI: `4.67.0` (resolver workspace baseline)

Repository pinning:

- `/Users/grig/work/repo/universalmanifest/.nvmrc` -> `22`
- package engine fields:
  - `/Users/grig/work/repo/universalmanifest/site/package.json`
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/package.json`
  - `/Users/grig/work/repo/universalmanifest/services/myum-resolver/package.json`

## Why this policy exists

- Prevent local vs CI runtime drift.
- Keep resolver/runtime behavior reproducible across environments.
- Reduce deploy surprises caused by mixed Node versions.

## Local Setup

```bash
cd /Users/grig/work/repo/universalmanifest
nvm use
node --version
```

Expected major version: `22`.

## CI Policy

GitHub Actions workflows should use Node `22` unless an explicit exception is documented in the workflow file and in this document.

Primary workflow files:

- `/Users/grig/work/repo/universalmanifest/.github/workflows/ci.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml`

## Validation Commands

```bash
cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean
cd /Users/grig/work/repo/universalmanifest/services/myum-resolver && npm run typecheck
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test && npm run journeys && npm run smoke:endpoints:dev
```

## Change Management

Any baseline change must update:

1. `.nvmrc`
2. relevant package `engines` fields
3. CI workflow Node versions
4. this runtime policy document
