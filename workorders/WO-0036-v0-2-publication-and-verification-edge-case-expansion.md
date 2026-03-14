# WO-0036 — v0.2 publication and verification edge-case expansion

**Status:** COMPLETED
**Created:** 2026-02-22
**Priority:** MEDIUM
**Source:** `docs/STATE-OF-THE-PROJECT.md`

## Objective

Advance v0.2 from draft artifacts toward stable publication readiness by publishing v0.2 artifacts at stable URLs and expanding verification edge-case fixtures.

## Why this work matters

`STATE-OF-THE-PROJECT` still identifies v0.2 publication and edge-case verification as remaining work. This WO converts that remaining milestone into explicit execution deliverables.

## Scope

In scope:

- Publish and verify stable delivery paths for v0.2 schema/context/profile artifacts.
- Expand v0.2 edge-case fixture coverage (valid and invalid) for signature/verification-adjacent behavior.
- Ensure docs and release guidance reflect actual published v0.2 artifact URLs and current maturity boundaries.

Out of scope:

- Additional integrity-profile families beyond current v0.2 baseline (tracked by `WO-0037`).
- Revocation cursor/events normative direction (tracked by `WO-0037`).

## Required deliverables

1. Updated v0.2 publication references in:
   - `docs/PUBLISHING-AND-VERSIONING.md`
   - `docs/RELEASING.md`
2. Expanded v0.2 fixtures in:
   - `examples/v0.2/`
3. Conformance updates in:
   - `spec/v0.2/CONFORMANCE.md`
4. Validation evidence report in:
   - `docs/reports/`

## Acceptance criteria

- [x] v0.2 artifact URLs used in docs resolve and match published files.
- [x] v0.2 fixtures include additional verification edge-case coverage beyond current baseline.
- [x] Package test/journey baseline remains green after fixture expansion.
- [x] Publishing/releasing docs clearly communicate v0.2 status and required adopter validation posture.

## Validation commands

- `cd packages/universal-manifest && npm test`
- `cd packages/universal-manifest && npm run journeys`
- `cd site && npm run build:clean`
- `rg -n 'v0.2|stable URL|schema.jsonld|schema.json|SIGNATURE-PROFILE' docs/PUBLISHING-AND-VERSIONING.md docs/RELEASING.md spec/v0.2/CONFORMANCE.md`

## Completion evidence (2026-02-22)

- Report:
  - `docs/reports/2026-02-22-wo-0036-v0.2-publication-and-edge-case-expansion-report.md`
- Updated docs/spec:
  - `docs/PUBLISHING-AND-VERSIONING.md`
  - `docs/RELEASING.md`
  - `spec/v0.2/CONFORMANCE.md`
  - `spec/v0.2/README.md`
- Added fixtures:
  - `examples/v0.2/invalid/invalid-signature-algorithm.jsonld`
  - `examples/v0.2/invalid/invalid-signature-canonicalization.jsonld`
  - `examples/v0.2/invalid/invalid-signature-created-format.jsonld`
  - `examples/v0.2/invalid/missing-signature-key-material.jsonld`
  - `examples/v0.2/invalid/invalid-signature-public-key.jsonld`
  - `examples/v0.2/invalid/issued-after-expires-signed.jsonld`
