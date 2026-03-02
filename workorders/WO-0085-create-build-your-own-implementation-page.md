# WO-0085 — Create "Build Your Own Implementation" Page for the Docs Site

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Spec-vs-Implementation Boundary Audit (2026-03-01), Recommendation R11, Action Item 7; Project Completeness Audit, Gap 5
**Tags:** [site], [docs], [onboarding]
**Blocks:** Multi-implementation adoption pathway
**Dependencies:** None (can start immediately; coordinates with WO-0084 sidebar restructure)
**Estimated effort:** 3-5 hours

## Objective

Create a new page at `site/src/content/docs/getting-started/implement.md` that provides a language-neutral implementation checklist for developers who want to build a UM implementation in any language.

## Why this work matters

There is currently no single page that tells a developer "here is how to build a UM implementation from scratch in your language of choice." The Quick Start and Concepts pages describe what UM is, but do not provide a language-neutral implementation path. The TypeScript helper is the only implementation shown, reinforcing the perception that UM requires TypeScript.

## Scope

### New file

**`/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/implement.md`**

### Content to include

1. **Language-neutral implementation checklist** — distilled from conformance requirements:
   - Parse a JSON-LD manifest
   - Validate required fields (`@context`, `@type`, `id`, `issuer`, `subject`, `issuedAt`, `ttl`)
   - Handle unknown fields (preserve and ignore)
   - Enforce TTL (time-to-live)
   - (v0.2) JCS canonicalization
   - (v0.2) Ed25519 signature verification
2. **Links to spec artifacts** — JSON Schema, JSON-LD context, conformance documents
3. **Links to conformance fixtures** — valid and invalid examples in `examples/`
4. **Note about the TypeScript helper** — available as a reference but not required
5. **"For implementers in other languages" callout** (from Recommendation R9)

### Cross-linking

- Link from Quick Start page
- Link from Concepts page
- Link from site landing page
- Link from conformance pages

## Acceptance criteria

- [ ] Page exists at the expected URL path.
- [ ] Implementation checklist covers both v0.1 and v0.2 requirements.
- [ ] No TypeScript-specific code is presented as the only way to implement.
- [ ] Links to JSON Schema, JSON-LD context, and fixtures are correct and functional.
- [ ] At least 3 other site pages link to this new page.
- [ ] `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` succeeds.

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- Manual review of the new page content.
- Check cross-links from Quick Start, Concepts, and landing page.
