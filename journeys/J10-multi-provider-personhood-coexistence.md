# Journey 10 -- Multi-provider personhood credential coexistence (lane)

## Goal
Prove that Universal Manifest fixtures can represent multiple proof-of-personhood credentials from different providers bound to social identities (Mastodon, Bluesky), support multiple DID methods, and include Chia credential lane references — all coexisting in valid manifests.

## Inputs
- Fixture: examples/v0.1/stubs/mastodon-personhood-multi-credential-manifest.jsonld
- Fixture: examples/v0.1/stubs/bluesky-personhood-multi-credential-manifest.jsonld
- Fixture: examples/v0.1/stubs/multi-did-method-coverage-manifest.jsonld
- Fixture: examples/v0.1/stubs/did-vc-credential-lane-manifest.jsonld

## Steps
1. Load each fixture and validate required manifest fields.
2. For mastodon and bluesky fixtures: verify at least 2 personhood credential claims exist per manifest.
3. For multi-did fixture: verify at least 3 distinct DID method references.
4. For chia fixture: verify Chia-specific credential and identity binding claims.
5. Verify consent-default-deny: absent consent keys are treated as denied.
6. Verify all fixtures can coexist (no conflicting @id or subject collisions).

## Expected outcomes
- All 4 fixtures pass structural validation.
- Multi-credential coexistence is proven (2+ claims per social manifest).
- Multi-DID method coverage is proven (3+ methods).
- Chia lane has concrete credential mapping.
- No policy conflicts between coexisting manifests.

## Evidence
- cd packages/universal-manifest && npm run journeys
- Fixture paths listed above

## Normative boundary reminder
This journey validates integration lanes. Provider-specific claims and DID method selections are guidance, not spec requirements.
