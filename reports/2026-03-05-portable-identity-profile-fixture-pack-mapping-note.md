# Portable Identity Profile Fixture Pack Mapping Note

Date: 2026-03-05  
Program: Portable Identity Profile Go-Now (`PIP-GN-02`)  
Repository: ``

## Purpose

Document how the new Portable Identity Profile fixtures map to implementation requirements, and record validation evidence.

## Fixture-to-requirement mapping

1. `examples/v0.1/stubs/portable-identity-profile-xr-minimal-manifest.jsonld`
- Requirement covered: minimal interoperable profile projection baseline.
- Application: consumer can resolve only core identity + minimal claim/consent envelope and continue safely.

2. `examples/v0.1/stubs/portable-identity-profile-xr-avatar-pointers-manifest.jsonld`
- Requirement covered: pointer-first avatar and wearable asset portability.
- Application: consumer resolves external avatar/wearable references without embedding large assets in the manifest.

3. `examples/v0.1/stubs/portable-identity-profile-xr-consent-matrix-manifest.jsonld`
- Requirement covered: explicit consent gating for profile/voice/capture/similar actions.
- Application: relying party checks consent matrix values before any disclosure or capture path.

4. `examples/v0.1/stubs/portable-identity-profile-xr-pairwise-subject-variant-a.jsonld`
- Requirement covered: pairwise subject variant support for pseudonymous correlation resistance.
- Application: relying party A receives one subject variant and cannot directly correlate across relying parties.

5. `examples/v0.1/stubs/portable-identity-profile-xr-pairwise-subject-variant-b.jsonld`
- Requirement covered: second pairwise variant to prove multi-relying-party separation behavior.
- Application: relying party B receives a distinct subject variant while preserving identical policy semantics.

6. `examples/v0.2/portable-identity-profile-xr-revocation-metadata-v02.jsonld`
- Requirement covered: signed profile envelope with revocation freshness hooks.
- Application: consumer verifies signature, then evaluates `statusRef` and `revocationCursor` for trust/freshness policy.

## Validation evidence

Validation command executed:

- `cd packages/universal-manifest && npm test`

Validation result summary (2026-03-05):

- valid fixtures: `32` passed
- valid fixtures: `0` failed
- invalid fixtures: `22` failed as expected
- invalid fixtures: `0` unexpected pass

## Notes

- During execution, signing mismatch was identified in `packages/universal-manifest/scripts/sign-fixture.mjs` (older keypair). The script was updated to the active v0.2 fixture keypair and the v0.2 Portable Identity Profile revocation fixture was re-signed.
