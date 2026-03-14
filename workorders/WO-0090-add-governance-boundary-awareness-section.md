# WO-0090 — Add Boundary-Awareness Section to Governance Document

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P2 (Nice-to-have)
**Source:** Spec-vs-Implementation Boundary Audit (2026-03-01), Action Item 14, Finding 3.4 (GOVERNANCE.md lines 23-28)
**Tags:** [docs], [structural]
**Blocks:** None (governance clarity improvement)
**Dependencies:** None
**Estimated effort:** 1 hour

## Objective

Add a boundary-awareness section to `docs/governance/GOVERNANCE.md` that distinguishes the normative specification scope from the supplementary implementation scope within the project.

## Why this work matters

The governance document currently defines project scope as including five co-equal items: "normative specification documents, JSON schemas and validation rules, conformance test suites, reference implementations and integration guides, documentation and adoption resources" (lines 23-28). This treats all five as equally fundamental, when architecturally the first three ARE the spec and the last two are supplementary. Without hierarchy, contributors may not understand which components have normative authority.

## Scope

### File to modify

**`docs/governance/GOVERNANCE.md`** (lines 23-28)

### Changes

1. Add a hierarchy statement that distinguishes:
   - **Normative scope:** Specification documents, JSON schemas, validation rules, conformance test suites
   - **Supplementary scope:** Reference implementations, integration guides, documentation, adoption resources

2. Add a brief statement explaining that normative components define the standard, while supplementary components help implementers adopt it but do not have normative authority.

## Acceptance criteria

- [ ] GOVERNANCE.md includes a clear hierarchy between normative and supplementary project components.
- [ ] The hierarchy is consistent with the layers defined in DEPTH-AND-SCOPE.md (Layers A-E).
- [ ] A new contributor reading the governance doc understands which components define the standard vs. which support adoption.

## Validation commands

- Manual review of `docs/governance/GOVERNANCE.md`.
