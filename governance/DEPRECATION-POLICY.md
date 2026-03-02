# Deprecation Policy

**Version:** 1.0
**Effective date:** 2026-03-02
**Status:** Active

## 1. Purpose

This policy defines lifecycle states, support windows, and obligations when Universal Manifest versions are superseded.

## 2. Lifecycle States

Every spec version is in one lifecycle state:

1. `draft`: actively changing; unsuitable for stable production commitments.
2. `stable`: recommended for production use; receives fixes and maintenance.
3. `deprecated`: still supported with restrictions; migration is required.
4. `end-of-life`: no active support; retained for historical reference only.

## 3. Minimum Support Periods

1. A stable version that becomes superseded remains supported for at least 6 months after successor stable release.
2. During deprecated state:
   - security and correctness fixes can be applied
   - no new feature work
   - migration guidance must stay available and current
3. After end-of-life:
   - no fixes
   - fixtures remain accessible as legacy artifacts
   - docs are clearly marked legacy

## 4. Deprecation Notice Requirements

Deprecation announcement must include:

1. impacted version
2. successor version
3. support end date (calendar date)
4. migration guide URL
5. escalation path for critical blockers

Publication points:

1. docs site release/changelog
2. `docs/DECISIONS.md`
3. relevant spec docs and conformance pages

## 5. v0.1 to v0.2 Timeline Policy

Project baseline policy for current transition:

1. v0.2 is the integrity-hardened successor track.
2. v0.1 remains supported during overlap period for at least 6 months after v0.2 stable declaration.
3. overlap period expectations:
   - both versions remain testable in conformance evidence
   - migration guidance is actively maintained in `docs/guides/MIGRATION-V01-V02.md`
4. post-overlap:
   - v0.1 moves to `deprecated`, then `end-of-life` per published dates

## 6. "Supported" vs "Deprecated" vs "End-of-Life"

### Supported

1. Included in conformance suite execution expectations.
2. Issues are triaged under normal SLA.
3. Documentation is maintained and considered current.

### Deprecated

1. Included for compatibility and controlled migration only.
2. Security and correctness maintenance only.
3. Documentation prominently signals migration requirement.

### End-of-life

1. Not part of active maintenance commitments.
2. Artifacts preserved for historical and audit use.
3. Not a target for new implementation work.

## 7. Adopter Responsibilities

Adopters should:

1. track published lifecycle notices
2. plan migration before support end date
3. pin conformance suite versions in CI during migration windows

## 8. Maintainer Responsibilities

Maintainers must:

1. provide migration docs before formal deprecation announcement
2. ensure conformance suite and docs are internally consistent
3. avoid policy contradictions across governance docs
4. publish clear rollback guidance for each major transition

## 9. Cross-References

- `docs/guides/MIGRATION-V01-V02.md`
- `docs/governance/BREAKING-CHANGE-POLICY.md`
- `docs/governance/GOVERNANCE.md`
