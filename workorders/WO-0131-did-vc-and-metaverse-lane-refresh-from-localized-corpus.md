# WO-0131 — DID + VC and Metaverse Lane Refresh from Localized Corpus

**Status:** IN_PROGRESS  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P1  
**Owner:** Integration Documentation  
**Source:** `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-25-user-centric-pointer-protocols-2025-landscape.md`, `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-26-universal-manifest-architectures-comprehensive-analysis.md`

## Objective

Refresh the DID + VC and metaverse integration lanes so they reflect the newly localized landscape and architecture material without overcommitting to unstable or non-normative protocol choices.

## Problem Statement

The current DID + VC and metaverse lane docs are directionally correct but underspecified in three places: they do not clearly reflect the composite-stack architecture, they do not explain protocol volatility and selection boundaries strongly enough, and they do not explicitly connect local-first runtime behavior to relying-party integration expectations.

## Scope

In scope:

- Update `integrations/did-vc.md` and site mirror.
- Update `integrations/metaverse.md` and site mirror.
- Add stronger language around protocol-family examples, volatility caveats, and non-lock-in boundaries.
- Cross-link to the architecture direction established in WO-0130.

Out of scope:

- Normative registry or conformance changes.
- Runtime code changes.
- Research-first closure of unresolved federation or proximity gaps.

## Deliverables

- `/Users/grig/work/repo/universalmanifest/integrations/did-vc.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/did-vc.md`
- `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/metaverse.md`

## Acceptance Criteria

- [ ] DID + VC lane includes bounded protocol examples and explicit volatility/non-lock-in caveats.
- [ ] Metaverse lane explicitly references trust/data/interaction layering and local-first runtime assumptions.
- [ ] Site mirrors remain synchronized with repo docs.
- [ ] No new normative requirement is implied.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0130-composite-architecture-and-active-runtime-alignment.md`
