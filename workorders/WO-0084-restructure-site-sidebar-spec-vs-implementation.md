# WO-0084 — Restructure Docs Site Sidebar to Separate Spec from Implementation

**Status:** COMPLETED
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Spec-vs-Implementation Boundary Audit (2026-03-01), Recommendation R5, R12, Action Item 6; Project Completeness Audit, Gap 14 (site IA); Verification report (integration lanes sidebar gap)
**Tags:** [site], [structural]
**Blocks:** Clear separation of spec reading paths from implementation-specific tooling
**Dependencies:** None (can be done independently)
**Estimated effort:** 3-5 hours

## Objective

Restructure the `universalmanifest.net` Starlight docs site sidebar to clearly separate specification content from implementation/tooling content. The TypeScript helper should not appear under "Getting Started" as if it were a prerequisite.

## Why this work matters

Currently, the site sidebar groups the TypeScript helper under "Getting Started," implying it is part of the core onboarding path. A reader following the natural navigation sequence encounters the TypeScript package as a prerequisite rather than as one optional tool. There is also no "Implementations" section that would signal to external adopters that multiple implementations are expected.

## Scope

### File to modify

**`site/astro.config.mjs`** — Sidebar configuration

### Recommended new sidebar structure

```
Getting Started
  What Is Universal Manifest?
  Concepts
  Quick Start
  Stub Manifests

Specification
  v0.1
  v0.2 (draft)

Conformance
  v0.1
  v0.2
  Resolver

Integrations
  (all integration lanes)

Tools & Reference Implementations
  TypeScript Helper (Reference Implementation)
  Manifest Workbench
  Verification Harness
  Implementation Sandbox

Publishing
  (existing publishing pages)

Proof
  (existing proof pages)

Governance
  (existing governance pages)
```

### Key changes

1. Move "TypeScript Helper" from "Getting Started" to "Tools & Reference Implementations."
2. Rename the sidebar label from "TypeScript Helper" to "TypeScript Helper (Reference)" or "TypeScript Reference Implementation."
3. Create a new "Tools & Reference Implementations" section (or rename existing "Tools" section) that clearly positions these as supplementary.
4. Consider adding a "Build Your Own Implementation" entry in "Getting Started" (coordinates with WO-0085).

### Integration lanes sidebar gap (from verification report)

The verification agent discovered that the site sidebar config (`astro.config.mjs`) explicitly lists only 7 integration lanes using individual item entries (NOT autogenerate). However, 3 additional integration lanes exist as content files but are NOT listed in the sidebar:

- `site/src/content/docs/integrations/healthcare-patient-consent.md` — **not in sidebar**
- `site/src/content/docs/integrations/education-credentials.md` — **not in sidebar**
- `site/src/content/docs/integrations/smart-home.md` — **not in sidebar**

Additionally, the catalog index page (`integrations/index.md`) and the reference runtime page may also be invisible in the sidebar depending on the config. Visitors would only discover these pages if they navigate to the catalog index or guess the URL.

**Fix required:** Either add these 3 lanes (and the catalog index) explicitly to the sidebar config, or switch the Integrations section to use Starlight's `autogenerate` directive instead of explicit item listing. If using autogenerate, verify that the label and ordering are acceptable.

## Acceptance criteria

- [ ] TypeScript Helper is NOT in the "Getting Started" sidebar section.
- [ ] TypeScript Helper appears in a clearly labeled "Tools" or "Implementations" section.
- [ ] The sidebar label includes "Reference" or "(Reference Implementation)" qualifier.
- [ ] A reader following "Getting Started" top-to-bottom encounters only spec-level content.
- [ ] ALL integration lane content pages are discoverable via the sidebar (including Healthcare, Education, Smart Home).
- [ ] `cd site && npm run build:clean` succeeds.
- [ ] All existing page URLs continue to work (no broken links).

## Validation commands

- `cd site && npm run build:clean`
- Manual review of sidebar navigation in browser.
