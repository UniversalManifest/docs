# WO-0139 — RP1/MSF Adversarial Attachment and Session Hardening

**Status:** COMPLETED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P1  
**Owner:** Spatial Integration Hardening  
**Source:** `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`

## Objective

Add fail-closed RP1/MSF proof for stale attachment traversal and expired or revoked session-context replay without expanding the Universal Manifest v0.1 core contract.

## Problem Statement

`WO-0138` deepened the RP1/MSF lane, but the remaining gap was adversarial proof. The project had positive-path spatial-fabric guidance and fixture coverage, but it did not yet prove what a consumer must do when child-scope attachment evidence is stale or when a portable session-context pointer is expired or revoked.

## Scope

In scope:

- Strengthen the positive-path RP1/MSF fixture with optional pointer freshness and status metadata.
- Add adversarial RP1/MSF fixtures for:
  - stale attachment-index evidence,
  - revoked or expired session-context evidence.
- Add executable proof coverage for fail-closed behavior.
- Refresh RP1 integration docs and sandbox narratives to match the hardening model.
- Synchronize state, critical-path, and decision records.

Out of scope:

- Any new required UM core fields.
- Promoting RP1/MSF-specific pointer members into normative v0.1 conformance obligations.
- Treating session context as durable portable identity state.

## Deliverables

- Updated positive-path RP1 fixture:
  - `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld`
- New adversarial fixtures:
  - `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/rp1-spatial-fabric-stale-attachment-manifest.jsonld`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/rp1-spatial-fabric-revoked-session-manifest.jsonld`
- New proof journey:
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/J22-rp1-attachment-freshness-and-session-safety.md`
- Updated journey runner:
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`
- Updated RP1 integration docs and sandbox flows:
  - `/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/rp1-spatial-fabric.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/integration-lanes/il-04-rp1-spatial-fabric.ts`
  - `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/integration-lanes/il-04-rp1-spatial-fabric-v2.ts`

## Acceptance Criteria

- [x] Positive-path RP1 fixture includes optional freshness/status metadata for attachment and session pointers.
- [x] Adversarial RP1 fixtures remain structurally valid while modeling stale attachment and revoked-session conditions.
- [x] The journey suite contains executable proof that stale attachment evidence blocks child-scope traversal and revoked or expired session context blocks replay.
- [x] RP1 integration docs and sandbox flows describe the same fail-closed behavior.
- [x] No UM core schema change is introduced.
- [x] Local verification passes:
  - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test`
  - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`
  - `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`

## Dependencies

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0138-rp1-msf-primary-source-refresh-and-integration-depth-pass.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-rp1-msf-primary-source-refresh-and-integration-depth-pass.md`

## Execution Notes

- Completed on 2026-03-06.
- Introduced `J22` for adversarial RP1/MSF hardening.
- Preserved the current architectural boundary: optional RP1 pointer metadata only, no new UM core semantics.
- Verification artifacts:
  - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-rp1-msf-adversarial-hardening-npm-test.txt`
  - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-rp1-msf-adversarial-hardening-journeys.txt`
  - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-rp1-msf-adversarial-hardening-site-build-clean.txt`
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/2026-03-06T18-57-58-721Z-journey-report.json`
