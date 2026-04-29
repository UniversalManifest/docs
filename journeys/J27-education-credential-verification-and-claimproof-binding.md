# J27 — Education Credential Verification and ClaimProof Binding

## Goal

Prove that an education-credential consumer can honor degree and skills disclosure consents, evaluate claim and `claimProof` issuer binding, and follow audience-of-one hiring policy without promoting transcript disclosure to the default path.

## Why this matters

The education lane depends on trustable credential disclosure, not just valid JSON. This journey turns that into executable evidence: baseline degree and certification claims, hiring-context restricted consents, registrar and certification claimProof bindings, and per-claim-expiration policy signals are all checked directly from the fixtures.

## Inputs

- Baseline degree + skill attestation fixture:
  - `examples/integrations/education-credentials/baseline-degree-skill-attestation-manifest.jsonld`
- Near-real employer verification fixture:
  - `examples/integrations/education-credentials/near-real-employer-verification-with-claimproof-manifest.jsonld`

## Expected behavior

1. Both fixtures preserve a valid v0.1 UM envelope.
2. Baseline consent posture allows degree and skill disclosure while keeping transcript access denied by default.
3. Baseline degree, enrollment, and certification claims remain issuer-attested and structurally distinct from manifest TTL.
4. Hiring-context degree verification is restricted to the named employer with explicit scope and priority.
5. Skills disclosure follows the same audience-of-one hiring posture.
6. Embedded and URI-reference `claimProof` shapes are both accepted when the issuer binding remains consistent.
7. The skill-attestation facet and embedded certification `claimProof` agree on the credential identifier.
8. Credential policy keeps per-claim expiration independent from manifest TTL and requires audience binding plus issuer-bound claim proof.

## Executable mapping

- Journey runner row: `J27`
- Implementation: `packages/universal-manifest/scripts/run-journeys.mjs`

## Evidence

Successful execution appears in the generated journey report under `docs/journeys/_artifacts/`.
