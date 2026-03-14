# WO-0109 — Add CI Workflow Decision Record and Update DECISIONS.md

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P2 (Nice-to-have)
**Source:** Documentation Freshness Audit (2026-03-01), Section 5.5, Priority 4 recommendation item 11
**Tags:** [docs]
**Blocks:** None (completeness)
**Dependencies:** None
**Estimated effort:** 30 minutes

## Objective

Add a decision record for the new expanded CI workflow (`ci.yml`, WO-0049) to `docs/DECISIONS.md`.

## Why this work matters

The freshness audit noted that `DECISIONS.md` references `.github/workflows/verify.yml` as the CI workflow (line 144), but a new `ci.yml` was added this week (WO-0049) with a 5-job pipeline. Both files exist, but the decision record does not mention the new expanded CI workflow. While not a factual error, it is incomplete and could confuse contributors about which CI workflow is authoritative.

## Scope

### File to modify

**`docs/DECISIONS.md`**

### Changes

1. Add a new decision entry recording the adoption of the 5-job CI pipeline (`ci.yml`).
2. Note the relationship between the original `verify.yml` and the new `ci.yml`.
3. Include the date of the decision and the WO reference (WO-0049).

## Acceptance criteria

- [ ] DECISIONS.md includes a decision entry for the CI workflow expansion.
- [ ] The entry explains the relationship between `verify.yml` and `ci.yml`.
- [ ] The entry includes the date and WO reference.

## Validation commands

- `rg -n "ci.yml" docs/DECISIONS.md` (should find the new entry).
