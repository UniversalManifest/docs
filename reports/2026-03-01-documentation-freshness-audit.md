# Documentation Freshness Audit — 2026-03-01

**Audit scope:** All changes from 2026-02-22 through 2026-03-01.
**Method:** Git log analysis, file inventory, cross-reference of key documents against actual repo state.

---

## 1. Executive Summary

The project has undergone a massive burst of work in the past week: 20+ work orders completed (WO-0042 through WO-0068, plus WO-0069 through WO-0080 for Sandbox V2), 40+ new files created, and multiple architectural decisions made. The uncommitted updates to `STATE-OF-THE-PROJECT.md`, `DECISIONS.md`, and `WO-INDEX.md` are reasonably current through 2026-02-28 but do not reflect the Sandbox V2 redesign (WO-0069 through WO-0080) completed on 2026-03-01. The documentation index (`docs/README.md`) is significantly stale -- it has not been updated to reference approximately 20 new document categories and files created this week. `CRITICAL-PATH.md` has not been updated at all during this period and does not mention the sandbox wave or external adopter wave.

---

## 2. Recent Changes Inventory

### Commits since 2026-02-22 (48 commits) [CORRECTION 2026-03-01: Original report stated 38 commits; actual count from `git log --since=2026-02-22` is 48.]

| Date | Commit | Summary |
|------|--------|---------|
| 02-22 | `12bfc51` | Remove internal CEO framing from public docs |
| 02-22 | `fdb1710` | Add WO-0035 through WO-0043 and reviewed animation upgrade proposal |
| 02-22 | `1e3d7e2` | Archive outdated SVG animations to dedicated directory |
| 02-22/23 | `4d3c032` | Lane B and C closeout reports |
| 02-23 | `1b4a49f` | New SVG infographics + style guide + QA test page |
| 02-23 | `91985f2` | Add CODE_OF_CONDUCT, CONTRIBUTING, LICENSE, SECURITY |
| 02-23 | `103c272` | Update manifest schema (schema.json updates, Lan to Um rename) |
| 02-23 | `eb56979` | Update WO-INDEX, add WO-0044 |
| 02-25/26 | `8e7d5b4` | Sync agents and audit project state, add SVG style guide |
| 02-26 | `6463d29` | Add remaining-work + branding-fix reports, journey artifacts |
| 02-26 | `90ea999` | Comprehensive code examples (10 examples + demo app) |
| 02-26 | `858e327` | Expand code examples ecosystem, add WO-0044 file |
| 02-26 | `240092f` | Add WO-0045 commercial explainers, CEO mandate inbox item |
| 02-26 | `8e6938d` | Add explainer documents, animation scripts, commercial journeys |
| 02-26 | `06aaf91` | Add integration template, authoring guide, 3 new integration lanes |
| 02-26 | `a578c56` | Add infographic styles inventory |
| 02-26 | `4f76c56` | Update WO-INDEX, add WO-0045 |
| 02-26 | `144b70b` | Add 15 core project diagrams (static SVGs) |
| 02-26 | `263675b` | Add 15 animation assets (numbered series) |
| 02-26 | `283032c` | Archive legacy animation assets |
| 02-26/27 | `76d168c` | Infographic styles inventory verification |
| 02-27 | `db1dc38` | Governance framework: branch protection, contributing registry, governance, maintainers, RFC template |
| 02-27 | `02989c2` | Add v0.2 examples and fixtures (4 valid, 3 invalid) |
| 02-27 | `be8f76d` | Update animation placement plan, QA checklist, spec docs |
| 02-27 | `a631e41` | Refresh 15 visual animation assets |
| 02-27 | `b59b36a` | Update core package: scripts, types, package.json |
| 02-28 | `9cc097d` | Comprehensive documentation: briefing, teaching scripts, WO-0053 through WO-0068 |
| 02-28 | `547dcd9` | Update WO-INDEX files |
| 02-28 | `e083df1` | Project maintenance and gaps |
| 02-28 | `b379933` | Standardize signature terminology ("signature envelope" to "signature"), add ENVELOPE-TOPOLOGY.md, ANIMATED-SVG-WORKFLOW.md |

### Uncommitted work (present in working tree, not yet committed)

- **Interactive Sandbox V1** (WO-0060 through WO-0068): 25 scenarios, browser validator, three-panel layout, 25 SVG illustrations, CI parity scripts. Files in `site/src/components/sandbox/`, `site/src/pages/sandbox/`, `site/src/scripts/sandbox/`, `site/src/styles/sandbox/`, `site/public/sandbox/`.
- **Interactive Sandbox V2** (WO-0069 through WO-0080): Complete UI redesign with HierarchyExplorer, DetailsCard, EntityColumn, ProtocolLens, SubjectPanel, SandboxLayoutV2, SandboxEngineV2 -- 25 V2 scenario files.
- **Capsule-Pod design**: `docs/design/CAPSULE-POD-DESIGN.md` + `docs/design/capsule-pod-reference/` (9 cinematic renders).
- **Permissions firewall design**: `docs/design/PERMISSIONS-FIREWALL-DESIGN.md`.
- **Sandbox UI mockup**: `docs/design/sandbox-ui-mockup.excalidraw`.
- **New stub fixture**: `examples/v0.1/stubs/cross-system-projection-manifest.jsonld`.
- **Updated docs**: STATE-OF-THE-PROJECT.md, DECISIONS.md, diagrams/README.md (all have uncommitted diffs).
- **Sandbox V2 proposal**: `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`.
- **Verification artifacts**: `.dev/ai/verification/`, `.dev/reviews/`.

---

## 3. Documentation Update Status

### Key documents from docs/README.md

| Document | Status | Issue (if any) |
|----------|--------|----------------|
| `docs/README.md` | **STALE** | Missing ~20 new document categories created this week. See Section 4 for full list. |
| `docs/STATE-OF-THE-PROJECT.md` | **Partially current** (uncommitted) | Uncommitted version is current through 2026-02-28 but does not reflect Sandbox V1 completion (WO-0060-0068 built) or Sandbox V2 (WO-0069-0080). Committed version is from 2026-02-23. |
| `docs/DECISIONS.md` | **Partially current** (uncommitted) | Uncommitted version adds 2 new decisions (Capsule-Pod, Excalidraw ON HOLD). Missing the WO-0060-0068 approval decision and terminology standardization decision (both occurred this week). |
| `docs/CRITICAL-PATH.md` | **STALE** | No commits this week. Does not mention: sandbox wave, external adopter wave, WO-0053-0068, or teaching scripts system. Last meaningful update was pre-2026-02-22. |
| `docs/workorders/WO-INDEX.md` | **Current** (committed) | Reflects all WOs through WO-0068 with correct statuses. Does not include WO-0069-0080 (V2 sandbox -- uncommitted work). |
| `docs/PROJECT-VISION.md` | Current | No issues. |
| `docs/DEPTH-AND-SCOPE.md` | Current | Updated during terminology cleanup. |
| `docs/PUBLISHING-AND-VERSIONING.md` | Current | No recent changes needed. |
| `docs/DOMAIN-ARCHITECTURE.md` | Current | No recent changes needed. |
| `docs/RELEASING.md` | Current | No recent changes needed. |
| `docs/DEPLOY-CHECKLIST.md` | Current | No recent changes needed. |
| `docs/CRUCIAL-DETAILS.md` | Current | No recent changes needed. |
| `docs/ENVELOPE-TOPOLOGY.md` | **New, indexed** | Created this week, already in docs/README.md. Good. |
| `docs/DONE-DONE-DEFINITION.md` | Current | No issues. |
| `docs/DONE-DONE-CHECKLIST.md` | Current | No issues. |
| `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md` | Current | No issues. |
| `docs/TS-HELPER-PACKAGE.md` | Current | No issues. |
| `docs/journeys/README.md` | Current | No issues. |
| `docs/diagrams/README.md` | **Partially current** (uncommitted) | Uncommitted version adds ON HOLD decision. Claims "16 production assets" -- this count is outdated. |
| `docs/STUB-MANIFESTS.md` | Current | Updated during terminology cleanup. |
| `docs/AGENT-OBSERVED-GAPS.md` | Current | No issues. |
| `integrations/reference-runtime.md` | Current | Updated during terminology cleanup. |
| `integrations/rp1-spatial-fabric.md` | Current | Updated during cleanup. |
| `integrations/social.md` | Current | No issues. |
| `integrations/metaverse.md` | Current | No issues. |
| `integrations/smart-glasses-ar.md` | Current | Updated during cleanup. |
| `spec/v0.1/README.md` | Current | Updated during terminology cleanup. |
| `spec/v0.1/CONFORMANCE.md` | Current | Updated during cleanup. |
| `spec/v0.2/SIGNATURE-PROFILE.md` | Current | Updated during terminology cleanup. |

### Cross-reference: STATE-OF-THE-PROJECT.md pointers

| Reference in STATE-OF-THE-PROJECT | Status | Issue |
|-----------------------------------|--------|-------|
| "latest condensed status summary" points to `docs/reports/2026-02-18-live-status-and-next-critical-path.md` | **STALE** | That report is from 2026-02-18 and shows WO-0014 as OPEN. It is far outdated as a "latest" reference. |
| "16 production animated SVGs" (line 51) | **Outdated** | 31 non-test production SVGs now exist (16 original scenario-prefixed + 15 numbered). |
| "46/46 fixtures" in verification section (line 223) | **Slightly outdated** | 46 committed fixtures is correct for committed state, but there is 1 new uncommitted stub. |
| WO-0060-0068 listed as "NOT_STARTED" | **Outdated** | Per handoff files, WO-0060-0068 are all COMPLETED (built and verified), but the code is uncommitted. |

---

## 4. New Artifacts Not Yet Indexed in docs/README.md

The following files and directories were created this week and are NOT referenced in `docs/README.md`:

### Documents

| File | Description | Created |
|------|-------------|---------|
| `docs/UNIVERSAL-MANIFEST-BRIEFING.md` | Full AI agent briefing document | 02-28 |
| `docs/MANDATE-interactive-implementation-sandbox.md` | CEO mandate for interactive sandbox | 02-28 |
| `docs/teaching-scripts/README.md` | Teaching scripts system index | 02-28 |
| `docs/teaching-scripts/01-ICONIC-REPRESENTATION.md` | Capsule-Pod iconic representation design | 02-28 |
| `docs/teaching-scripts/02-SCRIPT-FORMAT.md` | Teaching script format guide | 02-28 |
| `docs/teaching-scripts/03-SCRIPT-IDEAS.md` | Teaching script ideas | 02-28 |
| `docs/explainers/` (5 files) | Commercial explainer documents (paragraph, one-pager, full briefing, agent briefing, animation briefing) | 02-26 |
| `docs/scripts/` (4 files) | Animation scripts (what-is-um, how-it-works, why-it-matters, day-in-the-life) | 02-26 |
| `docs/guides/integration-authoring-guide.md` | Guide for writing integration lanes | 02-26 |
| `docs/journeys/commercial/` (5 files) | Commercial user journeys (creator, venue-operator, app-developer, privacy, enterprise) | 02-26 |
| `docs/governance/` (5 files) | Governance framework, branch protection, contributing registry, maintainers, RFC template | 02-27 |
| `docs/security/THREAT-MODEL.md` | Security threat model | 02-27 |
| `docs/design/ANIMATED-SVG-WORKFLOW.md` | Animated SVG production workflow | 02-28 |
| `docs/design/ANIMATED-SVG-SPEC.md` | Animated SVG specification | ~02-27 |
| `docs/design/ANIMATION-PLACEMENT-PLAN.md` | Animation placement plan | 02-23 |
| `docs/design/ANIMATION-QA-CHECKLIST.md` | Animation QA checklist | 02-23 |
| `docs/design/SVG-INFOGRAPHIC-STYLE-GUIDE.md` | SVG infographic style guide | 02-25 |
| `docs/design/INFOGRAPHIC-STYLES-INVENTORY.md` | Complete infographic styles inventory | 02-26 |
| `docs/design/CAPSULE-POD-DESIGN.md` | Capsule-Pod design spec (uncommitted) | 02-28 |
| `docs/design/PERMISSIONS-FIREWALL-DESIGN.md` | Permissions firewall design (uncommitted) | 02-28+ |
| `docs/design/capsule-pod-reference/` | Capsule-Pod cinematic reference renders (uncommitted) | 02-28 |

### Integration lanes (not in README.md)

| File | Description |
|------|-------------|
| `integrations/TEMPLATE.md` | Integration lane template |
| `integrations/oma-trust.md` | OMATrust integration lane |
| `integrations/proof-of-personhood.md` | Multi-provider proof-of-personhood lane |
| `integrations/chia-vc.md` | Chia DID/VC credential lane |
| `integrations/education-credentials.md` | Education credentials lane |
| `integrations/healthcare-patient-consent.md` | Healthcare patient consent lane |
| `integrations/smart-home.md` | Smart home lane |

Note: `oma-trust.md`, `proof-of-personhood.md`, and `chia-vc.md` are referenced in `STATE-OF-THE-PROJECT.md` but not in `docs/README.md`.

### Code and tooling (not in README.md)

| File/Directory | Description |
|----------------|-------------|
| `examples/code/` (14 directories) | 10 runnable code examples + Python + browser validate + README + CONTRIBUTING |
| `examples/demo-app/` | Full demo application |
| `site/src/pages/sandbox/` | Interactive sandbox pages (uncommitted) |
| `site/src/components/sandbox/` | 18 sandbox Astro components (uncommitted) |
| `site/src/scripts/sandbox/` | Sandbox engine, validator, scenarios (uncommitted) |
| `site/public/sandbox/illustrations/` | 25 SVG illustrations (uncommitted) |

### Foundation files (not in README.md)

| File | Description |
|------|-------------|
| `CODE_OF_CONDUCT.md` | Code of conduct |
| `CONTRIBUTING.md` | Contributing guide |
| `LICENSE` | License file |
| `SECURITY.md` | Security policy |

### Reports created this week (not in README.md)

| File | Date |
|------|------|
| `docs/reports/2026-02-23-remaining-work-to-final-vision.md` | 02-23 |
| `docs/reports/2026-02-23-comprehensive-critical-path-map-and-milestones.md` | 02-23 |
| `docs/reports/2026-02-23-first-time-reader-test-results-human.md` | 02-23 |
| `docs/reports/2026-02-26-branding-fix-schema-and-remaining-work.md` | 02-26 |
| `docs/reports/2026-03-01-spec-vs-implementation-boundary-audit.md` | 03-01 (uncommitted) |

---

## 5. Stale or Inconsistent Content

### 5.1 Animation count mismatch

- **Files affected:** `docs/STATE-OF-THE-PROJECT.md` (line 51), `docs/diagrams/README.md` (line 9), `docs/design/ANIMATED-SVG-WORKFLOW.md` (lines 3, 25, 720)
- **Issue:** All claim "16 production animated SVGs." The actual count in `site/public/animations/` is 33 SVG files total. Excluding 2 test files (`scenario-99-isometric-test.svg`, `scenario-99-nested-orbits-test.svg`) leaves 31 SVGs. Of those 31, 2 are pilot/earlier-iteration files (`um-core-flow-pilot.svg`, `um-overlay-lanes-pilot.svg`), leaving 29 non-test, non-pilot production SVGs: 14 scenario-prefixed files plus 15 newer numbered files (e.g., `1.3-overlay-lanes.svg`, `5.2-consent-policy-flow.svg`). Additionally, 15 static diagrams and 1 template exist in `site/public/diagrams/`. [CORRECTION 2026-03-01: Original report stated "31 production-quality SVGs" -- the count of 31 includes 2 pilot files. Excluding both test and pilot files, the production SVG count is 29.]
- **Fix needed:** Update the count to reflect the full inventory, or clarify which 16 are "the original" vs. the full set.

### 5.2 "Latest condensed status summary" pointer is stale

- **File:** `docs/STATE-OF-THE-PROJECT.md` (line 11)
- **Issue:** Points to `docs/reports/2026-02-18-live-status-and-next-critical-path.md` which shows WO-0014 as OPEN and has no awareness of work orders beyond WO-0019.
- **Fix needed:** Either update the referenced report, create a new current status report, or remove the "latest" characterization.

### 5.3 CRITICAL-PATH.md has no sandbox or external adopter phase

- **File:** `docs/CRITICAL-PATH.md`
- **Issue:** Stops at Phase 9 (Drift governance). Does not include:
  - The External Adopter Wave (WO-0053-0059, blocking Gate G4/G6)
  - The Interactive Sandbox Wave (WO-0060-0068, HIGHEST PRIORITY per CEO mandate)
  - The teaching scripts/visual identity system
  - The code examples ecosystem
- **Fix needed:** Add phases or milestones for these new work streams.

### 5.4 Sandbox WOs show "NOT_STARTED" but are completed

- **File:** `docs/STATE-OF-THE-PROJECT.md` (uncommitted version, lines 140-152)
- **Issue:** WO-0060 through WO-0068 are listed as "NOT_STARTED, HIGHEST PRIORITY" but per the handoff files (2026-02-28-17-18-00Z, 2026-02-28-18-50-00Z), all 9 WOs were completed and verified. The V2 redesign (WO-0069-0080) is also complete but untracked.
- **Fix needed:** Update WO-0060-0068 status to COMPLETED. Add WO-0069-0080 to the index.

### 5.5 CI workflow reference in DECISIONS.md

- **File:** `docs/DECISIONS.md` (line 144)
- **Issue:** References `.github/workflows/verify.yml` as the CI workflow. A new `ci.yml` was added this week (WO-0049) with a 5-job pipeline. Both files exist, but the decision record does not mention the new expanded CI workflow.
- **Minor:** No factual error, just incomplete.

### 5.6 Fixture count in STATE-OF-THE-PROJECT.md verification section

- **File:** `docs/STATE-OF-THE-PROJECT.md` (uncommitted version, line 223)
- **Issue:** States "46/46 fixtures" but an uncommitted new stub (`cross-system-projection-manifest.jsonld`) brings the total to 47. The number will need updating when that stub is committed.
- **Minor:** Only relevant after the stub is committed.

### 5.7 docs/README.md "Key docs" section references only one report

- **File:** `docs/README.md` (line 21)
- **Issue:** The only report referenced is `docs/reports/2026-02-18-live-status-and-next-critical-path.md`. There are now 37 report .md files (including 3 newly created audit reports and 1 template file), plus an `inputs/` subdirectory. The README provides no indication of the reports directory structure or the recent reports. [CORRECTION 2026-03-01: Original report stated 34 report files; actual count at time of this verification is 37 .md files. The original count of 34 was likely taken before the 3 audit reports were written to the same directory.]
- **Fix needed:** Add a mention of the `docs/reports/` directory or at minimum reference the most relevant recent reports.

### 5.8 WO-INDEX does not track WO-0069 through WO-0080

- **File:** `docs/workorders/WO-INDEX.md`
- **Issue:** The Sandbox V2 redesign (WO-0069 through WO-0080) was completed per the 2026-03-01 handoff but has no WO files and no index entries. These 12 WOs exist only in the handoff narrative.
- **Fix needed:** Either create formal WO files for WO-0069-0080 or document them as an addendum to the sandbox wave in WO-INDEX.

---

## 6. Recommended Updates (prioritized)

### Priority 1 — Commit or track uncommitted work

1. **Commit sandbox V1 (WO-0060-0068) code and artifacts.** The entire interactive sandbox is built, verified, and browser-tested but is entirely uncommitted. This is the single largest body of untracked work.
2. **Commit design docs** (CAPSULE-POD-DESIGN.md, capsule-pod-reference/, PERMISSIONS-FIREWALL-DESIGN.md, sandbox-ui-mockup.excalidraw).
3. **Commit STATE-OF-THE-PROJECT.md and DECISIONS.md diffs.** The uncommitted versions are substantially more current than the committed ones.
4. **Commit the new cross-system-projection stub fixture.**

### Priority 2 — Update docs/README.md

5. **Add all new document categories to the documentation index.** At minimum:
   - `docs/UNIVERSAL-MANIFEST-BRIEFING.md`
   - `docs/MANDATE-interactive-implementation-sandbox.md`
   - `docs/teaching-scripts/` directory
   - `docs/explainers/` directory
   - `docs/scripts/` directory
   - `docs/guides/` directory
   - `docs/journeys/commercial/` directory
   - `docs/governance/` directory
   - `docs/security/THREAT-MODEL.md`
   - `docs/design/ANIMATED-SVG-WORKFLOW.md` and related animation design docs
   - `docs/design/CAPSULE-POD-DESIGN.md`
   - `docs/design/INFOGRAPHIC-STYLES-INVENTORY.md`
   - New integration lanes (oma-trust, proof-of-personhood, chia-vc, education, healthcare, smart-home, TEMPLATE)
   - `examples/code/` and `examples/demo-app/`
   - Foundation files (CODE_OF_CONDUCT, CONTRIBUTING, LICENSE, SECURITY)

### Priority 3 — Fix stale cross-references

6. **Update CRITICAL-PATH.md** to include sandbox wave, external adopter wave, and teaching/visual identity phases.
7. **Update the animation count** from "16" to the actual number across `STATE-OF-THE-PROJECT.md`, `diagrams/README.md`, and `ANIMATED-SVG-WORKFLOW.md`.
8. **Update the "latest condensed status summary" pointer** in STATE-OF-THE-PROJECT.md to reference a more current report or remove the "latest" characterization.
9. **Update WO-0060-0068 status** from NOT_STARTED to COMPLETED in STATE-OF-THE-PROJECT.md.
10. **Add WO-0069-0080 entries** to WO-INDEX.md (or document their existence as part of the sandbox V2 handoff).

### Priority 4 — Minor consistency fixes

11. Add the new CI workflow (`ci.yml`, WO-0049) to DECISIONS.md or create a supplementary decision record.
12. Update fixture count when the new stub is committed.
13. Consider creating a fresh "condensed status report" to replace the 2026-02-18 version as the current status pointer.
