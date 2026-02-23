# WO-0038 Baseline Report — Drift Governance and Regression Verification

Date: 2026-02-22
Work order: `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0038-corpus-drift-governance-and-follow-on-workorder-cycle.md`

## Summary

Established recurring drift-governance runbook and executed a baseline run covering K2B integrity, journey parity, production-route health, and docs-link hygiene checks.

## Runbook and trigger criteria updates

- Added Phase 9 runbook section in:
  - `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`
- Added index reference to trigger criteria in:
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`

## Baseline run command results

1. Strict K2B gates
- Command:
  - `/opt/homebrew/bin/bash /Users/grig/.agents/scripts/validate-k2b-gates.sh /Users/grig/work/repo/universalmanifest --artifact-root /Users/grig/work/repo/universalmanifest/.dev/ai --strict`
- Result:
  - PASS (`41 pass, 0 warn, 0 fail`)

2. Journey parity
- Command:
  - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`
- Result:
  - PASS (`11 pass, 0 fail`)
  - Artifact:
    - `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/2026-02-23T01-05-33-390Z-journey-report.json`

3. Production routes
- Commands:
  - `curl -I https://universalmanifest.net/`
  - `curl -I https://universalmanifest.net/getting-started/workbench/`
  - `curl -I https://universalmanifest.net/proof/harness/`
- Result:
  - all `200`

4. Docs link-hygiene scan
- Command:
  - `rg -n '/harness/|/proof/|/getting-started/|/spec/|/conformance/|/workbench/|/integrations/' /Users/grig/work/repo/universalmanifest/site/src/content/docs --glob '*.md' | rg -v '\\]\\([^)]+'`
- Result:
  - one textual false-positive phrase in `/Users/grig/work/repo/universalmanifest/site/src/content/docs/conformance/resolver.md` (`standards/spec/docs` wording), no actionable route-path raw-link regression.

## Follow-on WO trigger assessment

- Triggered in this baseline run:
  - no new follow-on WOs required from command failures
- Existing follow-on WOs already active for hardening and policy gates:
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0034-documentation-status-coherence-and-stale-reference-reconciliation.md`
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0035-human-reader-testing-policy-and-onboarding-evidence-alignment.md`
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0036-v0-2-publication-and-verification-edge-case-expansion.md`
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0037-integrity-profile-revocation-and-adversarial-conformance-hardening.md`

