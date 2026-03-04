# WO-0119 — Resolver Route Canonicalization and Fixture Freshness Lock

**Status:** IN_PROGRESS
**Created:** 2026-03-04
**Updated:** 2026-03-04
**Priority:** P0
**Owner:** Runtime + Docs Surface
**Source:** Post-production runtime truth audit follow-on

## Objective

Eliminate resolver consumer-route redirect-loop risk and remove stale default fixture freshness in resolver runtime so the default production trust flow is meaningful.

## Problem Statement

Two production-critical reliability/trust issues were confirmed:

1. Route canonicalization conflict on `/resolver/` due wrapper-to-`.html` redirects.
2. Resolver fallback fixture used for default smoke path had expired `expiresAt`, causing deterministic trust-failure for strict consumers.

## Scope

In scope:

- ensure `/resolver/`, `/resolver/ops`, and `/resolver/result` resolve to usable pages without redirect-loop behavior
- ensure default resolver fixture has non-stale validity window
- verify local contract tests + site build + endpoint smoke
- define production deployment/verification acceptance criteria

Out of scope:

- replacing fallback fixture architecture with a write API
- changing resolver contract version

## Deliverables

1. Resolver route fix in site build pipeline (no wrapper-loop at `/resolver/`).
2. Resolver fallback fixture timestamp update in runtime source.
3. Verification evidence artifact with command outputs.
4. Production promotion checklist entry for this fix.

## Acceptance Criteria

- [x] `site/dist/resolver/index.html` serves consumer UI directly (not wrapper redirect shell).
- [x] Resolver fixture in source no longer has stale `expiresAt`.
- [x] Resolver contract suite passes locally.
- [x] Site build passes locally.
- [x] Production smoke + post-deploy verify pass (current production baseline).
- [ ] Updated resolver runtime is deployed to staging and production.
- [ ] Post-deploy probe confirms refreshed fixture validity in live resolver responses.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/src/index.ts`
- `/Users/grig/work/repo/universalmanifest/site/public/resolver/index.html`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/smoke-endpoints.mjs`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/post-deploy-verify.mjs`

## Verification Commands

```bash
cd /Users/grig/work/repo/universalmanifest/services/myum-resolver
npm test
```

```bash
cd /Users/grig/work/repo/universalmanifest/site
npm run build
```

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm run smoke:endpoints:prod
npm run verify:postdeploy:prod
```

```bash
UMID='urn:uuid:11111111-1111-4111-8111-111111111111'
ENC_UMID=$(node -p "encodeURIComponent(process.argv[1])" "$UMID")
curl -s "https://myum.net/${ENC_UMID}" | jq '{"@type": ."@type", issuedAt, expiresAt}'
```

## Progress Update (2026-03-04)

Implemented in repo this pass:

- Removed resolver Astro wrapper pages that caused redirect-shell output at canonical resolver routes:
  - `/Users/grig/work/repo/universalmanifest/site/src/pages/resolver/index.astro` (deleted)
  - `/Users/grig/work/repo/universalmanifest/site/src/pages/resolver/ops.astro` (deleted)
  - `/Users/grig/work/repo/universalmanifest/site/src/pages/resolver/result.astro` (deleted)
- Updated resolver fallback fixture validity window:
  - `/Users/grig/work/repo/universalmanifest/services/myum-resolver/src/index.ts`
    - `issuedAt` -> `2026-03-01T00:00:00.000Z`
    - `expiresAt` -> `2036-03-01T00:00:00.000Z`

Local verification evidence:

- `npm test` (resolver contract suite) -> PASS
- `npm run build` (site) -> PASS
- `npm run smoke:endpoints:prod` -> PASS
- `npm run verify:postdeploy:prod` -> PASS
  - report: `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/deploy-checks/2026-03-04T04-27-20-209Z-post-deploy-verification.md`

Remaining deployment action:

- Promote updated code through gated deploy workflow so production resolver payload freshness reflects updated fixture timestamps.
