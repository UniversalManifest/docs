# State of the Project — Universal Manifest

**Date:** 2026-02-12  
**Status:** Draft v0.1 spec + fixtures (early-adopter friendly, not yet “interop hardened”)

This repo is a **spec + fixtures + minimal tooling** project. It is not a running service.

## Current snapshot

### What exists now

- **v0.1 draft spec artifacts**
  - JSON-LD context: `spec/v0.1/schema.jsonld`
  - Structural schema: `spec/v0.1/schema.json`
  - Spec overview: `spec/v0.1/README.md`
  - Well-known name registry (draft): `spec/v0.1/REGISTRY.md`
  - Conformance checklist + fixtures list (draft): `spec/v0.1/CONFORMANCE.md`
- **Fixtures**
  - Baseline examples: `examples/v0.1/`
  - Near-real stubs: `examples/v0.1/stubs/`
  - Invalid fixtures (conformance): `examples/v0.1/invalid/`
  - Human index for fixtures + “vision drivers”: `docs/STUB-MANIFESTS.md`
- **Integration notes (non-normative)**
  - LAN/Shield caching + transport: `integrations/lan.md`
  - Social/profile adoption: `integrations/social.md`
- **Publishing + versioning plan**
  - Stable URLs + headers + immutability policy: `docs/PUBLISHING-AND-VERSIONING.md`
  - Domain split architecture (`universalmanifest.net` + `myum.net`): `docs/DOMAIN-ARCHITECTURE.md`
- **Official completion framework**
  - Done-done definition: `docs/DONE-DONE-DEFINITION.md`
  - Release checklist: `docs/DONE-DONE-CHECKLIST.md`
  - Evidence pack template: `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
- **Tooling**
  - TypeScript types + runtime assertion for v0.1: `packages/universal-manifest/`
  - Fixture validation run via `npm test` (build + validate valid + invalid fixtures)
- **v0.2 draft direction**
  - Proposed signature profile: `spec/v0.2/SIGNATURE-PROFILE.md`
- **Background research (non-normative)**
  - Imported docs under `research/` with an index at `research/README.md`

### What is *not* finalized yet (by design)

- A canonical, interoperable **signature format** (v0.1 signature is a permissive envelope)
- Canonicalization rules for signing/verifying (e.g., JSON-LD/RDF normalization profile)
- Revocation cursor/events as a normative part of the contract
- A complete conformance suite (we have baseline valid/invalid fixtures; TTL/replay/security cases remain)
- Stable hosting guarantees for the context/schema URLs (planned; see publishing plan)

## What we consider “done” for v0.1

v0.1 is “done enough” when:

1. A third-party system can parse manifests and safely ignore unknown fields.
2. Fixtures cover the baseline subject types (venue, device, creator) + one cross-system profile projection.
3. The spec clearly documents TTL + caching + ID guidance and why it exists.

We are close on (1) and (2). Remaining work is primarily around making (3) sharper and expanding conformance + signature guarantees.

For formal gate-level completion criteria and evidence requirements, use:

- `docs/DONE-DONE-DEFINITION.md`
- `docs/DONE-DONE-CHECKLIST.md`

## Next milestones (recommended)

### Milestone A — Conformance scaffolding (still v0.1.x)

- ✅ Added `spec/v0.1/CONFORMANCE.md` checklist (“what a consumer MUST do to claim v0.1 support”)
- ✅ Added initial invalid fixtures (missing required fields, wrong `@type`, bad shards)
- ✅ Updated `packages/universal-manifest` validator to assert invalid fixtures fail
- Next: add TTL edge-case fixtures (expired, issuedAfterExpires, far-future timestamps), and signature-related fixtures once v0.2 profile is chosen

### Milestone B — Signature profile (v0.2)

- Drafted an initial signature direction: `spec/v0.2/SIGNATURE-PROFILE.md`
- Next: decide final v0.2 profile and update schema/context/types accordingly

### Milestone C — Distribution + stability (v0.2+)

- Documented publishing + versioning plan: `docs/PUBLISHING-AND-VERSIONING.md`
- Next: publish context/schema at stable URLs and document migration policy (v0.x → v1.0 path)

## How other systems should adopt it today (v0.1)

Recommended adoption tier for external systems *right now*:

- Validate required fields (`@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`)
- Enforce TTL for caching decisions
- Use `pointers` and known `shards` for projection
- Treat `signature` as optional and/or “best effort” until the signature profile is finalized

## Notes on LAN relationship

LAN is a primary design driver, but the project goal is broader:

- LAN uses the manifest as a local-first capsule (edge ↔ display ↔ admin).
- Future “social profile” surfaces should treat the manifest as an envelope that drives projections (web profile pages, ActivityPub actor pointers, etc.).

This is why “LAN specifics” live in `integrations/` and `research/`, not in `spec/`.
