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

Interpretation for this run (2026-03-02):
- `git rev-list --left-right --count HEAD...origin/main` returned `1 0`
- This means local `main` is one commit behind `origin/main`.

Because this repository is actively being modified by other agents, do not force-sync blindly. Coordinate update timing before fast-forwarding local branch state.
