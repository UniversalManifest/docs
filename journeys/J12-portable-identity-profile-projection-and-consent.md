# Journey 12 -- Portable Identity Profile XR projection and consent behavior

## Goal
Prove that Portable Identity Profile fixtures support baseline XR projection using pointer-first profile/avatar assets with explicit consent gating.

## Inputs
- Fixture: examples/v0.1/stubs/portable-identity-profile-xr-minimal-manifest.jsonld
- Fixture: examples/v0.1/stubs/portable-identity-profile-xr-avatar-pointers-manifest.jsonld
- Fixture: examples/v0.1/stubs/portable-identity-profile-xr-consent-matrix-manifest.jsonld

## Steps
1. Validate required manifest envelope fields on all three fixtures.
2. Confirm minimal fixture exposes the canonical `portableIdentity.profile` pointer.
3. Confirm avatar fixture exposes `portableIdentity.avatar`, `portableIdentity.wearables`, and `portableIdentity.translationProfile` pointers.
4. Confirm consent fixture enforces explicit policy values for public profile and voice capture behavior.

## Expected outcomes
- All fixtures pass structural checks.
- Pointer-first profile/avatar projection fields are present.
- Consent values support default-deny relying-party behavior.

## Evidence
- cd packages/universal-manifest && npm test
- cd packages/universal-manifest && npm run journeys

## Normative boundary reminder
This journey verifies integration-lane behavior and sample key usage; it does not add new UM core required fields.
