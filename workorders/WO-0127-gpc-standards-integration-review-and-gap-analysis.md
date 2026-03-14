# WO-0127 — GPC Standards Integration Review and Gap Analysis (Three-Draft Pipeline)

**Status:** COMPLETED  
**Created:** 2026-03-05  
**Updated:** 2026-03-05  
**Priority:** P0  
**Owner:** Standards + Integration Architecture  
**Source:** User directive to evaluate W3C Global Privacy Control (`https://www.w3.org/TR/gpc/`) for direct integration/adoption in Universal Manifest

## Objective

Produce an exceptionally detailed, implementation-oriented assessment of the W3C Global Privacy Control (GPC) standard and determine exactly how Universal Manifest should integrate it, including overlap analysis, gap analysis, replacement candidates, and direct embedding options (including whether GPC should be modeled as a facet vs consent/signal layer).

## Problem Statement

Universal Manifest has strong consent and privacy signaling capabilities, but there is not yet a formal standards-aligned integration review for GPC. Without this, we risk either duplicating concepts already standardized by GPC or failing to align with emerging globally recognized mechanisms and their normative dependencies.

## Scope

In scope:

- Comprehensive review of W3C GPC spec text and all normative references.
- Detailed overlap/gap matrix between GPC semantics and current UM artifacts.
- Evaluation of direct integration patterns:
  - HTTP/runtime signal handling alignment (`Sec-GPC`, `navigator.globalPrivacyControl` semantics).
  - UM document-layer representation options.
  - Facet model option vs consent/claim/pointer model option.
- Explicit recommendation on what should replace or supersede existing UM concepts (if any).
- Drafting a final third-version synthesis with gaps closed and additional research where needed.

Out of scope:

- Immediate normative spec changes in `spec/v0.1` or `spec/v0.2` without explicit promotion decision.
- Legal advice; legal references are implementation context only.

## Required three-draft workflow

1. **Draft V1 (Primary Review)**
   - Complete deep reading of `https://www.w3.org/TR/gpc/`.
   - Extract key requirements, edge conditions, and protocol semantics.
   - Produce first integrated UM mapping.

2. **Draft V2 (Secondary Background Review)**
   - Independent background-agent review of V1.
   - Challenge assumptions, identify omissions, and tighten standards mapping.

3. **Draft V3 (Gap-Closed Final Review)**
   - Reconcile V1+V2 differences.
   - Execute targeted additional research for unresolved gaps.
   - Produce final comprehensive review with explicit integration recommendation set.

## Deliverables

Primary deliverables (all required):

1. V1 comprehensive review:
   - `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-review-v1-primary.md`
2. V2 secondary review:
   - `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-review-v2-secondary.md`
3. V3 final gap-closed review:
   - `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-review-v3-gap-closed.md`

Supporting deliverables:

4. Normative reference crosswalk:
   - `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-normative-reference-crosswalk.md`
5. UM artifact overlap index:
   - `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-um-overlap-and-gap-matrix.md`
6. Integration options decision memo (including facet vs non-facet recommendation):
   - `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-integration-options-and-recommendation.md`

Optional implementation-ready outputs (if confidence is high):

7. Draft non-normative integration lane:
   - `integrations/gpc-global-privacy-control.md`
8. Site mirror draft:
   - `site/src/content/docs/integrations/gpc-global-privacy-control.md`

## Core review questions (must be answered explicitly)

- What is GPC precisely, at transport/runtime/behavioral levels?
- Where does UM already overlap with GPC semantics?
- Where are UM gaps relative to GPC?
- Where does GPC leave gaps that UM can fill?
- Should any current UM concepts be replaced by GPC-aligned concepts?
- Can GPC be directly integrated as a facet, and should it?
- If not facet-first, what is the preferred UM representation and why?
- What migration path minimizes disruption and avoids semantic drift?

## Key source set

Primary standard:

- `https://www.w3.org/TR/gpc/` (W3C Working Draft, 2026-02-19)

Normative references listed by GPC:

- RFC5234 (ABNF)
- WHATWG HTML
- W3C Privacy Principles
- RFC2119 / RFC8174
- RFC3339
- RFC8259 (JSON)
- RFC8615 (Well-Known URIs)
- W3C WebDriver
- WHATWG Web IDL

Relevant UM context anchors:

- `spec/v0.1/README.md`
- `spec/v0.1/CONFORMANCE.md`
- `spec/v0.1/REGISTRY.md`
- `spec/v0.2/README.md`
- `spec/v0.2/CONFORMANCE.md`
- `spec/v0.2/SIGNATURE-PROFILE.md`
- `docs/security/THREAT-MODEL.md`
- `integrations/data-firewall-ux.md`
- `integrations/metaverse.md`

## Acceptance criteria

- [x] All three review drafts (V1, V2, V3) are completed and materially different where expected.
- [x] V3 includes explicit closure of every identified V2 gap.
- [x] Normative reference crosswalk is complete and includes implications for UM architecture.
- [x] Explicit recommendation provided for facet vs non-facet GPC integration.
- [x] Replacement/supersession candidates in UM are listed with rationale and risk.
- [x] Deliverables are fully contained in `.dev/ai/reports/gpc-wo-0127/`.

## Execution notes

- This work order is explicitly detail-first and should prioritize completeness over brevity.
- Secondary review must be independent and should actively challenge assumptions from V1.
- Any unresolved uncertainty in V2 must trigger targeted additional research before V3 is finalized.

## Execution progress log

- 2026-03-05: Draft V1 completed (primary standards interpretation and initial recommendation).
  - `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-review-v1-primary.md`
- 2026-03-05: Normative reference crosswalk completed.
  - `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-normative-reference-crosswalk.md`
- 2026-03-05: UM overlap/gap matrix completed.
  - `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-um-overlap-and-gap-matrix.md`
- 2026-03-05: Integration options memo completed (including facet vs non-facet decision path).
  - `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-integration-options-and-recommendation.md`
- 2026-03-05: Draft V2 completed (independent challenge pass with explicit gap list).
  - `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-review-v2-secondary.md`
- 2026-03-05: Draft V3 completed (gap closure, final recommendation, migration posture, risk register).
  - `.dev/ai/reports/gpc-wo-0127/2026-03-05-gpc-review-v3-gap-closed.md`

## Completion notes

- All required primary and supporting deliverables were produced.
- Optional implementation-ready outputs were not generated in this WO execution pass.
