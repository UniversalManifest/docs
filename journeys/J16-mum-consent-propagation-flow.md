# Journey 16 -- MUM consent propagation flow

## Goal
Prove that consent state can be transported and enforced consistently across multiple metaverse relying worlds.

## Inputs
- Fixture: examples/v0.1/stubs/metaverse-mum-consent-propagation-manifest.jsonld

## Steps
1. Validate required manifest envelope fields.
2. Verify consent matrix includes profile/social/voice/recording/preferences keys.
3. Verify consent values match expected enforcement posture.
4. Verify consent-envelope shard carries propagation scope metadata.

## Expected outcomes
- Fixture passes structural checks.
- Consent decisions remain explicit and portable.
- Propagation scope metadata is available for relying-party enforcement.

## Evidence
- cd packages/universal-manifest && npm test
- cd packages/universal-manifest && npm run journeys
