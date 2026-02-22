# WO-0014 — Interactive Manifest Workbench on universalmanifest.net

**Status:** COMPLETED  
**Created:** 2026-02-18

## Objective

Ship a first-class interactive workbench page on `universalmanifest.net` where implementers can:

- import an existing manifest
- inspect it in an explorer/editor
- add/update manifest types and sections
- validate conformance for the selected target version
- export the updated/new manifest

This is a CEO-priority proof surface for real adopter usability.

## Scope

In scope:

- Add a dedicated workbench route in the docs site (or linked tool surface) with:
  - Import: JSON/JSON-LD from file or paste
  - Explorer: structured view of core sections (`@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`, `shards`, `pointers`, `signature`)
  - Editor: guided add/update/remove flows for known fields
  - Validation: run structural + conformance checks and return actionable errors
  - Export: JSON and JSON-LD outputs
- Provide at least one starter template (minimal v0.1 manifest).
- Document browser-only privacy posture (no server-side storage by default).

Out of scope:

- Full identity/key management UX
- Multi-tenant backend storage
- Full registry governance UI

## Deliverables

- Workbench implementation in site codebase (`site/`)
- Workbench documentation page and usage instructions
- Test coverage for import/validate/export happy path and core error paths

## Corpus-Derived Requirement Addendum (2026-02-19T04:55:00Z)

Source linkage:
- `/Users/grig/work/repo/universalmanifest/.dev/ai/specs/2026-02-19-ia-delta-from-full-corpus.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/ingestion/records/2026-02-18-cross-source-conflicts.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`

Requirements added from full-corpus synthesis:
- Profile mode handling MUST remain identity-method neutral in core fields (`CON-UM-003`).
- Presets MUST include:
  - one cross-domain baseline manifest template
  - one metaverse exemplar template marked (`CON-UM-005`)
- Validation UX MUST map errors to current conformance surfaces (required fields/TTL/signature profile) and avoid creating a second contract (`CON-UM-002`, `CON-UM-004`).
- Workbench copy MUST preserve standards-neutral framing and place ecosystem-specific narrative in integration context (`CON-UM-006`).

## Acceptance criteria

- [x] `universalmanifest.net` exposes a discoverable Workbench entry point.
- [x] A user can import a manifest and see parsed sections in the explorer.
- [x] A user can create a new minimal manifest from scratch.
- [x] Validation reports required-field and TTL errors deterministically.
- [x] Export produces valid JSON/JSON-LD that round-trips through validation.
- [x] Tool is documented with clear limits (what it validates vs does not validate).
- [x] Tool exposes profile-mode behavior while keeping core identity method neutral.
- [x] Starter templates include cross-domain baseline + metaverse exemplar.

## Completion Evidence (2026-02-19T21:14:00Z)

Implementation artifacts:
- `/Users/grig/work/repo/universalmanifest/site/public/getting-started/workbench/`
- `/Users/grig/work/repo/universalmanifest/site/public/workbench/workbench.js`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/workbench.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/quick-start.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md`

Functional verification report:
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/2026-02-19-workbench-functional-checks.md`
- screenshot evidence:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/2026-02-19-workbench-ui-verification.png`

## Dependencies

- `packages/universal-manifest/` validation tooling
- `spec/v0.1/` and `spec/v0.2/` artifacts
- `docs/DONE-DONE-DEFINITION.md` and conformance pages
