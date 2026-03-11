# Journey 08 — Smart-glasses consent enforcement (lane)

## Goal

Demonstrate context-aware smart glasses recording/profile behavior as optional manifest overlays while keeping base UM validation unchanged.

## Inputs

- `examples/v0.1/stubs/smart-glasses-consent-allowed-manifest.jsonld`
- `examples/v0.1/stubs/smart-glasses-consent-denied-manifest.jsonld`

## Steps

1. Validate both fixtures with standard v0.1 validation.
2. Confirm allowed fixture permits capture/profile disclosures for declared keys.
3. Confirm denied fixture blocks capture/profile disclosures for declared keys.
4. Confirm unknown-field tolerance remains intact for smart glasses-specific keys and facets.

## Expected outcomes

- Both fixtures pass baseline v0.1 structural validation.
- Consent semantics are modelled through optional `consents` entries.
- smart glasses-specific keys do not alter required core-field contract.

## Evidence

- `cd packages/universal-manifest && npm test`
- `cd packages/universal-manifest && npm run journeys`
