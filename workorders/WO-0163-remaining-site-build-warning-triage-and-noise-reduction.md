# WO-0163 -- Remaining Site Build Warning Triage and Noise Reduction

**Status:** COMPLETED
**Priority:** P2
**Created:** 2026-03-17

## Objective

Resolve or explicitly disposition the remaining non-blocking site build warnings so `npm run build` noise reflects actual risk instead of known-but-untracked exceptions.

## Context

`WO-0162` closed the misleading Starlight duplicate-id warning by correcting the docs collection to use `docsLoader()`. That leaves three warnings in the current site build:

1. Vite warning that `src/scripts/sandbox/scenarios/index.ts` is both dynamically and statically imported.
2. Starlight route-priority warning because the custom landing page owns `/` while the docs router also defines a root route.
3. Pagefind warning that `/workbench/index/` has no outer `<html>` element and is therefore skipped by default indexing.

These warnings were known and non-blocking, but they remained as recurring build noise. This pass fixes the two warnings that were purely structural and records the remaining Starlight root-route warning as an intentional override with explicit rationale.

## Scope

In scope:

1. Investigate the sandbox mixed-import warning and determine whether chunking or import structure should change.
2. Decide whether the Starlight `/` route-priority warning should be structurally removed or explicitly retained as an intentional override.
3. Investigate the Pagefind `/workbench/index/` warning and determine whether the page should be made indexable, excluded intentionally, or wrapped/configured differently.
4. Preserve existing public routes and behavior while reducing warning noise.

Out of scope:

- Broader sandbox architecture redesign beyond what is required to remove or explain the warning.
- Landing-page redesign beyond route-ownership clarification.
- Workbench feature changes unrelated to search/indexing behavior.

## Deliverables

- Warning-by-warning disposition for the remaining site build warnings.
- Code or configuration fixes where removal is justified and low-risk.
- Documentation of any intentionally retained warnings and why they remain acceptable.
- Updated build evidence showing the post-triage warning state.

## Dependencies

- `WO-0161` established the custom landing page that currently produces the Starlight root-route priority warning.
- `WO-0162` removed the duplicate-id warning and narrowed the remaining build-noise set to these three items.

## Execution Notes

- Do not remove intentional route ownership or search behavior without documenting the tradeoff.
- Prefer small, targeted fixes over broad restructures.
- If a warning is intentionally retained, record the reason and the condition under which it should be revisited.
- Final dispositions from this pass:
  - sandbox mixed-import warning: fixed by removing the unused lazy-loader path and relying on the statically populated registry already imported by the sandbox route
  - Pagefind `/workbench/index/` warning: fixed by replacing the config redirect with an explicit HTML redirect page that includes a proper `<html>` root
  - Starlight `/` route-priority warning: intentionally retained because the landing-first root route introduced in `WO-0161` is supposed to override the old Starlight docs-root route

## Acceptance Criteria

- [x] Each remaining warning has a documented disposition: fixed, intentionally retained, or deferred with a concrete reason.
- [x] `npm run build` evidence reflects the new warning baseline accurately.
- [x] Public landing, docs, sandbox, and workbench routes remain functional after any changes.
