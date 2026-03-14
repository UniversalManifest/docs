# WO-0012 — User journeys → executable E2E proof suite (Universal Manifest)

**Status:** COMPLETED  
**Created:** 2026-02-17

## Objective

Define a small set of **canonical user journeys** for Universal Manifest adoption, then map each journey to an **executable test** suite that can be run end-to-end to produce auditable evidence that “the Universal Manifest concept works”.

This WO exists to turn the concept from “docs + fixtures” into **proof by runnable journeys**.

## Why this matters

- “Done done” must be evidenced by runnable outputs, not prose.
- The Universal Manifest aims to be adopted by other systems; those adopters need a clear, testable path.
- reference implementation is a primary driver, but this proof suite must remain **UM-first** (reference implementation integration is one consumer).

## Scope

In scope:

- Define 5–10 canonical user journeys (issuer, resolver, consumer, caching/logging, revocation/removal semantics).
- For each journey:
  - Inputs (fixture(s), environment assumptions)
  - Steps
  - Expected outcomes
  - Evidence artifacts (logs, screenshots, JSON outputs)
- Implement an executable test runner that can run the full suite locally.
- Provide a debug-friendly “test harness” web page where appropriate:
  - lists stub manifests (near-real data)
  - exercises resolver-style endpoints (contract tests)
  - validates fixtures and conformance expectations

Out of scope:

- Building production apps/UI beyond the harness
- Shipping a full SDK

## Suggested journey set (starting point)

1. **Issuer creates a manifest** (v0.1) with TTL, subject, facets/pointers.
2. **Consumer validates + ignores unknown fields** (forward compat).
3. **Resolver lookup** (`myum.net/{UMID}` semantics): unknown → 404; known → 200 or redirect.
4. **Device caching + logging**: cache full manifest “while in use”, persist only manifest `@id` references.
5. **Signature verification** (v0.2, after WO-0002): valid → accept; invalid → reject.
6. **Public profile projection (cross-implementation adopter)**: derive a safe public view from a manifest (future social media profile surface).
7. **Revocation/removal semantics**: removed/revoked → 410 (or documented policy).

## Deliverables

- Journeys definition doc:
  - `docs/journeys/README.md`
  - `docs/journeys/journey-01-*.md` … `journey-0N-*.md`
- Executable test suite:
  - new `npm` script(s) documented in repo root
  - produces a simple summary report on completion
- Optional harness page:
  - `site/harness/` (or equivalent; implementation choice deferred)
  - documented usage + what it proves

## Acceptance criteria

- [x] Each journey has a single source of truth doc with steps + expected outcomes.
- [x] One command runs the complete journey suite locally and exits non-zero on failure.
- [x] Evidence artifacts are produced (at minimum: structured JSON report + logs).
- [x] The suite is UM-first and does not require reference implementation to be present, except for any explicit implementation-specific journey subset.
- [x] Documentation links “journeys → tests” into the done-done evidence framework.

## References

- Done-done authority:
  - `docs/DONE-DONE-DEFINITION.md`
  - `docs/DONE-DONE-CHECKLIST.md`
  - `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
- Domain split:
  - `docs/DOMAIN-ARCHITECTURE.md`
- Conformance:
  - `spec/v0.1/CONFORMANCE.md`
- reference implementation stubs (context only):
  - `/Users/grig/work/repo/reference-platform/.dev/ai/handoffs/2026-02-11-21-52-41Z-handoff-reference-platform-universal-manifest-stubs.md`

## Post-Completion Corpus Delta Addendum (2026-02-19T04:57:00Z)

Source linkage:
- `.dev/ai/specs/2026-02-19-ia-delta-from-full-corpus.md`
- `docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`

New planning deltas to execute under WO-0017:
- add cross-domain overlay coverage to journey planning (venue, creator/profile, metaverse exemplar),
- add identity-method variant lanes while preserving method-agnostic core assertions,
- apply sequencing rubric driven by interoperability evidence quality.

Primary execution artifact:
- `docs/journeys/README.md`
