# RP1/MSF Adversarial Attachment and Session Hardening

Date: 2026-03-06  
Work order: `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0139-rp1-msf-adversarial-attachment-and-session-hardening.md`

## Summary

This pass closes the remaining RP1/MSF proof gap left after the primary-source refresh. The Universal Manifest core contract remains unchanged. Hardening is delivered through optional pointer-level freshness/status metadata, adversarial fixtures, a new proof journey (`J22`), and synchronized integration documentation.

## What changed

### 1. Positive-path RP1 fixture strengthened

Updated:
- `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld`

Added optional RP1 pointer metadata to the positive fixture:
- `rp1.attachmentIndex.observedAt`
- `rp1.attachmentIndex.expiresAt`
- `rp1.attachmentIndex.status = active`
- `rp1.sessionContext.observedAt`
- `rp1.sessionContext.expiresAt`
- `rp1.sessionContext.status = active`

Also made the attachment policy explicit about fail-closed behavior:
- `freshnessSource = rp1.attachmentIndex`
- `onFreshnessFailure = deny-child-scope-traversal`

### 2. Adversarial fixtures added

Created:
- `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/rp1-spatial-fabric-stale-attachment-manifest.jsonld`
- `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/rp1-spatial-fabric-revoked-session-manifest.jsonld`

These fixtures remain structurally valid UM documents while modeling two failure cases:
- stale attachment evidence that must block child-scope traversal,
- revoked or already-expired session context that must block replay/reuse.

### 3. New executable journey proof

Created:
- `/Users/grig/work/repo/universalmanifest/docs/journeys/J22-rp1-attachment-freshness-and-session-safety.md`

Updated:
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`
- `/Users/grig/work/repo/universalmanifest/docs/journeys/README.md`
- `/Users/grig/work/repo/universalmanifest/docs/journeys/journey-07-rp1-spatial-fabric-projection.md`

`J22` proves:
- stale `rp1.attachmentIndex` evidence blocks child-scope traversal,
- revoked or expired `rp1.sessionContext` blocks replay,
- these behaviors are implemented as integration-lane safety rules rather than core-schema obligations.

`J07` now also verifies the positive-path freshness/status metadata.

### 4. Integration docs and sandbox flows synchronized

Updated repo docs:
- `/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md`

Updated site docs:
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/rp1-spatial-fabric.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/governance/how-we-build.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/governance/decisions.md`

Updated sandbox scenarios:
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/integration-lanes/il-04-rp1-spatial-fabric.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/integration-lanes/il-04-rp1-spatial-fabric-v2.ts`

The public-facing explanation is now aligned with the proof model:
- fresh attachment/session pointers permit the happy path,
- stale or revoked evidence blocks traversal or replay,
- none of this changes the v0.1 core UM contract.

### 5. Governance and status synchronization

Updated:
- `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`
- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`

Added decision:
- RP1/MSF stale attachment indexes and revoked session context must fail closed.

## Architectural outcome

No core-schema gap was found for this hardening step.

The correct integration model is:
- keep RP1/MSF fields optional and non-normative,
- allow optional freshness/status metadata on those optional pointers,
- prove fail-closed runtime behavior with fixtures and journeys,
- avoid promoting spatial-fabric runtime semantics into the Universal Manifest core.

That means the current system can address this need without a UM v0.1 schema change.

## Verification

### Package tests

Command:
- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test`

Artifact:
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-rp1-msf-adversarial-hardening-npm-test.txt`

Result:
- PASS
- New RP1 fixtures validated successfully in the example suite.

### Journey proof

Command:
- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`

Artifacts:
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-rp1-msf-adversarial-hardening-journeys.txt`
- `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/2026-03-06T18-57-58-721Z-journey-report.json`

Result:
- PASS
- `22 pass, 0 fail`
- `J22` is present and passing.

### Site build

Command:
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`

Artifact:
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-rp1-msf-adversarial-hardening-site-build-clean.txt`

Result:
- PASS
- Non-blocking pre-existing warnings remain:
  - duplicate content-id warnings for `governance/decisions`, `governance/how-we-build`, and `integrations/rp1-spatial-fabric`
  - existing sandbox dynamic-import warning
  - existing Pagefind `/workbench/index/` warning

## Final position

This hardening wave confirms the current UM architecture is sufficient for RP1/MSF attachment/session safety.

The remaining rule is not “add more schema.” It is “keep proving fail-closed behavior at the integration edge.”
