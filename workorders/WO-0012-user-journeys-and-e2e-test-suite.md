# WO-0012 — User journeys → executable E2E proof suite (Universal Manifest)

**Status:** COMPLETED  
**Created:** 2026-02-17

## Objective

Define a small set of **canonical user journeys** for Universal Manifest adoption, then map each journey to an **executable test** suite that can be run end-to-end to produce auditable evidence that “the Universal Manifest concept works”.

This WO exists to turn the concept from “docs + fixtures” into **proof by runnable journeys**.

## Why this matters

- “Done done” must be evidenced by runnable outputs, not prose.
- The Universal Manifest aims to be adopted by other systems; those adopters need a clear, testable path.
- LAN is a primary driver, but this proof suite must remain **UM-first** (LAN integration is one consumer).

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

1. **Issuer creates a manifest** (v0.1) with TTL, subject, shards/pointers.
2. **Consumer validates + ignores unknown fields** (forward compat).
3. **Resolver lookup** (`myum.net/{UMID}` semantics): unknown → 404; known → 200 or redirect.
4. **Device caching + logging**: cache full manifest “while in use”, persist only manifest `@id` references.
5. **Signature verification** (v0.2, after WO-0002): valid → accept; invalid → reject.
6. **Public profile projection (non-LAN adopter)**: derive a safe public view from a manifest (future social media profile surface).
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
- [x] The suite is UM-first and does not require LAN to be present, except for any explicit LAN-journey subset.
- [x] Documentation links “journeys → tests” into the done-done evidence framework.

## References

- Done-done authority:
  - `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-DEFINITION.md`
  - `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-CHECKLIST.md`
  - `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
- Domain split:
  - `/Users/grig/work/repo/universalmanifest/docs/DOMAIN-ARCHITECTURE.md`
- Conformance:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md`
- LAN implementation stubs (context only):
  - `/Users/grig/work/lan/lan-platform/.dev/ai/handoffs/2026-02-11-21-52-41Z-handoff-lan-platform-universal-manifest-stubs.md`
