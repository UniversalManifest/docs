# RP1/MSF Primary-Source Refresh and Integration-Depth Pass

Date: 2026-03-06
Work order: `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0138-rp1-msf-primary-source-refresh-and-integration-depth-pass.md`

## Executive result

The RP1/MSF integration lane did not need a UM core change. It did need better primary-source grounding and a materially deeper explanation of how scope composition, attachments, runtime state, and asset delivery fit around Universal Manifest.

This pass localized four additional primary sources, refreshed provenance records, deepened the RP1/MSF integration guidance, and upgraded the lane fixture and proof expectations.

## Primary sources localized in this pass

- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-29-manifolder-readme.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-30-manifolder-data-model.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-31-manifolder-client.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-32-khronos-gltf-runtime-delivery.md`

## What these sources closed

### 1. Attachment-point composition

Before this pass, the lane said RP1 data could be pointed to, but it did not explain how linked spatial scopes actually compose.

The Manifolder data-model and client docs make the composition model concrete:
- a scope is a single connected Fabric instance,
- nodes can reference other MSF files,
- following those links creates child scopes,
- cycles are handled by the runtime, not by the manifest.

Resulting integration decision:
- UM may summarize attachment policy and point to attachment indexes,
- UM must not try to inline the live scope tree as portable identity state.

### 2. Primary vs secondary fabrics

The OMB review surfaced the need to distinguish primary vs secondary fabrics. The primary sources do not justify turning that into a rigid UM schema concept.

The better portable distinction is:
- parent/root/current scope,
- attached child scope,
- attachment point that links them.

The RP1 code does use internal `primary`/`secondary` object handling, but that is implementation detail. The manifest only needs the relationship summary that interoperable consumers can act on.

### 3. Runtime-only presence vs portable manifest state

The Manifolder client/runtime sources make the boundary clearer than the earlier lane text.

Runtime-only:
- live search results,
- loaded node trees,
- cached models/resources,
- active scope connections,
- view selection and expansion state.

Portable in UM:
- consent,
- pointers,
- compact anchor declarations,
- place membership,
- attachment-policy summaries,
- asset-profile hints,
- optional revocable session-context reference.

### 4. Asset and tooling boundaries

The Manifolder README and Khronos glTF source clarify that 3D assets remain runtime resources.

Resulting integration decision:
- use UM to point to asset-profile documents or declare lightweight delivery hints,
- keep `gltf`/`glb` payloads external,
- do not turn tool or viewer state into core manifest requirements.

## Repo changes made

### Integration guidance refreshed

- `/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/rp1-spatial-fabric.md`

### Proof/example surfaces deepened

- `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld`
- `/Users/grig/work/repo/universalmanifest/docs/journeys/journey-07-rp1-spatial-fabric-projection.md`

### Provenance refreshed

- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/SOURCE-MAP.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-index/CANDIDATE-SOURCES.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-index/SOURCE-SELECTION.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/ingestion/LEDGER.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/ingestion/records/2026-03-06-rp1-msf-source-refresh-stage0-triage.md`

## Final decision

- No RP1/MSF-specific core UM fields were added.
- The lane now explicitly supports:
  - root/current fabric pointers,
  - attachment-index pointers,
  - compact attachment-policy shards,
  - asset-profile pointers or lightweight declarations,
  - explicit runtime-only vs portable-state boundaries.
- GeoPose was considered as an adjacent future source family, but it was not required for this pass because the current lane still does not carry portable geodetic pose claims.

## Recommended next hardening step

If this lane needs another execution wave, it should target adversarial proof rather than additional conceptual expansion: stale attachment indexes, denied child-scope traversal, and revoked session-context pointers.
