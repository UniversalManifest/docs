# WO-0007 — `myum.net` resolver skeleton + `universalmanifest.net` static publish config

**Status:** NOT_STARTED  
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

- Worker skeleton and config (expected examples):
  - `infra/myum-worker/` (or equivalent)
  - `wrangler.toml` with KV bindings
- Resolver contract doc:
  - request/response examples for `200`, redirect, `404`, `410`
- Static publish config for `universalmanifest.net`:
  - headers/routing config file(s)
  - deployment instructions

## Acceptance criteria

- [ ] `myum.net/{UMID}` resolver skeleton runs locally via Wrangler
- [ ] KV schema is documented with required keys and value shape
- [ ] Endpoint contract documented with deterministic status semantics
- [ ] Static hosting config serves spec artifacts with correct content-type + CORS + cache headers
- [ ] `latest/` behavior (if enabled) is redirect-only to concrete versions
- [ ] Documentation includes production deployment checklist

## Dependencies

- Domain architecture decision:
  - `docs/DOMAIN-ARCHITECTURE.md`
- Publishing/versioning policy:
  - `docs/PUBLISHING-AND-VERSIONING.md`
  - `docs/RELEASING.md`

