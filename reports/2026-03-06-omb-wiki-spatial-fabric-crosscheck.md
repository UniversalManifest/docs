# OMB Wiki Spatial Fabric Crosscheck

Date: 2026-03-06
Work order: `WO-0136`
Status: complete
Recommendation: `source refresh`

## Executive summary

`omb.wiki` materially improves discovery of spatial-fabric concepts relevant to Universal Manifest, but it does not overturn the current Universal Manifest integration model.

The current repo already has the right core architectural stance:
- keep RP1/MSF-specific semantics out of UM required core fields,
- model RP1/MSF linkage as optional pointers and shards,
- gate cross-world and location-sensitive behavior with consent,
- prove compatibility through fixtures and journeys instead of hard-coding platform semantics into the normative core.

That part still looks correct.

What has changed is source visibility. `omb.wiki` now exposes a wider and fresher body of spatial-fabric material than the project had localized during `WO-0020`, especially around:
- map hierarchy and object classes,
- attachment-point composition and nested fabrics,
- service decomposition beyond the map itself,
- asset-streaming constraints,
- tool/data-model behavior for map exploration and scene assembly.

Those details are relevant to better RP1/MSF integration guidance, but the wiki itself is not stable enough to be treated as the source of record. In several places it is clearly draft-stage, incomplete, or procedural rather than normative. The correct action is therefore a `source refresh`: use `omb.wiki` as a discovery map, then pull the corresponding primary repositories/specifications before promoting any of the new concepts into repo guidance.

## Scope and method

This review audited the following `omb.wiki` pages for spatial-fabric / open-spatial-internet / RP1-adjacent content relevant to Universal Manifest:
- [Home](https://omb.wiki)
- [Spatial Fabric Architecture](https://omb.wiki/en/spatial-fabric/architecture)
- [Attaching a Campus to a Spherical Planet](https://omb.wiki/en/spatial-fabric/attach-campus)
- [Best Practices](https://omb.wiki/en/spatial-fabric/best-practices)
- [3D Model Guidelines](https://omb.wiki/en/spatial-fabric/model-guidelines)
- [Map Explorer](https://omb.wiki/en/tools/map-explorer)
- [Scene Assembler](https://omb.wiki/en/tools/scene-assembler)
- [Open Standards for the Metaverse](https://omb.wiki/en/standards)

It compared those pages against the current repo baseline, especially:
- `/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/rp1-spatial-fabric.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0020-rp1-source-ingestion-and-synthesis-materialization.md`
- `/Users/grig/work/repo/universalmanifest/docs/journeys/journey-07-rp1-spatial-fabric-projection.md`
- `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/integration-lanes/il-04-rp1-spatial-fabric.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/integration-lanes/il-04-rp1-spatial-fabric-v2.ts`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/ingestion/records/2026-02-18-cross-source-conflicts.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-19-rp1-learn-source-capture.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-20-rp1-dev-rdfabric-container-js.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-21-rp1-dev-rdfabric-partial-js.md`

## Authority rule

This review preserves the project rule already implied by `WO-0136`:
- `omb.wiki` is useful as a discovery and synthesis surface.
- Official repositories, specifications, and implementation code remain the source of record when the wiki differs, lags, or is incomplete.
- Universal Manifest should not promote new RP1/MSF semantics into normative behavior purely because they appear on the wiki.

This rule matters here because the wiki is visibly still being built in public and some pages are incomplete or operationally specific.

## Current repo baseline

The current repo already captures the following correctly:

1. **Core boundary is correct**
- The internal RP1 lane keeps RP1 semantics in optional pointers and shards rather than core required fields.
- This is stated directly in `/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md`.
- `CON-UM-007` explicitly decided to keep RP1 object-model specificity out of the UM minimal core.

2. **A concrete overlay exists**
- The fixture at `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld` already models:
  - `rp1.fabric`
  - `rp1.anchorSet`
  - `rp1.placeGraph`
  - `spatialAnchors`
  - `placeMembership`
  - consent-gated cross-world behavior

3. **Executable proof exists**
- `Journey 07` proves that RP1-style data can be carried as additive overlay material without changing v0.1 core requirements.
- The sandbox lane `IL-04` proves runtime extraction of anchors, place membership, and consent-driven linking behavior.

4. **The existing source corpus is intentionally thin**
- `WO-0020` localized only three RP1 sources:
  - one public-facing RP1 learn surface,
  - two RP1 developer JavaScript artifacts (`RDFabric` / config wiring).
- Those sources were enough to justify the original overlay boundary.
- They were not enough to fully document the broader spatial-fabric domain that the wiki now exposes.

## What `omb.wiki` adds beyond the current repo

The wiki adds real informational value. That value is mostly in breadth, vocabulary, and operational decomposition.

### 1. Spatial topology and object taxonomy

Wiki-discovered context:
- The architecture page describes the map service as a hierarchical query surface rather than a static downloadable artifact.
- It frames the map as three object classes: celestial, terrestrial, and physical.
- It defines example object types and parent/child constraints.
- It introduces surface/subsurface concepts and notes that parcel objects are the bridge from terrestrial to physical objects.

What the current repo already covers:
- Only generic spatial overlay concepts: anchors, place graph, optional pointers, and consent.
- No object taxonomy beyond the example shard names.

Assessment:
- This is **new context**, not a core-schema gap.
- UM does not need to encode the full MSF object model as required fields.
- But the integration docs currently under-explain what `rp1.placeGraph` and related pointers are expected to represent.

How this would apply in UM:
- Keep topology data external to the UM core.
- Carry it as a pointer or optional shard profile.
- Example:
  - `rp1.placeGraph` points to a map-service or topology resource.
  - A non-normative shard profile could describe `class`, `parentRef`, `placeType`, or `subsurfaceRef` for consumers that understand MSF-specific semantics.

### 2. Attachment points and nested-fabric composition

Wiki-discovered context:
- The architecture page includes an attachment-point heading, but the section is currently incomplete.
- The campus-attachment page is far more concrete and describes the actual composition pattern:
  - create a terrestrial sector on the parent fabric,
  - create parcels under that sector,
  - attach secondary spatial fabrics from parcels,
  - carry parent/child linkage via attachment metadata and external fabric references,
  - allow rotation and local orientation at the attachment point.
- The page repeatedly uses subordinate fabric linkage as the real mechanism of composition.

What the current repo already covers:
- `spatial.crossWorldLinking` consent.
- Optional RP1 pointers and shard names.
- No explicit attachment-point model.

Assessment:
- This is the most significant concept expansion surfaced by the wiki.
- It does **not** imply a UM core change.
- It **does** show that the current RP1 lane is too abstract if the goal is to explain how nested spatial fabrics actually compose.

How this would apply in UM:
- Treat attachment-point relationships as integration-lane metadata, not core identity schema.
- Example:
  - parent parcel manifest carries a pointer to a subordinate fabric URL;
  - optional attachment metadata includes orientation, local transform hints, and whether the child fabric is world-local or cross-world discoverable;
  - `spatial.crossWorldLinking` continues to gate whether the link can be exposed outside the parent fabric context.

### 3. Service decomposition beyond the map

Wiki-discovered context:
- The standards page expands spatial fabric into service roles, including:
  - map service,
  - avatar service,
  - persona service,
  - communication / real-time presence behavior.
- It also explains primary vs. secondary fabrics as a composition model.

What the current repo already covers:
- Identity and consent belong in UM.
- RP1-specific overlay material belongs in pointers/shards.
- Sandbox/fixture coverage focuses mostly on anchors and place membership.

Assessment:
- This confirms the repo’s current architecture instead of contradicting it.
- It sharpens the runtime/documentation boundary:
  - UM is good for subject identity, avatar pointers, persona preferences, consent, and routing metadata.
  - Live presence, voice state, transient position updates, and other real-time service state should remain runtime concerns.

How this would apply in UM:
- Example split:
  - UM stores avatar reference, persona preferences, and consent flags.
  - Runtime services manage live coordinates, active presence, current session voice, and low-latency synchronization.
- This is a documentation clarification opportunity, not a schema change.

### 4. Asset and streaming-profile constraints

Wiki-discovered context:
- The best-practices page provides concrete streamability limits and rendering constraints.
- Examples include:
  - a 200m x 200m area target budget,
  - `.glb` as the preferred file format,
  - no Draco compression,
  - capped file size,
  - flat-ground and standing-avatar assumptions,
  - reduced support for lights, instancing, and richer material complexity.
- The model-guidelines page adds resource tiers and per-tier triangle/texture budgets.

What the current repo already covers:
- The RP1 lane currently says large assets should live behind pointers.
- It does not currently explain RP1/MSF asset-profile expectations.

Assessment:
- This is a real guidance gap in the repo, but still non-normative.
- The gap is not “UM cannot carry this.”
- The gap is “UM does not yet explain how to express or point to a constrained asset profile for RP1/MSF consumers.”

How this would apply in UM:
- Example:
  - keep the asset itself external,
  - carry an optional pointer or profile fragment indicating expected asset package and compatibility lane,
  - let an RP1/MSF consumer read a lightweight declaration such as:
    - asset format family: `glTF/GLB`
    - profile lane: `rp1-streaming-basic`
    - transport class: `streamable`
- No need to place triangle budgets in core UM.
- If documented later, this should be an integration profile or registry entry, not a normative base requirement.

### 5. Tooling and interchange surfaces

Wiki-discovered context:
- The map-explorer page points to the open-source Manifolder repo and describes how MSF data is visualized.
- The scene-assembler page describes a JSON scene format, object libraries, Fabric URL binding, and a published-scene workflow.
- These pages are useful because they reveal actual operator and developer touchpoints, not just architecture prose.

What the current repo already covers:
- No explicit crosswalk from UM to Manifolder or Scene Assembler.
- Existing evidence focuses on fixture/journey validation rather than authoring or operational tools.

Assessment:
- This is a source-discovery win.
- It suggests new primary sources worth localizing.
- It does not yet justify any direct UM field additions.

How this would apply in UM:
- Example:
  - a UM pointer could reference a scene package, scene JSON, or related authoring artifact without embedding tool-specific schema into the core manifest.
  - if tool state matters, keep it behind a tool-specific pointer such as an RP1/MSF integration pointer family rather than core fields.

### 6. Coordinate / standards positioning

Wiki-discovered context:
- The standards page mentions DIDs, OpenXR, glTF, GeoPose, and the proposed NSO layer.
- It also frames spatial browsers as universal clients and spatial fabrics as the service-side substrate.

What the current repo already covers:
- DID-oriented identity lanes already exist elsewhere in the repo.
- The published integrations index currently describes RP1 as “GeoPose-aware manifest projection,” but the RP1 lane docs themselves do not provide a primary-source-backed GeoPose profile.

Assessment:
- The wiki helps identify adjacent standards families.
- It does **not** provide enough primary-source support to directly adopt GeoPose semantics into the RP1 lane.
- There is a mild documentation overhang here: the site index language is currently more specific than the internal RP1 lane evidence.

How this would apply in UM:
- Example:
  - keep current coordinates/anchor structures generic unless or until OGC GeoPose primary sources are localized and crosswalked.
  - if later adopted, do it as a profile mapping, not as a hard-coded replacement for the current generic spatial anchor structure.

## Where the wiki is weaker than the current repo position

There are several places where the repo’s current architectural discipline is stronger than the wiki content.

1. **Normative boundary discipline**
- The repo clearly separates normative core from non-normative integration guidance.
- The wiki mixes architecture, product guidance, implementation procedure, tooling docs, and advocacy language in one surface.

2. **Minimal-core discipline**
- The repo already made and documented `CON-UM-007`.
- The wiki presents much richer domain semantics, but does not itself answer which of those semantics belong in a portable user manifest versus external runtime systems.
- The repo’s answer remains better: most of this belongs outside the core manifest.

3. **Completeness**
- The architecture page’s attachment-point section is still incomplete.
- Several wiki pages show draft-stage roughness, typos, or operational assumptions.
- The wiki is therefore not ready to function as the authoritative basis for normative UM changes.

## Gap assessment: current repo vs. wiki-discovered detail

### No core-schema gap found

No evidence in this review shows that Universal Manifest needs new required core fields to support the wiki’s spatial-fabric concepts.

The existing model still holds:
- core UM for identity / consent / routing / profile fragments,
- optional pointers and shards for ecosystem-specific semantics,
- runtime services for live spatial and communication state.

### Real documentation/source gaps found

The meaningful gaps are elsewhere.

1. **Source corpus gap**
- `WO-0020` only localized three RP1 sources.
- Those sources do not cover the full spatial-fabric operational model now visible via `omb.wiki`.

2. **Integration-doc depth gap**
- `/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md` is directionally correct but too thin relative to the newly visible composition model.

3. **Evidence-profile gap**
- Existing fixture/journey material proves anchor and consent carriage.
- It does not yet prove nested-fabric attachment or asset-profile / authoring-profile behavior.

4. **Terminology/crosswalk gap**
- The repo does not yet clearly crosswalk:
  - primary vs. secondary fabrics,
  - attachment points,
  - map/avatar/persona/runtime service boundaries,
  - authoring tools versus portable manifest state.

## Primary-source-confirmed material vs. wiki-only material

### Primary-source-confirmed today

These points are already adequately grounded by the repo’s existing primary-source intake and implementation evidence:
- RP1/MSF-specific semantics should remain out of the core UM contract.
- RP1/MSF linkage can be represented through optional pointers and shards.
- Spatial anchors and place membership can be carried as additive overlay material.
- Cross-world behavior should be consent-gated.

Primary repo evidence:
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-20-rp1-dev-rdfabric-container-js.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-21-rp1-dev-rdfabric-partial-js.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/ingestion/records/2026-02-18-cross-source-conflicts.md`
- `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld`
- `/Users/grig/work/repo/universalmanifest/docs/journeys/journey-07-rp1-spatial-fabric-projection.md`

### Wiki-discovered but not yet sufficiently source-localized

These topics are useful discoveries from `omb.wiki`, but should not yet be treated as repo-authoritative without a source refresh:
- the full celestial / terrestrial / physical taxonomy,
- attachment-point composition patterns,
- sector/parcel nesting conventions,
- operational database procedures and transform workflows,
- asset budget/profile guidance for RP1/MSF rendering,
- Scene Assembler JSON as an operational interchange surface,
- GeoPose-specific positioning implications.

## Recommendation

Recommendation: `source refresh`

Why this is the correct recommendation:
- `omb.wiki` adds meaningful spatial-fabric detail that the project has not yet localized.
- That new detail mostly reveals **source coverage gaps**, not **schema gaps**.
- The wiki itself is still too draft-like, incomplete, and mixed-purpose to promote directly into normative or even semi-authoritative repo language.
- The right next move is therefore to refresh the RP1/MSF source set from primary repositories/specifications discovered or implied by the wiki, then use those refreshed sources to update the RP1 lane documentation.

## What should happen after the source refresh

Once primary sources are refreshed, a follow-on documentation pass should likely do three things.

1. **Expand the RP1/MSF integration lane**
- Add a clearer boundary between:
  - portable manifest state,
  - optional spatial overlay metadata,
  - runtime-only presence state,
  - authoring/tooling artifacts.

2. **Add one deeper example**
- Add a non-normative example showing nested composition:
  - parent fabric,
  - parcel or attachment context,
  - subordinate fabric pointer,
  - consent effect on discoverability.

3. **Add one deeper proof artifact**
- Add either:
  - a fixture/journey for attachment-point composition, or
  - a fixture/journey for asset-profile / external scene-package declaration.

## Suggested primary sources for the refresh

These are the most obvious next primary-source targets surfaced by the wiki audit:
- current RP1/MSF repositories or implementation docs behind the object model and attachment workflows,
- the Manifolder repository: [PatchedReality/Manifolder](https://github.com/PatchedReality/Manifolder)
- its technical docs: [docs/README.md](https://github.com/PatchedReality/Manifolder/blob/main/docs/README.md)
- Khronos primary sources for glTF profile references when asset constraints are discussed,
- OGC primary sources if the project wants to make any real GeoPose-specific claim,
- W3C DID primary sources if the RP1 lane later makes portable-identity specifics more explicit.

## Final conclusion

`omb.wiki` does contain meaningful spatial-fabric detail not currently reflected in the project’s localized RP1 source set.

However:
- it does **not** show that Universal Manifest needs a core contract change,
- it does **not** invalidate the current pointer/shard/consent overlay approach,
- it **does** show that the project’s spatial-fabric knowledge corpus should be refreshed from additional primary sources before further RP1/MSF integration decisions are made.

The strongest outcome from this audit is:
- keep the current UM architectural boundary,
- treat the wiki as a discovery map,
- refresh primary sources next,
- only then refresh RP1/MSF documentation and proof artifacts.
