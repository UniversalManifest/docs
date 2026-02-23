# Independent Next-Steps Plan -- Universal Manifest Project

**Date:** 2026-02-23
**Deliverable:** 3 of 3 (Independent, Unbiased History Audit)
**Scope:** Prioritized execution plan for remaining work, based on audit findings

---

## 1. Executive Summary

The Universal Manifest project has completed the majority of its planned work orders (33 of 39 marked COMPLETED), has a functioning production deployment at universalmanifest.net and myum.net, and has a solid v0.1 validation suite. However, the audit has identified five concrete gaps that prevent calling the project "done": (1) the v0.2 signature verification feature fails its only valid-manifest test, making v0.2 completion claims false; (2) onboarding documentation is hostile to newcomers due to pervasive undefined jargon; (3) a mandatory human-participant reader test has never been conducted, blocking two work orders under the project's own Policy A gate; (4) status documents contain stale completion claims that overstate actual delivery; and (5) three journey tests fail intermittently, suggesting fragile integration scenarios. This plan orders the remaining work so that each task unblocks subsequent tasks, and defines binary pass/fail closure criteria.

---

## 2. Open Gates and Blockers

| Gate ID | What it blocks | What is needed to unblock | Evidence path |
|---------|---------------|--------------------------|---------------|
| **WO-0035** (BLOCKED) | Final closure-grade completion claims for onboarding readiness; also blocks WO-0015 closure | At least one dated human-participant reader test report committed to `docs/reports/` | `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0035-human-reader-testing-policy-and-onboarding-evidence-alignment.md` (line 63: unchecked criterion; line 72: blocker statement) |
| **WO-0015** (BLOCKED) | Onboarding completion claim | Depends on WO-0035 (human evidence) AND WO-0039 (language rewrite); acceptance criterion 4 unchecked | `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md` (line 43: unchecked criterion) |
| **WO-0039** (NOT_STARTED) | Onboarding language clarity; prerequisite for meaningful human-reader testing | Full execution of 5 phases: inventory, rewrite, propagation fixes, guardrail automation, human validation | `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0039-onboarding-plain-language-rewrite-and-source-propagation-hardening.md` |
| **v0.2 signature verification** (no WO) | Validity of any claim that "v0.2 is complete and tested" | Debug and fix Ed25519 signature verification for `minimal-signed-manifest.jsonld` | `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/step2-technical-validation.md` (lines 177-178, 390-394) |
| **Status document drift** (no WO) | Trustworthiness of all project status claims | Reconcile `STATE-OF-THE-PROJECT.md`, `WO-INDEX.md`, `.dev/ai/workorders/WO-INDEX.md`, and `PROJECT-RULES.md` to reflect verified reality | `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/step-source-documents-extraction.md` (lines 411-466: contradiction analysis) |

---

## 3. Verified Remaining Work

### 3.1 -- P0: Fix v0.2 Signature Verification

- **Priority:** P0 (blocks everything that depends on v0.2 claims)
- **Task:** Debug and fix the Ed25519 signature verification failure in `packages/universal-manifest/` so that `examples/v0.2/minimal-signed-manifest.jsonld` passes validation.
- **Rationale:** The technical validation (Step 2) confirmed that `npm test` exits with code 1 because the only valid v0.2 signed manifest fails signature verification. This means all claims of "v0.2 signature support working" are currently false. The signature value, public key, or canonicalization logic may be misaligned. Evidence: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/step2-technical-validation.md` lines 177-178, 390-394.
- **Dependencies:** None.
- **Estimated scope:** Small (hours). The fixture file is at `/Users/grig/work/repo/universalmanifest/examples/v0.2/minimal-signed-manifest.jsonld`, the validation script at `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/validate-examples.mjs`, and the core logic at `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/src/index.ts`.

### 3.2 -- P0: Reconcile Status Document Drift

- **Priority:** P0 (blocks trust in any project status claim)
- **Task:** Audit and correct every status assertion in the following files so they match verified reality:
  - `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/workorders/WO-INDEX.md`
  - `/Users/grig/work/repo/universalmanifest/PROJECT-RULES.md`
- **Rationale:** The handoff file (2026-02-22T22:30:19Z) explicitly identified status inflation: "State file says 'All 30 work orders completed' while WO-0031 is NOT_STARTED and WO-0033 is IN_PROGRESS." Subsequent work may have resolved WO-0031 and WO-0033 (both now show COMPLETED with evidence), but the status documents also fail to reflect: WO-0015 BLOCKED, WO-0035 BLOCKED, WO-0039 NOT_STARTED, and the v0.2 signature failure. Evidence: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/step-source-documents-extraction.md` lines 411-466 and `/Users/grig/work/repo/universalmanifest/.dev/ai/handoffs/2026-02-22-22-30-19Z-handoff-universalmanifest.md` lines 35, 86.
- **Dependencies:** Should happen after 3.1 so v0.2 status can be accurately recorded.
- **Estimated scope:** Small (hours). This is a documentation reconciliation task.

### 3.3 -- P1: Investigate and Fix Journey Test Failures

- **Priority:** P1 (blocks closure of integration completeness claims)
- **Task:** Investigate why 3 of 11 journey tests failed during the audit's technical validation run, determine whether failures are transient (environment-specific) or persistent (code defects), and fix any persistent failures.
- **Rationale:** Step 2 technical validation recorded "8 pass, 3 fail" when running `npm run journeys`. However, a prior journey report from the same date (`2026-02-23T01-05-33-390Z-journey-report.json`) shows 11 pass, 0 fail. This suggests the failures may be transient or environment-dependent. The specific failing journeys were not identified in the Step 2 output. The audit report generated at `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/2026-02-23T01-45-51-016Z-journey-report.json` should contain the details. Evidence: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/step2-technical-validation.md` lines 264-287.
- **Dependencies:** None (can run in parallel with 3.1 and 3.2).
- **Estimated scope:** Small-to-Medium (hours to 1 day). Requires running journeys, inspecting the failure report, and determining root cause.

### 3.4 -- P1: Execute WO-0039 (Onboarding Plain-Language Rewrite)

- **Priority:** P1 (blocks closure of onboarding quality claims and is prerequisite for human-reader testing)
- **Task:** Execute all 5 phases of WO-0039:
  1. Build source-map inventory of all jargon injection points.
  2. Rewrite first-read onboarding pages (`universal-manifest-overview.md`, `index.md`, `concepts.md`, `quick-start.md`) for plain-language clarity.
  3. Propagate fixes to all docs/backend/tooling surfaces that embed stale wording.
  4. Implement automated terminology/readability guard script.
  5. Validate with human-reader check and publish evidence.
- **Rationale:** The Step 3 onboarding clarity review scored the documentation 2.5/5 for newcomer comprehension. Critical findings: "integration pair" undefined in the problem statement (overview.md line 34), "portable state capsule" undefined in the opening definition, concepts.md scored 1/5 and was assessed as "nearly useless for a newcomer." The audit identified 21 instances of undefined jargon across the 4 onboarding files. Evidence: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/step3-onboarding-clarity-review.md` lines 14-21 (executive summary), 376-408 (prioritized issues list), 426-446 (reader journey simulation).
- **Dependencies:** None for phases 1-4. Phase 5 overlaps with WO-0035 (human testing gate).
- **Estimated scope:** Medium (1-2 days). Four files need substantive rewrite, plus source-map analysis and guard script implementation.

### 3.5 -- P1: Resolve Astro Duplicate-ID Build Warnings

- **Priority:** P1 (quality issue that indicates content organization problems)
- **Task:** Eliminate the duplicate-ID warnings emitted during Astro site build. Ten content files produce duplicate-ID warnings despite WO-0028 claiming to have resolved this.
- **Rationale:** The Step 2 technical validation confirmed 10 duplicate-ID warnings during `npm run build:clean` (lines 54-63 of the build output). WO-0028 was marked COMPLETED with the claim of "warning-free clean build," but the audit's independent build run shows warnings persist. This is either a regression or an incomplete fix. Files affected: `conformance/v0.1.md`, `conformance/v0.2.md`, `getting-started/stub-manifests.md`, `getting-started/universal-manifest-overview.md`, `integrations/reference-runtime.md`, `integrations/chia-vc.md`, `integrations/oma-trust.md`, `integrations/proof-of-personhood.md`, `integrations/social.md`, `spec/v0.1.md`. Evidence: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/step2-technical-validation.md` lines 27-30, 54-63.
- **Dependencies:** None.
- **Estimated scope:** Small (hours). Likely a content configuration issue (duplicate entries in Astro data store or conflicting content collection definitions).

### 3.6 -- P1: Conduct Human-Participant Reader Test (WO-0035 / WO-0015 Closure)

- **Priority:** P1 (blocks project closure under Policy A)
- **Task:** Recruit at least one person who has NOT worked on this repository to follow the first-time reader testing protocol. Record their experience in a dated evidence artifact at `/Users/grig/work/repo/universalmanifest/docs/reports/YYYY-MM-DD-first-time-reader-test-results-human.md`. Update WO-0035 acceptance criterion 4 and WO-0015 acceptance criterion 4.
- **Rationale:** Policy A (decided 2026-02-22, recorded in `docs/DECISIONS.md` line 393) mandates human-participant evidence for closure-grade completion. No such evidence exists. The testing protocol is already defined at `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-19-first-time-reader-testing-protocol.md` and a human gate checklist exists at `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-22-first-time-reader-human-gate-checklist.md`. Evidence: `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0035-human-reader-testing-policy-and-onboarding-evidence-alignment.md` lines 63, 72.
- **Dependencies:** Must happen AFTER task 3.4 (WO-0039 onboarding rewrite). Testing the current jargon-heavy documentation would produce predictable negative results and waste the participant's time.
- **Estimated scope:** Small (hours for the test session itself, but requires human coordination which may take longer calendar time).

### 3.7 -- P2: Remove Insider Framing from Public Documentation

- **Priority:** P2 (quality improvement, partially addressed by WO-0039)
- **Task:** Remove or reframe all insider organizational language from public-facing documentation:
  - "CEO-directed integration lanes" (overview.md line 18, integrations/smart-glasses-ar.md line 8, integrations/rp1-spatial-fabric.md line 8)
  - "convergence profile" (overview.md line 12)
  - "MUM" / "Metaverse Universal Manifest" lineage references in onboarding context
  - Undefined "reference implementation" references in stub-manifests.md (line 22) and critical-path.md (line 78)
- **Rationale:** Step 3 found that insider project framing leaks into public documentation. "CEO-directed integration lanes" is organizational jargon irrelevant to external technical readers. "reference implementation" is an undefined term in user-facing docs. Evidence: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/step3-onboarding-clarity-review.md` lines 264-296 (insider framing analysis), 344-356 (propagation paths).
- **Dependencies:** Overlaps with task 3.4 (WO-0039). Can be executed as part of the same pass.
- **Estimated scope:** Small (hours). Targeted text edits across known files.

### 3.8 -- P3: Wrangler Version Update

- **Priority:** P3 (nice to have)
- **Task:** Update wrangler to v4.67.0+ to eliminate compatibility-date fallback warning and out-of-date version warning during resolver E2E tests (J04).
- **Rationale:** The journey report shows wrangler 3.114.17 with a warning about compatibility date "2026-02-17" falling back to "2025-07-18" and a deprecation warning. This is cosmetic but creates noise in test output and may eventually cause functional issues. Evidence: `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/2026-02-23T01-05-33-390Z-journey-report.json` (J04 stderr output).
- **Dependencies:** None.
- **Estimated scope:** Small (hours).

---

## 4. Recommended Execution Sequence

```
1. [Fix v0.2 signature verification (3.1)]
   depends on: nothing
   unblocks: accurate status reconciliation (3.2), test suite green (closure criteria)

2. [Investigate and fix journey test failures (3.3)]
   depends on: nothing (parallel with #1)
   unblocks: journey completeness claims, test suite green

3. [Resolve Astro duplicate-ID build warnings (3.5)]
   depends on: nothing (parallel with #1 and #2)
   unblocks: clean build (closure criteria), accurate WO-0028 status

4. [Reconcile status document drift (3.2)]
   depends on: #1, #2, #3 (need verified results to write accurate status)
   unblocks: trustworthy project status, accurate handoff for future agents

5. [Execute WO-0039 onboarding rewrite (3.4)]
   depends on: nothing (can start parallel with #1-#3, but #4 should update
               status docs before onboarding docs reference them)
   unblocks: meaningful human-reader testing (3.6), insider framing removal (3.7)

6. [Remove insider framing from public docs (3.7)]
   depends on: #5 (execute as part of the same editing pass)
   unblocks: clean onboarding documentation

7. [Conduct human-participant reader test (3.6)]
   depends on: #5 and #6 (must test the REWRITTEN docs, not the current jargon-heavy ones)
   unblocks: WO-0035 closure, WO-0015 closure, project closure under Policy A

8. [Update wrangler version (3.8)]
   depends on: nothing (can happen anytime)
   unblocks: cleaner test output
```

**Parallelism opportunities:**
- Tasks 1, 2, 3 can all execute in parallel (no dependencies between them).
- Task 5 can begin while 1-3 are in progress, though task 4 should ideally complete first.
- Task 8 can execute at any time.

---

## 5. Risks and Recommendations

### Risk 1: Status inflation recurrence

**What could go wrong:** Future agents mark work orders as COMPLETED based on partial execution or without verifying acceptance criteria. This has already happened -- the handoff file explicitly flagged WO-0031 and WO-0033 as NOT_STARTED/IN_PROGRESS while status documents claimed COMPLETED.

**Recommendation:** Add a validation step to the work order completion process: before marking any WO as COMPLETED, run all validation commands listed in the WO and record their exit codes in the completion evidence section. Do not mark COMPLETED if any validation command fails. Evidence: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/step-source-documents-extraction.md` lines 451-457.

### Risk 2: Onboarding jargon re-introduction

**What could go wrong:** After the WO-0039 rewrite, future edits re-introduce undefined jargon into first-read surfaces. The audit found jargon is hand-authored (not script-generated), so there is no automated guard.

**Recommendation:** Implement the automated terminology guard script specified in WO-0039 Phase 4. Define a denylist of terms (e.g., "integration pair", "convergence profile", "CEO-directed") that must not appear in files under `site/src/content/docs/getting-started/` or `site/src/content/docs/index.md` without an inline definition. Wire this to the build process. Evidence: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/step3-onboarding-clarity-review.md` lines 360-369, 488-493.

### Risk 3: v0.2 signature feature shipped without passing tests

**What could go wrong:** The project claims v0.2 support while the only valid signed manifest fails verification. External adopters attempting to use v0.2 signatures will encounter failures.

**Recommendation:** Until v0.2 signature verification passes tests, explicitly mark v0.2 as "experimental" or "in progress" in all public-facing documentation. Do not claim v0.2 is "complete" or "tested." Evidence: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/step2-technical-validation.md` lines 390-394, 431.

### Risk 4: WO-0028 regression (duplicate-ID warnings)

**What could go wrong:** WO-0028 was marked COMPLETED claiming "warning-free clean build," but the audit's independent build run produced 10 duplicate-ID warnings. This means either the fix regressed or the completion evidence was captured under different conditions than a fresh build.

**Recommendation:** Re-verify WO-0028 completion by running `cd /Users/grig/work/repo/universalmanifest/site && rm -rf .astro node_modules/.vite && npm run build 2>&1 | grep -i "duplicate"`. If warnings appear, reopen WO-0028. Evidence: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/step2-technical-validation.md` lines 27-30, 54-63.

### Risk 5: Human-reader testing is a single point of failure for project closure

**What could go wrong:** Policy A requires human-participant evidence. If no suitable participant can be recruited, the project can never reach "done" status under its own rules.

**Recommendation:** Define a minimum-viable test: one participant, one session, answering three specific questions after reading only the overview and quick-start pages. The protocol already exists at `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-19-first-time-reader-testing-protocol.md`. Ensure the test is lightweight enough to actually execute.

### Risk 6: Journey test flakiness masks real failures

**What could go wrong:** The audit found inconsistent journey results (11/11 pass in one run, 8/11 pass in another). If failures are transient (e.g., network-dependent, timing-dependent), they may mask real integration gaps that surface only in production.

**Recommendation:** After investigating the 3 failing journeys (task 3.3), add determinism to the test runner: pin environment variables, add retry logic for network-dependent tests, or mark genuinely optional tests (like J05 reference implementation smoke) explicitly so they do not count toward the pass/fail total.

---

## 6. Closure Criteria

Each criterion below is binary (pass/fail) and includes a verification method.

### 6.1 -- All tests pass

**Verification command:**
```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test
```
**Pass condition:** Exit code 0. Summary line shows "0 failed."

### 6.2 -- All journey tests pass

**Verification command:**
```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys
```
**Pass condition:** Exit code 0. Output shows "0 fail."

### 6.3 -- Site builds without warnings

**Verification command:**
```bash
cd /Users/grig/work/repo/universalmanifest/site && rm -rf .astro && npm run build 2>&1 | grep -ci "warn"
```
**Pass condition:** Output is `0` (no warning lines).

### 6.4 -- Production endpoints operational

**Verification command:**
```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run smoke:endpoints:prod
```
**Pass condition:** Exit code 0. Output shows "PASS."

### 6.5 -- No undefined jargon in first-read surfaces

**Verification command:**
```bash
rg -n -i "integration pair|convergence profile|CEO-directed|brittle mappings" /Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/ /Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md
```
**Pass condition:** No matches found (exit code 1 from ripgrep).

### 6.6 -- No insider framing in onboarding pages

**Verification command:**
```bash
rg -n "CEO-directed integration lanes" /Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/ /Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md
```
**Pass condition:** No matches found.

### 6.7 -- Human-participant reader test evidence exists

**Verification command:**
```bash
ls /Users/grig/work/repo/universalmanifest/docs/reports/*-first-time-reader-test-results-human.md
```
**Pass condition:** At least one file matches (exit code 0).

### 6.8 -- WO-0015 and WO-0035 acceptance criteria fully checked

**Verification command:**
```bash
rg "^\- \[ \]" /Users/grig/work/repo/universalmanifest/docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md /Users/grig/work/repo/universalmanifest/docs/workorders/WO-0035-human-reader-testing-policy-and-onboarding-evidence-alignment.md
```
**Pass condition:** No matches found (all checkboxes are `[x]`, not `[ ]`).

### 6.9 -- WO-0039 acceptance criteria fully checked

**Verification command:**
```bash
rg "^\- \[ \]" /Users/grig/work/repo/universalmanifest/docs/workorders/WO-0039-onboarding-plain-language-rewrite-and-source-propagation-hardening.md
```
**Pass condition:** No matches found.

### 6.10 -- Status documents are internally consistent

**Verification command:**
```bash
# All three status sources must agree on WO-0015, WO-0035, WO-0039 status
rg -n "WO-0015|WO-0035|WO-0039" /Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md /Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md /Users/grig/work/repo/universalmanifest/.dev/ai/workorders/WO-INDEX.md
```
**Pass condition:** Manual inspection confirms all three files report the same status for each work order. No file claims COMPLETED for a WO that another file shows as BLOCKED or NOT_STARTED.

### 6.11 -- No open BLOCKED or NOT_STARTED work orders

**Verification command:**
```bash
rg -n "^\*\*Status:\*\* (BLOCKED|NOT_STARTED)" /Users/grig/work/repo/universalmanifest/docs/workorders/WO-*.md
```
**Pass condition:** No matches found (all work orders are either COMPLETED or Done).

### 6.12 -- Automated terminology guard is operational

**Verification command:**
```bash
# The specific command name will be defined in WO-0039 Phase 4.
# Expected pattern: a script in packages/universal-manifest/scripts/ or site/scripts/
ls /Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/*jargon* /Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/*terminology* /Users/grig/work/repo/universalmanifest/site/scripts/*jargon* /Users/grig/work/repo/universalmanifest/site/scripts/*terminology* 2>/dev/null
```
**Pass condition:** At least one script file exists and is executable. Running it returns exit code 0 on current content.

---

**End of Independent Next-Steps Plan**
