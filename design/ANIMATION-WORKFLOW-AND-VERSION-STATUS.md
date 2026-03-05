# Animation Workflow and Version Status

Date: 2026-03-05
Agent Task ID: 58b6e17f_1772683277

This is the canonical operating document for animation replay generation in this repository.

## 1) Problem That Was Found

Two similar Scenario 01 source files existed:
- Correct visual source: `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-01-object-model.svg`
- Different variant: `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-01-um-object-model.svg`

Earlier replay runs used the different variant, which produced replay outputs that looked wrong compared to the expected Scenario 01 visual.

## 2) Only Approved Replay Process (Use This)

### A) Single-file replay

```bash
cd /Users/grig/work/repo/universalmanifest/site
npm run animation:replay -- \
  --source scenario-08-harness-explainer.svg \
  --name scenario-08-harness-explainer-replay-correct-source-YYYY-MM-DD.svg \
  --desc "Replay from expected canonical source scenario-08-harness-explainer.svg."
```

### B) Canonical full-set replay (recommended)

```bash
cd /Users/grig/work/repo/universalmanifest/site
npm run animation:replay:canonical -- --date YYYY-MM-DD
```

What this does:
- Replays a fixed canonical source list (15 source files).
- Writes outputs only to `/Users/grig/work/repo/universalmanifest/site/public/animations/repro/`.
- Uses the naming pattern: `*-replay-correct-source-YYYY-MM-DD.svg`.

Implementation:
- `/Users/grig/work/repo/universalmanifest/site/scripts/replay-canonical-batch.mjs`
- `/Users/grig/work/repo/universalmanifest/site/scripts/canonical-animation-sources.mjs`

### C) Mandatory verification after replay

```bash
cd /Users/grig/work/repo/universalmanifest/site
npm run animation:replay:verify -- --date YYYY-MM-DD
```

What verification checks:
- Each expected replay file exists.
- Replay matches source content, allowing only `<desc>` text differences.
- XML validation via `xmllint` when available.

Implementation:
- `/Users/grig/work/repo/universalmanifest/site/scripts/verify-canonical-replay.mjs`

## 3) Canonical Source Set (15 Files)

Authoritative source-of-truth list location:
- `/Users/grig/work/repo/universalmanifest/site/scripts/canonical-animation-sources.mjs`

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

Scenario 01 rule:
- For canonical replay, always use `scenario-01-object-model.svg`.
- Do not use `scenario-01-um-object-model.svg` for canonical replay output.

## 4) Explicitly Deprecated Replay Process (Do Not Use)

Do not do any of the following:

- Do not pick source files by name similarity.
- Do not generate replay files without the `-replay-correct-source-YYYY-MM-DD` suffix.
- Do not keep mixed replay sets in `/Users/grig/work/repo/universalmanifest/site/public/animations/repro/`.
- Do not use `scenario-01-um-object-model.svg` as the canonical source for Scenario 01 replay.

## 5) Replay Directory Hygiene Policy

Replay directory:
- `/Users/grig/work/repo/universalmanifest/site/public/animations/repro/`

Policy:
- Keep one dated canonical set only.
- Remove older replay variants after a new canonical set is generated and verified.

Cleanup command pattern:

```bash
find /Users/grig/work/repo/universalmanifest/site/public/animations/repro \
  -maxdepth 1 -type f -name '*.svg' \
  ! -name '*-replay-correct-source-YYYY-MM-DD.svg' -delete
```

## 6) 2026-03-05 Remediation Record

Completed in this remediation:
- Canonical replay set regenerated from correct sources.
- Replay directory cleaned to keep only the corrected canonical set.
- Public docs reference fixed to remove wrong Scenario 01 variant usage:
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/visual-explainers.md`

Current visual comparison artifacts (for human review):
- `/tmp/um_svg_compare/all-fixed-compare-after-cleanup-2026-03-05.html`
- `/tmp/um_svg_compare/all-fixed-compare-after-cleanup-2026-03-05.png`

## 7) Relationship to Production Generation Workflow

This file governs replay/reproducibility operations.

Production animation generation remains the prompt-pack workflow described in:
- `/Users/grig/work/repo/universalmanifest/docs/design/ANIMATED-SVG-WORKFLOW.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0030-animated-svg-explainer-prompt-pack-and-production-pipeline.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0042-animation-upgrade-phase-1-core-replacements-and-missing-scenarios.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0043-animation-upgrade-phase-2-tools-and-integration-lane-explainers.md`
