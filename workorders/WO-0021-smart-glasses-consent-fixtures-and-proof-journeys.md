# WO-0021 — Smart-glasses consent fixtures and proof journeys

**Status:** NOT_STARTED  
**Created:** 2026-02-20

## Objective

Turn smart-glasses AR consent guidance into executable fixture and journey evidence while preserving UM core-contract neutrality.

## Scope

In scope:
- add consent-focused fixture cases for recording visibility and auto-profile disclosure behavior.
- add journey/proof coverage for context-based consent enforcement.
- verify unknown-field tolerance remains intact with smart-glasses extension data.
- document outcomes in integration/proof docs as non-normative overlays.

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

- [ ] at least two smart-glasses consent fixtures are added (allowed/blocked scenario coverage).
- [ ] journey/proof execution includes smart-glasses consent behavior coverage.
- [ ] baseline fixture validation and journeys remain PASS.
- [ ] docs explicitly preserve non-normative boundary for smart-glasses lane.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0018-mum-lineage-and-emerging-integration-codification.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-20-master-forward-worklist.md`

