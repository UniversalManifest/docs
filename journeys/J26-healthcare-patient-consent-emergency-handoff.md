# J26 — Healthcare Patient Consent Emergency Handoff

## Goal

Prove that a receiving healthcare consumer can read emergency/allergy disclosures, respect audience-scoped record access, preserve ID-only audit retention, and carry the pairwise-to-legacy-record binding needed for emergency handoff.

## Why this matters

Healthcare portability is safety-critical. This journey converts the lane's proof story into executable evidence: emergency and allergy data are readable only through the expected consent posture, clinical record access is scoped to a named emergency department, stale-consent handling is fail-closed by policy, and long-term audit retention stays privacy-preserving.

## Inputs

- Baseline emergency/allergy share fixture:
  - `examples/integrations/healthcare-patient-consent/baseline-emergency-allergy-share-manifest.jsonld`
- Near-real emergency-department handoff fixture:
  - `examples/integrations/healthcare-patient-consent/near-real-emergency-department-handoff-manifest.jsonld`

## Expected behavior

1. Both fixtures preserve a valid v0.1 UM envelope.
2. Baseline consent posture allows emergency contacts and allergy alerts while keeping full record access denied by default.
3. Baseline allergy and emergency-contact facets contain actionable clinical data.
4. Emergency-department record access is restricted to the named organization and `emergency` / `clinical` contexts with explicit field scope and priority.
5. The pairwise patient DID is explicitly bound to the legacy EHR identifier through `identity.crossDidBinding`.
6. Coverage and binding claims preserve verifiable `claimProof` references instead of burying that state in prose.
7. Patient-consent freshness policy remains fail-closed for stale consent.
8. Audit-view policy keeps logs keyed to manifest identifiers and regulatory context rather than full payload retention.

## Executable mapping

- Journey runner row: `J26`
- Implementation: `packages/universal-manifest/scripts/run-journeys.mjs`

## Evidence

Successful execution appears in the generated journey report under `docs/journeys/_artifacts/`.
