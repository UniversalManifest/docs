# WO-0010 — Build out Universal Manifest support for reference implementation

**Status:** COMPLETED  
**Created:** 2026-02-12

## Objective

Expand concrete Universal Manifest support for the reference implementation from draft guidance to implementation-ready contracts and reference assets.

## Scope

In scope:

- Refine reference implementation integration contract across:
  - Edge issuer behavior
  - Display consumer behavior
  - Admin enrollment/policy flows
- Define endpoint contract for reference implementation UM retrieval and update signaling
- Provide reference implementation-focused fixture set and mapping docs
- Provide reference implementation stubs for reference implementation-side manifest handling (validation/caching/logging semantics)

Out of scope:

- Full production deployment across reference implementation environments
- Replacing existing reference implementation auth/identity systems end-to-end in one pass

## Deliverables

- Integration contract update:
  - `integrations/reference-runtime.md` (expanded, implementation-grade)
- reference implementation profile:
  - `integrations/runtime-profile.md` (reference implementation conventions; )
- reference implementation fixture mapping:
  - `docs/reports/2026-02-12-reference-implementation-manifest-support-map.md`
- Reference code stubs (if placed in this repo):
  - `packages/universal-manifest/src/` (or equivalent)

## Acceptance criteria

- [x] UM edge/display/admin responsibilities are explicit and testable
- [x] Manifest retrieval/update signaling contract is documented with examples
- [x] Caching and logging requirements align with existing decisions
- [x] Fixtures cover key reference implementation runtime scenarios
- [x] Reference stubs compile and pass tests (no additional code stubs required in this WO)

## Dependencies

- `integrations/reference-runtime.md`
- `docs/DECISIONS.md`
- `spec/v0.1/CONFORMANCE.md`
- `docs/workorders/WO-0007-myum-resolver-and-um-static-publish.md`
