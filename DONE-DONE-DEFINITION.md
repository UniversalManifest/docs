# Universal Manifest — Official Done-Done Definition

Status: Active  
Owner: Universal Manifest maintainers  
Last updated: 2026-02-13

This document is the canonical definition of what “done done” means for the Universal Manifest standard.

It is intentionally strict. “Implemented” is not enough. “Documented” is not enough. “Tested locally” is not enough.  
A release is only done when required gates are passed with auditable evidence.

## 1) Purpose

This definition exists to prevent:

- false completion claims
- version drift between docs, fixtures, and implementation
- overbuilding features that are not ready for standardization
- underbuilding critical reliability, interoperability, and governance requirements

It also gives contributors, adopters, and reviewers the same decision framework.

## 2) What “done done” means

“Done done” means:

- the targeted scope is explicitly defined
- every required acceptance gate has objective pass criteria
- evidence exists for each gate and can be independently reviewed
- unresolved risks are either closed or formally deferred with explicit impact

If any required gate fails, the release is not done.

## 3) Scope boundaries for this definition

This definition applies to:

- `spec/` contract artifacts
- conformance requirements and fixtures
- release and governance documentation
- integration guidance required for real-world adoption

This definition does not require:

- implementing every possible integration surface
- solving all future decentralized identity and trust-distribution challenges in v0.x
- replacing adopter-specific operational systems

## 4) Maturity targets

Universal Manifest tracks three maturity targets:

### Maturity A: Early-adopter ready (v0.x)

- stable enough for controlled adoption
- explicit non-final areas are documented
- conformance baseline exists

### Maturity B: Production-candidate standard

- strong interoperability evidence across multiple independent systems
- hardened conformance suite and integrity profile
- operational publishing and governance procedures are reliable

### Maturity C: World-ready standard

- broad, independent implementation success
- hardened security and compatibility guarantees
- sustainable governance and release cadence
- low ambiguity for external implementers

“World-ready” corresponds to Maturity C.

## 5) Required acceptance gates

All required gates must pass for the target maturity level.

## Gate G1: Contract completeness

Pass criteria:

- required fields and semantics are explicitly defined
- unknown-field behavior and extension rules are explicit
- versioning and compatibility rules are explicit
- registry conventions for names are documented

Required evidence:

- versioned spec docs in `spec/`
- schema and context alignment review
- contract-change decisions recorded in `docs/DECISIONS.md`

Failure examples:

- ambiguous field semantics
- no clear extension behavior
- implicit breaking changes

## Gate G2: Conformance testability

Pass criteria:

- consumer and issuer obligations are explicit
- valid and invalid fixtures exist for required cases
- a reproducible validation harness passes expected cases and fails invalid cases

Required evidence:

- `spec/v*/CONFORMANCE.md`
- `examples/` fixture set
- test run output from package validator scripts

Failure examples:

- fixtures exist but are not mapped to requirements
- tests pass only happy path
- invalid fixtures are missing for core requirements

## Gate G3: Integrity and trust profile

Pass criteria:

- integrity signature behavior is explicitly defined for target maturity
- canonicalization assumptions are explicit for any normative signature behavior
- verification behavior for failure states is explicit

Required evidence:

- integrity profile document (for v0.x this can be staged but must be explicit)
- fixtures covering signature and verification behaviors when normative

Failure examples:

- signature exists but semantics are unspecified
- verification mismatch between docs and fixtures
- no migration path between integrity profiles

## Gate G4: Interoperability proof

Pass criteria:

- at least one independent integration path demonstrates end-to-end consumption
- cross-system examples are available for projection/pointer use
- compatibility guidance is explicit for cross-runtime adopters

Required evidence:

- integration notes under `integrations/`
- near-real fixtures representing multiple subjects/use paths
- at least one external adopter-oriented walkthrough

Failure examples:

- origin-runtime-only assumptions hardcoded into normative text
- no evidence of cross-system projection behavior

## Gate G5: Publishing and discoverability

Pass criteria:

- canonical URLs and versioning policy are documented
- release process and artifact immutability rules are documented
- docs navigation supports first-time adoption without private context

Required evidence:

- publishing/versioning docs
- release procedure docs
- docs index with clear learning path

Failure examples:

- unstable artifact URLs
- undocumented release process
- docs require insider knowledge to navigate

## Gate G6: Governance and change control

Pass criteria:

- change decisions are logged with rationale
- break/non-break classification process is explicit
- deprecation and migration policy is explicit

Required evidence:

- `docs/DECISIONS.md`
- release/change policy docs

Failure examples:

- silent contract changes
- no migration guidance for adopters

## Gate G7: Operational realism

Pass criteria:

- guidance reflects local-first and partial-connectivity realities
- cache/TTL/log reference behavior is explicit where applicable
- anti-overbuild boundaries are documented

Required evidence:

- integration docs and examples
- explicit out-of-scope list
- operational notes in state and roadmap docs

Failure examples:

- impractical assumptions about always-online behavior
- contradictory recommendations between spec and integration guidance

## 6) Required gate set by maturity target

### For Early-adopter ready (v0.x)

Required gates: G1, G2, G4, G5, G6, G7  
G3 may be staged, but scope and limitations must be explicit.

### For Production-candidate standard

Required gates: G1 through G7 all fully passed.

### For World-ready standard

Required gates: G1 through G7 passed, plus:

- multi-organization independent interoperability evidence
- documented long-term governance capacity
- explicit security posture with incident and rollback protocols
- stable release cadence and migration reliability over time

## 7) World-ready (Maturity C) additional requirements

The standard is not world-ready until all conditions below are true:

- at least three independent organizations implement the spec successfully
- at least two implementations are outside the originating origin-runtime ecosystem
- no critical unresolved ambiguity remains in normative requirements
- compatibility guarantees and migration procedures are repeatedly demonstrated
- conformance suite covers baseline, edge, and adversarial misuse cases

## 8) Evidence requirements and auditability

Every gate claim must map to evidence artifacts.

Evidence must be:

- reproducible
- path-addressable
- date-stamped
- reviewable by someone not involved in the implementation

Recommended evidence packaging:

- use `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
- include command outputs for tests and validations
- include unresolved risk register with owner and target closure date

## 9) Prohibited completion claims

It is prohibited to claim “done done” when any of the following is true:

- required gate criteria are still “to be determined”
- tests are not reproducible
- docs and fixtures disagree
- release process is not documented
- open critical risks are unowned

## 10) Release sign-off protocol

A release sign-off must include:

- target maturity level
- gate-by-gate pass/fail with evidence links
- explicit deferrals and risk impact
- approver names/roles and date

No sign-off document means no done-done claim.

## 11) Relationship to other project docs

This document is authoritative for completion criteria and should be used with:

- `docs/DONE-DONE-CHECKLIST.md`
- `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
- `docs/STATE-OF-THE-PROJECT.md`
- `docs/DEPTH-AND-SCOPE.md`
- `docs/DECISIONS.md`

## 12) Change policy for this document

Changes to done-done criteria are high-impact.

Any change must:

- be justified in `docs/DECISIONS.md`
- state who is affected (maintainers, adopters, implementers)
- include migration implications for in-flight work

This prevents moving goalposts without accountability.
