# WO-0014 — Interactive Manifest Workbench on universalmanifest.net

**Status:** OPEN  
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

## Acceptance criteria

- [ ] `universalmanifest.net` exposes a discoverable Workbench entry point.
- [ ] A user can import a manifest and see parsed sections in the explorer.
- [ ] A user can create a new minimal manifest from scratch.
- [ ] Validation reports required-field and TTL errors deterministically.
- [ ] Export produces valid JSON/JSON-LD that round-trips through validation.
- [ ] Tool is documented with clear limits (what it validates vs does not validate).

## Dependencies

- `packages/universal-manifest/` validation tooling
- `spec/v0.1/` and `spec/v0.2/` artifacts
- `docs/DONE-DONE-DEFINITION.md` and conformance pages
