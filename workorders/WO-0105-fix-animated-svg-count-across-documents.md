# WO-0105 — Fix Animated SVG Count Across All Documents

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Documentation Freshness Audit (2026-03-01), Section 5.1, Priority 3 recommendation item 7; Verification report (count nuance: 29 production, not 31)
**Tags:** [docs]
**Blocks:** None (accuracy)
**Dependencies:** None
**Estimated effort:** 30 minutes - 1 hour

## Resolution

Verified actual inventory: 33 SVG files in `site/public/animations/`, minus 2 test files (`scenario-99-*-test.svg`) and 2 pilot files (`um-*-pilot.svg`) = 29 production SVGs.

Updated count from "16" to "29 production" (with qualification about the full 33 total) in:
- `docs/STATE-OF-THE-PROJECT.md` (line 51)
- `docs/diagrams/README.md` (line 9)
- `docs/design/ANIMATED-SVG-WORKFLOW.md` (lines 3, 25, 720)

## Objective

Update the animated SVG count from "16" to the actual number across all documents that reference this count, using the verified breakdown from the verification report.

## Why this work matters

The freshness audit found that three documents claim "16 production animated SVGs." The verification agent confirmed the actual inventory in `site/public/animations/` is:
- **33 total SVGs**
- **2 test files** (`scenario-99-*-test.svg`) -- exclude from production count
- **2 pilot files** (`um-*-pilot.svg`) -- earlier iterations, not production
- **29 non-test, non-pilot production SVGs**: 14 scenario-prefixed files + 15 numbered files (e.g., `1.3-overlay-lanes.svg`)
- Additionally, 15 static diagrams exist in `site/public/diagrams/`

The "16" claim is therefore significantly outdated regardless of how "production" is defined.

## Scope

### Files to update

1. **`/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`** (line 51) — "16 production animated SVGs" -> actual count
2. **`/Users/grig/work/repo/universalmanifest/docs/diagrams/README.md`** (line 9) — "16 production assets" -> actual count
3. **`/Users/grig/work/repo/universalmanifest/docs/design/ANIMATED-SVG-WORKFLOW.md`** (lines 3, 25, 720) — "16" -> actual count

### Verification

Run `ls /Users/grig/work/repo/universalmanifest/site/public/animations/ | wc -l` to confirm total count, then subtract test and pilot files.

### Decision needed

The update should specify the breakdown clearly. Recommended phrasing:
- "29 production animated SVGs (plus 2 test files and 2 pilot iterations)" or
- "33 animated SVGs in total (29 production, 2 pilots, 2 test files)"

Do NOT simply say "31" without qualification, as that count includes the 2 pilot files which are earlier iterations, not current production assets.

## Acceptance criteria

- [ ] All three files have the correct, matching SVG count.
- [ ] The count has been verified against the actual file inventory.
- [ ] `rg -n "16 production\|16 animated" /Users/grig/work/repo/universalmanifest/docs/` returns zero stale matches.

## Validation commands

- `ls /Users/grig/work/repo/universalmanifest/site/public/animations/ | wc -l` (verify actual count)
- `rg -n "16 production\|16 animated" /Users/grig/work/repo/universalmanifest/docs/`
