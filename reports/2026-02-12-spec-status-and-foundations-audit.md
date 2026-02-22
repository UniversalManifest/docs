# Universal Manifest — Spec Status + Foundations Audit (v0.1 snapshot)

Date: 2026-02-17  
Work Order: `docs/workorders/WO-0008-spec-status-scope-and-foundations-audit.md`  
Target maturity for this audit: **Early-adopter ready (v0.x)** (see `docs/DONE-DONE-DEFINITION.md`)

This report answers:

- What is the Universal Manifest spec responsible for (scope)?
- What does “done done” mean (by gates) and what is the current proximity?
- What foundational references were reviewed (in-repo + indexed external sources)?
- What are the prioritized gaps and next steps?

## 1) Scope (what the spec program owns)

Universal Manifest is a **portable state capsule** specification. The spec program owns:

- Document identity + lifecycle: `@id`, `manifestVersion`, `issuedAt`, `expiresAt`
- Subject binding: `subject` (stable identifier URI; DID recommended but not required)
- Composition primitives: `shards`, `pointers`
- Machine-actionable sections: `claims`, `consents`, `devices`
- Compatibility semantics: unknown-field tolerance, extension points, version policy
- Integrity envelope semantics by profile: `signature` (v0.1 permissive; v0.2 profile drafted)

Normative-ish surfaces (source of truth):

- `spec/v0.1/schema.jsonld`
- `spec/v0.1/schema.json`
- `spec/v0.1/README.md`
- `spec/v0.1/CONFORMANCE.md`
- `spec/v0.1/REGISTRY.md`

Required-to-adopt but surfaces:

- Fixtures: `examples/v0.1/` and `examples/v0.1/stubs/`
- Integration guides: `integrations/lan.md`, `integrations/social.md`
- Publishing/governance guidance: `docs/PUBLISHING-AND-VERSIONING.md`, `docs/RELEASING.md`, `docs/DECISIONS.md`

Explicitly out of scope for v0.1 / current maturity:

- A mandated DID method or identity provider
- A production resolver service implementation (contract skeleton is in WO-0007)
- A final, ecosystem-wide trust distribution + revocation network
- Restoration/recovery workflows driven by logs (IDs are logged now; recovery is future)

Canonical domain split (authoritative):

- Standards/docs/spec artifacts: `universalmanifest.net`
- Runtime resolver semantics: `myum.net/{UMID}`

Reference: `docs/DOMAIN-ARCHITECTURE.md`

## 2) Inventory snapshot (what exists now)

### A) Spec artifacts

- v0.1: `spec/v0.1/` includes schema + context + registry + conformance + README.
- v0.2 direction: `spec/v0.2/SIGNATURE-PROFILE.md` exists, but v0.2 schema/context do not yet exist.

### B) Fixtures

- Valid fixtures: 9 (core + near-real stubs)
- Invalid fixtures: 11 (structural + TTL freshness)

Primary fixture index: `docs/STUB-MANIFESTS.md`

### C) Tooling

- TypeScript helper package exists and validates fixtures:
  - `packages/universal-manifest/`

### D) Integration guidance

- `integrations/lan.md` (local-first caching/logging guidance)
- `integrations/social.md` (projection/adoption notes)

### E) Governance + completion framework

- Done-done definition and checklist are in place and treated as canonical:
  - `docs/DONE-DONE-DEFINITION.md`
  - `docs/DONE-DONE-CHECKLIST.md`
  - `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`

## 3) “Done done” gates — current maturity score (evidence-backed)

This evaluation targets **Maturity A: Early-adopter ready (v0.x)**.

### Gate G1: Contract completeness — **PASS (v0.1)**

Why:
- Required fields and core semantics exist in `spec/v0.1/README.md`.
- Unknown-field behavior is explicitly required in `spec/v0.1/CONFORMANCE.md`.
- Name registry draft exists in `spec/v0.1/REGISTRY.md`.

Risks/notes:
- Some semantics remain intentionally permissive (by design) to avoid overbuild.

### Gate G2: Conformance testability — **PASS (baseline)**

Why:
- Valid + invalid fixtures exist and are enumerated in `spec/v0.1/CONFORMANCE.md`.
- A reproducible harness exists in `packages/universal-manifest/` and is passing (see evidence appendix).

Risks/notes:
- “Adversarial / misuse” conformance depth is not covered (expected for later maturity).

### Gate G3: Integrity and trust profile — **STAGED (v0.1) / NOT PASSED (v0.2)**

Why:
- v0.1 signature envelope is explicitly permissive and non-interoperable.
- v0.2 signature profile draft exists (JCS + Ed25519 path), but it is not yet locked into schema/context/fixtures.

Work orders:
- WO-0002 (lock v0.2 profile + fixtures + schema/context)

### Gate G4: Interoperability proof — **PARTIAL**

Why:
- The repo has multi-subject near-real fixtures (venue, display, creator, social profile).
- LAN integration guidance exists and explicitly avoids polluting the spec (LAN details belong in `integrations/`).

What’s missing:
- A formal “journeys → executable tests” proof suite that can be run end-to-end as a concept demonstration.

Work orders:
- WO-0012 (journeys → E2E proof suite)

### Gate G5: Publishing and discoverability — **DOCS PASS / DEPLOYMENT NOT YET PROVEN**

Why:
- Publishing and release docs exist and define stable URL policy.
- Domain architecture is explicit (`universalmanifest.net` vs `myum.net`).

What’s missing:
- Deployment-ready, verified publishing configuration for `universalmanifest.net`.

Work orders:
- WO-0007 (static publish config + resolver skeleton)
- WO-0009 (professional docs site)

### Gate G6: Governance and change control — **PASS (basic)**

Why:
- `docs/DECISIONS.md` exists and is actively maintained.
- Done-done gate policy exists and is explicit.

What’s missing:
- A demonstrated “release cadence over time” is not expected at this maturity.

### Gate G7: Operational realism — **PASS (baseline)**

Why:
- TTL guidance and caching/logging semantics exist in conformance + integration docs.
- “Avoid overbuild” is explicitly stated as a policy in `docs/DEPTH-AND-SCOPE.md` and `docs/DONE-DONE-DEFINITION.md`.

## 4) Completion estimate (what “close” means right now)

For “Early-adopter ready v0.1.x (docs + fixtures + reference validator)”, the project is **substantially complete**.

For “Production-candidate standard”, the project is **not close** because it requires:

- a locked integrity profile (G3)
- deeper conformance suite
- deployment-proven publishing guarantees
- independent interoperability evidence outside LAN

For “World-ready standard”, the project is **not eligible to claim readiness** yet (see `docs/DONE-DONE-DEFINITION.md`, Maturity C requirements).

## 5) Foundations audit (what sources were reviewed)

### In-repo (UM) sources reviewed

- `docs/DEPTH-AND-SCOPE.md`
- `docs/STATE-OF-THE-PROJECT.md`
- `docs/DECISIONS.md`
- `docs/PUBLISHING-AND-VERSIONING.md`
- `docs/RELEASING.md`
- `docs/DOMAIN-ARCHITECTURE.md`
- `docs/DONE-DONE-DEFINITION.md`
- `spec/v0.1/*` and `examples/v0.1/*`
- `packages/universal-manifest/*`

### LAN implementation references reviewed (contextual; )

Copied into this repo for traceable evidence:

- `docs/reports/inputs/lan-platform-universal-manifest/`

Primary original locations:

- `/Users/grig/work/lan/lan-platform/UNIVERSAL-MANIFEST.md`
- `/Users/grig/work/lan/lan-platform/.dev/ai/handoffs/2026-02-11-21-52-41Z-handoff-lan-platform-universal-manifest-stubs.md`

### Indexed external references reviewed (GAS)

- GAS project index:
  - `/Users/grig/.agents/knowledge-sources/project-indexes/2026-02-13_10-03_universal-manifest_master-index.md`
- External UM research archive (inputs):
  - `/Users/grig/Downloads/INBOX-markdown/universal-manifest/`

## 6) Prioritized gap list (recommended next-step sequence)

1. **Lock the v0.2 integrity profile (and keep a Data Integrity path)**
   - Work order: `docs/workorders/WO-0002-signature-profiles-v0-2.md`
2. **Ship deployment-ready hosting skeletons**
   - Work order: `docs/workorders/WO-0007-myum-resolver-and-um-static-publish.md`
3. **Professional documentation site experience**
   - Work orders:
     - `docs/workorders/WO-0011-linux-foundation-project-docs-benchmark.md`
     - `docs/workorders/WO-0009-professional-docs-site-universalmanifest-net.md`
4. **Make “the concept works” provable with journeys → tests**
   - Work order: `docs/workorders/WO-0012-user-journeys-and-e2e-test-suite.md`
5. **LAN integration support (implementation-grade)**
   - Work order: `docs/workorders/WO-0010-build-out-lan-support.md`

## 7) What this audit does NOT claim

- This audit does not claim “world-ready” or “Linux Foundation-ready” today.
- This audit does not claim the resolver exists in production.
- This audit does not claim signature verification interoperability is finalized.

Those claims require passing the relevant gates with evidence packs.

