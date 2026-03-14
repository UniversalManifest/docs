# Universal Manifest Website Audit Report

Date: 2026-03-05
Scope: Published website source and directly served assets.
Audited paths:
- `site/src/content/docs`
- `site/src/scripts`
- `site/public`
- `site/astro.config.mjs`
- `site` (tracked root-level artifacts)

## Executive Summary

Critical issues found:
- Private filesystem path leakage in published docs: 6 files.
- Additional private path leakage in tracked site artifacts: 2 files.
- AR-oriented naming/copy that conflicts with requested smart-glasses-only language:
  - Docs/config: 11 files
  - Sandbox scripts/UI strings: 4 files
  - Public assets/fixtures: 15 files
- Publicly served archive/debug artifact directories under `/public`: 3 directories (24 files total).
- Tracked local screenshot/debug artifacts in `site/`: 29 files (`27` `.agent-browser*.png`, `1` `.devserver-4300.log`, `1` `qa-test.html`).

## Findings and Suggested Edits

### A) Private path leaks in published docs (P0)

1) File: `site/src/content/docs/implementations/index.md`
Problem:
- Exposes `/Users/grig/...` for adopter registry references.
Suggested edit:
- Replace with web-usable links.
- Preferred: publish adopter files under `/adopters/` and link to:
  - `/adopters/registry.json`
  - `/adopters/README.md`
- Alternate: link to GitHub URLs if you do not want to publish these files on the site.

2) File: `site/src/content/docs/governance/breaking-change-policy.md`
Problem:
- "Full policy source" points to local path `/Users/grig/...`.
Suggested edit:
- Replace with either:
  - internal website route (preferred), or
  - GitHub source URL.
- Remove all absolute local filesystem paths.

3) File: `site/src/content/docs/governance/release-cadence.md`
Problem:
- "Full cadence policy source" uses local path `/Users/grig/...`.
Suggested edit:
- Replace with site route or GitHub URL.

4) File: `site/src/content/docs/governance/incident-response.md`
Problem:
- "Full runbook source" uses local path `/Users/grig/...`.
Suggested edit:
- Replace with site route or GitHub URL.

5) File: `site/src/content/docs/governance/deprecation-policy.md`
Problem:
- "Full policy source" uses local path `/Users/grig/...`.
Suggested edit:
- Replace with site route or GitHub URL.

6) File: `site/src/content/docs/guides/migration-v01-v02.md`
Problem:
- "The full maintainer copy lives at" uses local path `/Users/grig/...`.
Suggested edit:
- Replace with website-readable link.
- Recommended: either inline full content on this page or link to GitHub source URL.

### B) Private path leaks in tracked site artifacts (P0)

7) File: `site/qa-test.html`
Problem:
- Contains hardcoded `file:///Users/grig/...` paths.
- Not suitable for publishable/public repo surface.
Suggested edit:
- Remove file from repo, or move to non-public dev-only location and rewrite with relative URLs.

8) File: `site/.devserver-4300.log`
Problem:
- Contains local paths (`/Users/grig/...` and `file:///Users/...`) and machine-specific debug output.
Suggested edit:
- Remove from git and add to ignore rules.

### C) Smart-glasses AR wording and route naming (P1)

Requested rule interpreted:
- Replace user-facing "Smart Glasses AR"/"AR ..." wording with "Smart Glasses" wording.

9) File: `site/astro.config.mjs`
Problem:
- Sidebar route uses `/integrations/smart-glasses/`.
Suggested edit:
- Rename canonical route to `/integrations/smart-glasses/`.
- Keep backward-compatible redirect from `/integrations/smart-glasses/` to `/integrations/smart-glasses/`.

10) File: `site/src/content/docs/integrations/smart-glasses-ar.md`
Problem:
- File slug and page text are AR-branded.
Suggested edit:
- Rename file to `smart-glasses.md`.
- Update title/copy to "Smart Glasses" terms.
- Keep legacy redirect for old route.

11) File: `site/src/content/docs/integrations/index.md`
Problem:
- Uses "Smart Glasses AR" lane name and AR wording in lane description/category prose.
Suggested edit:
- Change lane label to "Smart Glasses".
- Replace "AR social overlays" etc. with smart-glasses phrasing.
- Update lane link to `/integrations/smart-glasses/`.

12) File: `site/src/content/docs/integrations/social.md`
Problem:
- Links to old route `/integrations/smart-glasses/`.
Suggested edit:
- Update link to `/integrations/smart-glasses/`.

13) File: `site/src/content/docs/getting-started/universal-manifest-overview.md`
Problem:
- Contains "Smart-glasses AR ..." phrase.
Suggested edit:
- Replace with "Smart glasses ..." phrasing.

14) File: `site/src/content/docs/getting-started/concepts.md`
Problem:
- Mentions "AR devices" in cross-domain list.
Suggested edit:
- Replace with "smart glasses" (or neutral "wearable devices") depending on desired scope.

15) File: `site/src/content/docs/about/one-pager.md`
Problem:
- Uses "smart-glasses AR layer" wording.
Suggested edit:
- Replace with "smart-glasses layer" wording.

16) File: `site/src/content/docs/about/full-briefing.md`
Problem:
- Uses "Privacy-Conscious AR Glasses User" heading and AR-overlay language.
Suggested edit:
- Rename heading and prose to smart-glasses terminology only.

17) File: `site/src/content/docs/about/visual-explainers.md`
Problem:
- Uses "Smart Glasses AR" heading/description and anchor reference `#smart-glasses`.
Suggested edit:
- Rename section/anchor to smart-glasses-only wording.
- Update any internal jump links to the new anchor.

18) File: `site/src/content/docs/use-cases/privacy.md`
Problem:
- User-facing narrative repeatedly uses "AR" terms.
Suggested edit:
- Replace user-facing AR wording with smart-glasses wording.
- Keep or migrate machine keys (`ar.*`) via approach in section E.

19) File: `site/src/content/docs/publishing/changelog.md`
Problem:
- Lists lane as "Smart Glasses AR".
Suggested edit:
- Replace with "Smart Glasses".

### D) Smart-glasses AR wording in sandbox script UI strings (P1)

20) File: `site/src/scripts/sandbox/scenarios/integration-lanes/il-02-smart-glasses-consent.ts`
Problem:
- Runtime descriptions/messages contain "AR" wording.
Suggested edit:
- Update user-facing strings to smart-glasses wording.
- Decide whether to keep `ar.*` machine keys (recommended for compatibility) or migrate (breaking).

21) File: `site/src/scripts/sandbox/scenarios/integration-lanes/il-02-smart-glasses-consent-v2.ts`
Problem:
- Same issue: AR wording in role descriptions, step descriptions, messages.
Suggested edit:
- Replace AR wording in UI text.
- Keep/migrate machine keys based on compatibility decision.

22) File: `site/src/scripts/sandbox/scenarios/advanced/ad-01-cross-system-projection.ts`
Problem:
- Multiple user-facing strings describe "AR system/headset" projection.
Suggested edit:
- Rewrite labels to smart-glasses terminology.
- Preserve machine keys unless you explicitly plan a schema-level rename.

23) File: `site/src/scripts/sandbox/scenarios/advanced/ad-01-cross-system-projection-v2.ts`
Problem:
- Same issue as above (AR wording in V2 strings).
Suggested edit:
- Rewrite strings to smart-glasses terminology.

### E) Smart-glasses AR wording in public assets and fixtures (P1/P2)

24) File: `site/public/animations/scenario-13-smart-glasses-integration.svg`
Problem:
- Visible title/description/text contain "Smart Glasses AR", "AR Device", etc.
Suggested edit:
- Replace visible labels and metadata text with smart-glasses wording.

25) File: `site/public/animations/7.5-smart-glasses-integration.svg`
Problem:
- Contains visible "AR Overlay" label.
Suggested edit:
- Replace with smart-glasses overlay wording.

26) File: `site/public/animations/um-overlay-lanes-pilot.svg`
Problem:
- Contains visible "AR recording consent" text.
Suggested edit:
- Replace with smart-glasses recording consent wording.

27) File: `site/public/diagrams/1.4-system-overview.svg`
Problem:
- Contains "AR Glasses" node label.
Suggested edit:
- Replace with "Smart Glasses".

28) File: `site/public/diagrams/9.4-privacy-user-journey.svg`
Problem:
- Contains "AR glasses ..." text.
Suggested edit:
- Replace with "Smart glasses ..." wording.

29) File: `site/public/sandbox/illustrations/il-02.svg`
Problem:
- Description mentions AR consent flow.
Suggested edit:
- Replace with smart-glasses consent flow phrasing.

30) File: `site/public/animations/scenario-06-motion-tutorial.svg`
Problem:
- Contains `ar.recordingConsent` visible key label.
Suggested edit:
- Keep if preserving compatibility namespace; otherwise migrate with alias strategy.

31) File: `site/public/harness/fixtures/v0.1/stubs/smart-glasses-ar-consent-allowed-manifest.jsonld`
Problem:
- Filename and keys use AR namespace.
Suggested edit:
- Compatibility-safe option: keep as canonical machine fixture, but reword all UI/docs text.
- Breaking option: duplicate as `smart-glasses-consent-allowed-manifest.jsonld`, update references, keep old file as legacy alias.

32) File: `site/public/harness/fixtures/v0.1/stubs/smart-glasses-ar-consent-denied-manifest.jsonld`
Problem:
- Same as item 31.
Suggested edit:
- Same approach as item 31.

33) File: `site/public/sandbox/fixtures/v0.1/stubs/smart-glasses-ar-consent-allowed-manifest.jsonld`
Problem:
- Same as item 31.
Suggested edit:
- Same approach as item 31.

34) File: `site/public/sandbox/fixtures/v0.1/stubs/smart-glasses-ar-consent-denied-manifest.jsonld`
Problem:
- Same as item 31.
Suggested edit:
- Same approach as item 31.

35) File: `site/public/harness/fixtures/v0.1/stubs/cross-system-projection-manifest.jsonld`
Problem:
- Contains `ar.*` keys/types in fixture data.
Suggested edit:
- Keep for compatibility unless intentionally versioning namespace changes.

36) File: `site/public/sandbox/fixtures/v0.1/stubs/cross-system-projection-manifest.jsonld`
Problem:
- Same as item 35.
Suggested edit:
- Same as item 35.

### F) Publicly served archive/debug asset directories (P1)

37) Directory: `site/public/animations/archive_bad_svgs`
Problem:
- 15 legacy "bad" assets publicly served.
Suggested edit:
- Remove from `site/public` (or move to non-public archival location outside publish path).

38) Directory: `site/public/animations/archive-pre-wo-asset-011`
Problem:
- 8 pre-WO archive assets publicly served.
Suggested edit:
- Remove from `site/public` (or move out of publish path).

39) Directory: `site/public/diagrams/archive_bad_svgs`
Problem:
- 1 archived diagram publicly served.
Suggested edit:
- Remove from `site/public` (or move out of publish path).

### G) Tracked local work artifacts in site root (P1)

40) Files: `site/.agent-browser*.png` (27 tracked files)
Problem:
- Internal screenshot evidence committed in website project root.
Suggested edit:
- Remove from git history moving forward (delete tracked files now, add ignore rule).

41) File: `site/.devserver-4300.log`
Problem:
- Machine-specific debug log tracked in repo.
Suggested edit:
- Remove from git and ignore.

42) File: `site/qa-test.html`
Problem:
- Local QA scratch page with machine-specific file paths and non-production purpose.
Suggested edit:
- Remove or relocate to private dev-only area outside published website project.

### H) Maintainer-internal operational content exposed in public docs (P2)

These are not necessarily wrong technically, but match your concern about website-building notes and work artifacts in public docs.

43) File: `site/src/content/docs/publishing/deploy.md`
Problem:
- Contains maintainer runbook pointer (`docs/site/STAGING-PROMOTION-RUNBOOK.md`).
Suggested edit:
- Remove maintainer-note section from public page, or replace with generic governance/publishing policy links.

44) File: `site/src/content/docs/publishing/deploy-checklist.md`
Problem:
- Public page includes repository build command internals and repository-runbook pointer.
Suggested edit:
- Keep only platform-agnostic deployment contract requirements; move repo-specific commands to private maintainer docs.

45) File: `site/src/content/docs/publishing/production-smoke.md`
Problem:
- Includes maintainer workflow references (`docs/operations/...`, `.github/workflows/...`) and repo-centric commands.
Suggested edit:
- Keep high-level smoke contract checks; move repo-specific ops and CI details to maintainer docs.

## Recommended Execution Order

1. Remove P0 path leaks in published docs and site artifacts.
2. Rename smart-glasses route/links and reword user-facing AR copy.
3. Update SVG visible labels.
4. Decide compatibility strategy for `ar.*` machine keys/fixture filenames:
   - Compatibility-safe: keep keys, rename human text only.
   - Breaking: migrate namespace + fixture names with alias/deprecation plan.
5. Remove public archive directories and tracked debug artifacts.
6. Trim maintainer-internal operational content from public docs.

## Proposed compatibility stance for `ar.*` keys

Recommendation:
- Do not rename `ar.*` keys in v0.1 fixtures/scripts in the same pass as copy cleanup.
- Treat namespace migration as a separate versioned change (or add aliases) to avoid breaking sandbox scenarios, proof outputs, and downstream adopters.

