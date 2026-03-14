# First-Time Reader Testing Protocol (WO-0015)

Date: 2026-02-19
Project root: ``
Work order: `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`
Gate checklist: `docs/reports/2026-02-22-first-time-reader-human-gate-checklist.md`

## Goal

Validate that a new implementer can answer, after reading only the first-time path:
1. What is Universal Manifest?
2. How do I start?

## Pages under test

- `site/src/content/docs/getting-started/universal-manifest-overview.md`
- `site/src/content/docs/getting-started/quick-start.md`
- `site/src/content/docs/getting-started/workbench.md`

## Test script for human readers

1. Open:
- `http://127.0.0.1:4301/getting-started/universal-manifest-overview/`

2. Read only the linked first-time path:
- overview -> quick-start -> workbench

3. Answer in your own words:
- Q1: What is Universal Manifest?
- Q2: What are the first three implementation steps?

4. Pass criteria:
- Q1 answer includes portable state capsule + interoperability framing.
- Q2 answer includes core contract review, conformance/fixtures validation, and proof or workbench usage.

## Pilot run notes (internal)

- Pilot result: PASS for content sufficiency in current docs text.
- Reason:
  - overview explicitly defines UM and target audience,
  - quick-start gives sequential implementation steps,
  - workbench page provides practical import/edit/validate/export path.

## Optional follow-up

- Human-participant evidence is optional and can be used as additional onboarding quality signal.
- Optional artifact path:
- `docs/reports/YYYY-MM-DD-first-time-reader-test-results-human.md`
