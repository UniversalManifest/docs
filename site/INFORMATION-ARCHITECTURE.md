# universalmanifest.net — Information Architecture (IA)

This IA is designed to feel like “Linux Foundation-grade” documentation:

- implementer-first navigation
- clear separation of **what the spec is** vs **how to adopt it**
- stable links to versioned artifacts and conformance fixtures

This is the **standards/docs** site. Runtime UMID resolution is separate (`myum.net/{UMID}`).

## Primary audiences

1. Implementers (consumers/verifiers, issuers/signers)
2. Evaluators (does this solve my portability / local-first / interoperability problem?)
3. Maintainers (governance, change control, release process)

## Top-level navigation

- **Overview**
  - What is Universal Manifest?
  - Domain split (`universalmanifest.net` vs `myum.net`)
  - Adoption tiers and “not overbuild” boundaries
- **Getting Started**
  - Quick start (fixtures + conformance + minimal validation)
  - Concepts (manifest, facets, pointers, TTL, unknown-field behavior)
- **Specification**
  - v0.1 (schema/context, required fields, extension rules)
  - v0.2 (draft) signature profile artifacts
- **Conformance**
  - v0.1 conformance checklist
  - v0.2 conformance checklist (draft)
  - Fixtures: valid + invalid
  - How to run reference harness
- **Publishing**
  - Publishing & versioning plan
  - Releasing process
  - Artifact immutability policy
- **Integrations**
  - reference implementation integration
  - Social/profile adoption notes
- **Proof**
  - User journeys
  - Executable proof suite (journeys → tests)
  - Harness page (fixtures + resolver quick tester)
- **Governance**
  - Decisions log
  - Done-done definition + checklist + evidence pack template

## Canonical “read first” path (first-time implementer)

1. Overview → What problem is this solving?
2. Getting Started → What do I need to implement?
3. Specification v0.1 → required fields + extension rules
4. Conformance v0.1 → fixtures + harness
5. Publishing → stable URLs + versioning guarantees
6. Proof → run journeys test suite for confidence

## Source-of-truth mapping (site pages → repo docs)

The site should mirror the repo’s authoritative docs:

- `docs/README.md` (docs index)
- `docs/DOMAIN-ARCHITECTURE.md` (domain split)
- `docs/PUBLISHING-AND-VERSIONING.md` + `docs/RELEASING.md`
- `docs/DONE-DONE-DEFINITION.md` + `docs/DONE-DONE-CHECKLIST.md` + `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
- `docs/journeys/README.md` (journeys → tests)
- Spec and conformance:
  - `spec/v0.1/*`
  - `spec/v0.2/*`

