# Animation Workflow and Version Status

Date: 2026-03-05
Agent Task ID: 58b6e17f_1772683277

This document defines the single approved animation process for Universal Manifest and records the root-cause of the Scenario 01 regression.

## 1) What Went Wrong (Root Cause)

There were two different Scenario 01 SVG files in production assets:

- Canonical/current visual: `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-01-object-model.svg`
- Legacy variant: `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-01-um-object-model.svg`

Timeline:
- 2026-02-25 (`1b4a49f`): `scenario-01-um-object-model.svg` added.
- 2026-02-27 (`a631e41`): `scenario-01-object-model.svg` added in visual refresh wave.
- Prompt-pack naming and some references continued to point at the `-um-` variant, creating inconsistent outputs and confusion.

## 2) Current Approved Process

### Production generation

Use the animation prompt pack as the generation source:
- `/Users/grig/work/repo/universalmanifest/.dev/ai/prompts/animation/`

Scenario 01 canonical prompt file:
- `/Users/grig/work/repo/universalmanifest/.dev/ai/prompts/animation/SCENARIO-01-object-model.md`

### Production output location

Generated SVGs belong in:
- `/Users/grig/work/repo/universalmanifest/site/public/animations/`

No separate replay lane is used.

### Verification (mandatory)

```bash
cd /Users/grig/work/repo/universalmanifest/site
npm run animation:verify:canonical
```

Script:
- `/Users/grig/work/repo/universalmanifest/site/scripts/verify-canonical-animations.mjs`

Canonical source list used by verification:
- `/Users/grig/work/repo/universalmanifest/site/scripts/canonical-animation-sources.mjs`

## 3) Canonical Source Set

1. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-01-object-model.svg`
2. `/Users/grig/work/repo/universalmanifest/site/public/animations/um-overlay-lanes-pilot.svg`
3. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-03-consent-policy-flow.svg`
4. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-04-user-journey-sequence.svg`
5. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-06-motion-tutorial.svg`
6. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-07-workbench-explainer.svg`
7. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-08-harness-explainer.svg`
8. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-09-social-integration.svg`
9. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-10-pop-integration.svg`
10. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-11-omatrust-integration.svg`
11. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-12-rp1-integration.svg`
12. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-13-smart-glasses-integration.svg`
13. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-14-metaverse-integration.svg`
14. `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-15-chia-vc-integration.svg`
15. `/Users/grig/work/repo/universalmanifest/site/public/animations/um-core-flow-pilot.svg`

## 4) Explicitly Forbidden for Canonical Output

- `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-01-um-object-model.svg` (legacy variant; not canonical)
- Any docs reference to `/animations/repro/` (retired path)

## 5) Replay Retirement (2026-03-05)

Replay scripts and replay artifact lane were removed from active workflow.

Removed scripts:
- `/Users/grig/work/repo/universalmanifest/site/scripts/replay-animation.mjs`
- `/Users/grig/work/repo/universalmanifest/site/scripts/replay-canonical-batch.mjs`
- `/Users/grig/work/repo/universalmanifest/site/scripts/verify-canonical-replay.mjs`

Removed artifact lane:
- `/Users/grig/work/repo/universalmanifest/site/public/animations/repro/`

## 6) Relationship to Production Workflow Docs

Primary generation workflow:
- `/Users/grig/work/repo/universalmanifest/docs/design/ANIMATED-SVG-WORKFLOW.md`

Foundational work orders:
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0030-animated-svg-explainer-prompt-pack-and-production-pipeline.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0042-animation-upgrade-phase-1-core-replacements-and-missing-scenarios.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0043-animation-upgrade-phase-2-tools-and-integration-lane-explainers.md`
