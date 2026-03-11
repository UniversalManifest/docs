# Journey 15 -- MUM onboarding projection flow

## Goal
Prove that MUM onboarding data can project identity/profile/avatar/inventory overlays into relying worlds while preserving UM core neutrality.

## Inputs
- Fixture: examples/v0.1/stubs/metaverse-mum-onboarding-projection-manifest.jsonld

## Steps
1. Validate required manifest envelope fields.
2. Verify onboarding pointers include profile, avatar, and inventory references.
3. Verify onboarding consents allow profile and inventory projection.
4. Verify cross-world profile facet exists for world projection metadata.

## Expected outcomes
- Fixture passes structural checks.
- Pointer-first onboarding projection is represented.
- Consent posture is explicit and machine-actionable.

## Evidence
- cd packages/universal-manifest && npm test
- cd packages/universal-manifest && npm run journeys
