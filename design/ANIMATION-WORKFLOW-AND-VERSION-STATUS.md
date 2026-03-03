# Animation Workflow and Version Status

Date: 2026-03-02

This document is the canonical clarification for which animation workflow is active, which historical tracks are deprecated, and how to reproduce assets without touching production files.

## Current Production Workflow (Active)

The active production system is the WO-0030 prompt-pack pipeline, with WO-0042 and WO-0043 as the completed production upgrade waves.

Authoritative references:
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0030-animated-svg-explainer-prompt-pack-and-production-pipeline.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0042-animation-upgrade-phase-1-core-replacements-and-missing-scenarios.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0043-animation-upgrade-phase-2-tools-and-integration-lane-explainers.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/prompts/animation/`
- `/Users/grig/work/repo/universalmanifest/docs/design/ANIMATED-SVG-WORKFLOW.md`
- `/Users/grig/work/repo/universalmanifest/docs/design/ANIMATED-SVG-SPEC.md`
- `/Users/grig/work/repo/universalmanifest/docs/design/ANIMATION-QA-CHECKLIST.md`

Production output locations:
- `/Users/grig/work/repo/universalmanifest/site/public/animations/`
- `/Users/grig/work/repo/universalmanifest/site/public/diagrams/`

## Deprecated and Historical Tracks

The following are historical/deprecated for production animation output:

- Excalidraw exports for production visuals:
  - Excalidraw may still be used for whiteboarding or planning.
  - Excalidraw is not the production source for live animated explainers.

- Legacy/archived pre-upgrade assets:
  - `/Users/grig/work/repo/universalmanifest/site/public/animations/archive_bad_svgs/`
  - `/Users/grig/work/repo/universalmanifest/site/public/animations/archive-pre-wo-asset-011/`

These directories are retained for provenance and comparison only.

## Version Lineage and Website-Visible Tracks

The website currently exposes multiple animation naming tracks, but they map to one active generation system (prompt-pack animated SVG workflow):

- Scenario-prefixed dark-theme assets (primary production track):
  - Example references in docs pages:
    - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/visual-explainers.md`
    - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/proof/harness.md`
  - Key files:
    - `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-01-object-model.svg`
    - `/Users/grig/work/repo/universalmanifest/site/public/animations/scenario-08-harness-explainer.svg`

- Numbered transparent-background alternates (legacy-compatible presentation track, not default):
  - `/Users/grig/work/repo/universalmanifest/site/public/animations/6.2-harness-explainer.svg`
  - These are still visible on the gallery page as alternate versions, but scenario-prefixed assets are preferred for primary docs contexts.

Commit provenance for the investigated files:
- `scenario-08-harness-explainer.svg`
  - Introduced: commit `1b4a49f` on 2026-02-25 (`feat: add new SVG infographics and a style guide...`)
  - Refreshed: commit `a631e41` on 2026-02-27 (`feat: refresh visual assets`)
- `scenario-01-object-model.svg`
  - Added in current filename form: commit `a631e41` on 2026-02-27 (`feat: refresh visual assets`)
- `6.2-harness-explainer.svg` (numbered alternate)
  - Added: commit `263675b` on 2026-02-26 (`feat: add animation assets`)

Operational interpretation:
- The active system for currently visible website animations is the WO-0030 prompt-pack generation approach and its upgrade waves (WO-0042, WO-0043).
- Legacy tracks remain for compatibility/provenance, but are not the canonical source for new production animation creation.

## Reproduction Protocol (Safe)

When testing reproducibility:

1. Never overwrite files in `/site/public/animations/` or `/site/public/diagrams/`.
2. Write replay outputs to:
   - `/Users/grig/work/repo/universalmanifest/site/public/animations/repro/`
3. Validate each replay:
   - XML validity (`xmllint`)
   - accessibility markers (`role=\"img\"`, `aria-labelledby`, `<title>`, `<desc>`)
   - reduced motion fallback (`prefers-reduced-motion`)
   - size budget from `ANIMATED-SVG-SPEC.md`
4. Keep evidence in:
   - `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/`

## Repro Outputs from 2026-03-02

Current replay artifacts:
- `/Users/grig/work/repo/universalmanifest/site/public/animations/repro/scenario-01-object-model-replay-new-content-2026-03-02.svg`
- `/Users/grig/work/repo/universalmanifest/site/public/animations/repro/scenario-08-harness-explainer-replay-2026-03-02.svg`

Related evidence:
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/2026-03-02-animation-diagram-forensics-report.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/2026-03-02-scenario-01-strict-replay-result.md`

## Head Revision Status Check

To check local vs remote head:

```bash
cd /Users/grig/work/repo/universalmanifest
git fetch origin
git rev-parse HEAD
git rev-parse origin/main
git rev-list --left-right --count HEAD...origin/main
```

Interpretation guidance:
- Output format is `<left> <right>`.
- `left` = commits only on local `HEAD`.
- `right` = commits only on `origin/main`.

Observed in this session (2026-03-02), due concurrent edits:
- `1 0` -> `3 0` -> `0 0` -> `1 0` -> `0 0`

Because this repository is actively being modified by other agents, this status is intentionally treated as a live snapshot. Re-run the check commands immediately before synchronization actions.
