# Decisions (Universal Manifest)

## 2026-02-11 — v0.1 bootstrap decisions

### Separate spec repo

- The Universal Manifest lives as a **fully separate repo** at `/Users/grig/work/repo/universalmanifest/`.
- LAN consumes it, but it is versioned and maintained independently.

### Manifest ID generation (`@id`)

- v0.1 recommendation: issuers generate `@id` as `urn:uuid:<uuidv4>`.
- Rationale: globally unique, offline-safe, and avoids premature content-addressing commitments.

### Device caching + logging (NVIDIA Shield / public display)

- Cache the **full manifest JSON** while actively in use.
- Persist only **manifest ID references** (`@id`) in logs/telemetry.
- Future recovery may use those IDs, but recovery workflows are intentionally out of scope for v0.1.

### Security scope (v0.1)

- `signature` is present only as a permissive placeholder envelope.
- Cryptographic signing/verification formats are intentionally deferred until canonicalization rules and integration needs are confirmed.

## 2026-02-12 — Public domain split for standards vs resolver

### Standards + docs host

- Canonical public standards/docs domain is **`universalmanifest.net`**.
- This site hosts learning material and versioned spec artifacts intended for external adoption.

### UMID resolver host

- Canonical resolver domain is **`myum.net`**, with lookup pattern: `https://myum.net/{UMID}`.
- This domain is for manifest resolution/retrieval behavior, not spec governance docs.

### Compatibility policy

- Existing `localartist.network` namespace references in v0.1 are treated as compatibility aliases.
- New publishing guidance uses `universalmanifest.net` as canonical for spec artifacts.
- Previously published URLs must remain resolvable (no breaking URL churn).

## 2026-02-13 — Official done-done framework adopted

### Decision

- Adopt a formal, gate-based done-done framework as the official release readiness authority:
  - `docs/DONE-DONE-DEFINITION.md`
  - `docs/DONE-DONE-CHECKLIST.md`
  - `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`

### Rationale

- Prevent ambiguous completion claims.
- Require auditable evidence for release readiness.
- Separate “early-adopter ready” from “world-ready” using explicit maturity targets.

### Policy impact

- Future release claims MUST include a completed evidence pack.
- “Done done” claims without gate evidence are invalid.

## 2026-02-13 — Record-primitive vision direction captured

### Decision

- Capture CEO direction that Universal Manifest composition should center on a **Record** primitive:
  - records can be leaf or nested/container
  - records can be exchanged via push and pull/request
  - records may declare their own schema/standards context
  - records/attributes require permission states with field-level policy control

### Rationale

- Supports multi-domain extensibility without forcing a single rigid schema too early.
- Aligns with local-first and cross-system interoperability goals.

### Policy impact

- Treat this as vision-level guidance until translated into normative spec artifacts.
- Any normative adoption of record semantics/permissions must flow through versioned spec + conformance updates.

## 2026-02-17 — Journeys → tests as proof of concept (validation direction)

### Decision

- Define canonical **user journeys** for Universal Manifest adoption and map them to an **executable end-to-end test suite** as the primary evidence mechanism for “the concept works”.

### Rationale

- Prevent “done by documentation” without runnable proof.
- Provide a clear, adoptable path for external implementers (Linux Foundation-grade expectations).
- Keep LAN as an important consumer without making UM “about LAN”.

### Policy impact

- Treat “journeys → tests” as a required output for maturity claims and future “done done” evidence packs.
- Tracked as work order: `docs/workorders/WO-0012-user-journeys-and-e2e-test-suite.md`.

## 2026-02-17 — v0.2 signature profile baseline (interoperability hardening)

### Decision

- Adopt a pragmatic, adoption-first v0.2 integrity baseline:
  - Canonicalization: **JCS (RFC 8785)**
  - Signature: **Ed25519**
  - Signature encoding: **base64url**
- Keep a future **Data Integrity** path as additive (not either-or).

### Rationale

- JCS + Ed25519 is broadly implementable across languages without requiring JSON-LD tooling.
- The signature profile is a major interop-hardening step without forcing identity method standardization.

### Policy impact

- v0.2 artifacts exist in `spec/v0.2/` (schema + context + conformance + profile).
- Fixture verification and harness support for v0.2 must validate the signature profile deterministically.

## 2026-02-17 — TS helper package distribution policy (do not publish yet)

### Decision

- Keep the TypeScript helper package **private/internal** for now:
  - `packages/universal-manifest/` (`@localartistnetwork/universal-manifest`)

### Rationale

- Avoid “public SDK drift” while the spec is still in v0.x and publishing/governance is stabilizing.
- The primary adoption contract is the published spec artifacts + fixtures, not a single implementation library.

### Policy impact

- No npm or public registry publishing until:
  - v0.2 artifacts are published at stable URLs, and
  - the docs site for `universalmanifest.net` is “implementer-grade”.

## 2026-02-17 — CI verification + endpoint smoke added (repeatable proof)

### Decision

- Add a repo-native CI verification workflow and a small endpoint smoke script.
  - CI workflow: `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml`
  - Endpoint smoke: `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/smoke-endpoints.mjs`

### Rationale

- Make “proof” repeatable and reviewer-friendly for adopters (Linux Foundation-grade expectation).
- Provide an outside-in contract check for `universalmanifest.net` (docs) and `myum.net` (resolver) without requiring a front-end app.

### Policy impact

- Post-deploy checks for publishing should include endpoint smoke:
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest` → `npm run smoke:endpoints:prod`

## 2026-02-17 — Repository relocation + GAS split onboarding model

### Decision

- Relocate Universal Manifest from:
  - `/Users/grig/work/repo/universalmanifest`
- To:
  - `/Users/grig/work/repo/universalmanifest`
- Align agent onboarding to the GAS split model:
  - `AGENTS.md` = immutable global rules copy
  - `PROJECT-RULES.md` = project-specific rules and onboarding
- Expand `.dev` structure to GAS-standard working directories.

### Rationale

- Reduce ongoing LAN/UM context bleed from shared parent path.
- Make project identity, onboarding, and handoffs clearer for future agents.
- Match current GAS guidance and tooling assumptions.

### Policy impact

- All new path references should use `/Users/grig/work/repo/universalmanifest`.
- Legacy path references are historical only and should be updated when touched.
