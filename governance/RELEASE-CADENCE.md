# Release Cadence Policy

**Version:** 1.0
**Effective date:** 2026-03-02
**Status:** Active

## 1. Purpose

This document defines expected release cadence and review windows for specification and conformance artifacts.

## 2. Spec Release Cadence

Universal Manifest spec releases are demand-driven, not calendar-driven.

1. Major releases: for breaking contract changes after full RFC + migration planning.
2. Minor releases: for additive normative improvements and clarified requirements.
3. Patch releases: for corrections that do not alter expected conformant behavior.

## 3. Conformance Suite Release Cadence

Conformance suite follows semver with explicit adopter safety rules:

1. Major: breaking fixture expectation changes.
2. Minor: additive fixture coverage.
3. Patch: fixture/test harness bug fixes that preserve expected conformant behavior.

## 4. Minimum Review Periods

1. Non-breaking normative changes: minimum 2-week review period.
2. Breaking normative changes: minimum 3-month migration notice before enforcement, except emergency security path.

## 5. Release Preconditions

Before release, maintainers must ensure:

1. relevant conformance runs pass for supported versions
2. migration notes exist when behavior changes
3. governance docs and decision log are updated
4. deployment/smoke checks pass for public surfaces

## 6. Operational Rhythm

Recommended maintainer rhythm:

1. Weekly triage of release candidates and queued RFC impacts.
2. Monthly review of adopter feedback trends and potential patch/minor needs.
3. Quarterly governance audit for policy consistency and lifecycle status updates.

## 7. References

- `docs/RELEASING.md`
- `docs/governance/GOVERNANCE.md`
- `docs/governance/BREAKING-CHANGE-POLICY.md`
- `docs/governance/DEPRECATION-POLICY.md`
- `docs/governance/INCIDENT-RESPONSE.md`
