# Animation Workflow and Version Status

Date: 2026-03-05
Agent Task ID: 58b6e17f_1772683277

This document defines the single approved animation process for Universal Manifest and records the root-cause of the Scenario 01 regression.

## 1) What Went Wrong (Root Cause)

There were two different Scenario 01 SVG files in production assets:

- Canonical/current visual: `site/public/animations/scenario-01-object-model.svg`
- Legacy variant: `site/public/animations/scenario-01-um-object-model.svg`

Timeline:
- 2026-02-25 (`1b4a49f`): `scenario-01-um-object-model.svg` added.
- 2026-02-27 (`a631e41`): `scenario-01-object-model.svg` added in visual refresh wave.
- Prompt-pack naming and some references continued to point at the `-um-` variant, creating inconsistent outputs and confusion.

## 2) Current Approved Process

### Production generation

Use the surviving workflow record as the generation source:
- `docs/design/ANIMATED-SVG-WORKFLOW.md`

Scenario 01 canonical prompt file:
- Historical `.dev` scenario prompt file referenced by earlier workflow revisions is not present in the current checkout.

### Production output location

Generated SVGs belong in:
- `site/public/animations/`

No separate replay lane is used.

### Verification (mandatory)

```bash
cd site
npm run animation:verify:canonical
```

Script:
- `site/scripts/verify-canonical-animations.mjs`

Canonical source list used by verification:
- `site/scripts/canonical-animation-sources.mjs`

## 3) Canonical Source Set

1. `site/public/animations/scenario-01-object-model.svg`
2. `site/public/animations/um-overlay-lanes-pilot.svg`
3. `site/public/animations/scenario-03-consent-policy-flow.svg`
4. `site/public/animations/scenario-04-user-journey-sequence.svg`
5. `site/public/animations/scenario-06-motion-tutorial.svg`
6. `site/public/animations/scenario-07-workbench-explainer.svg`
7. `site/public/animations/scenario-08-harness-explainer.svg`
8. `site/public/animations/scenario-09-social-integration.svg`
9. `site/public/animations/scenario-10-pop-integration.svg`
10. `site/public/animations/scenario-11-omatrust-integration.svg`
11. `site/public/animations/scenario-12-rp1-integration.svg`
12. `site/public/animations/scenario-13-smart-glasses-integration.svg`
13. `site/public/animations/scenario-14-metaverse-integration.svg`
14. `site/public/animations/scenario-15-did-vc-integration.svg`
15. `site/public/animations/um-core-flow-pilot.svg`

## 4) Explicitly Forbidden for Canonical Output

- `site/public/animations/scenario-01-um-object-model.svg` (legacy variant; not canonical)
- Any docs reference to `/animations/repro/` (retired path)

## 5) Replay Retirement (2026-03-05)

Replay scripts and replay artifact lane were removed from active workflow.

Removed scripts:
- `site/scripts/replay-animation.mjs`
- `site/scripts/replay-canonical-batch.mjs`
- `site/scripts/verify-canonical-replay.mjs`

Removed artifact lane:
- `site/public/animations/repro/`

## 6) `um-core-flow-pilot.svg` Generation Map

Target file:
- `site/public/animations/um-core-flow-pilot.svg`

Provenance (git):
- First introduced: `52c1377` (2026-02-22)
- Replaced in infographic/style wave: `1b4a49f` (2026-02-25)
- Refreshed to current dark-theme version: `a631e41` (2026-02-27)

Source path for regeneration:
- Historical `.dev` prompt-pack files referenced by earlier workflow revisions are not present in the current checkout.
- Use `docs/design/ANIMATED-SVG-WORKFLOW.md` together with `site/public/animations/` for the surviving regeneration context.

Important:
- This file has no exact hash match in infographics-kit deterministic outputs.
- Canonical stage labels for this file are `Resolve -> Validate -> Consume`.
- Save regenerated output directly to the canonical path above (overwrite is expected for canonical maintenance).

Post-generation gate:
- `cd site && npm run animation:verify:canonical`

## 7) Relationship to Production Workflow Docs

Primary generation workflow:
- `docs/design/ANIMATED-SVG-WORKFLOW.md`

Foundational work orders:
- `docs/workorders/WO-0030-animated-svg-explainer-prompt-pack-and-production-pipeline.md`
- `docs/workorders/WO-0042-animation-upgrade-phase-1-core-replacements-and-missing-scenarios.md`
- `docs/workorders/WO-0043-animation-upgrade-phase-2-tools-and-integration-lane-explainers.md`
