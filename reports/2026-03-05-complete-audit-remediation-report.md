# Complete Audit and Remediation Report

Generated: 2026-03-05T06:44:55Z

## Scope audited

- Published site content and source:
  - `site/src/content/`
  - `site/public/`
  - `site/src/scripts/`
- Non-site docs/content:
  - `docs/`
  - `integrations/`
  - `adopters/`

## Headline result

- Public-scope private-path issues (`/Users/grig/...`): **0 remaining**
- Public-scope AR wording issues: **0 remaining**
- Full-repo private-path issues: **2002 remaining**
- Full-repo AR wording issues: **51 remaining**

The remaining full-repo issues are concentrated in historical/internal records (`docs/reports/`, `docs/workorders/`, `docs/journeys/_artifacts/`) and are fully listed in the inventories below.

## Problems found and edits applied

### 1) Private absolute local paths in public docs

Problem:
- Public-facing docs contained local absolute paths with personal username (`/Users/grig/...`).

Edits applied:
- Replaced repo-local absolute paths with repo-relative references or `<repo-root>` placeholders.
- Replaced `~/.agents`-related local paths with home-relative references where needed.
- Converted key path lists into online-reviewable Markdown links in:
  - `adopters/README.md`
  - `integrations/oma-trust.md`
  - `integrations/rp1-spatial-fabric.md`
  - `integrations/social.md`

Verification:
- `docs/reports/2026-03-05-users-grig-occurrences-public-scope.txt` contains 0 lines.

### 2) AR wording normalization to smart glasses

Problem:
- Public-facing copy used AR phrasing (`Smart Glasses AR`, `AR overlays`, etc.) instead of requested smart glasses wording.

Edits applied:
- Reworded user-facing copy to smart glasses wording across site/docs/integrations.
- Kept technical schema keys like `ar.recording.faceVisible` unchanged to avoid breaking fixtures/runtime compatibility.
- Renamed integration lane files/routes:
  - `integrations/smart-glasses-ar.md` -> `integrations/smart-glasses.md`
  - `site/src/content/docs/integrations/smart-glasses-ar.md` -> `site/src/content/docs/integrations/smart-glasses.md`
  - Route updated to `/integrations/smart-glasses/`
- Updated nav and all non-historical references to the new lane path.

Verification:
- `docs/reports/2026-03-05-ar-occurrences-public-scope.txt` contains 0 lines.
- No non-historical references remain for:
  - `smart-glasses-ar`
  - `/integrations/smart-glasses-ar/`
  - `integrations/smart-glasses-ar.md`

### 3) AR-labeled fixture filenames

Problem:
- Fixture filenames still used `smart-glasses-ar-...` naming.

Edits applied:
- Renamed fixtures:
  - `examples/v0.1/stubs/smart-glasses-ar-consent-allowed-manifest.jsonld` -> `examples/v0.1/stubs/smart-glasses-consent-allowed-manifest.jsonld`
  - `examples/v0.1/stubs/smart-glasses-ar-consent-denied-manifest.jsonld` -> `examples/v0.1/stubs/smart-glasses-consent-denied-manifest.jsonld`
- Updated all non-historical references in:
  - conformance expected/report files
  - journey runner (`packages/universal-manifest/scripts/run-journeys.mjs`)
  - site sandbox/harness fixture references

### 4) Web-irrelevant tracked artifacts in `site/`

Problem:
- Tracked debug screenshots, logs, QA scratch files, and archived bad-SVG directories were committed in `site/`.

Edits applied:
- Removed tracked top-level artifacts:
  - `site/.agent-browser*.png` (27 files)
  - `site/.devserver-4300.log`
  - `site/qa-test.html`
- Removed tracked artifact archives:
  - `site/public/animations/archive_bad_svgs/`
  - `site/public/animations/archive-pre-wo-asset-011/`
  - `site/public/diagrams/archive_bad_svgs/`
- Removed untracked generated artifact dir:
  - `site/public/animations/generated-tests/`

## Complete inventories (every line item)

- Full repo private-path inventory:
  - `docs/reports/2026-03-05-users-grig-occurrences-full.txt`
- Full repo AR inventory:
  - `docs/reports/2026-03-05-ar-occurrences-full.txt`
- Public-scope private-path inventory:
  - `docs/reports/2026-03-05-users-grig-occurrences-public-scope.txt`
- Public-scope AR inventory:
  - `docs/reports/2026-03-05-ar-occurrences-public-scope.txt`

## Remaining issues and suggested next edit

### Remaining private-path issues (2002 lines)

Location concentration:
- `docs/workorders/` (974 lines)
- `docs/reports/` (785 lines)
- `docs/journeys/` (168 lines, mostly `_artifacts`)
- `docs/operations/` (7 lines)

Suggested edit:
- Run a historical-doc redaction pass that replaces:
  - `/Users/grig/work/repo/universalmanifest` -> `<repo-root>`
  - `/Users/grig/.agents` -> `~/.agents`
- Or move workorders/reports artifacts to a non-public archive location.

### Remaining AR issues (51 lines)

Location concentration:
- `docs/reports/` (35 lines)
- `docs/workorders/` (13 lines)
- `spec/` (3 lines)

Suggested edit:
- Keep as historical fidelity, or run a second normalization pass limited to `docs/reports/` and `docs/workorders/`.

## Verification run

- `cd site && npm run build` -> success (existing duplicate-id/content warnings remain pre-existing).
- `cd packages/universal-manifest && npm test` -> success.
- `cd packages/universal-manifest && npm run journeys` -> success (generated journey artifact removed after verification).
