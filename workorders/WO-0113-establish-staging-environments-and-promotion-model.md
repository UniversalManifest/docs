# WO-0113 — Establish Staging Environments and Promotion Model

**Status:** BLOCKED  
**Created:** 2026-03-02  
**Updated:** 2026-03-02  
**Priority:** P0  
**Owner:** Platform / DevOps  
**Source:** Follow-on from deployment/runtime hardening review  
**Blocker:** Staging domains are not yet resolving (`staging.universalmanifest.net`, `staging.myum.net`), so staging verification gates cannot pass.

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

- [ ] Staging docs domain serves built site and versioned `/ns/...` artifacts.
- [ ] Staging resolver domain serves `/health`, `/.well-known/myum-resolver.json`, and `/{UMID_PATH}` using staging KV only.
- [ ] Existing smoke scripts can run against staging with explicit base URLs.
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

- `npm run smoke:endpoints:staging` -> FAIL (`fetch failed` for staging docs and resolver hosts)
- `npm run verify:postdeploy:staging` -> FAIL (`fetch failed` for staging docs host)

External unblock actions required:

1. Provision and route staging domains in Cloudflare DNS/Pages/Workers.
2. Confirm staging docs and resolver deployments are live.
3. Rerun staging smoke and post-deploy verification commands.
