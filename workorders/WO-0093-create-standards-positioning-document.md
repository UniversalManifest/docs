# WO-0093 — Create Standards Positioning Document

**Status:** COMPLETED
**Created:** 2026-03-01
**Completed:** 2026-03-01
**Priority:** P0 (Critical)
**Source:** Project Completeness and Vision Audit (2026-03-01), Gaps 10, 11, 13, 20, 21, Recommended Actions P0-3
**Tags:** [docs], [site]
**Blocks:** Credibility with standards bodies and formal evaluators
**Dependencies:** None
**Estimated effort:** 4-6 hours

## Objective

Create a standards positioning document that explicitly explains UM's relationship to formal standards processes, adjacent standards, and standards bodies. This document should exist both as a repo document and as a published site page.

## Why this work matters

The completeness audit found that UM has no dedicated document explaining its relationship to formal standards processes. The governance document describes UM as "a standards-track specification" but does not explain which standards track or body. References to W3C, IETF, OMA3, and the Metaverse Standards Forum are scattered across multiple files with no single authoritative positioning statement.

## Scope

### New files to create

1. **`docs/STANDARDS-POSITIONING.md`** — Repo-level document
2. **`site/src/content/docs/about/standards-positioning.md`** — Published site page

### Content to cover

1. **Standards UM builds on:** JSON-LD (W3C), DIDs (W3C), Verifiable Credentials (W3C), JCS/RFC 8785 (IETF), Ed25519, `.well-known`/RFC 8615 (IETF)

2. **How UM relates to adjacent efforts:**
   - W3C Verifiable Credentials — "VCs are individual claims. UM is a container that can carry VCs alongside other data."
   - DIDComm — messaging protocol vs. document format
   - Solid Pods — storage mechanism vs. document specification
   - OIDC — authentication vs. state portability
   (Content available in `docs/explainers/full-briefing.md` competitive positioning section)

3. **Relationship to standards bodies:**
   - Metaverse Standards Forum (MSF) — MUM lineage, current relationship status
   - OMA3 / OMATrust — active integration lane, assessment report, current status
   - W3C — standards UM builds on, potential future engagement
   - IETF — RFCs used, no active engagement
   - Linux Foundation — documentation model influence

4. **Standardization intent:** Whether/when/how the project intends to engage with formal standards bodies. Currently the gap analysis report lists this as "D.8 Formal standards body submission (if desired)" with "(if desired)" indicating the decision has not been made. This document should make the current position explicit.

## Acceptance criteria

- [ ] Standards positioning document exists in both `docs/` and on the public site.
- [ ] All five standards bodies mentioned in the project (MSF, OMA3, W3C, IETF, LF) are addressed.
- [ ] UM's relationship to at least 4 adjacent standards (VCs, DIDComm, Solid, OIDC) is clearly articulated.
- [ ] The current standardization intent is explicitly stated (even if the answer is "undecided").
- [ ] `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` succeeds.

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- Manual review of document completeness against the five standards bodies.
