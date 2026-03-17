# WO-0162 -- Agent Path Drift Reconciliation and Starlight Warning Cleanup

**Status:** IN_PROGRESS
**Priority:** P1
**Created:** 2026-03-16

## Objective

Reconcile the older agent-facing authority docs with the new onboarding path and landing/docs split, while resolving or at least isolating the Starlight duplicate-id warnings now appearing during site builds on the affected docs pages.

## Context

WO-0159 through WO-0161 established the new public agent path, publication gates, and landing-first surface. The follow-on gap is that several older authority documents still needed to be aligned to that new path.

During this cleanup pass, the content updates landed, but the site build still emits unresolved duplicate-id warnings from the Starlight content loader on changed docs pages. The routes still build and serve, but the warning remains unexplained on the current working tree.

## Scope

In scope:

1. Reconcile older authority docs with the new public agent path.
2. Keep the standards-host versus runtime-host split explicit in both site docs and repo docs.
3. Investigate the duplicate-id warning and determine whether it can be fixed immediately.
4. If not fixable in this pass, record the failure mode and next action explicitly.

Out of scope:

- Broader IA redesign beyond the already completed landing/docs split.
- Resolver runtime contract changes.
- New public agent-service capabilities.

## Deliverables

- Updated authority and boundary docs.
- Updated internal docs index entries for the agent-friendly public surface.
- Investigation note or closeout explaining the Starlight duplicate-id warning state.

Current artifacts in progress:

- `site/src/content/docs/about/agent-briefing.md`
- `docs/explainers/agent-briefing.md`
- `site/src/content/docs/publishing/domain-split.md`
- `docs/DOMAIN-ARCHITECTURE.md`
- `docs/README.md`
- `site/src/content/docs/for-agents.md`
- `site/src/content/docs/external-agent-onboarding.md`

## Dependencies

- WO-0159 provides the onboarding and adoption-doc baseline.
- WO-0160 provides the publication-gate baseline.
- WO-0161 provides the landing/docs split those docs now need to describe.

## Execution Notes

- Do not silently weaken or remove the new public agent path while attempting to clean the warning.
- If the warning cannot be fixed quickly, document it and preserve the working public routes.
- Prefer the smallest safe structural change that keeps `/for-agents/` and `/for-agents/external-agent-onboarding/` stable.

## Acceptance Criteria

- [x] Legacy authority docs reflect the current landing/docs/discovery/runtime split.
- [ ] The build warning is either resolved or explicitly documented with root cause and next action.
- [x] Public agent routes remain stable.
