# Phase 9 Drift-Recovery Playbook

**Purpose:** Procedural remediation for failures of the Phase 9 drift-governance mandatory command set. Converts the one-off restoration pattern exercised in WO-0206 into a repeatable maintainer playbook.

**Scope:** Applies whenever the Phase 9 gate (`.github/workflows/phase-9-gate.yml`) or the manual mandatory command set (documented in `docs/CRITICAL-PATH.md` Phase 9 section) fails.

**Companion documents:**

- `docs/CRITICAL-PATH.md` -- Phase 9 cadence, mandatory command set, and follow-on WO thresholds.
- `.github/workflows/phase-9-gate.yml` -- automated gate that runs the non-K2B portion of the mandatory command set.
- `docs/workorders/WO-0206-k2b-drift-governance-artifact-contract-restoration.md` -- reference case study.
- `docs/workorders/WO-0208-phase-9-drift-governance-automation-hardening.md` -- the WO that created this playbook.

---

## 1. Triage -- confirm the failure is real

Before any remediation, reproduce the failure locally against a clean checkout on `main`.

```bash
cd /path/to/universalmanifest
git fetch origin main
git checkout main
git pull --ff-only

# Run the full mandatory command set (manual K2B step first):
bash ~/.agents/scripts/validate-k2b-gates.sh "$PWD" --artifact-root .dev/ai --strict
cd packages/universal-manifest && npm ci && npm test && npm run journeys && cd -
cd site && npm ci && npx tsx scripts/test-validator-parity.mjs && cd -
rg -n '/harness/|/proof/|/getting-started/|/spec/|/conformance/|/workbench/|/integrations/' \
  site/src/content/docs --glob '*.md' | rg -v '\]\([^)]+'
curl -I -s https://universalmanifest.net/
curl -I -s https://universalmanifest.net/getting-started/workbench/
curl -I -s https://universalmanifest.net/proof/harness/
```

If any command fails locally, proceed to the matching section below. If all pass locally but CI reports a failure, re-run the CI job and attach the local evidence to the failure ticket before escalating.

---

## 2. Symptom -> Diagnosis -> Remediation

### 2.1 Strict K2B gate fails (`validate-k2b-gates.sh ... --strict`)

**Symptom:** `0 pass, N warn, M fail` with missing files under `.dev/ai/knowledge-index/`, `.dev/ai/ingestion/`, `.dev/ai/research/`, `.dev/ai/reports/K2B-*`, `.dev/ai/workorders/WO-INDEX.md`, etc.

**Why this is NOT gated by CI:** The strict K2B contract depends on `.dev/ai/` artifacts that are intentionally gitignored (they contain agent scratch, internal audits, and source-selection records). Vendoring them into the tracked surface would expose internal state; running the gate in CI without them would always fail. The gate is therefore a manual maintainer step. See the rationale section of `WO-0208`.

**Diagnosis checklist:**

1. Is `.dev/ai/` present at all in the local checkout? Fresh clones will not have it. Restore from the authoritative source that contains the artifact contract (see WO-0206 case study below).
2. Are the paths recorded inside `knowledge-index/PROJECT-MASTER-INDEX.md` and `ingestion/LEDGER.md` absolute local paths that actually exist, or stale `~` paths / URLs / pre-move paths?
3. Did a recent commit remove `.dev/ai/` from the public spec tree (as happened in commit `3f30d6b`)? If yes, the contract needs to be restored from the pre-removal commit (`3eef43b` was the source used in WO-0206).

**Remediation:**

1. Identify a legitimate source for the missing artifacts -- either the last commit that had them or a maintainer archive. Do NOT fabricate artifacts to make the gate pass.
2. Restore the full artifact families listed in WO-0206 "Resolution":
   - `.dev/ai/knowledge-index/`
   - `.dev/ai/knowledge-corpus/`
   - `.dev/ai/ingestion/`
   - `.dev/ai/research/`
   - `.dev/ai/reports/K2B-BOOTSTRAP-REPORT-*.md`
   - `.dev/ai/reports/K2B-DECISION-AUDIT-*.md`
   - `.dev/ai/reports/extraction-inventory.md`
   - `.dev/ai/reports/validation-report.md`
   - `.dev/ai/reports/build-extraction.md`
   - `.dev/ai/workorders/` (and `WO-INDEX.md` specifically)
   - `.dev/ai/decisions/`
   - `.dev/ai/specs/`
3. Path-normalize index/ledger/source-map files to current absolute local paths so the strict gate can verify real files on disk.
4. Re-run the gate. Target state: `N pass, 0 warn, 0 fail` (WO-0206 landed at 41/0/0).
5. Capture the verified run in a new WO closeout or append to the triggering WO.

### 2.2 `npm test` fails in `packages/universal-manifest`

**Symptom:** Example fixture validation fails, or GPC validator fails, or the build step itself errors.

**Diagnosis:** `npm test` is `npm run build && npm run validate:examples && npm run validate:gpc`. Determine which stage failed from the log.

**Remediation:**

- Build failure -> fix the TypeScript/bundler error; no WO unless the fix spans multiple files or introduces new public API.
- `validate:examples` failure on a fixture -> check whether the fixture was hand-edited, resigned via `scripts/resign-all-v02.mjs`, or is a valid example that needs updating. See `docs/FIXTURE-SOURCE-OF-TRUTH-AND-PUBLISHED-MIRROR-POLICY.md`.
- GPC validator failure -> the grammatical pattern contract changed; update either the validator or the fixtures, never silently skip.

**Escalation threshold:** Open a WO if the fix requires spec changes, multi-package coordination, or more than ~30 minutes.

### 2.3 `npm run journeys` fails

**Symptom:** Preflight fails, or any of the ~23 journey runs returns non-zero.

**Diagnosis:** Journey artifacts live in `docs/journeys/_artifacts/`. Compare the failing run against the last known-good artifact to localize the regression.

**Remediation:**

- Preflight fail: environment (Node version, missing deps) -- fix the local env, not the journey.
- Individual journey fail: inspect the journey script under `packages/universal-manifest/scripts/journeys/` (or wherever the run-journeys entry point resolves). Determine whether the journey spec changed or the underlying validator behaviour drifted.
- Regenerate artifacts only after the root cause is understood.

**Escalation threshold:** Open a WO if journey failure indicates a validator semantic change, or if multiple journeys fail simultaneously (suggests a shared dependency regressed).

### 2.4 Validator parity fails (`site/scripts/test-validator-parity.mjs`)

**Symptom:** Node vs. browser validator output diverges on one or more fixtures.

**Diagnosis:** Parity is a structural invariant -- the browser-side Ed25519 validator must produce byte-identical verdicts to the Node-side validator for the same fixture. A divergence is almost always caused by a recent change to one of:

- `packages/universal-manifest/` validator source
- `site/src/` validator wiring (bundled imports, serialization)
- a fixture that was updated in one location but not the published mirror (see `FIXTURE-SOURCE-OF-TRUTH-AND-PUBLISHED-MIRROR-POLICY.md`)

**Remediation:**

- Locate the diverging fixture from the parity report.
- Diff the Node and browser verdicts; the side that changed most recently is usually wrong.
- Resync the fixture mirrors via `site/scripts/sync-sandbox-fixtures` (or the equivalent npm script) and re-run parity.

**Escalation threshold:** Open a WO if parity divergence crosses the serialization layer (canonical JSON form changed) or if it affects more than one fixture family.

### 2.5 Docs link-hygiene scan returns hits

**Symptom:** Phase 9 ripgrep command returns non-empty output.

**Command (from CRITICAL-PATH.md):**

```bash
rg -n '/harness/|/proof/|/getting-started/|/spec/|/conformance/|/workbench/|/integrations/' \
  site/src/content/docs --glob '*.md' \
  | rg -v '\]\([^)]+'
```

**Diagnosis:** The scan finds bare path strings (not inside a markdown link target `](...)`) referencing core site routes. Each hit is a drift candidate: either a path was mentioned as plain text and should be linkified, or the route was aliased/moved and the doc still references the old path.

**Remediation:**

1. Open each file reported by the scan.
2. For each hit, classify: (a) should be a markdown link -> wrap in `[text](/path/)`; (b) code block example that happens to match the pattern -> confirm the route still exists and move on (the regex does not exclude fenced code blocks; consider adding an explicit exclusion only if the false-positive rate becomes high); (c) stale reference to a retired route -> fix per `docs/CANONICAL-ROUTE-AND-COMPATIBILITY-ALIAS-POLICY.md`.
3. Re-run the scan until it returns empty.

**Escalation threshold:** Open a WO if the scan reveals a systematic route rename or alias policy change.

### 2.6 Production route HEAD check fails

**Symptom:** `curl -I` returns non-2xx/3xx for one of:

- `https://universalmanifest.net/`
- `https://universalmanifest.net/getting-started/workbench/`
- `https://universalmanifest.net/proof/harness/`

**Diagnosis order:**

1. Retry from a clean environment. Cloudflare occasionally returns transient 5xx or cached-negative responses; a single `curl -I` is not conclusive.
2. Check the deploy pipeline (`.github/workflows/deploy-gated.yml`) for a failed or skipped recent deploy.
3. Check the synthetic monitoring workflow (`.github/workflows/synthetic-monitoring.yml`) -- if its ping-monitor is also failing, the outage is live.
4. Open `https://dash.cloudflare.com/` route rules and verify the canonical route is still mapped. `docs/CANONICAL-ROUTE-AND-COMPATIBILITY-ALIAS-POLICY.md` documents the expected mapping.

**Remediation:**

- Cache-only flap -> wait out one CF edge cycle (~60s) and re-check.
- Deploy skipped -> re-trigger `deploy-gated.yml`.
- Route rule drift -> restore the canonical rule, then file a WO to prevent recurrence.

**Escalation threshold:** Open a P0 WO immediately if the root path returns non-2xx and persists for more than one edge cycle.

---

## 3. WO-0206 case study -- reference restoration procedure

This is the canonical worked example for a strict K2B gate failure.

**Trigger:** Running the Phase 9 mandatory command set on 2026-04-24. The strict K2B gate returned `0 pass, 12 warn, 13 fail`. The `.dev/ai/` artifact root was present but its contract files had been removed.

**Root cause:** Commit `3f30d6b` ("remove internal AI orchestration state from the public spec tree") removed the `.dev/ai/` contract families from the tracked tree. The removal was correct policy (those artifacts are agent scratch and should not ship on the public spec surface) but left the strict K2B gate without anything to validate against in a fresh checkout.

**Restoration procedure executed:**

1. Identified the last legitimate source commit that still contained the artifacts: `3eef43b` ("chore: add AI orchestration, audit, handoff, and post-deploy verification logs"), immediately preceding `3f30d6b`.
2. Restored the full artifact families (listed in section 2.1 above) from `3eef43b` into the local `.dev/ai/` tree. Because `.dev/ai/` is gitignored, this restoration is local-only and does not re-enter the tracked surface.
3. Path-normalized the restored index, ledger, and source-map files so every recorded path is an absolute local path that resolves on this checkout, rather than a historical `~` path, a URL, or a pre-move local path.
4. Re-ran the strict K2B gate. Result: `41 pass, 0 warn, 0 fail`.
5. Re-ran the remaining Phase 9 mandatory commands. All passed (journeys 23/23, three production routes 200, link-hygiene empty).
6. Updated `docs/CRITICAL-PATH.md`, `docs/STATE-OF-THE-PROJECT.md`, and `docs/workorders/WO-INDEX.md` to reflect the verified state.

**Key lessons captured in WO-0208:**

- The strict K2B gate cannot run in CI without either vendoring `.dev/ai/` (unsafe -- widens the tracked surface to include sensitive agent state) or rewriting the gate against a tracked governance mirror. The decision documented in WO-0208 is to keep the gate manual and to rely on this playbook to make the procedure fast.
- Link-hygiene, parity, journeys, and `npm test` all CAN run in CI and are now gated in `.github/workflows/phase-9-gate.yml`. Had that gate existed on 2026-04-24, the K2B failure would still have required manual intervention, but the non-K2B mandatory commands would have caught any co-drift automatically instead of depending on a maintainer to remember the checklist.

---

## 4. Escalation thresholds

Open a new work order (follow `docs/workorders/WO-INDEX.md` numbering) when any of the following are true:

- Any mandatory command fails and the fix is estimated to take more than 30 minutes OR touches more than one package/surface.
- A failure recurs after a fix (suggests the root cause was not addressed).
- Status documents (`CRITICAL-PATH.md`, `STATE-OF-THE-PROJECT.md`, `WO-INDEX.md`) contradict the verified gate state.
- Newly ingested corpus signals require IA/spec/proof deltas beyond trivial wording.
- Production route drift affects the root path or persists past one CF edge cycle.

Do NOT open a WO for:

- A single transient CF 5xx that recovers on retry.
- A link-hygiene hit that can be fixed in under 5 minutes with no policy implications.
- A local environment failure (missing Node version, missing ripgrep) that does not reproduce in CI.

---

## 5. After remediation -- record the run

For any remediation that touched the tracked tree or changed the gate state, record the evidence under `docs/reports/drift-scans/` with a timestamp prefix (see `~/.agents/scripts/get-filename-prefix.sh`). The Phase 9 workflow writes its own scheduled-run reports to the same directory; manual runs should follow the same format so the audit trail is uniform.

Minimum recorded fields:

- UTC timestamp
- Trigger (scheduled, manual, WO-driven)
- Which mandatory commands ran and their result
- Link to the fix commit or WO if any tracked files changed
- Final PASS/FAIL status
