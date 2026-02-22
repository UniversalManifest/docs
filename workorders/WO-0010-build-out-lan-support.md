# WO-0010 — Build out Universal Manifest support for LAN

**Status:** COMPLETED  
**Created:** 2026-02-12

## Objective

Expand concrete Universal Manifest support for Local Artist Network (LAN) from draft guidance to implementation-ready contracts and reference assets.

## Scope

In scope:

- Refine LAN integration contract across:
  - Edge issuer behavior
  - Display consumer behavior
  - Admin enrollment/policy flows
- Define endpoint contract for LAN UM retrieval and update signaling
- Provide LAN-focused fixture set and mapping docs
- Provide reference implementation stubs for LAN-side manifest handling (validation/caching/logging semantics)

Out of scope:

- Full production deployment across LAN environments
- Replacing existing LAN auth/identity systems end-to-end in one pass

## Deliverables

- Integration contract update:
  - `integrations/lan.md` (expanded, implementation-grade)
- LAN profile:
  - `integrations/lan-profile.md` (LAN conventions; )
- LAN fixture mapping:
  - `docs/reports/2026-02-12-lan-manifest-support-map.md`
- Reference code stubs (if placed in this repo):
  - `packages/universal-manifest/src/lan/` (or equivalent)

## Acceptance criteria

- [x] LAN edge/display/admin responsibilities are explicit and testable
- [x] Manifest retrieval/update signaling contract is documented with examples
- [x] Caching and logging requirements align with existing decisions
- [x] Fixtures cover key LAN runtime scenarios
- [x] Reference stubs compile and pass tests (no additional code stubs required in this WO)

## Dependencies

- `integrations/lan.md`
- `docs/DECISIONS.md`
- `spec/v0.1/CONFORMANCE.md`
- `docs/workorders/WO-0007-myum-resolver-and-um-static-publish.md`
