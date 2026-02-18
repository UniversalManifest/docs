# WO-0007 — `myum.net` resolver skeleton + `universalmanifest.net` static publish config

**Status:** COMPLETED  
**Created:** 2026-02-12

## Objective

Create implementation-ready infrastructure artifacts for:

1. `myum.net` resolver skeleton (Cloudflare Worker + KV schema + endpoint contract)
2. `universalmanifest.net` standards site static publishing configuration

## Scope

In scope:

- Resolver skeleton package/folder with:
  - Cloudflare Worker entrypoint
  - KV namespace binding contract
  - UMID lookup flow and response semantics
  - endpoint contract documentation for `GET /{UMID}` and health/metadata endpoints
- Static publishing config for `universalmanifest.net` with:
  - versioned spec artifact routing under `/ns/universal-manifest/vX.Y/`
  - content-type/header rules for `.jsonld` and `.json`
  - CORS and caching policy
  - optional `latest/` redirect behavior
- Deployment/readme notes sufficient for first deploy in Cloudflare

Out of scope:

- Production data ingestion pipeline for resolver entries
- Full auth/governance/admin UI
- DNS ownership transfer or registrar operations

## Deliverables

- Worker skeleton and config:
  - `services/myum-resolver/`
  - `services/myum-resolver/wrangler.toml` (KV binding contract)
- Resolver contract doc:
  - `services/myum-resolver/README.md` (request/response examples for `200`, redirect, `404`, `410`)
- Static publish config for `universalmanifest.net`:
  - `deploy/universalmanifest.net/_headers`
  - `deploy/universalmanifest.net/_redirects`
  - `deploy/universalmanifest.net/build.mjs` (builds `deploy/universalmanifest.net/dist/`)
  - `deploy/universalmanifest.net/README.md` (deployment instructions)

## Acceptance criteria

- [x] `myum.net/{UMID}` resolver skeleton runs locally via Wrangler
- [x] KV schema is documented with required keys and value shape
- [x] Endpoint contract documented with deterministic status semantics
- [x] Static hosting config serves spec artifacts with correct content-type + CORS + cache headers
- [x] `latest/` behavior (if enabled) is redirect-only to concrete versions
- [x] Documentation includes production deployment checklist

## Dependencies

- Domain architecture decision:
  - `docs/DOMAIN-ARCHITECTURE.md`
- Publishing/versioning policy:
  - `docs/PUBLISHING-AND-VERSIONING.md`
  - `docs/RELEASING.md`
