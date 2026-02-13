# WO-0006 — Domain + hosting architecture (`universalmanifest.net` + `myum.net`)

**Status:** Done  
**Created:** 2026-02-12

## Objective

Adopt the two-domain architecture:

- `universalmanifest.net` for standards/docs/spec artifacts
- `myum.net/[UMID]` for manifest resolution and retrieval

## Scope

In scope:

- Document architecture and responsibilities per domain
- Update publishing/versioning/release docs to reflect new canonical host
- Add compatibility guidance for existing `localartist.network` references

Out of scope:

- Production deployment of DNS/CDN/origin
- Implementing the full resolver backend

## Acceptance criteria

- [x] Decision recorded in `docs/DECISIONS.md`
- [x] Hosting docs reference `universalmanifest.net` as canonical spec host
- [x] Manifest resolver behavior documented for `myum.net/[UMID]`
- [x] Migration compatibility with `localartist.network` documented
