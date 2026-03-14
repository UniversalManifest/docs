# WO-0043 — Animation upgrade phase 2: tools and integration-lane explainers

**Status:** COMPLETED
**Created:** 2026-02-23
**Priority:** HIGH
**Source:** `.dev/ai/proposals/2026-02-23-21-41-41-universalmanifest-animation-upgrade-proposal.md`
**Depends on:** `WO-0042`

## Objective

Execute Phase 2 of the animation-upgrade proposal by generating and integrating explainer animations for tool surfaces and integration lanes, then updating placement and QA artifacts to closure-ready state.

## Why this work matters

Phase 1 upgrades core assets, but onboarding still lacks contextual explainers where users actually make implementation decisions. Tool pages and integration lanes need targeted visuals to reduce comprehension time and improve adoption confidence.

## Scope

In scope:

- Generate tool-surface explainer animations for:
  - Workbench
  - Verification Harness
- Generate integration-lane explainer animations for:
  - Social/profile
  - Proof-of-personhood
  - OMATrust
  - RP1 spatial fabric
  - Smart glasses AR
  - Metaverse
  - Chia VC
- Integrate generated assets into corresponding docs pages under:
  - `site/src/content/docs/getting-started/`
  - `site/src/content/docs/proof/`
  - `site/src/content/docs/integrations/`
- Update placement and QA tracking documents to reflect generated/integrated assets:
  - `docs/design/ANIMATION-PLACEMENT-PLAN.md`
  - `docs/design/ANIMATION-QA-CHECKLIST.md`

Out of scope:

- Regenerating Phase 1 assets unless required to fix integration defects.
- Spec, schema, resolver, or journey semantics changes.

## Required deliverables

1. Tool explainer SVGs (minimum 2) in `site/public/animations/`.
2. Integration-lane explainer SVGs (minimum 7) in `site/public/animations/`.
3. Docs page integrations (embed/link) for all generated explainers.
4. Updated placement and QA documents showing completion status and evidence.
5. Verification evidence in this WO including build and spot-check results.

## Acceptance criteria

- [ ] Tool explainer assets exist and are integrated in workbench/harness docs surfaces.
- [ ] Seven integration-lane explainer assets exist and are integrated in corresponding lane pages.
- [ ] `ANIMATION-PLACEMENT-PLAN.md` is updated with final mapping and status.
- [ ] `ANIMATION-QA-CHECKLIST.md` is updated with pass/fail evidence for generated assets.
- [ ] Site build passes after all integrations (`npm run build:clean`).
- [ ] New animations preserve accessibility/reduced-motion constraints from `ANIMATED-SVG-SPEC.md`.

## Validation commands

- `cd site && npm run build:clean`
- `rg -n "animations/" site/src/content/docs/getting-started site/src/content/docs/proof site/src/content/docs/integrations`
- `rg -n "<title>|<desc>|prefers-reduced-motion" site/public/animations/*.svg`

## Dependencies

- `WO-0042` completion (core asset quality baseline and scenario completeness).
- Existing animation prompt system and design constraints:
  - `.dev/ai/prompts/animation/`
  - `docs/design/ANIMATED-SVG-SPEC.md`

## Sequencing

1. Confirm `WO-0042` completion and artifact readiness.
2. Generate tool explainers and integrate.
3. Generate lane explainers and integrate.
4. Update placement/QA docs and run final build validation.
