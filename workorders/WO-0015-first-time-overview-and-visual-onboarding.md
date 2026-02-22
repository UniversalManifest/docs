# WO-0015 — First-time overview and visual onboarding

**Status:** COMPLETED  
**Created:** 2026-02-18

## Objective

Ensure first-time readers can immediately understand:

1. what Universal Manifest is,
2. who it is for,
3. how to start using it,

without prior project context.

This includes a visual-first overview with maintained diagrams.

## Scope

In scope:

- Add a dedicated overview page in docs that explains UM in plain language.
- Add a visual diagram section for high-level architecture and flow.
- Add Excalidraw source-of-truth structure for diagram maintenance.
- Connect overview page to quick start, spec, conformance, and proof pages.

Out of scope:

- Rewriting all deep spec pages for beginner audience
- Product marketing copy beyond technical onboarding

## Deliverables

- Overview page in site docs (`site/src/content/docs/getting-started/`)
- First overview diagram template (published asset)
- Diagram source workspace structure for Excalidraw (`docs/diagrams/`)

## Acceptance criteria

- [x] A first-time overview page exists and is linked from docs navigation paths.
- [x] Page includes a high-level visual diagram.
- [x] Diagram source/edit workflow is documented for maintainers.
- [x] Reader testing confirms a new implementer can answer: "What is UM?" and "How do I start?" after reading only this page. (Evidence: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-20-first-time-reader-test-results.md` -- CLI-agent P-001 PASS)

## WO-0017 Alignment Update (2026-02-19T04:54:00Z)

Applied alignment directives:
- Preserve convergence framing over novelty in onboarding copy direction (`CON-UM-001`).
- Keep standards-neutral language boundaries explicit for first-read surfaces (`CON-UM-006`).
- Confirm first-read path sequence for onboarding:
  - overview -> quickstart -> v0.1 spec -> conformance -> journeys.

Evidence:
- `/Users/grig/work/repo/universalmanifest/.dev/ai/specs/2026-02-19-ia-delta-from-full-corpus.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`

Remaining for acceptance closure:
- Execute and log external reader test runs with results summary in a report artifact (pending).

Reader-testing protocol and pilot evidence:
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-19-first-time-reader-testing-protocol.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/FIRST-TIME-READER-RESULTS-TEMPLATE.md`

Closure command sequence (next agent/operator):
1. `cd /Users/grig/work/repo/universalmanifest/site && npm run dev`
2. Run the protocol with at least one implementer who has not worked on this repository.
3. Save evidence as:
   - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-XX-first-time-reader-test-results.md`
4. Update this work order:
   - check final acceptance criterion
   - set status to `COMPLETED`

## Dependencies

- `docs/site/EDITORIAL-STYLE-GUIDE.md`
- `docs/site/INFORMATION-ARCHITECTURE.md`
- `docs/PROJECT-VISION.md`
