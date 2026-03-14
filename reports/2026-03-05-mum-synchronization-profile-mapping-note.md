# Metaverse MUM Synchronization Profile Mapping Note

Date: 2026-03-05  
Program: Metaverse Universal Manifest Go-Now (`MUM-GN-05`)  
Repository: ``

## Purpose

Record how the synchronization profile maps to metaverse integration behavior, freshness checks, and change-log journeys.

## Mapping

1. Guide source
- `docs/guides/MUM-SYNCHRONIZATION-PROFILE.md`
- Site mirror: `site/src/content/docs/guides/mum-synchronization-profile.md`

2. Integration and cross-link mapping
- Integration lane: `integrations/metaverse.md`
- Site lane: `site/src/content/docs/integrations/metaverse.md`
- Quick references:
  - `docs/guides/QUICK-REFERENCE.md`
  - `site/src/content/docs/guides/quick-reference.md`

3. Fixture and scenario mapping
- `examples/v0.1/stubs/metaverse-mum-consent-propagation-manifest.jsonld`
- `examples/v0.1/stubs/metaverse-mum-preferences-bundle-manifest.jsonld`
- `examples/v0.2/metaverse-mum-cache-freshness-and-change-log-v02.jsonld`

4. Journey mapping
- `docs/journeys/J16-mum-consent-propagation-flow.md`
- `docs/journeys/J19-mum-preferences-bundle-projection-flow.md`
- `docs/journeys/J20-mum-freshness-and-change-log-flow.md`

## Evidence artifacts

- Link/cross-reference scan:
  - `docs/reports/2026-03-05-mum-synchronization-profile-link-scan.txt`
- Validation artifacts:
  - `docs/reports/2026-03-05-gn06-conformance-npm-test.txt`
  - `docs/reports/2026-03-05-gn06-journeys-run.txt`
  - `docs/reports/2026-03-05-gn06-site-build-clean.txt`
