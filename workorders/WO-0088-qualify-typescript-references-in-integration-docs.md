# WO-0088 — Qualify TypeScript-Specific References in Integration and Template Documents

**Status:** COMPLETED
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Spec-vs-Implementation Boundary Audit (2026-03-01), Recommendations R12, R14, Findings 3.3, Action Items 12, 15
**Tags:** [implementation], [docs]
**Blocks:** Integration docs should not assume TypeScript
**Dependencies:** None
**Estimated effort:** 2-3 hours

## Objective

Qualify or replace TypeScript-specific references in integration documents and the integration template so that integration guidance is language-neutral by default.

## Why this work matters

Integration documents are used by external adopters to understand how to implement UM in their domain. If integration docs assume TypeScript, external adopters using other languages receive the incorrect impression that integration requires TypeScript.

## Scope

### Files to modify

1. **`/Users/grig/work/repo/universalmanifest/integrations/TEMPLATE.md`** (line 122)
   - Change: "run `assertUniversalManifestV01` from the `packages/universal-manifest` test harness"
   - To: "validate against the v0.1 JSON Schema and conformance fixtures. If using the TypeScript reference implementation, run `assertUniversalManifestV01` from the `packages/universal-manifest` test harness."

2. **`/Users/grig/work/repo/universalmanifest/integrations/social.md`** (line 34)
   - Qualify the reference to `packages/universal-manifest -> npm run journeys` as "Executable proof (TypeScript reference implementation):" rather than "Executable proof (cross-runtime adopter):".
   - Add a note that any conformant implementation can serve as proof.

3. **`/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md`** (line 11)
   - Qualify the reference to the TS journey runner script as "TypeScript reference implementation status evidence."

4. **Any other integration files** that reference `packages/universal-manifest` or `npm run` without qualification.

### Verification search

Run `rg -n "packages/universal-manifest|npm run|npm test" /Users/grig/work/repo/universalmanifest/integrations/` to find all instances that need qualification.

## Acceptance criteria

- [ ] Integration TEMPLATE.md does not assume TypeScript as the only validation path.
- [ ] All `packages/universal-manifest` references in integration docs are qualified as "TypeScript reference implementation."
- [ ] The template instructs new integration authors to validate against the schema and fixtures first, with the TypeScript helper as one option.
- [ ] `rg -n "packages/universal-manifest" /Users/grig/work/repo/universalmanifest/integrations/` returns only qualified references.

## Validation commands

- `rg -n "packages/universal-manifest" /Users/grig/work/repo/universalmanifest/integrations/`
- `rg -n "npm run\|npm test" /Users/grig/work/repo/universalmanifest/integrations/`
- Manual review of each match for proper qualification.
