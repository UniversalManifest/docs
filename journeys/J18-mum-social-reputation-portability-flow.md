# Journey 18 -- MUM social and reputation portability flow

## Goal
Prove that social graph and reputation overlays can be transported across worlds with explicit disclosure controls.

## Inputs
- Fixture: examples/v0.1/stubs/metaverse-mum-social-reputation-portability-manifest.jsonld

## Steps
1. Validate required manifest envelope fields.
2. Verify reputation-level and reputation-score claims are present.
3. Verify social and reputation pointers are present.
4. Verify social/reputation disclosure consents align with expected policy.

## Expected outcomes
- Fixture passes structural checks.
- Social and reputation references are portable and pointer-first.
- Disclosure posture is explicit and auditable.

## Evidence
- cd packages/universal-manifest && npm test
- cd packages/universal-manifest && npm run journeys
