# WO-0099 — Create Standards Landscape Comparison Page for the Site

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Project Completeness and Vision Audit (2026-03-01), Gaps 3, 12, 22, Recommended Action P1-8
**Tags:** [site], [docs]
**Blocks:** Evaluator ability to understand UM's position in the ecosystem
**Dependencies:** WO-0093 (Standards Positioning Document — provides source content)
**Estimated effort:** 3-4 hours

## Objective

Publish a "Standards Landscape" or "How UM Compares" page on the public site that shows where UM fits relative to existing standards and specifications.

## Why this work matters

The completeness audit found that the competitive positioning content from `docs/explainers/full-briefing.md` is strong and well-written but exists only in an internal repo document. Evaluators comparing UM to W3C VCs, DIDComm, Solid, and OIDC currently have no public-facing resource to inform their assessment.

## Scope

### Source content

From `docs/explainers/full-briefing.md` — Competitive Positioning section comparing UM to:
- W3C Verifiable Credentials
- DIDComm
- Solid Pods
- OIDC (OpenID Connect)

### New site page

**`site/src/content/docs/about/standards-landscape.md`** (or `about/how-um-compares.md`)

### Content structure

1. **Standards UM builds on** — JSON-LD, DIDs, VCs, JCS, Ed25519
2. **Comparison table** — UM vs. W3C VCs vs. DIDComm vs. Solid vs. OIDC
   - What each solves
   - How UM complements (not replaces) each
   - Key differentiators
3. **Ecosystem diagram** — Visual showing UM's position (optional, SVG preferred)
4. **"UM is complementary"** message — UM works WITH these standards, not against them

### Sidebar integration

Add to the "About" section of the site sidebar.

## Acceptance criteria

- [ ] Standards landscape page exists on the public site.
- [ ] At least 4 adjacent standards/specs are compared to UM.
- [ ] The page clearly communicates UM's complementary (not competitive) relationship.
- [ ] A comparison table provides quick-glance differentiation.
- [ ] `cd site && npm run build:clean` succeeds.

## Validation commands

- `cd site && npm run build:clean`
- Manual review for accuracy and fair comparison.
