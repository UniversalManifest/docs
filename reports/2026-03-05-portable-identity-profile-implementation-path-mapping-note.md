# Portable Identity Profile XR Implementation Path Mapping Note

Date: 2026-03-05  
Program: Portable Identity Profile Go-Now (`PIP-GN-05`)  
Repository: `/Users/grig/work/repo/universalmanifest`

## Purpose

Record how the implementation-path guide maps to existing Portable Identity Profile fixtures, journeys, and integration behavior.

## Mapping

1. Guide source
- `docs/guides/PORTABLE-IDENTITY-PROFILE-XR-IMPLEMENTATION-PATH.md`
- Site mirror: `site/src/content/docs/guides/portable-identity-profile-xr-implementation-path.md`

2. Consumer algorithm and consent enforcement mapping
- Integration lane: `integrations/portable-identity-profile-xr.md`
- Site lane: `site/src/content/docs/integrations/portable-identity-profile-xr.md`

3. Fixture mapping
- `examples/v0.1/stubs/portable-identity-profile-xr-minimal-manifest.jsonld`
- `examples/v0.1/stubs/portable-identity-profile-xr-avatar-pointers-manifest.jsonld`
- `examples/v0.1/stubs/portable-identity-profile-xr-consent-matrix-manifest.jsonld`
- `examples/v0.1/stubs/portable-identity-profile-xr-pairwise-subject-variant-a.jsonld`
- `examples/v0.1/stubs/portable-identity-profile-xr-pairwise-subject-variant-b.jsonld`
- `examples/v0.2/portable-identity-profile-xr-revocation-metadata-v02.jsonld`

4. Journey mapping
- `docs/journeys/J12-portable-identity-profile-projection-and-consent.md`
- `docs/journeys/J13-portable-identity-profile-pairwise-privacy.md`
- `docs/journeys/J14-portable-identity-profile-revocation-aware-policy.md`

## Evidence artifacts

- Link/cross-reference scan:
  - `docs/reports/2026-03-05-portable-identity-profile-implementation-path-link-scan.txt`
- Validation artifacts:
  - `docs/reports/2026-03-05-gn06-conformance-npm-test.txt`
  - `docs/reports/2026-03-05-gn06-journeys-run.txt`
  - `docs/reports/2026-03-05-gn06-site-build-clean.txt`
