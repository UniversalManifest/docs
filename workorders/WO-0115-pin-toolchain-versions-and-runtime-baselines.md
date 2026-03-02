# WO-0115 — Pin Toolchain Versions and Runtime Baselines

**Status:** NOT_STARTED  
**Created:** 2026-03-02  
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

- [ ] Documented canonical Node + Wrangler versions exist and are discoverable.
- [ ] CI uses policy-aligned runtime versions for relevant jobs.
- [ ] Local developer setup can detect unsupported runtime versions before build/test.
- [ ] Site build, resolver typecheck, package test/journeys, and smoke all pass on pinned baseline.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/.github/workflows/ci.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml`
- `/Users/grig/work/repo/universalmanifest/site/package.json`
- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/package.json`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/package.json`

## Verification Commands (Target)

```bash
cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean
cd /Users/grig/work/repo/universalmanifest/services/myum-resolver && npm run typecheck
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test && npm run journeys && npm run smoke:endpoints:dev
```
