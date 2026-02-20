# Universal Manifest Master Forward Worklist

Date: 2026-02-20
Project root: `/Users/grig/work/repo/universalmanifest`
Purpose: single source list of all remaining known work from this checkpoint forward.
Scope rule: includes product, docs, proof, deployment, K2B, and governance work still required to reach completion claims.

## Execution update (2026-02-20)

Completed in this cycle:

1. `J03` journey reliability fixed; `npm run journeys` now passes `5/5`.
2. Latest `universalmanifest.net` Pages artifact deployed; workbench routes are live.
3. Resolver routing expanded to include `www.myum.net/*`; health checks return `200`.
4. Production endpoint smoke re-run and passing.
5. Follow-on work order created and closed:
   - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0019-resolver-j03-reliability-and-routing-hardening.md`

Highest-priority remaining blocker:

1. Complete external reader-testing evidence and close `WO-0015`.

## 0) Checkpoint stabilization (do first)

1. Reconcile current working tree noise before next implementation cycle.
2. Preserve and isolate runtime-generated `.wrangler` state changes from source-controlled work. (completed 2026-02-20)
3. Review unexpected `AGENTS.md`/local environment file diffs and decide keep/revert policy explicitly.
4. Commit and push the current codification batch (MUM lineage + metaverse/RP1/smart-glasses docs) as a clean checkpoint.
5. Update handoff/status artifacts after checkpoint commit so next agents start from an unambiguous baseline.

## 1) Immediate delivery blockers (must clear)

1. Close `WO-0015` by executing external reader testing and adding real participant evidence.
2. Fix journey `J03` (`myum resolver E2E`) so `npm run journeys` passes 5/5. (completed 2026-02-20)
3. Deploy latest site build to Cloudflare Pages so workbench routes return 200. (completed 2026-02-20)
4. Verify `/getting-started/workbench/` is live. (completed 2026-02-20)
5. Verify `/workbench/index.html` is live. (completed 2026-02-20; canonical redirect `308` -> `/workbench/` with `200` target)
6. Re-run prod smoke after deploy and attach evidence artifact. (completed 2026-02-20)

## 2) Open work order closure requirements

1. `WO-0015` completion actions:
2. Run protocol at `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-19-first-time-reader-testing-protocol.md`.
3. Record results using `/Users/grig/work/repo/universalmanifest/docs/reports/FIRST-TIME-READER-RESULTS-TEMPLATE.md`.
4. Check final acceptance criterion and set status `COMPLETED` in `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`.
5. Create follow-on WO for resolver `J03` defect if not already tracked as a dedicated WO.

## 3) K2B system integrity and consistency tasks

1. Keep strict validator green on every major transition:
2. `/opt/homebrew/bin/bash /Users/grig/.agents/scripts/validate-k2b-gates.sh /Users/grig/work/repo/universalmanifest --artifact-root /Users/grig/work/repo/universalmanifest/.dev/ai --strict`
3. Refresh `/Users/grig/work/repo/universalmanifest/.dev/ai/ingestion/GATES.md` so project-local wording is consistent with strict gate evidence.
4. Run a new K2B provenance audit after integrating new CEO lanes and deployment fixes.
5. Update source-selection/integration records whenever new external sources are added.
6. Ensure every newly selected source has origin mapping and downstream artifact linkage.

## 4) RP1 ingestion and evidence work (currently codified but not ingested)

1. Identify authoritative RP1 source documents and add them to K2B candidate inventory.
2. Run Stage -1/0 ingestion triage for RP1 sources (selected/deferred/excluded with rationale).
3. Localize selected RP1 sources into knowledge corpus imports with provenance mapping.
4. Reconcile RP1 conflicts with existing UM architecture and document decisions.
5. Materialize RP1 synthesis into concrete artifacts:
6. Integration doc updates.
7. At least one fixture addition.
8. At least one journey/proof scenario.
9. Open and execute follow-on WO(s) for RP1 implementation if synthesis output exceeds direct edit scope.

## 5) Smart-glasses AR lane implementation evidence

1. Convert current non-normative policy guidance into testable fixtures.
2. Add consent-focused fixture cases for recording visibility and auto-profile disclosure.
3. Add proof journey(s) that exercise context-based consent enforcement.
4. Ensure unknown-field tolerance remains intact with AR-specific extensions.
5. Record outcome in conformance/proof docs without leaking non-normative keys into mandatory core contract.

## 6) Metaverse lane implementation evidence

1. Expand from documented lane to executable proof artifacts.
2. Add metaverse-focused fixture(s) beyond existing exemplar template.
3. Add journey coverage for cross-world identity/profile/asset pointer projection.
4. Validate that metaverse additions remain optional overlays and do not scope-anchor the core spec.

## 7) Conformance and security hardening (v0.1.x + v0.2)

1. Add deeper TTL edge and misuse/adversarial fixture coverage.
2. Expand v0.2 verification edge-case fixtures (signature and failure matrix).
3. Publish v0.2 artifacts at stable URLs after lock criteria are met.
4. Finalize v0.2 migration guidance and resolver semantics for edge cases.
5. Decide and document policy for additional integrity profiles beyond baseline.
6. Decide and document revocation cursor/event direction.

## 8) Resolver and interoperability hardening

1. Resolve seeded UMID lookup instability causing `J03` failures.
2. Add deterministic resolver test setup/teardown for reliable local E2E.
3. Confirm resolver contract behavior for cache headers/errors/privacy posture in docs and tests.
4. Ensure `myum.net` production behavior matches documented contract.
5. Verify domain variants/routing behavior (including `www.myum.net`) are explicitly configured and tested.

## 9) Deployment and production alignment

1. Keep repo `main` and production deployments in sync with an auditable deploy cadence.
2. Update/confirm Cloudflare Pages deployment path for latest site artifacts.
3. Add post-deploy verification step that checks critical routes and contract endpoints.
4. Archive deployment proof logs/screenshots in `.dev/ai/reports/` per release cycle.

## 10) Docs and onboarding completion quality

1. Close external-reader comprehension loop (`WO-0015`).
2. Ensure first-contact docs explicitly connect overview -> quick start -> workbench -> conformance -> proof.
3. Keep integration pages synchronized with source-of-truth decisions.
4. Update state and critical-path docs whenever milestones close.

## 11) Governance and release readiness

1. Record all normative-impact decisions in `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`.
2. Prepare done-done evidence pack when claiming release readiness.
3. Complete release checklist and production smoke evidence before any completion claim.
4. Keep `STATE-OF-THE-PROJECT` aligned with actual runtime truth (tests, deployment, open WOs).

## 12) Work-order and backlog hygiene

1. Convert all loose ends into explicit WOs when >30 minutes or multi-step.
2. Create new WOs for untracked but required work:
3. Resolver `J03` fix and reliability. (completed as `WO-0019`)
4. RP1 source ingestion and synthesis materialization.
5. Smart-glasses fixture/journey implementation.
6. Metaverse fixture/journey implementation hardening.
7. Production deployment drift prevention automation.
8. Keep WO index current and statuses accurate on every closure.

## 13) Current completion gate to claim “all planned work complete”

1. `WO-0015` is `COMPLETED` with external evidence committed.
2. Journey suite passes without failures (`5/5`).
3. Workbench docs/tool routes are live in production (`200`).
4. RP1 ingestion is either completed with traceable artifacts or explicitly deferred with dated rationale and approved follow-on WO.
5. Strict K2B validator remains green after all above updates.
6. State/decisions/work-order docs all reflect the same truth snapshot.

## 14) Canonical evidence files to keep updating during execution

1. `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
2. `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
3. `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`
4. `/Users/grig/work/repo/universalmanifest/.dev/ai/ingestion/GATES.md`
5. `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/2026-02-20-k2b-integration-completeness-report.md`
6. `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/`
