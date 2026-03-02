# Regression Prevention Policy

**Version**: 1.0  
**Effective Date**: 2026-03-02  
**Status**: Active

## Purpose

This policy defines how Universal Manifest prevents conformance regressions for active adopters while the specification and fixture suites evolve.

## Conformance Suite Compatibility Rules

1. New fixtures may be added without breaking existing adopters.
2. Existing fixture expected results must not change in a backward-incompatible way without a major suite version bump.
3. Conformance suite versioning follows semantic versioning:
   - major: breaking fixture expectation or normative behavior change
   - minor: additive fixtures and non-breaking coverage expansion
   - patch: non-behavioral corrections (metadata, docs, typo fixes)

## Required Change Controls

For pull requests that modify `spec/`, `examples/`, or `conformance/`:

1. Run conformance checks against the reference implementation.
2. Identify whether any previously passing baseline fixture now fails.
3. Document expected fixture deltas in the pull request description.
4. If behavior changes are normative, route through RFC and spec improvement queue.
5. Notify affected adopters when release-impacting behavior changes are approved.

## Baseline Pinning for Adopters

Adopters can pin to a stable fixture subset while upgrading:

- Use `--baseline` in the conformance runner to execute baseline fixtures only.
- Use `--versions` to constrain tested spec versions.
- Use a pinned suite artifact/version in CI and record that value in conformance reports.

Example:

```bash
node conformance/runner/cli.mjs \
  --mode command \
  --adapter-command "node conformance/adapters/typescript/adapter.mjs" \
  --versions 0.2 \
  --baseline \
  --suite-version 1.0.0-draft \
  --report ./conformance-report.json
```

## CI Gate Expectation

The project policy requires a conformance regression gate on pull requests that verifies baseline stability against the reference implementation.

If CI wiring is incomplete, maintainers must run equivalent checks manually before merge and track automation as follow-up work.

## Notification Protocol

When a merged change can affect adopter behavior:

1. Identify impacted adopters via `/Users/grig/work/repo/universalmanifest/adopters/registry.json`.
2. Post release notes with:
   - changed fixtures and spec versions
   - migration guidance
   - target timeline
3. Link notification evidence from the related issue or RFC.

## Related Documents

- [Governance](./GOVERNANCE.md)
- [Adopter Feedback SLA](./ADOPTER-SLA.md)
- [Spec Improvement Queue](./SPEC-IMPROVEMENT-QUEUE.md)
