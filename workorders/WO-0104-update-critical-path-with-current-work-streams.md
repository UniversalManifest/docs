# WO-0104 — Update CRITICAL-PATH.md with Current Work Streams

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P0 (Critical)
**Source:** Documentation Freshness Audit (2026-03-01), Section 5.3, Priority 3 recommendation item 6
**Tags:** [docs]
**Blocks:** Project roadmap visibility — critical path document is primary planning reference
**Dependencies:** None
**Estimated effort:** 2-3 hours

## Objective

Update `docs/CRITICAL-PATH.md` to include the current work streams that are not mentioned: the Interactive Sandbox wave, the External Adopter wave, the teaching scripts/visual identity system, and the code examples ecosystem.

## Why this work matters

The freshness audit found that CRITICAL-PATH.md has received no commits during the 2026-02-22 to 2026-03-01 period and stops at Phase 9 (Drift governance). It does not mention the sandbox wave (WO-0060-0068, HIGHEST PRIORITY per CEO mandate), the external adopter wave (WO-0053-0059, blocking Gate G4/G6), the teaching scripts system, or the code examples ecosystem. As the project's primary planning reference, this document must reflect current reality.

## Scope

### File to modify

**`/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`**

### Phases/milestones to add

1. **Interactive Sandbox Wave** (WO-0060-0068) — HIGHEST PRIORITY per CEO mandate
   - Foundation and browser validator
   - Three-panel layout and step engine
   - Scenario modal and navigation
   - Getting Started, Trust & Verification, Integration Lane, and Edge Case/Advanced scenarios
   - Visual polish and CI parity

2. **Sandbox V2 Redesign** (WO-0069-0080) — HierarchyExplorer, DetailsCard, EntityColumn, ProtocolLens, SubjectPanel, SandboxLayoutV2, SandboxEngineV2

3. **External Adopter Verification Wave** (WO-0053-0059) — blocks Gates G4 and G6
   - Standalone conformance test suite
   - Reference implementation repository
   - Adopter onboarding document package
   - Adopter feedback loop
   - Spec-vs-implementation documentation clarity
   - v0.1-to-v0.2 migration guide
   - Governance completion

4. **Teaching Scripts and Visual Identity System** — Stage 3, 20 script ideas defined

5. **Code Examples Ecosystem** — 10 runnable examples, demo app

### Status updates for existing phases

Review and update the status of existing phases (1-9) to reflect completions from the past week.

## Acceptance criteria

- [ ] CRITICAL-PATH.md includes the sandbox wave as a phase or milestone.
- [ ] CRITICAL-PATH.md includes the external adopter wave.
- [ ] CRITICAL-PATH.md includes the teaching scripts system.
- [ ] CRITICAL-PATH.md includes the code examples ecosystem.
- [ ] Existing phase statuses are current.
- [ ] The ordering reflects actual priority (sandbox first per CEO mandate).

## Validation commands

- `rg -n "sandbox\|Sandbox" /Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md` (should find references)
- `rg -n "adopter\|Adopter" /Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md` (should find references)
- Manual review of phase ordering and completeness.
