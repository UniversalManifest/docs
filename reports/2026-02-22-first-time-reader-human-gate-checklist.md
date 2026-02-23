# First-Time Reader Human Gate Checklist (WO-0015 / WO-0035)

Date: 2026-02-22
Project root: `/Users/grig/work/repo/universalmanifest`
Gate policy: Policy A (human participant evidence required)

## Purpose

Define exactly what a human participant should see and be able to explain before onboarding can be considered closure-grade complete.

## Pages the participant must use

- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/quick-start.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/workbench.md`

Local route sequence:

1. `http://127.0.0.1:4301/getting-started/universal-manifest-overview/`
2. Follow to quick-start.
3. Follow to workbench.

## What the participant is supposed to see

1. Clear definition of Universal Manifest as a portable state capsule (not LAN-only product copy).
2. Clear statement of interoperability purpose (shared envelope across systems; no forced single identity/provider stack).
3. A practical start path:
   - understand contract,
   - implement minimal consumer behavior,
   - validate with fixtures/tools.
4. Workbench scope boundaries:
   - what it helps with (import/edit/validate/export),
   - what it does not replace (full production key-management/governance systems).

## Pass questions (ask verbatim)

1. "What is Universal Manifest?"
2. "What are the first three implementation steps?"

## Required answer characteristics

Q1 must include:

- portable state capsule framing
- interoperability framing

Q2 must include:

- core contract review
- conformance/fixtures validation
- proof/workbench usage

## Gate decision

- PASS:
  - participant answers both questions with required characteristics
- FAIL:
  - either answer misses required characteristics
- PARTIAL:
  - answers are close but materially incomplete; document exactly what was unclear

## Evidence artifact requirement

Save a dated report as:

- `/Users/grig/work/repo/universalmanifest/docs/reports/YYYY-MM-DD-first-time-reader-test-results-human.md`

Minimum report fields:

- participant identifier and role
- pages read
- verbatim answers to Q1 and Q2
- evaluator verdict (PASS/FAIL/PARTIAL)
- rationale

## Closure rule

`WO-0015` may be marked `COMPLETED` only after at least one human participant run is documented with PASS under this checklist.
