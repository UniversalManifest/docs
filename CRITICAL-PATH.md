# Universal Manifest — Critical Path

This document captures the minimal execution sequence to make Universal Manifest broadly adoptable and eventually “world-ready”.

“World-ready” is not a vibe. It requires passing the gates in `docs/DONE-DONE-DEFINITION.md` with evidence.

## Phase 0 — Define “done” (gates + evidence)

- Read: `docs/DONE-DONE-DEFINITION.md`
- Use: `docs/DONE-DONE-CHECKLIST.md`
- Capture: `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`

## Phase 1 — Make v0.1 adoptable (minimal contract)

Goal: third parties can adopt UM without choosing your identity provider, storage, or framework.

Must-have:

- clear v0.1 contract (required fields + TTL semantics)
- unknown-field tolerance (forward compatibility)
- fixtures: valid + invalid + near-real stubs
- conformance checklist + basic validator tooling

## Phase 2 — Harden interoperability (v0.2 signature profile)

Goal: two independent implementations can sign/verify the same payload the same way.

Must-have:

- signature profile (canonicalization + signing + verification rules)
- signed fixtures and invalid-signature fixtures
- a reference verifier (small, testable, not a framework)

## Phase 3 — Publish like a real standard (`universalmanifest.net`)

Goal: newcomers can understand and adopt the spec quickly, and the URLs are stable.

Must-have:

- spec/docs site with clear navigation and a first-time reader path
- stable URLs for schema/context artifacts
- versioning + immutability policy

## Phase 4 — Make UMIDs resolvable (`myum.net/{UMID}`)

Goal: a consumer can resolve a manifest by UMID with a deterministic contract (headers, caching, errors, privacy posture).

Must-have:

- resolver endpoint contract + examples
- minimum privacy posture (what is public vs not, and why)
- tests that exercise resolution end-to-end

## Phase 5 — Prove it across surfaces (LAN + non-LAN)

Goal: demonstrate the spec is not “just for LAN” while still letting LAN be a primary design driver.

Must-have:

- LAN integration recipe (non-normative)
- at least one non-LAN adopter journey (e.g., profile projection)
- journeys act as proof, not marketing

## Phase 6 — Onboarding clarity + interactive adopter tooling

Goal: first-time adopters can understand UM quickly and validate real manifests without writing custom tooling first.

Must-have:

- clear “What is Universal Manifest?” overview for first-contact readers
- visual onboarding diagrams maintained with source assets
- interactive manifest workbench (import, create, validate, export)
- explicit boundaries between reference tooling and normative spec contract
