# WO-0003 — Publish spec artifacts + release process

**Status:** BLOCKED  
**Created:** 2026-02-12

## Objective

Make Universal Manifest adoptable by external systems by publishing the versioned context/schema at stable URLs on `universalmanifest.net`, with correct headers and an explicit release process.

## Scope

In scope:

- Decide hosting mechanism (Cloudflare Pages/R2/etc.)
- Ensure stable URLs resolve:
  - `https://universalmanifest.net/ns/universal-manifest/v0.1/schema.jsonld`
  - `https://universalmanifest.net/ns/universal-manifest/v0.1/schema.json`
- Ensure correct headers (Content-Type, CORS, immutable caching)
- Document “latest/” alias behavior (redirect only)
- Document how new versions are released and kept immutable

Out of scope:

- Running production services

## Acceptance criteria

- [ ] URLs resolve over HTTPS and return correct content types (requires actual deployment + DNS)
- [ ] Post-deploy smoke is executable and passes (docs + resolver contract)
- [x] CORS enabled for browser tooling (configured via `_headers`)
- [x] Immutable caching for versioned paths (configured via `_headers`)
- [x] Release checklist documented (see `docs/RELEASING.md` + `docs/PUBLISHING-AND-VERSIONING.md`)
- [x] Cloudflare Pages deployment runbook exists (deployment-ready)
- [x] Compatibility aliases for previously published `localartist.network` namespace URLs are documented (do not break old references)

## Blockers (external actions required)

This WO is blocked on actions that require Cloudflare account + DNS control:

1. Deploy `universalmanifest.net` (Cloudflare Pages)
   - Runbook: `/Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
2. Deploy `myum.net` resolver (Cloudflare Worker + KV)
   - Runbook: `/Users/grig/work/repo/universalmanifest/services/myum-resolver/CLOUDFLARE-DEPLOY.md`
3. Validate both domains with the combined smoke (required for claiming “published”)
   - Runbook: `/Users/grig/work/repo/universalmanifest/docs/PRODUCTION-DEPLOY-SMOKE.md`
   - Command: `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run smoke:endpoints:prod`

## References

 - `docs/PUBLISHING-AND-VERSIONING.md`
 - `deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
 - `docs/LEGACY-LOCALARTIST-NETWORK-COMPATIBILITY.md`
 - Endpoint smoke script: `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/smoke-endpoints.mjs`
 - Production deploy smoke runbook: `/Users/grig/work/repo/universalmanifest/docs/PRODUCTION-DEPLOY-SMOKE.md`
