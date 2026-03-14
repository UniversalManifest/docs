# WO-0130 — Composite Architecture and Active Runtime Alignment

**Status:** COMPLETED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P0  
**Owner:** Vision + Integration Architecture  
**Source:** `.dev/ai/knowledge-corpus/imports/external-25-user-centric-pointer-protocols-2025-landscape.md`, `.dev/ai/knowledge-corpus/imports/external-26-universal-manifest-architectures-comprehensive-analysis.md`, `.dev/ai/knowledge-corpus/imports/external-27-peermesh-universal-manifest-vision.md`

## Objective

Align the repo’s source-of-truth architecture framing with the newly localized source corpus by making the composite-stack model and the local-first active-runtime/push model explicit in vision and reference-runtime documentation.

## Problem Statement

The newly localized sources reinforce a consistent architecture pattern: Universal Manifest operates as a composite stack with distinct trust, data, and interaction layers, and real deployments often require a user-controlled active runtime that handles local-first state, push/pull sync, and bridge adapters for closed surfaces. The current project docs partially imply this but do not express it clearly enough in the source-of-truth architecture documents.

## Scope

In scope:

- Update `docs/PROJECT-VISION.md` with explicit composite-stack architecture framing.
- Update `integrations/reference-runtime.md` and its site mirror with local-first source-of-truth plus active-runtime behavior.
- Add a decision record documenting the composite-stack / active-runtime direction.
- Keep all updates non-normative and spec-first.

Out of scope:

- DID/VC lane refresh details beyond foundation framing.
- Metaverse-lane specific operational refinements.
- New normative spec or conformance requirements.

## Deliverables

1. Vision/source-of-truth updates:
   - `docs/PROJECT-VISION.md`
2. Reference runtime alignment:
   - `integrations/reference-runtime.md`
   - `site/src/content/docs/integrations/reference-runtime.md`
3. Decision synchronization:
   - `docs/DECISIONS.md`
   - `site/src/content/docs/governance/decisions.md`

## Acceptance Criteria

- [x] `docs/PROJECT-VISION.md` explicitly describes the trust/data/interaction composite stack and pointer-first storage separation.
- [x] `integrations/reference-runtime.md` documents a user-controlled active runtime with local-first state and push/pull bridge behavior.
- [x] The reference-runtime site mirror stays in sync.
- [x] A decision record captures the non-normative architecture direction without changing conformance requirements.

## Dependencies

- `docs/workorders/WO-0129-universal-manifest-inbox-dedupe-import-and-archive.md`
- `.dev/ai/knowledge-corpus/imports/external-25-user-centric-pointer-protocols-2025-landscape.md`
- `.dev/ai/knowledge-corpus/imports/external-26-universal-manifest-architectures-comprehensive-analysis.md`
- `.dev/ai/knowledge-corpus/imports/external-27-peermesh-universal-manifest-vision.md`

## Execution Progress (2026-03-06)

Completed in this pass:

- Updated `docs/PROJECT-VISION.md` with:
  - composite-stack framing,
  - subject-controlled active-runtime guidance,
  - explicit pointer-first storage separation,
  - and an active-runtime loop model.
- Updated `integrations/reference-runtime.md` and its site mirror:
  - `site/src/content/docs/integrations/reference-runtime.md`
  with active-runtime, bridge-adapter, and local-first source-of-truth language.
- Added a new architecture decision record to:
  - `docs/DECISIONS.md`
  - `site/src/content/docs/governance/decisions.md`
- Verified the public docs surface still builds:
  - `cd site && npm run build:clean`

## Completion notes

- WO-0130 established the foundation needed for lane-specific follow-on work orders.
- The architecture direction remains non-normative and does not change v0.1 or v0.2 conformance behavior.
