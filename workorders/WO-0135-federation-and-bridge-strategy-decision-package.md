# WO-0135 — Federation and Bridge Strategy Decision Package

**Status:** NOT_STARTED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P1  
**Owner:** Runtime and Integration Architecture  
**Source:** `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-protocol-volatility-proximity-and-federation-research-first-decision-package.md`

## Objective

Convert the current architecture fragments around subject-controlled runtimes, external substrates, and closed-surface adapters into a standards-neutral decision package for federation and bridge strategy.

## Problem Statement

UM already documents pointer-first runtime behavior and adapter-style integration, but it does not yet provide a single comparison framework for canonical private state, public projection, trust federation, live relay/sync, and closed-surface bridge roles across external substrates.

## Scope

In scope:

- Define role-based evaluation criteria for storage, federation, sync, and bridge substrates.
- Compare how those roles attach to UM without making any one substrate appear normative.
- Produce a promotion recommendation for future guidance updates to runtime and integration docs.

Out of scope:

- Selecting one mandatory storage or federation protocol.
- Core schema changes.
- Implementing a reference bridge adapter.

## Deliverables

- A new report under `/Users/grig/work/repo/universalmanifest/docs/reports/`
- Governance synchronization if a stronger runtime guidance profile is approved

## Acceptance Criteria

- [ ] The decision package is role-based rather than vendor-based.
- [ ] Source-of-truth, refresh, and failure-mode expectations are explicit.
- [ ] Closed-surface behavior remains clearly non-normative.
- [ ] The result states whether follow-on guidance work is justified and where it should land.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0132-research-first-protocol-volatility-proximity-and-federation-gaps.md`
