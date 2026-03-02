# WO-0108 — Create Formal Work Order Files for Sandbox V2 (WO-0069 through WO-0080)

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Documentation Freshness Audit (2026-03-01), Section 5.8
**Tags:** [docs], [structural]
**Blocks:** Work order tracking completeness
**Dependencies:** WO-0107 (sandbox should be committed first)
**Estimated effort:** 2-3 hours

## Objective

Create formal work order files for WO-0069 through WO-0080 (Sandbox V2 redesign) and add them to WO-INDEX.md. These 12 WOs currently exist only in handoff narrative files with no formal WO documentation.

## Why this work matters

The freshness audit found that the Sandbox V2 redesign (WO-0069 through WO-0080) was completed per the 2026-03-01 handoff but has no WO files and no index entries. These 12 WOs exist only in the handoff narrative. Without formal WO files, the work cannot be tracked, verified, or referenced by other work orders.

## Scope

### Source of truth

The handoff files that describe the V2 work:
- `.dev/ai/handoffs/2026-03-01-03-55-34Z-handoff-universalmanifest.md`
- `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

### Work order files to create

Create files for WO-0069 through WO-0080 at `docs/workorders/WO-00NN-short-description.md`, following the existing format. Each should include:
- Status (COMPLETED, per handoff)
- Objective
- Scope
- Key files created
- Acceptance criteria (satisfied)

### WO-INDEX.md update

Add all 12 new WO entries to the Sandbox V2 section of `docs/workorders/WO-INDEX.md`.

## Acceptance criteria

- [ ] 12 work order files exist (WO-0069 through WO-0080).
- [ ] Each file follows the standard WO format.
- [ ] Each file's status reflects the completed state.
- [ ] WO-INDEX.md includes entries for all 12 WOs.
- [ ] A new "Sandbox V2 Redesign" section exists in WO-INDEX.md.

## Validation commands

- `ls /Users/grig/work/repo/universalmanifest/docs/workorders/WO-007*.md` (should show WO-0069 through WO-0079)
- `ls /Users/grig/work/repo/universalmanifest/docs/workorders/WO-0080*.md` (should exist)
- `rg -n "WO-0069\|WO-0080" /Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md` (should find entries)
