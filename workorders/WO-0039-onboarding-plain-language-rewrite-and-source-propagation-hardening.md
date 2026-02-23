# WO-0039 — Onboarding plain-language rewrite and source-propagation hardening

**Status:** NOT_STARTED
**Created:** 2026-02-23
**Priority:** HIGH
**Source:** Direct user review of `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md`
**Agent Task ID:** `b617cafd_1771721466`

## Objective

Rewrite first-read onboarding language so it is understandable without prior UM context, then harden all source paths (docs + backend/tooling/templates) so unclear jargon and misleading framing do not reappear.

## Why this work matters

Current onboarding copy still uses undefined jargon in critical first-read sections (for example, "integration pair"), which assumes technical context readers may not have. If only a docs sentence is changed but source templates/test artifacts/tooling outputs are not corrected, drift will reintroduce the same problem.

## Problem statement (current failure)

In `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md`, the "What problem it solves" section uses language that is not explained before use:

- "Without UM, each integration pair tends to invent custom payloads and brittle mappings."

That line must be rewritten in plain language and aligned with supporting docs/testing artifacts so onboarding claims are clear and stable.

## Scope

In scope:

- Rewrite first-read onboarding content for plain-language clarity:
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/concepts.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/quick-start.md`
- Ensure first-use terminology is either defined immediately or replaced with plain language.
- Perform source-of-language inventory across docs and backend/tooling surfaces that can re-inject wording:
  - docs pages, protocol/templates, scripts output strings, package/service readme/help text, and validation artifacts.
- Update all discovered source surfaces that encode outdated onboarding phrasing.
- Add an automated terminology/readability guard command that fails on defined banned/undefined jargon patterns in first-read surfaces.
- Update style/process docs to codify the guardrail and review expectations.

Out of scope:

- Changing normative schema semantics or resolver contract behavior.
- Removing required lineage/compatibility records already governed by existing decisions.

## Execution phases (methodical multi-day plan)

### Phase 1 — Inventory and source map

- [ ] Build a full inventory of wording sources that touch onboarding narrative.
- [ ] Create a root-cause/source-map report with file paths and ownership.

### Phase 2 — Onboarding rewrite

- [ ] Rewrite first-read pages for non-assumptive language.
- [ ] Ensure "problem statement" text explains terms before use.
- [ ] Keep UM-first, standards-neutral boundaries explicit.

### Phase 3 — Propagation fixes (docs + backend/tooling)

- [ ] Update templates/protocols/reports that currently embed old wording.
- [ ] Update backend/tooling-facing strings if they carry onboarding language.
- [ ] Re-run scans to confirm no stale phrase reintroduction paths remain.

### Phase 4 — Guardrail automation

- [ ] Implement a terminology/readability drift-check script.
- [ ] Wire script to a repeatable local command (and CI path if available).
- [ ] Document allowlist/denylist policy and maintenance procedure.

### Phase 5 — Human validation and closure evidence

- [ ] Execute human-reader check on rewritten onboarding pages.
- [ ] Publish dated evidence artifact showing comprehension outcomes.
- [ ] Reconcile WO-0015 and WO-0035 references to the updated wording.

## Required deliverables

1. Source-map + rewrite plan report:
   - `/Users/grig/work/repo/universalmanifest/docs/reports/YYYY-MM-DD-wo-0039-onboarding-language-source-map-and-rewrite-plan.md`
2. Rewritten onboarding content in first-read docs (paths in Scope).
3. Propagation updates in all identified source files that can reintroduce stale wording.
4. Terminology/readability guard script + documented command usage.
5. Completion evidence report:
   - `/Users/grig/work/repo/universalmanifest/docs/reports/YYYY-MM-DD-wo-0039-onboarding-language-hardening-completion-report.md`

## Acceptance criteria

- [ ] First-read onboarding sections no longer assume unexplained jargon knowledge.
- [ ] Terms like "integration pair" are either removed or explicitly defined before first use.
- [ ] Source-map report identifies all language injection points that affect onboarding wording.
- [ ] No stale target phrasing remains in active docs/templates/source strings after rewrite.
- [ ] Automated guard command passes on current content and fails when banned phrasing is reintroduced.
- [ ] Human-reader evidence artifact is published and linked.
- [ ] WO-0015 and WO-0035 references are updated so closure claims reflect rewritten baseline.

## Validation commands

- `rg -n -i "integration pair|brittle mappings|undefined jargon|prior art" /Users/grig/work/repo/universalmanifest/site/src/content/docs /Users/grig/work/repo/universalmanifest/docs`
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test`
- `<new terminology guard command added in this WO>`

## Dependencies and sequencing notes

- This WO should be executed before final closure of onboarding-readability claims under:
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0035-human-reader-testing-policy-and-onboarding-evidence-alignment.md`
- Maintain policy consistency with:
  - `/Users/grig/work/repo/universalmanifest/docs/site/EDITORIAL-STYLE-GUIDE.md`
  - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`

## Handoff instructions for the writing-focused agent

- Start with Phase 1 and produce the source map before editing narrative text.
- Treat docs and backend/tooling/template strings as one system; do not ship docs-only wording edits.
- Prefer plain-language phrasing first, then add precise technical terms with immediate definitions.
- Record every file touched and reason in the completion report for traceability across long-running execution.
