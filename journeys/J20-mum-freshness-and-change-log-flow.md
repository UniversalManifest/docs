# Journey 20 -- MUM freshness and change-log flow

## Goal
Prove that v0.2 MUM flows can carry freshness and revocation metadata with explicit change-log references.

## Inputs
- Fixture: examples/v0.2/metaverse-mum-cache-freshness-and-change-log-v02.jsonld

## Steps
1. Validate required v0.2 manifest envelope fields and signature block.
2. Verify signature metadata includes algorithm, canonicalization, statusRef, and revocationCursor.
3. Verify pointers include profile, compliance proof, and change-log references.
4. Verify compliance-share consent is present for trust-sensitive transactions.

## Expected outcomes
- Fixture passes structural/signature-profile checks.
- Freshness and revocation hooks are available for relying-party policy.
- Change-log reference is portable and pointer-first.

## Evidence
- cd packages/universal-manifest && npm test
- cd packages/universal-manifest && npm run journeys
