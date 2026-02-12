# WO-0003 — Publish spec artifacts + release process

**Status:** Proposed  
**Created:** 2026-02-12

## Objective

Make Universal Manifest adoptable by external systems by publishing the versioned context/schema at stable URLs on `localartist.network`, with correct headers and an explicit release process.

## Scope

In scope:

- Decide hosting mechanism (Cloudflare Pages/R2/etc.)
- Ensure stable URLs resolve:
  - `https://localartist.network/ns/universal-manifest/v0.1/schema.jsonld`
  - `https://localartist.network/ns/universal-manifest/v0.1/schema.json`
- Ensure correct headers (Content-Type, CORS, immutable caching)
- Document “latest/” alias behavior (redirect only)
- Document how new versions are released and kept immutable

Out of scope:

- Running production services

## Acceptance criteria

- [ ] URLs resolve over HTTPS and return correct content types
- [ ] CORS enabled for browser tooling
- [ ] Immutable caching for versioned paths
- [ ] Release checklist documented and followed for the next version bump

## References

- `docs/PUBLISHING-AND-VERSIONING.md`

