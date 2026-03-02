# Breaking-Change Policy

**Version:** 1.0
**Effective date:** 2026-03-02
**Status:** Active

## 1. Purpose

This policy defines how Universal Manifest identifies, reviews, approves, communicates, and delivers breaking changes to normative artifacts and conformance expectations.

## 2. Definition of a Breaking Change

A change is breaking when a previously conformant implementation can become non-conformant, or when previously valid operational behavior becomes invalid, without opt-in by adopters.

Breaking changes include:

1. Normative spec updates that alter required fields, required values, field semantics, or validation behavior.
2. Conformance fixture expectation changes that turn previously passing behavior into failing behavior.
3. Removal or incompatible transformation of normative artifacts at stable URLs.
4. Signature profile requirement changes that invalidate existing conformant issuer/consumer behavior.

Not breaking:

1. New optional fields that preserve unknown-field tolerance.
2. Clarifications that do not alter semantics.
3. Additive fixture coverage where existing fixtures and expectations remain valid.
4. Non-normative documentation improvements.

## 3. Standard Breaking-Change Process

1. Open RFC using `docs/governance/RFC-TEMPLATE.md`.
2. Classify impact:
   - affected versions
   - affected conformance levels
   - consumer impact
   - issuer impact
3. Include mandatory artifacts in RFC:
   - compatibility impact assessment
   - migration path and rollback path
   - adopter communication plan
   - expected timeline (minimum 3 months notice for non-emergency breaking changes)
4. TSC review and decision under `docs/governance/GOVERNANCE.md`.
5. If approved:
   - publish migration documentation
   - update conformance fixtures and versioning metadata
   - announce to adopters and link remediation steps
6. Preserve support for superseded version according to `docs/governance/DEPRECATION-POLICY.md`.

## 4. Emergency Breaking-Change Process

Emergency path is only for active security risk or severe integrity failure.

1. Open emergency RFC/incident record immediately.
2. Review window target: 48 hours.
3. Communicate initial advisory to affected adopters within 24 hours.
4. Ship mitigation or breaking correction with clear rollback guidance.
5. Publish full post-incident report in `docs/reports/`.

Emergency path does not bypass migration guidance; it compresses timeline.

## 5. Versioning Rules

1. Normative breaking changes require a new major spec line or equivalent explicit version boundary.
2. Conformance suite expectation changes that break existing passing behavior require a major suite bump.
3. Additive fixture coverage without regressions uses minor bump.
4. Fixture bugfixes that preserve expected conformant behavior use patch bump.

## 6. Adopter Communication Requirements

For every approved breaking change, maintainers must provide:

1. What changed.
2. Who is affected.
3. Upgrade steps.
4. Rollback path.
5. Deadlines and lifecycle milestones.

Communication channels:

1. GitHub release notes.
2. Governance/changelog docs.
3. Direct issue notifications for registered adopters where applicable.

## 7. Change Log Requirement

Every breaking change must be recorded in:

1. `docs/DECISIONS.md`
2. release notes and migration references
3. relevant spec/conformance changelog sections

Entry must include date, version, rationale, migration link, and rollback link.

## 8. Compliance Checklist

Before merging a breaking change:

1. RFC approved.
2. Migration guide published.
3. Deprecation timeline declared.
4. Conformance expectations updated and validated.
5. Communication artifacts prepared.
6. Rollback procedure documented.
