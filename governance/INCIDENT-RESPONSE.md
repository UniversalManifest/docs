# Incident Response and Rollback

**Version:** 1.0
**Effective date:** 2026-03-02
**Status:** Active

## 1. Purpose

This runbook defines how Universal Manifest maintainers detect, triage, resolve, and retrospectively analyze incidents affecting normative artifacts, conformance, or publishing reliability.

## 2. Incident Categories

1. Spec defect: normative text is wrong or materially ambiguous.
2. Conformance suite bug: fixture content or expected outcomes are incorrect.
3. Publication failure: canonical artifacts at stable URLs are incorrect or unavailable.
4. Security vulnerability: exploit path affecting integrity, authenticity, or trust guarantees.

## 3. Severity Levels

1. `P0-critical`: security compromise, widespread validation failure, or unavailable critical artifacts.
2. `P1-high`: significant adopter impact, no safe workaround.
3. `P2-medium`: limited impact or documented workaround exists.

## 4. Response Time Targets

1. P0: acknowledgment within 4 hours.
2. P1: acknowledgment within 24 hours.
3. P2: acknowledgment within 1 week.

## 5. Incident Workflow

1. Detect: CI signal, adopter report, or maintainer observation.
2. Triage: assign category and severity.
3. Communicate: acknowledge incident and indicate next update window.
4. Investigate: establish root cause and blast radius.
5. Fix: implement correction with explicit validation plan.
6. Verify: rerun conformance and operational checks.
7. Resolve: publish remediation summary and close incident.
8. Retrospective: capture lessons and policy/process updates.

## 6. Rollback Procedures

### 6.1 Spec rollback

1. Revert normative text to last known-good versioned artifact.
2. Republish corrected artifact set at canonical URLs.
3. Publish correction note and migration/impact details.

### 6.2 Conformance suite rollback

1. Revert to previous suite tag/version.
2. Confirm known-good behavior via runner execution.
3. Communicate temporary pin guidance to adopters.

### 6.3 Publication rollback

1. Redeploy previous verified build artifacts.
2. Re-check canonical endpoints and cache headers.
3. Run smoke checks for docs and resolver surfaces.

### 6.4 Automated rollback (operator playbook)

The `Rollback (Manual)` GitHub Actions workflow (`.github/workflows/rollback-manual.yml`) re-deploys a chosen prior git ref to staging or production and re-runs the same smoke + post-deploy verify harness used by `deploy-gated.yml`. Use this when the documented manual rollback is too slow (target MTTR: ~5 minutes for resolver, ~10 minutes for docs).

**When to use:** P0 or P1 incident where reverting code via a known-good prior ref is faster than rolling forward with a fix.

**Operator steps:**

1. Identify the last known-good git ref (tag preferred, SHA acceptable). Cross-check against:
   - `docs/reports/deploy-checks/` (artifact filenames carry the deployed ref)
   - the most recent green `Deploy (Gated)` workflow run
2. Open GitHub → Actions → `Rollback (Manual)` → `Run workflow`.
3. Select inputs:
   - `environment`: `staging` or `production`
   - `git-ref`: the prior ref to re-deploy (e.g., `spec-v0.2.0`, or a commit SHA)
   - `confirm`: must equal `ROLLBACK` exactly (hard sanity gate; the workflow fails immediately if not matched)
4. Click `Run workflow`. The workflow will:
   - Re-checkout, rebuild the publish bundle and resolver from the target ref
   - Re-deploy Cloudflare Pages and the resolver Worker against the chosen environment
   - Re-run `smoke:endpoints:{env}` and `verify:postdeploy:{env}`
   - Upload a rollback audit record artifact (`rollback-record-{env}`)
5. After the workflow finishes:
   - Download the `rollback-record-{env}` artifact and commit the contained markdown file to `docs/reports/rollbacks/{date}-{env}-{ref}.md`.
   - Download `rollback-deploy-checks-{env}` and attach the smoke/verify artifacts to the incident report (per section 8).
   - Open or update the incident report under `docs/reports/` with the rollback record link, root cause hypothesis, and the planned roll-forward fix.

**If the workflow fails:**

- `confirm_gate` failure: the `confirm` input did not equal `ROLLBACK`. Re-run with the correct value.
- `rollback_docs` or `rollback_resolver` failure: deploy did not complete. Investigate Cloudflare auth and target ref before re-running. Do NOT retry blindly against production.
- `verify_rollback` failure: deploy completed but smoke or post-deploy verify failed. The target ref may itself be unhealthy against the current environment configuration. Escalate to manual rollback (section 6.3) and choose a different prior ref.

**Audit trail location:** `docs/reports/rollbacks/{YYYY-MM-DD}-{env}-{ref}.md` (record per invocation).

## 7. Communication Template

Initial advisory should include:

1. incident ID
2. severity and category
3. current impact
4. immediate mitigation guidance
5. next status update target

Resolution notice should include:

1. root cause
2. fix summary
3. verification evidence paths
4. required adopter actions (if any)

## 8. Incident Report Template

Store reports in `docs/reports/`.

Required sections:

1. Incident ID and date.
2. Severity and category.
3. Detection source.
4. Timeline of actions.
5. Root cause analysis.
6. Impact analysis.
7. Fix and rollback details.
8. Verification evidence.
9. Lessons learned and process changes.

## 9. Simulation Requirement

At least one incident simulation per major governance milestone should be run and documented to prove the runbook is executable, not theoretical.

Current simulation evidence:

- `docs/reports/2026-03-02-incident-simulation-evidence.md`
