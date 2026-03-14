# Spec vs. Implementation Boundary Audit

**Date:** 2026-03-01
**Scope:** Full project audit of Universal Manifest at ``
**Purpose:** Assess how clearly the project distinguishes between "Universal Manifest as a specification" and "Universal Manifest as an implementation," and recommend concrete improvements.

---

## 1. Executive Summary

The Universal Manifest project has a **strong foundational awareness** of the spec-vs-implementation boundary. The `DEPTH-AND-SCOPE.md` document explicitly defines layers A through E from normative spec to research. Integration documents consistently include "Boundary: normative vs non-normative" sections. The domain split (`universalmanifest.net` for the standard, `myum.net` for the resolver) is architecturally sound. However, the boundary **blurs significantly** in three areas: (1) spec-directory documents reference the TypeScript helper as if it were the canonical verification path rather than one reference implementation; (2) onboarding entry points (root `README.md`, site landing page, the AI briefing) present UM as a product with a TypeScript library rather than as a specification that anyone can implement in any language; and (3) the co-location of spec artifacts and implementation code in a single repository, without strong visual or structural separation in the docs site navigation, causes readers to perceive the TypeScript helper as inseparable from the spec itself. The project already has a NOT_STARTED work order (`WO-0057`) that targets exactly this problem, confirming that the maintainers are aware of the gap. This audit provides the detailed findings that `WO-0057` Phase 1 calls for.

---

## 2. Current State of the Boundary

### 2.1 Onboarding Documents

**Files reviewed:**
- `README.md`
- `PROJECT-RULES.md`
- `docs/README.md`
- `docs/PROJECT-VISION.md`
- `docs/DEPTH-AND-SCOPE.md`
- `docs/STATE-OF-THE-PROJECT.md`
- `docs/CRITICAL-PATH.md`
- `docs/DONE-DONE-DEFINITION.md`
- `docs/UNIVERSAL-MANIFEST-BRIEFING.md`

**Assessment:** Mixed. The root `README.md` is the first thing a newcomer sees, and its "Quick start" section immediately sends the reader to `cd packages/universal-manifest && npm test`. This frames UM as "a TypeScript project you install" rather than "a specification you read and implement." The `STATE-OF-THE-PROJECT.md` correctly states "This repo is a spec + fixtures + minimal tooling project. It is not a running service" (line 8), which is good. `DEPTH-AND-SCOPE.md` is excellent -- it explicitly defines layers A through E and says "This is a spec repo, not an application" (line 29). `PROJECT-RULES.md` has a reasonable structure but its "Build, Test, and Development Commands" section (lines 43-48) lists only TypeScript/npm commands, reinforcing a single-implementation perception. `CRITICAL-PATH.md` Phase 5 says "demonstrate the spec is not 'just for reference implementation'" (line 56), showing awareness but using the legacy name "reference implementation" that leaks implementation identity into the spec context. `DONE-DONE-DEFINITION.md` is spec-first and implementation-neutral -- it is one of the cleanest documents in the repo.

**Verdict:** The deeper documents are well-positioned. The outermost onboarding surfaces (root `README.md`, `PROJECT-RULES.md`) are implementation-flavored.

### 2.2 Spec Artifacts

**Files reviewed:**
- `spec/v0.1/README.md`
- `spec/v0.1/CONFORMANCE.md`
- `spec/v0.1/REGISTRY.md`
- `spec/v0.2/README.md`
- `spec/v0.2/SIGNATURE-PROFILE.md`
- `spec/v0.2/CONFORMANCE.md`

**Assessment:** Mostly clean, with several specific leaks.

The v0.1 spec `README.md` contains a section header "ID + caching guidance (Shield / public display)" (line 49) -- "Shield" is an implementation-specific device name (NVIDIA Shield TV Pro) that has no place in spec text. The same file references `Reference implementation: /packages/universal-manifest/src/index.ts` (line 78) directly in the Security Considerations section. The v0.2 spec `README.md` also references `Reference implementation: /packages/universal-manifest/src/index.ts:272-302` (line 47) inline with normative-adjacent text. Both v0.1 and v0.2 `CONFORMANCE.md` files reference the TypeScript test harness (`packages/universal-manifest/ -> npm test`) as the "Reference harness" in their final sections.

The `REGISTRY.md` file refers to "Solid Pod URL" (line 14) in the facet name description for `canonicalProfilePointer`, which leaks a specific storage technology into what should be technology-neutral registry guidance.

The `SIGNATURE-PROFILE.md` is clean -- it describes the profile in implementation-neutral terms with a clear verifier checklist that does not assume any particular language or runtime.

**Verdict:** Spec artifacts are mostly well-written but contain isolated implementation-specific references that should be removed or qualified.

### 2.3 Implementation Code and Tooling

**Files reviewed:**
- `packages/universal-manifest/` (via docs references)
- `docs/TS-HELPER-PACKAGE.md`
- `site/src/content/docs/getting-started/typescript-helper.md`

**Assessment:** The TypeScript helper documentation is well-bounded. `TS-HELPER-PACKAGE.md` explicitly says what the package provides and does not provide, and its distribution policy section is clear that the package is private and supplementary. The site page for the TypeScript helper opens with "It is optional -- you can implement the spec in any language" (line 5), which is the right framing. However, the package name in `TS-HELPER-PACKAGE.md` still uses the legacy `@localartistnetwork/universal-manifest` scope (line 14), which embeds the origin runtime's brand into the package identity.

The `services/myum-resolver/` directory is implementation code for the resolver. It is appropriately separated from the spec directory but is not explicitly called out as "reference implementation" in the docs site navigation.

**Verdict:** Implementation artifacts are reasonably self-aware but the packaging and naming carry legacy implementation-branding artifacts.

### 2.4 Integration Guidance

**Files reviewed:**
- `integrations/reference-runtime.md`
- `integrations/social.md`
- `integrations/metaverse.md`
- `integrations/smart-glasses-ar.md`
- `integrations/rp1-spatial-fabric.md`
- `integrations/healthcare-patient-consent.md`
- `integrations/TEMPLATE.md`

**Assessment:** Strong. Every integration document includes a "Boundary: normative vs non-normative" section that clearly states the normative contract lives in `spec/` and the integration file is guidance only. The integration template (`TEMPLATE.md`) enforces this pattern for new lanes. The `reference-runtime.md` opens with "This document describes one reference implementation pattern... It is guidance, not the normative spec" (lines 1-6). The healthcare integration goes further with an explicit checklist item: "No normative language used in this non-normative document" (line 227).

Two concerns: (1) `integrations/social.md` references `packages/universal-manifest -> npm run journeys` (line 34) as "Executable proof (cross-runtime adopter)," which frames a TypeScript command as the proof mechanism for a spec-level claim. (2) `integrations/TEMPLATE.md` instructs template users to "run `assertUniversalManifestV01` from the `packages/universal-manifest` test harness" (line 122), making the TypeScript helper the default validation path for new integration authors.

**Verdict:** Integration documents are the strongest area for boundary clarity. Minor TypeScript-specific references need qualification.

### 2.5 Teaching Materials and Explainers

**Files reviewed:**
- `docs/teaching-scripts/README.md`
- `docs/explainers/one-pager.md`
- `docs/explainers/paragraph.md`
- `docs/explainers/agent-briefing.md`
- `docs/UNIVERSAL-MANIFEST-BRIEFING.md`

**Assessment:** The teaching scripts directory is well-designed and spec-first -- it explicitly says "Abstract the spec. A viewer should understand what Universal Manifest does without knowing that it uses JSON-LD, Ed25519, or JCS" (line 84). The one-pager and paragraph explainers are spec-level descriptions with no implementation leakage.

The `agent-briefing.md`, however, leads with the npm package name and TypeScript validation library in the Key Facts section (line 20-22) and positions them alongside the spec site and resolver as if they are equally fundamental components of what UM "is." The "For Developers" positioning statement (line 51) says "The TypeScript helper library handles validation" as the primary developer value proposition, rather than presenting the spec and fixtures as the primary contract with the TypeScript helper as one optional tool.

The `UNIVERSAL-MANIFEST-BRIEFING.md` is the most comprehensive briefing and is largely spec-first, but it includes specific implementation examples (NVIDIA Shield TV Pro as a display device in example fixture, line 234; "example.pod.provider" in fixture URLs, line 229) that embed implementation context into what reads like normative specification text.

**Verdict:** Teaching materials at the abstract level are excellent. Detailed briefings and agent-facing materials blur the line by featuring the TypeScript package prominently.

### 2.6 Site Content (universalmanifest.net)

**Files reviewed:**
- `site/src/content/docs/index.md`
- `site/src/content/docs/getting-started/universal-manifest-overview.md`
- `site/src/content/docs/getting-started/concepts.md`
- `site/src/content/docs/getting-started/quick-start.md`
- `site/src/content/docs/getting-started/typescript-helper.md`
- `site/src/content/docs/spec/v0.1.md`
- `site/src/content/docs/spec/v0.2.md`
- `site/src/content/docs/integrations/index.md`
- `site/src/content/docs/integrations/reference-runtime.md`
- `site/src/content/docs/conformance/resolver.md`
- `site/src/content/docs/publishing/domain-split.md`

**Assessment:** The site landing page (`index.md`) does not include any statement that UM is a specification implementable in any language. It positions UM as "a portable document format" (line 6), which is neutral but does not affirmatively communicate the spec-vs-implementation distinction. The TypeScript helper is not mentioned on the landing page, which is good. However, the "Choose a starting path" section (lines 43-60) includes "Tools" for the workbench and harness but does not distinguish between spec-reading paths and implementation-specific paths.

The `getting-started/universal-manifest-overview.md` is well-written and spec-first. The "Current integration targets" section (lines 39-46) correctly says "These are integration guidance for specific use cases, not additional requirements imposed by the spec." The `concepts.md` page is clean and implementation-neutral. The `quick-start.md` page is also clean, though it links to the TypeScript helper without mentioning that implementations in other languages are equally valid.

The site navigation structure groups the TypeScript helper under "Getting Started," which implies it is a prerequisite for getting started rather than one optional tool. A reader following the natural navigation sequence encounters the TypeScript package as part of the core onboarding path.

The conformance pages (`v0.1.md`, `v0.2.md`) are spec-level and language-neutral. The resolver conformance page is explicitly "implementation-grade" (line 14), meaning it is written so that anyone can build a conforming resolver.

The integration catalog (`integrations/index.md`) is one of the strongest documents for boundary clarity: it opens with "Each integration lane is non-normative guidance" (line 10) and provides a template-driven contribution process.

**Verdict:** The site content is generally well-positioned but lacks an explicit "UM is a specification, not a library" statement on key entry points. The navigation structure does not clearly separate spec content from implementation content.

### 2.7 Governance and Decisions

**Files reviewed:**
- `docs/DECISIONS.md`
- `docs/governance/GOVERNANCE.md`

**Assessment:** `DECISIONS.md` explicitly records the decision to keep the repo separate from the reference implementation (2026-02-11, line 7-8), to keep the TS helper private to avoid "public SDK drift" (2026-02-17, line 125-137), and to relocate the repo to reduce "reference implementation/UM context bleed" (2026-02-17, line 164-173). These decisions show strong architectural awareness.

`GOVERNANCE.md` defines the project scope as "a standards-track specification" (line 21) but then lists "Reference implementations and integration guides" (line 26) as part of the project scope without clarifying that these are supplementary to the spec. The phrasing "the project includes: normative specification documents, JSON schemas and validation rules, conformance test suites, reference implementations and integration guides, documentation and adoption resources" (lines 23-28) treats all five items as co-equal components, when architecturally the first three are the spec and the last two are implementation/guidance.

**Verdict:** Decision records are strong. Governance framing is slightly implementation-inclusive without hierarchy.

---

## 3. Specific Findings

### 3.1 Implementation Details in Spec Documents

| File | Location | Issue | Severity |
|------|----------|-------|----------|
| `spec/v0.1/README.md` | Line 49, section header | "ID + caching guidance (Shield / public display)" -- "Shield" is NVIDIA Shield, an implementation-specific device | HIGH |
| `spec/v0.1/README.md` | Line 78 | "Reference implementation: `/packages/universal-manifest/src/index.ts`" inline in Security Considerations | HIGH |
| `spec/v0.1/CONFORMANCE.md` | Line 61 | "Consumers SHOULD follow `integrations/reference-runtime.md` guidance" -- conformance doc should not reference a specific implementation's guidance | MEDIUM |
| `spec/v0.1/CONFORMANCE.md` | Lines 131-135 | "Reference harness (repo-local)" section directs to `packages/universal-manifest/ -> npm test` | MEDIUM |
| `spec/v0.1/REGISTRY.md` | Line 14 | "often a Solid Pod URL" -- names a specific storage technology in registry guidance | LOW |
| `spec/v0.2/README.md` | Line 47 | "Reference implementation: `/packages/universal-manifest/src/index.ts:272-302`" with line numbers | HIGH |
| `spec/v0.2/CONFORMANCE.md` | Lines 96-98 | "Reference harness" section points to TS package | MEDIUM |

### 3.2 Onboarding Framing Issues

| File | Location | Issue | Severity |
|------|----------|-------|----------|
| `README.md` | Lines 17-23 | "Quick start" immediately shows `cd packages/universal-manifest && npm test` as the first thing to do | HIGH |
| `README.md` | Entire file | No statement that UM is a specification implementable in any language | HIGH |
| `site/src/content/docs/index.md` | Entire file | No "UM is a specification" callout on the docs site landing page | HIGH |
| `PROJECT-RULES.md` | Lines 43-48 | "Build, Test, and Development Commands" lists only npm/TS commands | MEDIUM |
| `docs/explainers/agent-briefing.md` | Lines 20-22 | npm package listed alongside the spec site and resolver in "Key Facts" as co-equal | MEDIUM |
| `docs/explainers/agent-briefing.md` | Line 51 | "The TypeScript helper library handles validation" as the developer value proposition | MEDIUM |

### 3.3 Cross-Contamination in Integration and Proof Documents

| File | Location | Issue | Severity |
|------|----------|-------|----------|
| `integrations/social.md` | Line 34 | Points to TS package as "Executable proof (cross-runtime adopter)" | MEDIUM |
| `integrations/TEMPLATE.md` | Line 122 | Instructs authors to use TS helper for validation: "run `assertUniversalManifestV01` from the `packages/universal-manifest` test harness" | MEDIUM |
| `integrations/rp1-spatial-fabric.md` | Line 11 | References TS journey runner script as source status evidence | LOW |

### 3.4 Navigation and Structural Issues

| File / Area | Issue | Severity |
|-------------|-------|----------|
| Site sidebar navigation | TypeScript Helper is under "Getting Started" alongside spec-level content, suggesting it is a prerequisite rather than one optional tool | MEDIUM |
| Site sidebar navigation | No "Implementations" or "Reference Implementation" section separate from spec content | HIGH |
| `docs/governance/GOVERNANCE.md` | Lines 23-28: "The project includes: ... Reference implementations and integration guides" without hierarchy | LOW |

### 3.5 Legacy Naming and Branding Leaks

| File | Location | Issue | Severity |
|------|----------|-------|----------|
| `docs/TS-HELPER-PACKAGE.md` | Line 14 | Package name still uses `@localartistnetwork/universal-manifest` | MEDIUM |
| `docs/UNIVERSAL-MANIFEST-BRIEFING.md` | Line 234 | Fixture example mentions "NVIDIA Shield TV Pro enrolled to venue edge" in what reads like normative example text | LOW |
| `site/src/content/docs/governance/decisions.md` | Line 18 | "Device caching + logging (public display / Shield)" -- implementation brand name in governance page | LOW |

---

## 4. What Is Already Good

Several areas demonstrate strong and deliberate spec-vs-implementation separation:

### 4.1 DEPTH-AND-SCOPE.md: The Gold Standard

`docs/DEPTH-AND-SCOPE.md` is the single best document in the repo for boundary clarity. It explicitly defines five layers (A through E) from normative spec to research, states "This is a spec repo, not an application" (line 29), and provides an adoption-tier model (Tiers 0-4) that is entirely language-neutral. Every other document in the project should be measured against this standard.

### 4.2 Integration Document Pattern

The `integrations/` directory consistently uses a "Boundary: normative vs non-normative" header pattern. Every integration document states that normative authority lives in `spec/` and `conformance/`. The integration template enforces this for new contributions. This is a well-designed, scalable pattern.

### 4.3 Integration Catalog on the Site

`site/src/content/docs/integrations/index.md` opens with the strongest spec-vs-implementation framing on the entire site: "Each integration lane is non-normative guidance. The core specification stays the same regardless of domain."

### 4.4 Domain Split Architecture

The `universalmanifest.net` / `myum.net` domain split is architecturally sound and well-documented. `DOMAIN-ARCHITECTURE.md` and the site's domain-split page clearly explain why specification hosting and runtime resolution are separate concerns.

### 4.5 Decision Records

`docs/DECISIONS.md` contains explicit decisions about:
- Keeping the spec repo separate from the reference implementation (2026-02-11)
- Not publishing the TS helper to npm yet to avoid "public SDK drift" (2026-02-17)
- Relocating the repo to reduce "reference implementation/UM context bleed" (2026-02-17)
- `CON-UM-006`: "standards-neutral framing boundaries" as a resolved conflict (2026-02-19)

### 4.6 DONE-DONE Framework

The done-done framework (`DONE-DONE-DEFINITION.md`, `DONE-DONE-CHECKLIST.md`) is entirely spec-first. Its Gate G4 (Interoperability proof) explicitly requires evidence that is NOT limited to the origin runtime. The maturity targets are defined in terms of independent implementations, not in terms of any single codebase.

### 4.7 Conformance Documents as Spec-Level Contracts

The conformance pages for both v0.1 and v0.2 are written as language-neutral behavioral contracts. They define what consumers and issuers MUST do in terms of behavior, not in terms of any API or library call. The v0.2 verifier checklist is a model example of implementation-neutral spec writing.

### 4.8 Teaching Scripts Philosophy

The teaching-scripts README explicitly says "Abstract the spec" and "A viewer should understand what Universal Manifest does without knowing that it uses JSON-LD, Ed25519, or JCS." This is the right philosophy for maintaining the boundary in user-facing educational content.

### 4.9 STATE-OF-THE-PROJECT Origin-Runtime Section

`docs/STATE-OF-THE-PROJECT.md` lines 316-322 include a "Notes on origin-runtime relationship" section that explicitly says "the reference implementation is a primary design driver, but the project goal is broader" and explains why implementation specifics live in `integrations/`, not `spec/`. This is exactly the kind of clarification that should be more prominent.

### 4.10 WO-0057 Already Exists

Work order WO-0057 ("Spec-vs-Implementation Documentation Clarity") already identifies this exact problem with a detailed execution plan. This confirms the maintainers' awareness and provides a ready-made work structure. The present audit provides the Phase 1 deliverable that WO-0057 calls for.

---

## 5. Recommendations

### 5.1 Document-Level Changes (Labels, Headers, Disclaimers)

**R1. Add "UM is a specification" banner to the three highest-traffic entry points.**

The following files need an explicit statement that UM is a specification implementable in any language:

- `README.md` (root README)
- `site/src/content/docs/index.md` (site landing page)
- `spec/v0.1/README.md` (v0.1 spec entry)
- `spec/v0.2/README.md` (v0.2 spec entry)

Suggested standard language (adapted from WO-0057):

> Universal Manifest is an open specification for portable state capsules. It is not tied to any particular programming language, framework, or runtime. The TypeScript helper in this repository is one reference implementation; you can build a conformant implementation in any language using the published spec artifacts and conformance fixtures.

**R2. Remove implementation-specific device names from spec documents.**

The section header "ID + caching guidance (Shield / public display)" in `spec/v0.1/README.md` should be changed to "ID + caching guidance (constrained devices / public displays)".

**R3. Qualify or move "Reference implementation" pointers in spec documents.**

The inline references to `/packages/universal-manifest/src/index.ts` in `spec/v0.1/README.md` and `spec/v0.2/README.md` should be either:
- Moved to a separate "Reference Implementation Notes" section clearly marked as non-normative, or
- Replaced with a note like "See the conformance fixtures for validation examples. A TypeScript reference implementation is available in `packages/universal-manifest/` for those who want one."

**R4. Remove the SHOULD reference to `integrations/reference-runtime.md` from `spec/v0.1/CONFORMANCE.md`.**

Line 61 of the v0.1 conformance doc says "Consumers SHOULD follow `integrations/reference-runtime.md` guidance." A conformance document should not direct implementers to a specific implementation's guidance with SHOULD language. Replace with: "See `integrations/reference-runtime.md` for one reference implementation pattern (non-normative)."

### 5.2 Structural Changes

**R5. Restructure the docs site sidebar to separate spec from implementation.**

Current structure groups the TypeScript helper under "Getting Started." Recommended structure:

```
Getting Started
  What Is Universal Manifest?
  Concepts
  Quick Start
  Stub Manifests

Specification
  v0.1
  v0.2 (draft)

Conformance
  v0.1
  v0.2
  Resolver

Integrations
  (all integration lanes)

Tools & Reference Implementation
  TypeScript Helper (reference implementation)
  Manifest Workbench
  Verification Harness

Publishing
  (existing publishing pages)

Proof
  (existing proof pages)

Governance
  (existing governance pages)
```

This makes the TypeScript helper explicitly a "tool" or "reference implementation" rather than a core onboarding prerequisite.

**R6. Restructure root README to lead with the spec, not the TypeScript package.**

The root README's "Quick start" section should lead with:
1. Read the v0.1 specification
2. Review example manifests (fixtures)
3. Read the conformance requirements

Then, optionally:
4. Try the TypeScript reference implementation (if using TypeScript/JavaScript)

Currently it leads with `cd packages/universal-manifest && npm test`, which frames the TS helper as the starting point.

### 5.3 Language Guidelines

**R7. Establish canonical language for the spec-implementation distinction.**

Add the following language-guideline section to `PROJECT-RULES.md`:

| Context | Use | Avoid |
|---------|-----|-------|
| Referring to the spec | "the specification," "the UM spec," "the standard" | "the library," "the package," "our implementation" |
| Referring to the TS helper | "the TypeScript reference implementation," "one reference implementation" | "the implementation," "the validator," "the UM library" |
| Describing validation | "conformance testing," "fixture validation" | "npm test" (without qualifying that this is the TS helper) |
| Describing what UM "is" | "a specification," "a portable document format standard" | "a TypeScript library," "a product," "our platform" |
| In spec text | "Implementations MUST..." or "Consumers MUST..." | "The package does..." or "Run npm test to verify..." |
| In integration guidance | "Any conformant implementation can..." | "Use the packages/universal-manifest helper to..." |

**R8. Replace "Shield" with "constrained device" or "public display" in all spec-adjacent text.**

The word "Shield" (referring to NVIDIA Shield TV Pro) should not appear in any `spec/` document. It is appropriate in `integrations/reference-runtime.md` and fixture descriptions.

### 5.4 Onboarding Changes

**R9. Add a "For implementers in other languages" callout to the Quick Start page.**

`site/src/content/docs/getting-started/quick-start.md` should include a note after the spec-reading section:

> The examples on this page use the TypeScript reference implementation for convenience. You can implement the same validation logic in any language. The specification, conformance requirements, and fixtures are language-neutral. Start with the [conformance page](/conformance/v01/) for a language-independent implementation checklist.

**R10. Update `PROJECT-RULES.md` Agent-Specific Instructions to include boundary awareness.**

The "Agent-Specific Instructions" section should include an instruction like:

> When producing documentation or user-facing content, always frame Universal Manifest as a specification first. Reference the TypeScript helper only as "one reference implementation" or "the TypeScript reference implementation." Never imply that adopters must use TypeScript, npm, or the packages in this repo.

### 5.5 Site Content Changes

**R11. Add a "Build Your Own Implementation" page.**

Create a new page at `site/src/content/docs/getting-started/implement.md` that provides:
- A language-neutral implementation checklist (distilled from conformance)
- Links to the spec artifacts (JSON Schema, JSON-LD context)
- Links to the conformance fixtures
- A note that the TypeScript helper is available as a reference but is not required

This page should be linked from the Quick Start, the Concepts page, and the site landing page.

**R12. Qualify the TypeScript helper page title in the sidebar.**

Change the sidebar label from "TypeScript Helper" to "TypeScript Helper (Reference)" or move it to a "Tools & Implementations" section to avoid the impression that it is part of the core spec.

### 5.6 Specific Text Fixes

**R13. Fix `spec/v0.1/REGISTRY.md` line 14.**

Change "Pointer to canonical identity/profile source (often a Solid Pod URL)" to "Pointer to canonical identity/profile source (any stable URL)."

**R14. Fix `integrations/TEMPLATE.md` line 122.**

Change "run `assertUniversalManifestV01` from the `packages/universal-manifest` test harness" to "validate against the v0.1 JSON Schema. If using the TypeScript reference implementation, run `assertUniversalManifestV01`."

**R15. Fix `docs/explainers/agent-briefing.md` Key Facts section.**

Move the npm package from the "Key Facts" section to a separate "Reference Implementation" section lower in the document, so it is not co-equal with the spec site and resolver.

---

## 6. Proposed Action Items

Prioritized from highest to lowest impact. Each item is tagged with its primary domain.

### Priority 1: Critical (blocks external perception)

1. **[docs]** Add "UM is a specification" banner to root `README.md`, site landing page (`index.md`), and both spec README files (`spec/v0.1/README.md`, `spec/v0.2/README.md`). Use the standard language from R1.

2. **[spec]** Remove the "Shield" device name from `spec/v0.1/README.md` line 49 section header. Replace with "constrained devices / public displays."

3. **[spec]** Remove or qualify inline `Reference implementation: /packages/universal-manifest/src/index.ts` references in `spec/v0.1/README.md` (line 78) and `spec/v0.2/README.md` (line 47). Move to a clearly marked non-normative note.

4. **[docs]** Restructure root `README.md` Quick Start to lead with the spec and fixtures, with the TypeScript helper as an optional step.

5. **[spec]** Change the SHOULD reference to `integrations/reference-runtime.md` in `spec/v0.1/CONFORMANCE.md` (line 61) to a non-normative note.

### Priority 2: High (improves first-contact clarity)

6. **[structural]** Restructure docs site sidebar to separate "Specification" and "Conformance" from "Tools & Reference Implementation."

7. **[docs]** Add a "Build Your Own Implementation" page to the site's Getting Started section.

8. **[docs]** Add a "For implementers in other languages" callout to `getting-started/quick-start.md`.

9. **[docs]** Update `PROJECT-RULES.md` to include spec-vs-implementation language guidelines (R7) and agent boundary-awareness instructions (R10).

10. **[docs]** Reposition the npm package in `docs/explainers/agent-briefing.md` -- move it from "Key Facts" to a "Reference Implementation" section.

### Priority 3: Medium (reduces ambiguity)

11. **[spec]** Fix `spec/v0.1/REGISTRY.md` line 14: replace "often a Solid Pod URL" with "any stable URL."

12. **[implementation]** Fix `integrations/TEMPLATE.md` line 122: qualify the TypeScript-specific validation instruction.

13. **[implementation]** Qualify the `packages/universal-manifest/ -> npm test` references in `spec/v0.1/CONFORMANCE.md` (line 134) and `spec/v0.2/CONFORMANCE.md` (line 98) as "TypeScript reference harness (one of many possible implementations)."

14. **[docs]** Add boundary-awareness section to `docs/governance/GOVERNANCE.md` distinguishing the normative spec scope from supplementary implementation scope.

15. **[docs]** Qualify TypeScript references in `integrations/social.md` (line 34) and `integrations/rp1-spatial-fabric.md` (line 11) as reference-implementation-specific.

### Priority 4: Low (polish and consistency)

16. **[implementation]** Update the legacy `@localartistnetwork/universal-manifest` package name in `docs/TS-HELPER-PACKAGE.md` to the current package name.

17. **[docs]** Remove or qualify "Shield" references in `site/src/content/docs/governance/decisions.md` (line 18).

18. **[docs]** Review the briefing's fixture example that mentions "NVIDIA Shield TV Pro enrolled to venue edge" (`UNIVERSAL-MANIFEST-BRIEFING.md` line 234) -- consider whether implementation-specific device names belong in the comprehensive briefing or whether they should be replaced with generic device descriptions.

19. **[structural]** Coordinate with WO-0054 (reference implementation repository) -- when the reference implementation moves to its own repo, many of the co-location issues identified here will resolve naturally. Until then, the documentation changes above are the critical mitigation.

20. **[docs]** Add the `STATE-OF-THE-PROJECT.md` "Notes on origin-runtime relationship" text (lines 316-322) to the site landing page or the overview page, as it is the clearest statement of the spec-implementation relationship in the entire project but is buried in a status document.

---

## Appendix: Relationship to WO-0057

This audit serves as the Phase 1 deliverable for work order `WO-0057` (Spec-vs-Implementation Documentation Clarity). The findings table in Section 3 maps directly to the audit report format that WO-0057 Phase 1 calls for: "file path, line number, and proposed fix."

The action items in Section 6 can be executed as WO-0057 Phases 2 through 5, with the priority ordering in this report serving as the recommended execution sequence. Phase 2 (key entry-point messaging) corresponds to Priority 1 items. Phase 3 (code example qualification) corresponds to Priority 2-3 items. Phase 4 (navigation restructure) corresponds to Priority 2 item 6. Phase 5 (integration docs) corresponds to Priority 3 items 12 and 15.

---

## Appendix: Files Reviewed

Complete list of files read during this audit:

**Onboarding and orientation:** `README.md`, `PROJECT-RULES.md`, `docs/README.md`, `docs/PROJECT-VISION.md`, `docs/DEPTH-AND-SCOPE.md`, `docs/STATE-OF-THE-PROJECT.md`, `docs/CRITICAL-PATH.md`, `docs/DONE-DONE-DEFINITION.md`, `docs/UNIVERSAL-MANIFEST-BRIEFING.md`, `docs/ENVELOPE-TOPOLOGY.md`

**Spec artifacts:** `spec/v0.1/README.md`, `spec/v0.1/CONFORMANCE.md`, `spec/v0.1/REGISTRY.md`, `spec/v0.2/README.md`, `spec/v0.2/SIGNATURE-PROFILE.md`, `spec/v0.2/CONFORMANCE.md`

**Implementation and tooling:** `docs/TS-HELPER-PACKAGE.md`, `packages/universal-manifest/` (via references)

**Integration guidance:** `integrations/reference-runtime.md`, `integrations/social.md`, `integrations/metaverse.md`, `integrations/smart-glasses-ar.md`, `integrations/rp1-spatial-fabric.md`, `integrations/healthcare-patient-consent.md`

**Teaching and explainers:** `docs/teaching-scripts/README.md`, `docs/explainers/one-pager.md`, `docs/explainers/paragraph.md`, `docs/explainers/agent-briefing.md`

**Site content:** `site/src/content/docs/index.md`, `site/src/content/docs/getting-started/universal-manifest-overview.md`, `site/src/content/docs/getting-started/concepts.md`, `site/src/content/docs/getting-started/quick-start.md`, `site/src/content/docs/getting-started/typescript-helper.md`, `site/src/content/docs/spec/v0.1.md`, `site/src/content/docs/spec/v0.2.md`, `site/src/content/docs/integrations/index.md`, `site/src/content/docs/integrations/reference-runtime.md`, `site/src/content/docs/conformance/resolver.md`, `site/src/content/docs/publishing/domain-split.md`

**Governance:** `docs/DECISIONS.md`, `docs/governance/GOVERNANCE.md`

**Work orders:** `docs/workorders/WO-0057-spec-vs-implementation-documentation-clarity.md`

**Search patterns applied:** `Shield|NVIDIA|reference implementation` across `spec/` and `site/src/content/docs/`; `packages/universal-manifest|npm test|npm run` across `spec/` and `integrations/`; `normative|non-normative` across `site/src/content/docs/`.
