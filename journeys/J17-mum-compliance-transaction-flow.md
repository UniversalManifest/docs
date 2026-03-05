# Journey 17 -- MUM compliance transaction flow

## Goal
Prove that trust-sensitive transaction flows can be represented through claims, consent, and compliance-proof pointers.

## Inputs
- Fixture: examples/v0.1/stubs/metaverse-mum-compliance-transaction-manifest.jsonld

## Steps
1. Validate required manifest envelope fields.
2. Verify compliance-status claim is present.
3. Verify compliance-sharing and credential-presentation consents are explicit.
4. Verify compliance-proof pointer is present for verifier fetch.

## Expected outcomes
- Fixture passes structural checks.
- Compliance decision material is pointer-first and consent-gated.
- Transaction policy metadata is available for policy engines.

## Evidence
- cd packages/universal-manifest && npm test
- cd packages/universal-manifest && npm run journeys
