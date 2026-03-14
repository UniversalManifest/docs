# WO-0094 — Fix GitHub Repository URL Inconsistencies

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P0 (Critical)
**Source:** Project Completeness and Vision Audit (2026-03-01), Gap 27, Recommended Action P0-5; Verification report correction (4 URLs, not 2)
**Tags:** [docs], [site], [structural]
**Blocks:** Public presentation readiness (broken links destroy credibility)
**Dependencies:** Decision on which GitHub URL is canonical
**Estimated effort:** 1-2 hours

## Resolution

Canonical GitHub URL determined from `git remote -v`: `https://github.com/grigb/universal-manifest`

All four legacy URL patterns were standardized to the canonical URL across all active source files:
- `github.com/LocalArtistNetwork/universalmanifest` -- replaced in `site/astro.config.mjs`, `site/src/content/docs/getting-started/adopt.md`
- `github.com/WebOfTrustInfo/universal-manifest` -- replaced in `.github/ISSUE_TEMPLATE/rfc.yml`, `CONTRIBUTING.md`, `docs/governance/CONTRIBUTING-REGISTRY.md`, `docs/governance/MAINTAINERS.md`
- `github.com/nicholasgrigoriadis/universalmanifest` -- replaced in `docs/explainers/agent-briefing.md`, `docs/explainers/full-briefing.md`
- `github.com/universalmanifest/universalmanifest` and `github.com/universalmanifest/universal-manifest` -- replaced in `examples/code/CONTRIBUTING.md`, `examples/code/README.md`, `site/src/content/docs/integrations/smart-home.md`, `site/src/content/docs/integrations/healthcare-patient-consent.md`, `site/src/content/docs/integrations/index.md`, `site/src/content/docs/integrations/education-credentials.md`

Also updated stale npm package name references (`@nicholasgrigoriadis/universal-manifest` to `universal-manifest`) in agent-briefing.md and full-briefing.md.

Historical report/audit files were not modified (they record what was found at the time of the audit).

## Objective

Resolve the inconsistency between GitHub repository URLs used across the project and ensure a single canonical URL is used everywhere.

## Why this work matters

The completeness audit found GitHub URL inconsistencies, and the verification agent confirmed the problem is worse than originally reported. At least **4 different GitHub URLs** exist across the project:

1. `github.com/LocalArtistNetwork/universalmanifest` — used in `site/astro.config.mjs` (site header link)
2. `github.com/WebOfTrustInfo/universal-manifest` — used in governance docs, `CONTRIBUTING.md`
3. `github.com/nicholasgrigoriadis/universalmanifest` — used in agent briefing, full briefing
4. `github.com/universalmanifest/universalmanifest` — used in code examples

This inconsistency must be resolved before any public presentation — a broken or incorrect GitHub link on the official site destroys credibility instantly.

## Scope

### Investigation

1. Determine which GitHub URL is the canonical current location of the repository.
2. Search all files for references to ALL FOUR known URL patterns.

### Files likely affected

- **`site/astro.config.mjs`** — Site header GitHub link (uses `LocalArtistNetwork`)
- **`docs/governance/GOVERNANCE.md`** — Governance references (uses `WebOfTrustInfo`)
- **`CONTRIBUTING.md`** — Contributing guide (uses `WebOfTrustInfo`)
- **`docs/explainers/agent-briefing.md`** — Agent briefing (uses `nicholasgrigoriadis`)
- **`docs/explainers/full-briefing.md`** — Full briefing (uses `nicholasgrigoriadis`)
- **Code example files** — (use `universalmanifest/universalmanifest`)
- **Any other file** referencing any of the four URL patterns

### Search commands

```bash
rg -n "github.com/LocalArtistNetwork" 
rg -n "github.com/WebOfTrustInfo" 
rg -n "github.com/nicholasgrigoriadis" 
rg -n "github.com/universalmanifest" 
rg -n "github.com.*universalmanifest\|github.com.*universal-manifest" 
```

### Fix

Update ALL references across ALL FOUR patterns to use the single canonical URL.

## Acceptance criteria

- [ ] A single canonical GitHub URL is used in ALL files across the project.
- [ ] `rg -n "github.com" site/` returns only the canonical URL (for the UM repo itself).
- [ ] The site header GitHub icon links to the correct, accessible repository.
- [ ] No governance or documentation files reference an incorrect or outdated GitHub URL.
- [ ] All four legacy URL patterns return zero matches: `LocalArtistNetwork`, `WebOfTrustInfo`, `nicholasgrigoriadis`, and any non-canonical `universalmanifest` org URL.

## Validation commands

- `rg -n "github.com/LocalArtistNetwork" `
- `rg -n "github.com/WebOfTrustInfo" `
- `rg -n "github.com/nicholasgrigoriadis" `
- `rg -n "github.com/universalmanifest" ` (verify only canonical URL remains)
- Manual verification that the canonical URL resolves in a browser.
