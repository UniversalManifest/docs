# WO-0178 -- `/spec/latest/` Inline TOC Layout Bugfix and GAS Visual Verification

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-04-13
**Completed:** 2026-04-13

## Objective

Fix the `/spec/latest/` table-of-contents layout bug where collapsing or hiding the sidebar switches the TOC into inline mode and causes the bottom of the TOC to overlap the specification body text, producing illegible visual corruption.

## Context

This bug has now survived multiple attempted fixes and must be treated as a dedicated work item instead of casual follow-on cleanup.

Observed failure mode:

- On `universalmanifest.net/spec/latest/`, collapsing or hiding the sidebar moves the TOC into inline mode.
- In inline mode, the TOC visually overlaps the first body content below it.
- The result is unreadable, broken rendering in the live public spec surface.

This is not just a cosmetic detail. `/spec/latest/` is the public standards page already being shared externally, so this regression affects the credibility of the current draft surface directly.

## Scope

In scope:

1. Reproduce the overlap defect in the current local and/or rendered `/spec/latest/` page.
2. Identify the exact cause in the inline TOC mode CSS and any supporting toggle logic.
3. Fix the layout so inline mode keeps the TOC in normal document flow without text overlap.
4. Verify that both states work:
   - sidebar/pinned mode
   - inline/collapsed mode
5. Perform explicit visual confirmation with the GAS browser workflow before closing the work.

Out of scope:

- Broad redesign of the spec page.
- Changing the normative spec content.
- Reworking the wider homepage MVP or public nav beyond what is needed for this bug.

## Deliverables

- A concrete layout fix for inline TOC mode on `/spec/latest/`.
- Visual verification evidence that the collapsed/inline TOC no longer overlaps the body copy.
- Notes on the exact root cause and the tested view states.

## Files Involved

- `docs/W3C-STYLE-SPEC.html`
- `site/src/pages/spec/latest.astro` if route-wrapper changes are needed

## Execution Notes

- This work should be delegated to a sub-agent rather than consuming more orchestrator loop time.
- Verification must include an actual browser-based repro/fix cycle, not just a static build.
- GAS `agent-browser` validation is required as part of acceptance.
- Delegated in Paperclip as `SUM-57` and assigned to the Dev Worker for implementation plus browser verification.
- `SUM-57` is currently `blocked` because the Dev Worker can be checked out, but Paperclip returns `Board access required` when attempting to resume or invoke its heartbeat from this shell.

## Progress Notes

- Fixed inline TOC flow by adding explicit clearance and bottom spacing in `docs/W3C-STYLE-SPEC.html`.
- Verified with `agent-browser` on both desktop sidebar mode and desktop inline/collapsed mode after rebuilding `site`.
- Current browser measurements on desktop show `body.toc-inline`, `#toc` at `position: static`, `float: none`, and a positive gap between the TOC bottom and the first content section.

## Acceptance Criteria

- [x] The TOC overlap bug is reproducibly fixed in inline/collapsed mode.
- [x] The spec body content below the TOC remains fully legible after the sidebar is hidden/collapsed.
- [x] Sidebar mode still renders correctly.
- [x] Local build passes after the fix.
- [x] Browser-based visual verification is completed with the GAS browser workflow.
