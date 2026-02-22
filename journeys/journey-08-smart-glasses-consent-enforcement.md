# Journey 08 — Smart-glasses consent enforcement (lane)

## Goal

Demonstrate context-aware AR recording/profile behavior as optional manifest overlays while keeping base UM validation unchanged.

## Inputs

- `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/smart-glasses-ar-consent-allowed-manifest.jsonld`
- `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/smart-glasses-ar-consent-denied-manifest.jsonld`

## Steps

1. Validate both fixtures with standard v0.1 validation.
2. Confirm allowed fixture permits capture/profile disclosures for declared keys.
3. Confirm denied fixture blocks capture/profile disclosures for declared keys.
4. Confirm unknown-field tolerance remains intact for AR-specific keys and shards.

## Expected outcomes

- Both fixtures pass baseline v0.1 structural validation.
- Consent semantics are modelled through optional `consents` entries.
- AR-specific keys do not alter required core-field contract.

## Evidence

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test`
- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`
