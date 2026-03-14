# Metaverse MUM Fixture Pack Scenario Mapping Note

Date: 2026-03-05  
Program: Metaverse Universal Manifest Go-Now (`MUM-GN-03`)  
Repository: ``

## Purpose

Map each new MUM fixture to its scenario requirement and capture execution evidence.

## Fixture-to-scenario mapping

1. `examples/v0.1/stubs/metaverse-mum-onboarding-projection-manifest.jsonld`
- Scenario coverage: Scenario 1 (cross-platform identity and asset onboarding/projection).
- Application: exposes `metaverse.profile`, `metaverse.avatar`, and `metaverse.inventory` pointers for world projection.

2. `examples/v0.1/stubs/metaverse-mum-consent-propagation-manifest.jsonld`
- Scenario coverage: Scenario 2 (unified privacy and consent control).
- Application: carries explicit consent states for profile/social/voice/recording/preferences synchronization.

3. `examples/v0.1/stubs/metaverse-mum-compliance-transaction-manifest.jsonld`
- Scenario coverage: Scenario 3 (secure and compliant transactions).
- Application: combines compliance-status claim + compliance-proof pointer + compliance-sharing consent.

4. `examples/v0.1/stubs/metaverse-mum-social-reputation-portability-manifest.jsonld`
- Scenario coverage: Scenario 4 (persistent social graph and reputation).
- Application: carries social graph + reputation pointers with disclosure consents.

5. `examples/v0.1/stubs/metaverse-mum-preferences-bundle-manifest.jsonld`
- Scenario coverage: Scenario 5 (preference/security/credential bundle behavior).
- Application: models language/financial/logistics/security/credential preference families with sync consent.

6. `examples/v0.2/metaverse-mum-cache-freshness-and-change-log-v02.jsonld`
- Scenario coverage: Freshness/change-log behavior required by MUM operational continuity.
- Application: includes signature + `statusRef` + `revocationCursor` and a change-log pointer for freshness-aware sync policies.

## Validation evidence

Validation command:

- `cd packages/universal-manifest && npm test`

Result summary (2026-03-05):

- valid fixtures: `38` passed
- valid fixtures: `0` failed
- invalid fixtures: `22` failed as expected
- invalid fixtures: `0` unexpected pass

Artifact:

- `docs/reports/2026-03-05-gn03-conformance-npm-test.txt`
