# Incident Simulation Evidence — Conformance Suite Bug Rollback

**Date:** 2026-03-02
**Agent Task ID:** e0a7fe60_1772165606
**Scenario:** Simulated conformance suite bug (incorrect expected result) with rollback verification
**Category:** Conformance Suite Bug
**Severity:** P1 (simulated)

## 1. Simulation Objective

Prove the incident response and rollback runbook is executable by simulating a faulty conformance fixture expectation, observing failure in conformance execution, restoring known-good expectations, and confirming recovery.

## 2. Injected Fault

Temporary local mutation (not committed):

- File: `conformance/v0.2/expected.json`
- Fixture entry: `valid/minimal-signed-manifest.jsonld`
- Fault: changed `expectedResult` from `accept` to `reject`

## 3. Detection Evidence

Runner command (with faulty expectation):

```bash
cd conformance/runner
node ./cli.mjs --mode command --adapter-command "node ../adapters/typescript/adapter.mjs" --versions 0.2 --report ./conformance-report-sim-fail.json
```

Observed output:

- `Pass: false`
- `v0.2 -> total: 15, passed: 14, failed: 1, skipped: 0`

Artifacts:

- `conformance/runner/conformance-report-sim-fail.json`
- `/tmp/um-incident-sim-fail.log`

## 4. Triage and Communication Draft (Simulation)

- Assigned severity: P1 (`conformance suite bug impacting adopter CI confidence`)
- Initial communication draft:
  - "We identified an incorrect fixture expectation in v0.2 conformance definitions. Please pin current known-good suite while remediation is applied. No spec contract change was introduced."

## 5. Fix and Rollback Verification

Fix action:

- Restored `conformance/v0.2/expected.json` from known-good backup.

Recovery command:

```bash
cd conformance/runner
node ./cli.mjs --mode command --adapter-command "node ../adapters/typescript/adapter.mjs" --versions 0.2 --report ./conformance-report-sim-recovered.json
```

Observed output:

- `Pass: true`
- `v0.2 -> total: 15, passed: 15, failed: 0, skipped: 0`

Artifacts:

- `conformance/runner/conformance-report-sim-recovered.json`
- `/tmp/um-incident-sim-recovered.log`

## 6. Post-Fix Verification

- Verified simulation marker text is absent from `conformance/v0.2/expected.json`.
- Confirmed no persistent diff remained in the fixture file after rollback.

## 7. Retrospective Notes

What worked:

1. Conformance runner detected regression immediately.
2. Known-good rollback restored expected behavior quickly.

What to harden next:

1. Add automation that checks for unexpected expected-result churn in fixture manifests.
2. Require explicit reviewer acknowledgment for any change in `expectedResult` fields.

## 8. Policy Links

- `docs/governance/INCIDENT-RESPONSE.md`
- `docs/governance/REGRESSION-PREVENTION.md`
- `docs/governance/BREAKING-CHANGE-POLICY.md`
