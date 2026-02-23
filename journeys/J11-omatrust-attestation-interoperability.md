# Journey 11 -- OMATrust attestation interoperability lane

## Goal
Prove that Universal Manifest fixtures can represent OMATrust signals across proof-based, trusted-attester, and lifecycle-edge cases without breaking core manifest validation behavior.

## Inputs

- Fixture: /Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/oma-trust-proof-based-service-manifest.jsonld
- Fixture: /Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/oma-trust-trusted-attester-service-manifest.jsonld
- Fixture: /Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/oma-trust-lifecycle-edge-service-manifest.jsonld

## Steps

1. Load each fixture and assert required UM fields exist.
2. For proof-based fixture: verify trust mode and proof-type fields are present and valid.
3. For trusted-attester fixture: verify trusted-attester trust mode plus endorsement/certification claims.
4. For lifecycle-edge fixture: verify revoked and superseded lifecycle states are represented.
5. Verify fixture IDs are unique and no parser-breaking collisions occur.

## Expected outcomes

- All three fixtures pass structural checks.
- Trust mode switching is explicit and deterministic.
- Lifecycle transitions are machine-readable.
- OMATrust lane data coexists with UM core envelope requirements.

## Evidence

- Command: `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`
- Runner implementation: `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`

