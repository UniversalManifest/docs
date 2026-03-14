# WO-0029 — Docs nav order, labels, tools placement, and overview clarity pass

**Status:** COMPLETED
**Created:** 2026-02-22

## Objective

Apply a focused docs UX/IA pass to improve discoverability and first-read comprehension:

- reorder and relabel the Integrations section for strategic priority and readability.
- remove reference implementation from the Integrations sidebar set.
- add a dedicated top-level Tools section in the left sidebar.
- remove "Highlighted Tools" from Overview.
- rewrite Overview framing so fresh readers can quickly understand what Universal Manifest is and why it matters.

## Required change set

### A) Integrations ordering and labels

Implement this left-nav order under Integrations:

1. Social/Profile
2. Proof-of-Personhood
3. OMATrust
4. RP1 Spatial Fabric
5. Smart Glasses
6. Metaverse
7. Chia DID/VC (bottom)

Rules:
- remove reference implementation from Integrations nav (page may remain in repo/history but should not appear in current integrations navigation).
- remove the word "Integration" from labels/titles where it appears in integration page titles.
- rename "Smart Glasses AR Integration" label to "Smart Glasses".
- keep Smart Glasses framing as current AI/HUD usage now; AR is future-facing. Do not include "siloed hardware" phrasing.

### B) Sidebar: create Tools section

- create a top-level sidebar section `Tools` at the bottom of the global list (below Governance).
- move tool entry points there:
  - Manifest Workbench (`/getting-started/workbench/`)
  - Verification Harness (`/proof/harness/`)
- remove these links from the Getting Started emphasis path as primary nav destinations.

### C) Overview page cleanup + reframing

In `/` Overview page:
- remove the "Highlighted Tools" section.
- improve the top-level description for first-time readers ("fresh context") to make UM easier to grok quickly.
- keep language concrete and implementation-relevant, not abstract marketing.
- preserve alignment with docs that define normative boundaries and proof requirements.

## Implementation paths (expected)

- `site/astro.config.mjs`
- `site/src/content/docs/index.md`
- `site/src/content/docs/integrations/social.md`
- `site/src/content/docs/integrations/proof-of-personhood.md`
- `site/src/content/docs/integrations/oma-trust.md`
- `site/src/content/docs/integrations/rp1-spatial-fabric.md`
- `site/src/content/docs/integrations/smart-glasses-ar.md`
- `site/src/content/docs/integrations/metaverse.md`
- `site/src/content/docs/integrations/chia-vc.md`
- `site/src/content/docs/getting-started/workbench.md`
- `site/src/content/docs/proof/harness.md`

## Acceptance criteria

- [x] Integrations nav order matches the specified sequence exactly.
- [x] reference implementation is not displayed in Integrations nav.
- [x] Integration labels no longer include "Integration"; "Smart Glasses AR Integration" becomes "Smart Glasses".
- [x] Tools appears as a top-level sidebar section at the bottom with Workbench + Verification Harness links.
- [x] Overview no longer contains "Highlighted Tools".
- [x] Overview opening description is rewritten for first-time comprehension and reviewed for clarity.
- [x] Site build passes: `cd site && npm run build`.
- [x] Live verification checklist is run after deploy for `/`, integrations pages, workbench, and harness.

## Completion evidence

- Updated sidebar/nav config:
  - `site/astro.config.mjs`
- Updated overview framing:
  - `site/src/content/docs/index.md`
- Integration labels and ordering metadata:
  - `site/src/content/docs/integrations/social.md`
  - `site/src/content/docs/integrations/proof-of-personhood.md`
  - `site/src/content/docs/integrations/oma-trust.md`
  - `site/src/content/docs/integrations/rp1-spatial-fabric.md`
  - `site/src/content/docs/integrations/smart-glasses-ar.md`
  - `site/src/content/docs/integrations/metaverse.md`
  - `site/src/content/docs/integrations/chia-vc.md`
  - `site/src/content/docs/integrations/reference-runtime.md`
- Tools docs visibility adjustments:
  - `site/src/content/docs/getting-started/workbench.md`
  - `site/src/content/docs/proof/harness.md`
- Live deploy and verification report:
  - `docs/reports/2026-02-22-wo-0029-nav-live-verification.md`

## Validation commands

- `cd site && npm run build`
- `cd site && npm run build:clean`
- `agent-browser --session um-navcheck open https://universalmanifest.net/`
- `agent-browser --session um-navcheck open https://universalmanifest.net/integrations/social/`
- `agent-browser --session um-navcheck open https://universalmanifest.net/getting-started/workbench/`
- `agent-browser --session um-navcheck open https://universalmanifest.net/proof/harness/`

## Dependencies

- `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`
- `docs/workorders/WO-0014-interactive-manifest-workbench.md`
- `docs/workorders/WO-0025-documentation-human-readability-and-links.md`
- `docs/workorders/WO-0026-workbench-and-harness-redesign.md`
- `docs/workorders/WO-0027-omatrust-integration-lane-execution.md`
