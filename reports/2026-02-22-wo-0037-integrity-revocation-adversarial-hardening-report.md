# WO-0037 Completion Report — Integrity/Revocation/Adversarial Hardening

Date: 2026-02-22
Work order: `docs/workorders/WO-0037-integrity-profile-revocation-and-adversarial-conformance-hardening.md`

## Summary

Completed aggressive normative-documentation hardening for profile identification and revocation-aware direction, plus adversarial fixture expansion and validation.

## Decision record updates

- `docs/DECISIONS.md`
  - added explicit 2026-02-22 decisions for:
    - Policy A onboarding gate (`WO-0035`)
    - integrity/revocation hardening posture (`WO-0037`)

## Spec/conformance hardening updates

- `spec/v0.2/SIGNATURE-PROFILE.md`
  - added profile-identifier rules (`algorithm` + `canonicalization`)
  - added revocation metadata direction (`statusRef`, `revocationCursor`)
  - added revocation-aware verifier extension behavior
- `spec/v0.2/CONFORMANCE.md`
  - added profile identification and unsupported-profile requirements
  - added revocation extension conformance behavior
  - added explicit adversarial/misuse expectation matrix

## Adversarial fixture set

Added invalid fixtures:

- `examples/v0.2/invalid/invalid-signature-algorithm.jsonld`
- `examples/v0.2/invalid/invalid-signature-canonicalization.jsonld`
- `examples/v0.2/invalid/invalid-signature-created-format.jsonld`
- `examples/v0.2/invalid/missing-signature-key-material.jsonld`
- `examples/v0.2/invalid/invalid-signature-public-key.jsonld`
- `examples/v0.2/invalid/issued-after-expires-signed.jsonld`

## Verification evidence

- `cd packages/universal-manifest && npm test` -> PASS
- `cd site && npm run build:clean` -> PASS
- `rg -n 'integrity|revocation|cursor|adversarial|misuse' docs/DECISIONS.md spec/v0.2/SIGNATURE-PROFILE.md spec/v0.2/CONFORMANCE.md`
  - expected markers present

