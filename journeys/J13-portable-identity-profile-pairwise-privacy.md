# Journey 13 -- Portable Identity Profile pairwise subject privacy

## Goal
Prove that pairwise subject variants can represent the same verification posture across distinct relying-party contexts without direct cross-context correlation.

## Inputs
- Fixture: examples/v0.1/stubs/portable-identity-profile-xr-pairwise-subject-variant-a.jsonld
- Fixture: examples/v0.1/stubs/portable-identity-profile-xr-pairwise-subject-variant-b.jsonld

## Steps
1. Validate required manifest envelope fields for both fixtures.
2. Verify subjects are distinct across variant A and variant B.
3. Verify manifest `@id` values are distinct.
4. Verify both fixtures maintain equivalent verification claim semantics.
5. Verify profile pointers are present and distinct across variants.

## Expected outcomes
- Both fixtures pass structural checks.
- Pairwise subjects are distinct while preserving equivalent trust posture.
- Profile pointer material remains relying-party specific.

## Evidence
- cd packages/universal-manifest && npm test
- cd packages/universal-manifest && npm run journeys

## Normative boundary reminder
Pairwise subject strategy is an integration pattern; UM core does not mandate one DID method or one pairwise mechanism.
