# WO-0137 — Role-Based Runtime, Federation, and Bridge Guidance Refresh

**Status:** COMPLETED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P1  
**Owner:** Runtime and Documentation Architecture  
**Source:** `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-federation-and-bridge-strategy-decision-package.md`

## Objective

Refresh the shared runtime and synchronization guidance so the repo explicitly uses the new role-based federation and bridge taxonomy without making any one substrate appear normative.

## Problem Statement

The federation/bridge decision package concluded that follow-on guidance work is justified first in shared runtime and synchronization documents. The current docs already have the correct architecture direction, but they do not yet express the new role model, source-of-truth rules, or substrate-boundary language clearly enough.

## Scope

In scope:

- Update shared guidance surfaces to express:
  - canonical private state authority,
  - public projection broker,
  - trust federation gatekeeper,
  - relay/sync coordinator,
  - edge availability custodian,
  - closed-surface bridge adapter.
- Make source-of-truth, refresh, and failure-mode language more explicit.
- Preserve the rule that no single external substrate is normative for UM.

Out of scope:

- Core schema changes.
- New substrate-specific public integration lanes.
- Executing RP1/MSF source localization work.

## Deliverables

- Updated shared guidance docs under:
  - `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md`
  - `/Users/grig/work/repo/universalmanifest/docs/guides/MUM-SYNCHRONIZATION-PROFILE.md`
  - site mirrors if applicable
- Governance/state synchronization where wording changes affect public project posture

## Acceptance Criteria

- [x] Shared runtime and synchronization docs clearly use the role-based taxonomy.
- [x] Source-of-truth, refresh, and failure-mode expectations are explicit in the refreshed guidance.
- [x] No substrate is presented as normative for UM.
- [x] Closed-surface adapters remain clearly non-normative.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0135-federation-and-bridge-strategy-decision-package.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-federation-and-bridge-strategy-decision-package.md`

## Execution Notes

- Completed on 2026-03-06.
- Updated shared guidance surfaces:
  - `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/reference-runtime.md`
  - `/Users/grig/work/repo/universalmanifest/docs/guides/MUM-SYNCHRONIZATION-PROFILE.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/guides/mum-synchronization-profile.md`
- Outcome:
  - the shared docs now express the role-based runtime/federation/bridge taxonomy,
  - source-of-truth and offline failure rules are more explicit,
  - no substrate is presented as normative for UM.
