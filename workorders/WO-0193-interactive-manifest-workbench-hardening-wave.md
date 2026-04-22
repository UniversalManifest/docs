# WO-0193 -- Interactive Manifest Workbench Hardening Wave

**Status:** COMPLETED
**Priority:** P2
**Created:** 2026-04-13

## Objective

Harden the interactive manifest workbench beyond its first public release so it becomes a more durable long-term tool surface.

## Context

The current state explicitly says advanced hardening of the interactive manifest workbench remains unfinished beyond the first public release. The route is now reintegrated, but the tool itself still deserves a hardening wave.

## Scope

In scope:

1. Identify the highest-value hardening gaps in the workbench.
2. Improve reliability, editing safety, validation confidence, and long-term maintainability.
3. Preserve the current public route/payload architecture unless a bounded migration is justified.

Out of scope:

- replacing the workbench with a brand-new tool without evidence

## Deliverables

- Workbench hardening plan and execution slice.
- Verification evidence for the hardened tool behavior.

## Dependencies

- WO-0183 canonical route and compatibility alias policy.
- Existing workbench payload and shared-shell hosting model.

## Acceptance Criteria

- [x] The key post-first-release hardening gaps are documented.
- [x] The workbench becomes more reliable and maintainable.
- [x] Verification evidence exists for the hardening slice.

## Completion Notes

- The chosen hardening slice addressed silent loss and misuse of unapplied edits in the workbench.
- Core draft-state and validation logic was extracted into a testable module, and the UI now autosaves local drafts, warns before destructive actions, and reports draft status clearly.
- Closeout evidence is recorded in `docs/reports/2026-04-22-interactive-manifest-workbench-hardening-wave.md`.
