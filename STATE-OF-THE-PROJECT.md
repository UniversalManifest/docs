# State of the Project — Universal Manifest

**Date:** 2026-02-18  
**Status:** v0.1/v0.2 artifacts, docs site, and resolver are now live in production (`universalmanifest.net` + `myum.net`); next critical work is onboarding clarity and interactive adopter tooling.
**Canonical repository path:** `/Users/grig/work/repo/universalmanifest`
**Legacy path (for historical references):** `/Users/grig/work/lan/universal-manifest`

This repo is a **spec + fixtures + minimal tooling** project. It is not a running service.

For the “what has to happen next” sequence, see: `docs/CRITICAL-PATH.md`.
For the latest condensed status summary, see: `docs/reports/2026-02-18-live-status-and-next-critical-path.md`.

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
- **Proof surfaces (executable + visual)**
  - Journeys → executable proof suite: `docs/journeys/` (run via `packages/universal-manifest` → `npm run journeys`)
  - Harness → visual endpoint/fixture debugger: `site/public/harness/index.html` (served at `/harness/index.html`)
  - Endpoint smoke (dev/prod) for docs + resolver contract: `packages/universal-manifest/scripts/smoke-endpoints.mjs`
- **Visual onboarding assets (new)**
  - Excalidraw source-of-truth scaffold: `docs/diagrams/`
  - Published diagram assets path: `site/public/diagrams/`
- **Public docs IA + editorial polish**
  - Explicit sidebar labels/order and adopter-first navigation in the docs site
  - “Critical Path” reframed as adopter-facing “Adoption Roadmap”
  - Integration pages now include clear implementation checklists + fixture links + non-normative boundaries
- **v0.2 draft signature profile (artifacts exist)**
  - Signature profile: `spec/v0.2/SIGNATURE-PROFILE.md`
  - Draft schema + context: `spec/v0.2/schema.json` + `spec/v0.2/schema.jsonld`
  - Draft conformance: `spec/v0.2/CONFORMANCE.md`
  - Fixtures: `examples/v0.2/`
- **Background research (non-normative)**
  - Imported docs under `research/` with an index at `research/README.md`

### What is *not* finalized yet (by design)

- v0.1 signature is still a permissive envelope; v0.2 defines an interop profile but remains draft until publishing and broader adopter verification
- Additional integrity profiles (e.g., Data Integrity / RDF canonicalization) beyond the v0.2 baseline
- Revocation cursor/events as a normative part of the contract
- A complete conformance suite (we have baseline valid/invalid fixtures; TTL/replay/security cases remain)
- Interactive manifest workbench for import/create/validate/export (`WO-0014`)
- First-time onboarding validation with external reader testing (`WO-0015`)

## Work-order status (2026-02-18)

- Completed: `WO-0001` through `WO-0013` (including `WO-0003` publishing/deploy)
- Open: `WO-0014` interactive workbench
- In progress: `WO-0015` first-time overview and visual onboarding
- In progress: `WO-0016` GAS index scan and knowledge integration ledger

## Local verification status (latest runs)

- `site` build (`npm run build:clean`): PASS
- `packages/universal-manifest` tests (`npm test`): PASS
- Journeys proof (`npm run journeys`): PASS
- Endpoint smoke dev (`npm run smoke:endpoints:dev`): PASS
- Endpoint smoke prod (`npm run smoke:endpoints:prod`): PASS
- Harness autorun (`/harness/index.html?autorun=1`): PASS

## What we consider “done” for v0.1

v0.1 is “done enough” when:

1. A third-party system can parse manifests and safely ignore unknown fields.
2. Fixtures cover the baseline subject types (venue, device, creator) + one cross-system profile projection.
3. The spec clearly documents TTL + caching + ID guidance and why it exists.

The project satisfies (1) and (2) with runnable evidence and now has production deployment proof. Remaining work is primarily interoperability hardening plus first-time adopter experience/tooling.

For formal gate-level completion criteria and evidence requirements, use:

- `docs/DONE-DONE-DEFINITION.md`
- `docs/DONE-DONE-CHECKLIST.md`

## Next milestones (recommended)

### Milestone A — Conformance scaffolding (still v0.1.x)

- ✅ Added `spec/v0.1/CONFORMANCE.md` checklist (“what a consumer MUST do to claim v0.1 support”)
- ✅ Added initial invalid fixtures (missing required fields, wrong `@type`, bad shards)
- ✅ Updated `packages/universal-manifest` validator to assert invalid fixtures fail
- Next: add deeper TTL and misuse/adversarial fixtures for v0.1.x and v0.2.x as the suite hardens

### Milestone B — Signature profile (v0.2)

- ✅ Chose a v0.2 baseline profile (JCS + Ed25519) and added draft artifacts + fixtures:
  - `spec/v0.2/SIGNATURE-PROFILE.md`
  - `spec/v0.2/schema.json` + `spec/v0.2/schema.jsonld`
  - `spec/v0.2/CONFORMANCE.md`
  - `examples/v0.2/`
- Next: publish v0.2 artifacts at stable URLs and expand fixtures for verification edge-cases

### Milestone C — Distribution + stability (v0.2+)

- Documented publishing + versioning plan: `docs/PUBLISHING-AND-VERSIONING.md`
- Production deployment is live:
  - `https://universalmanifest.net` (Cloudflare Pages)
  - `https://myum.net` (Cloudflare Worker + KV)
- Next: harden v0.2 migration policy and resolver edge-case semantics
  - Cloudflare Pages runbook: `deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
  - Resolver contract: `services/myum-resolver/CONTRACT.md`

### Milestone D — Adopter onboarding + interactive tooling

- CEO-priority first-time overview work is underway (`WO-0015`)
- CEO-priority interactive manifest workbench is planned (`WO-0014`)
- Next: ship first public version of the workbench and validate onboarding comprehension with external readers

## How other systems should adopt it today (v0.1)

Recommended adoption tier for external systems *right now*:

- Validate required fields (`@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`)
- Enforce TTL for caching decisions
- Use `pointers` and known `shards` for projection
- Treat `signature` as optional and/or “best effort” until the signature profile is finalized
- For v0.2 drafts: verify signatures when present and required by that profile

## Notes on LAN relationship

LAN is a primary design driver, but the project goal is broader:

- LAN uses the manifest as a local-first capsule (edge ↔ display ↔ admin).
- Future “social profile” surfaces should treat the manifest as an envelope that drives projections (web profile pages, ActivityPub actor pointers, etc.).

This is why “LAN specifics” live in `integrations/` and `research/`, not in `spec/`.

## Agent onboarding status

Universal Manifest has been aligned to the GAS split model for onboarding consistency:

- `AGENTS.md` contains the global immutable rules copy.
- `PROJECT-RULES.md` contains Universal Manifest-specific instructions and operational context.
- `.dev` now includes GAS-style directory scaffolding for handoffs, workorders, reports, and inbox capture.
