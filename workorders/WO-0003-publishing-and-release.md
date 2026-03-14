# WO-0003 — Publish spec artifacts + release process

**Status:** COMPLETED  
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

- [x] URLs resolve over HTTPS and return correct content types (deployment + DNS completed)
- [x] Post-deploy smoke is executable and passes (docs + resolver contract)
- [x] CORS enabled for browser tooling (configured via `_headers`)
- [x] Immutable caching for versioned paths (configured via `_headers`)
- [x] Release checklist documented (see `docs/RELEASING.md` + `docs/PUBLISHING-AND-VERSIONING.md`)
- [x] Cloudflare Pages deployment runbook exists (deployment-ready)
- [x] Compatibility aliases for previously published `localartist.network` namespace URLs are documented (do not break old references)

## Completion record (2026-02-18)

Completed external deployment actions:

1. `universalmanifest.net` deployed on Cloudflare Pages
2. `myum.net` resolver deployed on Cloudflare Workers + KV
3. Production smoke validated with:
   - `cd packages/universal-manifest && npm run smoke:endpoints:prod`
   - Result: **PASS**

Validation notes:

- Versioned schema/context endpoints resolve with expected content types and headers.
- `latest/` alias behavior is redirect-based with non-immutable caching.
- Resolver contract endpoints (`/health`, `/.well-known`, UMID resolution) are reachable in production.

## References

 - `docs/PUBLISHING-AND-VERSIONING.md`
 - `deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
 - `docs/LEGACY-LOCALARTIST-NETWORK-COMPATIBILITY.md`
 - Endpoint smoke script: `packages/universal-manifest/scripts/smoke-endpoints.mjs`
 - Production deploy smoke runbook: `docs/PRODUCTION-DEPLOY-SMOKE.md`
