# Phase 9 Drift Scan Reports

This directory holds the audit trail for Phase 9 drift-governance scans.

**Source of truth:** `docs/CRITICAL-PATH.md` Phase 9 section and `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md`.

**Writers:**

- Scheduled: `.github/workflows/phase-9-gate.yml` (job `phase-9-drift-scan`) writes a timestamped report on every weekly cron run and on manual `workflow_dispatch`.
- Manual: maintainers who run the mandatory command set by hand should drop a report here with the same format.

## Filename convention

`YYYY-MM-DD-HH-MM-SS-phase-9-drift-scan.md` (UTC timestamp). Use `~/.agents/scripts/get-filename-prefix.sh` for the prefix when writing manually.

## Minimum fields per report

- UTC timestamp
- Trigger: scheduled | workflow_dispatch | manual-maintainer | wo-driven
- Commands executed and their individual PASS/FAIL
- Run URL (if CI-triggered)
- Final PASS/FAIL
- Link to remediation WO if any tracked files changed

## Retention

Reports are retained indefinitely in git for audit purposes. The CI workflow additionally uploads each report as an artifact with 90-day retention for ad-hoc download.

## Note on K2B strict gate

The strict K2B gate (`~/.agents/scripts/validate-k2b-gates.sh --strict`) depends on gitignored `.dev/ai/` artifacts and is not run inside CI. Manual runs that include the K2B gate should record its result in the same report file; CI-generated reports explicitly note that the K2B step was skipped. See the playbook for remediation of K2B gate failures.
