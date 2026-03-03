# WO-0113 — Establish Staging Environments and Promotion Model

**Status:** COMPLETED  
**Created:** 2026-03-02  
**Updated:** 2026-03-03  
**Priority:** P0  
**Owner:** Platform / DevOps  
**Source:** Follow-on from deployment/runtime hardening review  
**Completed:** 2026-03-02

## Objective

Create a first-class staging topology for both public surfaces so changes can be verified end-to-end before production promotion:

- standards/docs surface (currently `universalmanifest.net`)
- resolver surface (currently `myum.net`)

## Problem Statement

Current deployment guidance is production-centric. The project has strong smoke and verification scripts, but no formalized staging environment pair and promotion contract. This increases risk of deployment drift and production-only discovery of integration breaks.

## Scope

In scope:

- define and provision staging domains
  - docs: `staging.universalmanifest.net` (or equivalent)
  - resolver: `staging.myum.net` (or equivalent)
- define staging-to-production promotion rules
- define environment data separation and parity requirements
- define staging verification gates using existing smoke/post-deploy tooling

Out of scope:

- rewriting resolver contract behavior
- introducing non-Cloudflare hosting providers

## Deliverables

1. Environment architecture doc update covering:
   - production vs staging domain matrix
   - route mapping
   - DNS and TLS expectations
   - isolation boundaries
2. Resolver environment split plan:
   - separate KV namespace IDs for staging and production
   - explicit binding strategy per environment
3. Promotion contract:
   - required checks before prod promotion
   - rollback entry points
4. Runbook updates:
   - deploy + verify steps for staging and production

## Acceptance Criteria

- [x] Staging docs domain serves built site and versioned `/ns/...` artifacts.
- [x] Staging resolver domain serves `/health`, `/.well-known/myum-resolver.json`, and `/{UMID_PATH}` using staging KV only.
- [x] Existing smoke scripts can run against staging with explicit base URLs.
- [x] Documented promotion flow exists from staging to production.
- [x] Rollback procedure is documented and executable.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/docs/DOMAIN-ARCHITECTURE.md`
- `/Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/CLOUDFLARE-DEPLOY.md`

## Verification Commands (Target)

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
node scripts/smoke-endpoints.mjs --mode prod --docs-base https://staging.universalmanifest.net --resolver-base https://staging.myum.net
```

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
node scripts/post-deploy-verify.mjs --mode prod --docs-base https://staging.universalmanifest.net --resolver-base https://staging.myum.net --resolver-www-base https://www.staging.myum.net
```

## Progress Update (2026-03-02)

Repository deliverables completed:

- Added staging/production promotion and rollback runbook:
  - `/Users/grig/work/repo/universalmanifest/docs/site/STAGING-PROMOTION-RUNBOOK.md`
- Added resolver staging environment configuration:
  - `/Users/grig/work/repo/universalmanifest/services/myum-resolver/wrangler.toml` (`[env.staging]`)
- Added staging verification scripts:
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/package.json` (`smoke:endpoints:staging`, `verify:postdeploy:staging`)
- Updated architecture/deployment docs to include staging/promotion model:
  - `/Users/grig/work/repo/universalmanifest/docs/DOMAIN-ARCHITECTURE.md`
  - `/Users/grig/work/repo/universalmanifest/docs/DEPLOY-CHECKLIST.md`
  - `/Users/grig/work/repo/universalmanifest/docs/site/DEPLOYMENT.md`

Verification results:

- custom-domain checks remain pending DNS propagation:
  - `npm run smoke:endpoints:staging` -> currently fails on unresolved `staging.*` hosts
  - `npm run verify:postdeploy:staging` -> currently fails on unresolved `staging.*` hosts

Provisioning update:

- created Cloudflare Pages staging project:
  - `universalmanifest-net-staging` (`https://universalmanifest-net-staging.pages.dev`)
- created staging resolver KV namespaces:
  - primary: `bafa21a750e74b09b353509ed97098ac`
  - preview: `a169ea948d7b45c49ef4a87b685c5858`
- deployed staging resolver:
  - `https://myum-resolver-staging.grig-624.workers.dev`
- fallback staging verification now passes with explicit base URLs:
  - `node scripts/smoke-endpoints.mjs --mode prod --docs-base https://universalmanifest-net-staging.pages.dev --resolver-base https://myum-resolver-staging.grig-624.workers.dev` -> PASS
  - `node scripts/post-deploy-verify.mjs --mode prod --docs-base https://universalmanifest-net-staging.pages.dev --resolver-base https://myum-resolver-staging.grig-624.workers.dev --resolver-www-base https://myum-resolver-staging.grig-624.workers.dev` -> PASS
  - report: `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/deploy-checks/2026-03-02T22-59-38-831Z-post-deploy-verification.md`

Completion addendum (2026-03-03):

- Staging custom domains are now active for both surfaces:
  - docs: `https://staging.universalmanifest.net` (served via `um-docs-staging-proxy` custom-domain Worker in front of staging Pages content)
  - resolver: `https://staging.myum.net` and `https://www.staging.myum.net` (served via `myum-resolver-staging` custom domains)
- Staging vars now target custom domains by default:
  - `STAGING_DOCS_BASE=https://staging.universalmanifest.net`
  - `STAGING_RESOLVER_BASE=https://staging.myum.net`
  - `STAGING_RESOLVER_WWW_BASE=https://www.staging.myum.net`
- Cloud verification evidence:
  - Synthetic staging monitoring SUCCESS:
    - `https://github.com/grigb/universal-manifest/actions/runs/22602225159`
  - Gated deploy (staging verification) SUCCESS:
    - `https://github.com/grigb/universal-manifest/actions/runs/22602253533`
  - Staging custom-domain provisioning workflow SUCCESS:
    - `https://github.com/grigb/universal-manifest/actions/runs/22602353923`
