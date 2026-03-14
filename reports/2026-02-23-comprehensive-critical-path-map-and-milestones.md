# Universal Manifest - Comprehensive Critical Path Map and Milestones

Date: 2026-02-23  
Project root: ``  
Primary source docs:
- `docs/CRITICAL-PATH.md`
- `docs/workorders/WO-INDEX.md`
- `docs/STATE-OF-THE-PROJECT.md`

## 1) Executive map

This project has completed the core delivery arc (spec, conformance, publish, resolver, proof lanes, and governance hardening). The remaining closure path is onboarding-gate related.

Current critical-path gates:
- `WO-0039` is `IN_PROGRESS` (Phase 5 human validation still open).
- `WO-0035` is `BLOCKED` pending dated human-participant onboarding evidence.
- `WO-0015` is `BLOCKED` pending `WO-0035` and `WO-0039`.

Everything else on the main delivery spine is complete enough for ongoing operations and drift governance.

## 2) Phase-by-phase milestone map

## Phase 0 - Define done (gates and evidence)

Goal:
- Establish release-readiness gates and objective evidence standards.

Milestones achieved:
- Done-done framework established and in active use.

Primary artifacts:
- `docs/DONE-DONE-DEFINITION.md`
- `docs/DONE-DONE-CHECKLIST.md`
- `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
- `docs/workorders/WO-0008-spec-status-scope-and-foundations-audit.md` (`COMPLETED`)

Status: COMPLETE

## Phase 1 - Make v0.1 adoptable (minimal contract)

Goal:
- External adopters can parse, validate, and safely consume manifests.

Milestones achieved:
- v0.1 schema/context and conformance baseline published.
- valid/invalid fixtures and validator workflow in place.
- integration support moved from project-specific framing to broader runtime framing.

Key WOs:
- `WO-0002`, `WO-0004`, `WO-0005`, `WO-0010`, `WO-0011` (all complete)

Status: COMPLETE

## Phase 2 - Harden interoperability (v0.2 signature profile)

Goal:
- Deterministic sign/verify behavior across independent implementations.

Milestones achieved:
- v0.2 profile and artifact set shipped.
- edge-case and adversarial fixture expansion completed.
- signature verification investigation resolved as working.

Key WOs:
- `docs/workorders/WO-0036-v0-2-publication-and-verification-edge-case-expansion.md` (`COMPLETED`)
- `docs/workorders/WO-0037-integrity-profile-revocation-and-adversarial-conformance-hardening.md` (`COMPLETED`)
- `docs/workorders/WO-0040-v0-2-signature-verification-fix.md` (`COMPLETED`)

Status: COMPLETE

## Phase 3 - Publish like a real standard

Goal:
- Stable docs/spec hosting with clear adopter navigation and immutable versioning posture.

Milestones achieved:
- domain split and publishing policies established.
- docs site professionalism and nav/readability passes completed.
- stale status/link hygiene passes completed.

Key WOs:
- `WO-0003`, `WO-0006`, `WO-0007`, `WO-0009`, `WO-0025`, `WO-0028`, `WO-0029`, `WO-0032`, `WO-0033`, `WO-0041` (completed)

Status: COMPLETE

## Phase 4 - Make UMIDs resolvable

Goal:
- Deterministic resolver contract and reliable route behavior.

Milestones achieved:
- resolver skeleton, contract, and endpoint smoke established.
- J03 reliability and route hardening completed.
- production drift prevention automation implemented.

Key WOs:
- `WO-0007`, `WO-0013`, `WO-0019`, `WO-0023` (completed)

Status: COMPLETE

## Phase 5 - Prove across surfaces

Goal:
- Demonstrate multi-lane applicability through executable journey proof.

Milestones achieved:
- journey framework completed and expanded.
- RP1, smart-glasses, metaverse, OMATrust, PoP/social/Chia lanes materialized.
- journey parity and decoupling hardening completed.

Key WOs:
- `WO-0012`, `WO-0020`, `WO-0021`, `WO-0022`, `WO-0024`, `WO-0027`, `WO-0031` (completed)

Status: COMPLETE

## Phase 6 - Full-corpus synthesis before expansion

Goal:
- Keep IA/journeys/workbench evolution grounded in full-source ingestion and conflict handling.

Milestones achieved:
- ledger and synthesis execution completed.
- recurring drift governance criteria operationalized.

Key WOs:
- `WO-0016`, `WO-0017`, `WO-0038` (completed)

Status: COMPLETE

## Phase 7 - Onboarding clarity and interactive adopter tooling

Goal:
- First-contact readers understand UM quickly and can execute adoption path confidently.

Milestones achieved:
- interactive workbench shipped and redesigned.
- onboarding rewrite system hardening mostly complete.

Open milestones:
- human validation artifacts required for closure-grade onboarding claims.

Key WOs:
- `docs/workorders/WO-0014-interactive-manifest-workbench.md` (`COMPLETED`)
- `docs/workorders/WO-0039-onboarding-plain-language-rewrite-and-source-propagation-hardening.md` (`IN_PROGRESS`; Phase 5 open)
- `docs/workorders/WO-0035-human-reader-testing-policy-and-onboarding-evidence-alignment.md` (`BLOCKED`; waiting human evidence)
- `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md` (`BLOCKED`; depends on WO-0035 + WO-0039)

Status: IN PROGRESS (critical open gate)

## Phase 8 - Lineage-grounded expansion lanes

Goal:
- Preserve lineage while scaling cross-domain integrations.

Milestones achieved:
- lineage codified.
- metaverse, RP1, smart-glasses lanes documented and proven.

Key WOs:
- `WO-0018`, `WO-0020`, `WO-0021`, `WO-0022` (completed)

Status: COMPLETE

## Phase 9 - Drift governance and closure-regression checks

Goal:
- Prevent status drift and claim inflation over time.

Milestones achieved:
- recurring governance cadence and trigger thresholds documented.
- status-document reconciliation pass completed.

Key WOs:
- `docs/workorders/WO-0038-corpus-drift-governance-and-follow-on-workorder-cycle.md` (`COMPLETED`)
- `docs/workorders/WO-0041-status-document-drift-reconciliation.md` (`COMPLETED`)

Status: ACTIVE OPERATIONAL LOOP

## 3) Dependency edges (critical path graph)

Primary dependency edges:
- `WO-0039` Phase 5 (human validation evidence) -> required to support onboarding closure claims.
- `WO-0035` (policy gate) -> requires dated human-participant artifact.
- `WO-0015` -> cannot close until both `WO-0035` and `WO-0039` are fully closed.

Implication:
- The project-level closure path is bottlenecked by human evidence capture and onboarding-gate reconciliation, not by missing core technical implementation.

## 4) Current milestone scoreboard

Completed milestones:
- Core spec and conformance baseline
- Signature/interoperability hardening
- Production docs and resolver deployment posture
- Multi-lane integration proof and journey parity
- Drift-governance framework

Open milestones:
- Human-participant onboarding evidence
- Final onboarding closure synchronization (`WO-0039` -> `WO-0035` -> `WO-0015`)

## 5) Critical path from today to closure

Step 1:
- Execute human reader validation run using the existing protocol/checklist and publish dated results artifact.
- Primary files:
  - `docs/reports/2026-02-19-first-time-reader-testing-protocol.md`
  - `docs/reports/2026-02-22-first-time-reader-human-gate-checklist.md`
  - `docs/reports/2026-02-23-first-time-reader-test-results-human.md` (template)

Step 2:
- Close `WO-0039` Phase 5 acceptance criteria with the human evidence linked.

Step 3:
- Close `WO-0035` blocker criterion (mandatory human evidence satisfied).

Step 4:
- Close `WO-0015` final acceptance criterion and set status `COMPLETED`.

Step 5:
- Run Phase 9 verification command set and publish a dated closure-grade status reconciliation report.

## 6) Verification checkpoint commands

- `cd site && npm run build:clean`
- `cd packages/universal-manifest && npm test`
- `cd packages/universal-manifest && npm run journeys`
- `cd packages/universal-manifest && npm run smoke:endpoints:prod`
- `cd packages/universal-manifest && npm run check:terminology`
- `/opt/homebrew/bin/bash /Users/grig/.agents/scripts/validate-k2b-gates.sh  --artifact-root .dev/ai --strict`

## 7) Notes on status consistency

Observed drift risk:
- Some status summaries lag WO-file reality over time.

Working rule:
- For milestone calls, treat individual WO files plus latest verification outputs as authoritative.
- Reconcile `docs/STATE-OF-THE-PROJECT.md`, `docs/workorders/WO-INDEX.md`, and `.dev/ai/workorders/WO-INDEX.md` after any status transition.
