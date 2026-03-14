# WO-0086 — Add Spec-vs-Implementation Language Guidelines and Agent Boundary Awareness

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Spec-vs-Implementation Boundary Audit (2026-03-01), Recommendations R7, R9, R10, Action Items 8-9
**Tags:** [docs], [onboarding]
**Blocks:** Consistent messaging across all future documentation
**Dependencies:** None
**Estimated effort:** 2-3 hours

## Objective

Establish canonical language guidelines for the spec-vs-implementation distinction and add boundary-awareness instructions to agent-facing and contributor-facing documentation.

## Why this work matters

Without explicit language guidelines, new documentation naturally drifts toward implementation-flavored language ("the implementation," "the validator," "npm test"). Adding a reference table and explicit agent instructions prevents this drift in all future writing.

## Scope

### 1. Add language guideline table to PROJECT-RULES.md

Add a "Spec-vs-Implementation Language" section to `PROJECT-RULES.md` with the following table:

| Context | Use | Avoid |
|---------|-----|-------|
| Referring to the spec | "the specification," "the UM spec," "the standard" | "the library," "the package," "our implementation" |
| Referring to the TS helper | "the TypeScript reference implementation," "one reference implementation" | "the implementation," "the validator," "the UM library" |
| Describing validation | "conformance testing," "fixture validation" | "npm test" (without qualifying that this is the TS helper) |
| Describing what UM is | "a specification," "a portable document format standard" | "a TypeScript library," "a product," "our platform" |
| In spec text | "Implementations MUST..." or "Consumers MUST..." | "The package does..." or "Run npm test to verify..." |
| In integration guidance | "Any conformant implementation can..." | "Use the packages/universal-manifest helper to..." |

### 2. Add agent boundary-awareness instruction to PROJECT-RULES.md

Add to the "Agent-Specific Instructions" section:

> When producing documentation or user-facing content, always frame Universal Manifest as a specification first. Reference the TypeScript helper only as "one reference implementation" or "the TypeScript reference implementation." Never imply that adopters must use TypeScript, npm, or the packages in this repo.

### 3. Add "For implementers in other languages" callout

Add a callout to `site/src/content/docs/getting-started/quick-start.md`:

> The examples on this page use the TypeScript reference implementation for convenience. You can implement the same validation logic in any language. The specification, conformance requirements, and fixtures are language-neutral. Start with the conformance page for a language-independent implementation checklist.

## Acceptance criteria

- [ ] PROJECT-RULES.md contains the language guideline table.
- [ ] PROJECT-RULES.md agent instructions include boundary-awareness directive.
- [ ] Quick Start page includes the "For implementers in other languages" callout.
- [ ] Language guidelines are clear enough that an AI agent reading them would produce spec-first documentation.

## Validation commands

- `rg -n "specification first" PROJECT-RULES.md`
- `rg -n "other languages" site/src/content/docs/getting-started/quick-start.md`
