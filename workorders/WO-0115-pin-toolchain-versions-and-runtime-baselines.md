# WO-0115 — Pin Toolchain Versions and Runtime Baselines

**Status:** COMPLETED  
**Created:** 2026-03-02  
**Updated:** 2026-03-02  
**Completed:** 2026-03-02  
**Priority:** P1  
**Owner:** Platform / Developer Experience  
**Source:** Follow-on from deployment/runtime hardening review

## Objective

Eliminate local-vs-CI runtime drift by standardizing and pinning supported Node/Wrangler/toolchain versions across docs site, resolver service, and package workflows.

## Problem Statement

Current workflows use multiple Node versions across jobs, and repository-wide runtime pinning is incomplete. This increases nondeterminism across local development, CI, and deploy execution.

## Scope

In scope:

- define canonical Node version policy by workspace/package
- pin toolchain versions in repository metadata and CI
- add developer-facing setup guardrails and compatibility checks

Out of scope:

- changing package architecture
- introducing a monorepo build system migration

## Deliverables

1. Runtime policy document:
   - supported Node versions
   - Wrangler version policy
2. Repo-level pinning files and package metadata updates (as needed):
   - `.nvmrc` and/or equivalent
   - `engines` fields in package manifests
3. CI alignment:
   - reduce unexplained Node-version variance across workflows
4. Validation command:
   - one command/check to assert local runtime compatibility

## Acceptance Criteria

- [x] Documented canonical Node + Wrangler versions exist and are discoverable.
- [x] CI uses policy-aligned runtime versions for relevant jobs.
- [x] Local developer setup can detect unsupported runtime versions before build/test.
- [x] Site build, resolver typecheck, package test/journeys, and smoke all pass on pinned baseline.

## Dependencies

- `.github/workflows/ci.yml`
- `.github/workflows/verify.yml`
- `site/package.json`
- `services/myum-resolver/package.json`
- `packages/universal-manifest/package.json`

## Verification Commands (Target)

```bash
cd site && npm run build:clean
cd services/myum-resolver && npm run typecheck
cd packages/universal-manifest && npm test && npm run journeys && npm run smoke:endpoints:dev
```

## Completion Evidence (2026-03-02)

Delivered artifacts:

- Node baseline pin:
  - `.nvmrc`
- Runtime/toolchain policy:
  - `docs/guides/RUNTIME-BASELINE.md`
- Engine pinning:
  - `site/package.json`
  - `packages/universal-manifest/package.json`
  - `services/myum-resolver/package.json`
- CI runtime alignment (`node-version: 22`):
  - `.github/workflows/ci.yml`
  - `.github/workflows/verify.yml`
  - `.github/workflows/deploy-gated.yml`
  - `.github/workflows/synthetic-monitoring.yml`

Verification results:

- `cd site && npm run build:clean` -> PASS
- `cd services/myum-resolver && npm run typecheck` -> PASS
- `cd packages/universal-manifest && npm test` -> PASS
- `cd packages/universal-manifest && npm run journeys` -> PASS
- `cd packages/universal-manifest && npm run smoke:endpoints:dev` -> PASS (with local resolver running at `http://127.0.0.1:8787`)
- `cd packages/universal-manifest && npm run smoke:endpoints:prod` -> PASS
