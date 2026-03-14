# Universal Manifest Project History Roadmap and Replay Protocol

Date: 2026-02-23  
Project: ``  
Agent Task ID: `b617cafd_1771721466`

## Purpose

This document provides a reproducible, source-cited roadmap of the project from inception to current state so another agent can independently reconstruct history and evaluate outcomes with minimal bias.

Important posture:
- Treat this roadmap as a navigation aid.
- Treat primary source files and git history as authority.
- If any statement here conflicts with source files, source files win.

## Project start and current anchor

Project bootstrap anchor (git):
- 2026-02-11 16:06:45 -0700
- Commit: `904538b`
- Message: `chore: bootstrap universal manifest spec repo`

Current head anchor at roadmap creation:
- 2026-02-22 18:20:41 -0700
- Commit: `ebbde1d`
- Message: `Create work order to rewrite docs`

Command to verify:
- `git -C  log --reverse --date=iso --pretty=format:'%ad %h %s' | sed -n '1,5p'`
- `git -C  log --date=iso --pretty=format:'%ad %h %s' | sed -n '1,5p'`

## Chronological roadmap (major milestones)

## 2026-02-11: Repo bootstrap and v0.1 foundation

Major outcomes:
- New dedicated UM repo established.
- Initial v0.1 artifacts created (`schema`, `context`, `README`, baseline examples).
- Initial reference implementation integration note and TS helper skeleton created.

Primary evidence:
- `docs/WORKLOG-2026-02-11.md`
- `spec/v0.1/README.md`
- `spec/v0.1/schema.json`
- `spec/v0.1/schema.jsonld`

## 2026-02-12: Conformance scaffolding, publishing architecture, and early WO system

Major outcomes:
- Near-real stubs and invalid fixtures added.
- v0.1 conformance checklist added.
- v0.2 signature direction draft started.
- Domain split recorded (`universalmanifest.net` standards, `myum.net/{UMID}` resolver).
- Work-order tracking system formalized.

Primary evidence:
- `docs/WORKLOG-2026-02-12.md`
- `spec/v0.1/CONFORMANCE.md`
- `docs/DOMAIN-ARCHITECTURE.md`
- `docs/PUBLISHING-AND-VERSIONING.md`
- `docs/workorders/WO-INDEX.md`

## 2026-02-13: Gate-based completion model adopted

Major outcomes:
- Official done-done framework adopted with evidence requirements.
- Completion claims became gate-driven instead of narrative-only.

Primary evidence:
- `docs/DECISIONS.md` (2026-02-13 sections)
- `docs/DONE-DONE-DEFINITION.md`
- `docs/DONE-DONE-CHECKLIST.md`
- `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`

## 2026-02-17: Proof model hardening and repo/system alignment

Major outcomes:
- Journeys-as-proof direction codified.
- v0.2 integrity baseline decision recorded (JCS + Ed25519).
- CI verification and endpoint smoke integrated.
- Repo relocation and GAS split onboarding model recorded.

Primary evidence:
- `docs/DECISIONS.md` (2026-02-17 sections)
- `.github/workflows/verify.yml`
- `packages/universal-manifest/scripts/smoke-endpoints.mjs`
- `PROJECT-RULES.md`

## 2026-02-18: CEO-priority onboarding and tooling wave

Major outcomes:
- Interactive workbench prioritized (`WO-0014`).
- First-time overview and visual onboarding prioritized (`WO-0015`).
- Knowledge integration ledger and deferred-corpus conflict protocol formalized.

Primary evidence:
- `docs/DECISIONS.md` (2026-02-18 sections)
- `docs/workorders/WO-0014-interactive-manifest-workbench.md`
- `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`
- `docs/workorders/WO-0016-gas-index-scan-and-knowledge-integration-ledger.md`
- `.dev/ai/ingestion/records/2026-02-18-cross-source-conflicts.md`

## 2026-02-19: Full-corpus synthesis materialized into IA, journeys, and workbench planning

Major outcomes:
- WO-0017 synthesis execution pass completed.
- IA and journey planning outputs linked to concrete implementation WOs.
- Critical-path stabilization work queued and advanced.

Primary evidence:
- `docs/DECISIONS.md` (2026-02-19 section)
- `.dev/ai/specs/2026-02-19-ia-delta-from-full-corpus.md`
- `docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`
- `docs/reports/2026-02-20-master-forward-worklist.md`

## 2026-02-20: Lineage codification + lane expansion + resolver reliability hardening

Major outcomes:
- MUM lineage recorded and metaverse/RP1/smart-glasses integration lanes codified.
- Resolver parity/routing hardening decisions captured.
- DID method and proof-of-personhood provider selections recorded.
- WO-0018 through WO-0024 execution wave completed.

Primary evidence:
- `docs/DECISIONS.md` (2026-02-20 sections)
- `docs/workorders/WO-0018-mum-lineage-and-emerging-integration-codification.md`
- `docs/workorders/WO-0019-resolver-j03-reliability-and-routing-hardening.md`
- `docs/workorders/WO-0020-rp1-source-ingestion-and-synthesis-materialization.md`
- `docs/workorders/WO-0021-smart-glasses-consent-fixtures-and-proof-journeys.md`
- `docs/workorders/WO-0022-metaverse-lane-fixtures-and-proof-hardening.md`
- `docs/workorders/WO-0023-production-deployment-drift-prevention-automation.md`
- `docs/workorders/WO-0024-multi-provider-proof-of-personhood-social-did-chia-integration.md`

## 2026-02-21 to 2026-02-22: Docs/tooling hardening and governance wave

Major outcomes:
- Readability, navigation, and UX hardening work completed (`WO-0025` to `WO-0034` except policy-gated items).
- OMATrust lane materialized (`WO-0027`).
- Astro build hardening completed (`WO-0028`).
- Journey parity/decoupling and status coherence work completed (`WO-0031`, `WO-0034`).
- v0.2 publication edge cases and integrity/revocation posture hardening completed (`WO-0036`, `WO-0037`).
- Drift governance cadence and trigger criteria established (`WO-0038`).
- Onboarding policy gate set to mandatory human evidence (`WO-0035` remains blocked).

Primary evidence:
- `docs/workorders/WO-0025-documentation-human-readability-and-links.md`
- `docs/workorders/WO-0026-workbench-and-harness-redesign.md`
- `docs/workorders/WO-0027-omatrust-integration-lane-execution.md`
- `docs/workorders/WO-0028-astro-content-cache-clean-build-hardening.md`
- `docs/workorders/WO-0029-docs-nav-order-and-overview-clarity-pass.md`
- `docs/workorders/WO-0030-animated-svg-explainer-prompt-pack-and-production-pipeline.md`
- `docs/workorders/WO-0031-journey-proof-parity-and-decoupling-hardening.md`
- `docs/workorders/WO-0032-published-docs-stale-status-scan-and-fix.md`
- `docs/workorders/WO-0033-published-docs-label-first-link-normalization.md`
- `docs/workorders/WO-0034-documentation-status-coherence-and-stale-reference-reconciliation.md`
- `docs/workorders/WO-0035-human-reader-testing-policy-and-onboarding-evidence-alignment.md`
- `docs/workorders/WO-0036-v0-2-publication-and-verification-edge-case-expansion.md`
- `docs/workorders/WO-0037-integrity-profile-revocation-and-adversarial-conformance-hardening.md`
- `docs/workorders/WO-0038-corpus-drift-governance-and-follow-on-workorder-cycle.md`

## 2026-02-23: New rewrite/hardening order for onboarding language propagation

Major outcomes:
- New systemic work order opened to address onboarding language clarity and source-propagation drift risk.
- This explicitly requires docs and backend/tooling/template source-path hardening, not docs-only edits.

Primary evidence:
- `docs/workorders/WO-0039-onboarding-plain-language-rewrite-and-source-propagation-hardening.md`
- `docs/workorders/WO-INDEX.md`
- `.dev/ai/workorders/WO-INDEX.md`
- `docs/STATE-OF-THE-PROJECT.md`

## Current state snapshot (as of 2026-02-23)

Completed major wave:
- `WO-0001` through `WO-0034`, excluding policy-gated residuals in onboarding closure.
- `WO-0036`, `WO-0037`, `WO-0038` completed.

Active/non-complete gates:
- `WO-0035` is BLOCKED pending dated human-participant evidence artifact.
- `WO-0039` is NOT_STARTED and defines the onboarding rewrite + propagation hardening path.

Primary evidence:
- `docs/STATE-OF-THE-PROJECT.md`
- `docs/workorders/WO-INDEX.md`

## Reproducible replay protocol for an independent agent

## Stage 0: Environment and integrity checks

Run:
- `pwd`
- `git -C  status --short`
- `git -C  rev-parse --abbrev-ref HEAD`
- `git -C  log --reverse --date=iso --pretty=format:'%ad %h %s' | sed -n '1,40p'`

Goal:
- Confirm correct repo.
- Record current branch/worktree state.
- Capture timeline anchors before interpretation.

## Stage 1: Source-of-truth reading order

Read in order:
1. `AGENTS.md`
2. `PROJECT-RULES.md`
3. `docs/README.md`
4. `docs/STATE-OF-THE-PROJECT.md`
5. `docs/CRITICAL-PATH.md`
6. `docs/DECISIONS.md`
7. `docs/workorders/WO-INDEX.md`
8. `.dev/ai/workorders/WO-INDEX.md`
9. `.dev/ai/handoffs/2026-02-22-22-30-19Z-handoff-universalmanifest.md`
10. `docs/workorders/WO-0035-human-reader-testing-policy-and-onboarding-evidence-alignment.md`
11. `docs/workorders/WO-0039-onboarding-plain-language-rewrite-and-source-propagation-hardening.md`

## Stage 2: Rebuild milestone chronology from primary files

Run:
- `for f in docs/workorders/WO-*.md; do id=$(basename \"$f\" .md); created=$(rg -n \"^\\*\\*Created:\\*\\*\" \"$f\" | sed -E 's/^[0-9]+:\\*\\*Created:\\*\\*\\s*//'); st=$(rg -n \"^\\*\\*Status:\\*\\*\" \"$f\" | sed -E 's/^[0-9]+:\\*\\*Status:\\*\\*\\s*//'); title=$(sed -n '1s/^# //p' \"$f\"); printf \"%s|%s|%s|%s|%s\\n\" \"$id\" \"$created\" \"$st\" \"$title\" \"$f\"; done | sort -V`
- `rg -n \"^## 2026\" docs/DECISIONS.md`
- `ls -lt docs/reports | sed -n '1,120p'`

Goal:
- Produce an independently verified date-sequenced timeline.
- Identify gaps between WO status, decisions, and reports.

## Stage 3: Re-run core technical proof commands

Run:
- `cd site && npm run build:clean`
- `cd packages/universal-manifest && npm test`
- `cd packages/universal-manifest && npm run journeys`
- `cd packages/universal-manifest && npm run smoke:endpoints:dev`
- `cd packages/universal-manifest && npm run smoke:endpoints:prod`

Goal:
- Validate current code/docs claims against executable evidence.

## Stage 4: Produce independent outputs

Required outputs:
1. Independent history audit report:
   - `docs/reports/YYYY-MM-DD-independent-history-audit.md`
2. Contradictions/drift report:
   - `docs/reports/YYYY-MM-DD-independent-drift-and-contradictions.md`
3. Recommended execution order for remaining work:
   - `docs/reports/YYYY-MM-DD-independent-next-steps-plan.md`

Output quality rules:
- Every milestone claim must cite at least one absolute-path source.
- Separate verified facts from inferred conclusions.
- Mark any unresolved ambiguity explicitly.

## Primary source inventory for unbiased review

Core state and decision docs:
- `docs/STATE-OF-THE-PROJECT.md`
- `docs/CRITICAL-PATH.md`
- `docs/DECISIONS.md`

Work-order control plane:
- `docs/workorders/WO-INDEX.md`
- `.dev/ai/workorders/WO-INDEX.md`
- `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`
- `docs/workorders/WO-0035-human-reader-testing-policy-and-onboarding-evidence-alignment.md`
- `docs/workorders/WO-0039-onboarding-plain-language-rewrite-and-source-propagation-hardening.md`

Historical anchors:
- `docs/WORKLOG-2026-02-11.md`
- `docs/WORKLOG-2026-02-12.md`
- `docs/reports/2026-02-18-live-status-and-next-critical-path.md`
- `.dev/ai/handoffs/2026-02-22-22-30-19Z-handoff-universalmanifest.md`
