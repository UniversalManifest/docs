# WO-0004 — Expand conformance fixtures (TTL + unknown fields)

**Status:** In progress  
**Created:** 2026-02-12

## Objective

Expand the v0.1 conformance fixtures and harness to cover:

- TTL sanity checks (issued/expires ordering, expired-for-use examples)
- “Unknown fields must be ignored” examples (forward compatibility)

## Scope

In scope:

- Add new valid fixtures
- Add new invalid fixtures
- Update `packages/universal-manifest` test harness to validate these rules
- Update `spec/v0.1/CONFORMANCE.md` fixture list accordingly

Out of scope:

- v0.2 signature conformance (tracked in WO-0002)

## Acceptance criteria

- [ ] `npm test` passes (valid fixtures + expected invalid fixtures)
- [ ] Conformance doc lists the new fixtures
- [ ] Harness reports useful errors when a fixture unexpectedly passes/fails

