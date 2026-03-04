# WO-0120 — Harness 307 Contract Parity and Trust-Matrix Coverage

**Status:** COMPLETED
**Created:** 2026-03-04
**Updated:** 2026-03-04
**Priority:** P1
**Owner:** QA Surface + Resolver Tooling
**Source:** WO-0112 Phase-2 follow-on and runtime parity audit

## Objective

Align harness resolver handling with contract semantics by treating `307` as valid resolution behavior when `Location` is present, and expand matrix verification coverage.

## Problem Statement

Harness resolver actions currently treat all non-2xx responses as failures, which incorrectly marks contract-valid redirect responses (`307`) as failures and trains users toward incorrect resolver assumptions.

## Scope

In scope:

- update harness direct + b64u resolve actions to accept `307` + `Location`
- keep header and manifest checks for `200` payload branch
- preserve explicit failure behavior for invalid statuses and malformed redirect responses
- define trust-matrix extension plan for future automation

Out of scope:

- changing resolver runtime redirect status code
- adding full browser E2E framework in this work order

## Deliverables

1. Harness logic update for redirect-aware pass/fail classification.
2. Updated summary messages for redirect branch clarity.
3. Follow-on acceptance/verification plan for full status matrix checks.

## Acceptance Criteria

- [x] `resolverResolveAction()` accepts `307` with `Location` as pass.
- [x] `resolverResolveB64uAction()` accepts `307` with `Location` as pass.
- [x] Missing `Location` on `307` remains fail.
- [x] Existing payload validation/signature checks remain for `200` branch.
- [x] Browser-level screenshot/console evidence captured on deployed harness route.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/site/public/harness/index.html`
- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/CONTRACT.md`
- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/scripts/contract-tests.mjs`

## Verification Commands

```bash
cd /Users/grig/work/repo/universalmanifest/site
npm run build
```

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm run smoke:endpoints:prod
```

## Progress Update (2026-03-04)

Implemented in repo this pass:

- Updated redirect handling for both resolver fetch actions:
  - `/Users/grig/work/repo/universalmanifest/site/public/harness/index.html`
  - `307` with `Location` now reports pass summary
  - `307` missing `Location` reports fail summary
  - status display now marks `307` as non-error for resolver action feedback

Verification completed:

- Site build passes after harness logic change.
- Production endpoint smoke remains passing.

Browser evidence:

- Harness live verification (post-deploy) confirms redirect branch pass on deployed `/harness/` route:
  - screenshot: `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/deploy-checks/2026-03-04-harness-opaque-redirect-pass.png`
  - tested UMID: `urn:uuid:22222222-2222-4222-8222-222222222222` (redirect record in production KV)
  - smoke + post-deploy reports:
    - `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/deploy-checks/2026-03-04T04-52-22-400Z-post-deploy-verification.md`

Completion note:

- WO-0120 is complete as of 2026-03-04 with deployed verification evidence.
