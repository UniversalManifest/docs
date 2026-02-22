# WO-0021 — Smart-glasses consent fixtures and proof journeys

**Status:** COMPLETED  
**Created:** 2026-02-20

## Objective

Turn smart-glasses AR consent guidance into executable fixture and journey evidence while preserving UM core-contract neutrality.

## Scope

In scope:
- add consent-focused fixture cases for recording visibility and auto-profile disclosure behavior.
- add journey/proof coverage for context-based consent enforcement.
- verify unknown-field tolerance remains intact with smart-glasses extension data.
- document outcomes in integration/proof docs as overlays.

Out of scope:
- introducing smart-glasses-specific required core fields in v0.1/v0.2 without versioned spec updates.

## Deliverables

- fixture additions under:
  - `/Users/grig/work/repo/universalmanifest/examples/`
- journey/proof updates under:
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/`
- integration documentation updates:
  - `/Users/grig/work/repo/universalmanifest/integrations/smart-glasses-ar.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/smart-glasses-ar.md`

## Acceptance criteria

- [x] at least two smart-glasses consent fixtures are added (allowed/blocked scenario coverage).
- [x] journey/proof execution includes smart-glasses consent behavior coverage.
- [x] baseline fixture validation and journeys remain PASS.
- [x] docs explicitly preserve boundary for smart-glasses lane.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0018-mum-lineage-and-emerging-integration-codification.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-20-master-forward-worklist.md`

## Completion evidence (2026-02-20)

- Fixtures:
  - `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/smart-glasses-ar-consent-allowed-manifest.jsonld`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/smart-glasses-ar-consent-denied-manifest.jsonld`
- Journey coverage:
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/journey-08-smart-glasses-consent-enforcement.md`
  - executable journey check integrated in:
    - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs` (`J04` overlay assertions)
- Verification:
  - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test` -> PASS
  - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys` -> PASS
