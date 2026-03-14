# WO-0087 — Reposition TypeScript Helper in Agent Briefing and Explainer Documents

**Status:** COMPLETED
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Spec-vs-Implementation Boundary Audit (2026-03-01), Recommendation R15, Action Item 10; Findings 3.2 (agent-briefing)
**Tags:** [docs]
**Blocks:** Correct positioning of UM in AI agent context
**Dependencies:** None
**Estimated effort:** 1-2 hours

## Objective

Reposition the npm package / TypeScript helper in `docs/explainers/agent-briefing.md` and related explainer documents so it is not presented as co-equal with the specification and resolver.

## Why this work matters

The agent briefing currently lists the npm package in the "Key Facts" section (lines 20-22) alongside the spec site and resolver, as if they are equally fundamental components of what UM "is." The "For Developers" positioning statement (line 51) says "The TypeScript helper library handles validation" as the primary developer value proposition. This causes AI agents consuming the briefing to present UM as a TypeScript project.

## Scope

### Files to modify

1. **`docs/explainers/agent-briefing.md`**
   - Move the npm package from the "Key Facts" section to a separate "Reference Implementation" section lower in the document.
   - Update the "For Developers" positioning to lead with the spec and fixtures, mentioning the TypeScript helper as one optional tool.

2. **`docs/UNIVERSAL-MANIFEST-BRIEFING.md`** (line 234)
   - Review the fixture example that mentions "NVIDIA Shield TV Pro enrolled to venue edge" and consider replacing with a generic device description (e.g., "public display device enrolled to venue edge").
   - Note: This item overlaps with WO-0089 (Fix Legacy Naming and Branding Leaks). If WO-0089 is executed first, this item may already be resolved.

## Acceptance criteria

- [ ] Agent briefing "Key Facts" does not list the npm package as a co-equal component.
- [ ] A separate "Reference Implementation" section exists in the agent briefing.
- [ ] "For Developers" positioning leads with spec and fixtures, not the TypeScript helper.
- [ ] UNIVERSAL-MANIFEST-BRIEFING.md fixture example uses generic device descriptions where possible.
- [ ] An AI agent reading the updated briefing would describe UM as "a specification" rather than "a TypeScript library."

## Validation commands

- Manual review of updated agent briefing structure.
- `rg -n "npm" docs/explainers/agent-briefing.md` (should not appear in Key Facts section).
