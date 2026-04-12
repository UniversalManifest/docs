# WO-0042 — Animation upgrade phase 1: core replacements and missing scenarios

**Status:** COMPLETED
**Created:** 2026-02-23
**Priority:** HIGH
**Source:** `.dev/ai/proposals/2026-02-23-21-41-41-universalmanifest-animation-upgrade-proposal.md`

## Objective

Execute Phase 1 of the animation-upgrade proposal by replacing pilot/core animation assets and generating the missing scenario animations identified as incomplete after WO-0030.

## Why this work matters

Current pilot animations are functional but not yet production-grade for high-confidence onboarding. Missing scenario coverage leaves the animation system incomplete and reduces consistency across onboarding narratives.

## Scope

In scope:

- Replace existing pilot animations with production-quality assets:
  - `site/public/animations/um-core-flow-pilot.svg`
  - `site/public/animations/um-overlay-lanes-pilot.svg`
- Upgrade static overview diagram to animated explainer while preserving conceptual parity:
  - `site/public/diagrams/universal-manifest-overview-template.svg`
- Generate missing scenario outputs from existing WO-0030 prompt system:
  - Scenario 01 (object model)
  - Scenario 03 (consent/policy)
  - Scenario 04 (user journey)
  - Scenario 06 (motion tutorial)
- Store generated scenario assets in canonical animations path:
  - `site/public/animations/`
- Ensure generated/replaced assets satisfy accessibility and performance constraints defined in:
  - `docs/design/ANIMATED-SVG-SPEC.md`

Out of scope:

- Tool-specific and integration-lane-specific explainer generation (Phase 2; WO-0043).
- Normative spec or conformance semantic changes.

## Required deliverables

1. Replaced pilot animation files (2).
2. Upgraded animated overview template (1).
3. Newly generated scenario animation assets for 01/03/04/06 (minimum 4).
4. Brief execution evidence section added to this WO documenting generated files and checks run.

## Acceptance criteria

- [ ] `um-core-flow-pilot.svg` and `um-overlay-lanes-pilot.svg` are replaced with production-quality versions.
- [ ] `universal-manifest-overview-template.svg` is upgraded to animated form.
- [ ] Scenario 01/03/04/06 assets exist under `site/public/animations/`.
- [ ] Every new/replaced SVG includes accessibility metadata (`<title>`, `<desc>`) and reduced-motion support.
- [ ] Site build passes after integration (`npm run build:clean`).
- [ ] No regression in docs-page rendering where these assets are used.

## Validation commands

- `cd site && npm run build:clean`
- `rg -n "<title>|<desc>|prefers-reduced-motion" site/public/animations/*.svg site/public/diagrams/*.svg`
- `find site/public/animations -maxdepth 1 -type f -name '*.svg' | sort`

## Dependencies

- Existing prompt system from `WO-0030`:
  - `docs/design/ANIMATED-SVG-WORKFLOW.md`
- Technical constraints:
  - `docs/design/ANIMATED-SVG-SPEC.md`

## Sequencing

- This work order should complete before `WO-0043` begins integration-lane and tool-specific expansion.
