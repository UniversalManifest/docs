# Portable Identity Profile Journey Pack Mapping Note

Date: 2026-03-05  
Program: Portable Identity Profile Go-Now (`PIP-GN-03`)  
Repository: ``

## Purpose

Map the new Portable Identity Profile journey IDs to implementation requirements and capture proof artifacts.

## Journey-to-requirement mapping

1. `J12` / `docs/journeys/J12-portable-identity-profile-projection-and-consent.md`
- Requirement coverage: onboarding projection and pointer/consent behavior.
- Executable function: `journeyPortableIdentityProfileProjection`.
- Application: validates profile/avatar pointer sets and consent gating values.

2. `J13` / `docs/journeys/J13-portable-identity-profile-pairwise-privacy.md`
- Requirement coverage: pairwise DID privacy behavior.
- Executable function: `journeyPortableIdentityPairwisePrivacy`.
- Application: validates subject/pointer separation across relying-party variants.

3. `J14` / `docs/journeys/J14-portable-identity-profile-revocation-aware-policy.md`
- Requirement coverage: revocation-aware policy checks.
- Executable function: `journeyPortableIdentityRevocationAwarePolicy`.
- Application: validates v0.2 signature metadata and revocation/freshness fields.

## Runner and report evidence

Runner update:

- `packages/universal-manifest/scripts/run-journeys.mjs`

Journey index update:

- `docs/journeys/README.md`

Execution command:

- `cd packages/universal-manifest && npm run journeys`

Result summary (2026-03-05):

- preflight: `1` pass, `0` fail
- journeys: `14` pass, `0` fail

Artifacts:

- `docs/reports/2026-03-05-gn03-journeys-run.txt`
- `docs/journeys/_artifacts/2026-03-05T15-12-58-478Z-journey-report.json`
