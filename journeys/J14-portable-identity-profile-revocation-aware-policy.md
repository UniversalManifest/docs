# Journey 14 -- Portable Identity Profile revocation-aware policy checks

## Goal
Prove that Portable Identity Profile v0.2 fixtures provide signed, freshness-aware metadata for revocation-sensitive policy evaluation.

## Inputs
- Fixture: examples/v0.2/portable-identity-profile-xr-revocation-metadata-v02.jsonld

## Steps
1. Validate required v0.2 manifest envelope fields and signature block presence.
2. Confirm signature metadata includes `algorithm=Ed25519` and `canonicalization=JCS-RFC8785`.
3. Confirm revocation/freshness fields (`statusRef`, `revocationCursor`) are present.
4. Confirm consent and proof-bundle pointer fields required for policy gating are present.

## Expected outcomes
- Fixture passes structural and signature-profile checks in conformance suite.
- Revocation metadata is available for relying-party freshness decisions.
- Policy-relevant pointer and consent fields are present.

## Evidence
- cd packages/universal-manifest && npm test
- cd packages/universal-manifest && npm run journeys

## Normative boundary reminder
This journey demonstrates revocation-aware integration behavior using existing v0.2 optional metadata fields.
