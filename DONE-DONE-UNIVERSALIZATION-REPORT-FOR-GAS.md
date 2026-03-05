# Done-Done Universalization Report for GAS Agent

Date: 2026-02-13  
Audience: Agent building a universal "done done" process + skill in Global Agents System (GAS)  
Source project: Universal Manifest (`<repo-root>`)

## 1) Executive Summary

This project now has an explicit, auditable, gate-based definition of "done done" that can be generalized into GAS as a reusable process/skill.

Core value:

- converts subjective completion into objective gate checks
- separates maturity levels (early-adopter vs world-ready)
- requires evidence, not narrative claims
- prevents false "done" declarations

The design is intentionally domain-agnostic and can be extracted as a generic template.

## 2) Artifacts Created (Primary Inputs for GAS)

Canonical definition:

- `docs/DONE-DONE-DEFINITION.md`

Execution checklist:

- `docs/DONE-DONE-CHECKLIST.md`

Evidence/sign-off template:

- `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`

Linked project context:

- `docs/STATE-OF-THE-PROJECT.md`
- `docs/DEPTH-AND-SCOPE.md`
- `docs/DECISIONS.md`

## 3) Process Model to Reuse in GAS

Universal pattern:

1. Define maturity target (A/B/C or equivalent)
2. Enumerate required gates for that target
3. Attach objective pass criteria per gate
4. Require evidence artifacts for each gate
5. Require explicit defer/risk ownership
6. Require final sign-off record

If any required gate fails, done-done fails.

## 4) Gate Pattern (Portable)

Current gate set from this project:

- G1 Contract completeness
- G2 Conformance testability
- G3 Integrity/trust profile
- G4 Interoperability proof
- G5 Publishing/discoverability
- G6 Governance/change control
- G7 Operational realism

Portable extraction rule:

- keep gate IDs stable (`G1..Gn`)
- keep pass criteria objective and testable
- make evidence path mandatory
- separate gate definitions from project-specific examples

## 5) What to Extract Into GAS Skill

Recommended GAS skill modules:

### Module A: Definition bootstrap

- generate `DONE-DONE-DEFINITION.md` for any project from a standard scaffold
- require maturity tiers and required gates

### Module B: Checklist generator

- generate `DONE-DONE-CHECKLIST.md` from gate definitions
- enforce one-to-one mapping from gate criteria to checkbox items

### Module C: Evidence pack generator

- generate `DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
- include sign-off, deferrals, and blocking risks

### Module D: Claim validator

- reject "done" claims that do not include evidence artifacts
- flag missing gate evidence and unresolved critical risks

## 6) Adaptation Guidance (Any Project Type)

For API/spec projects:

- keep conformance and compatibility gates mandatory

For product/feature projects:

- replace contract gate with requirements/behavior gate
- retain evidence/sign-off and governance gates

For infra/devops projects:

- add reliability/SLO and incident-response gates
- keep rollout/rollback evidence mandatory

## 7) Anti-Patterns This Solves

- "Works on my machine" marked as done
- docs-only completion without verification
- tests passing but no release governance
- silent scope changes during implementation
- world-ready claims without independent interoperability evidence

## 8) Integration Points for GAS

Where this should plug into GAS flow:

- work-order completion logic
- release readiness checks
- handoff/hard-stop decisions
- QA sign-off requirements

Suggested trigger:

- any work item claiming completion above trivial size must produce a done-done evidence pack

## 9) Recommended Next Steps for GAS Agent

1. Extract a neutral "Done-Done Core" template from this project’s 3 docs.
2. Create a GAS skill that instantiates those docs in target repos.
3. Add a validator script/rule that blocks completion without evidence pack.
4. Add guidance for maturity thresholds so "world-ready" has stronger requirements than "v0.x-ready."
5. Publish a short "How to adopt Done-Done in 15 minutes" guide for agents.

## 10) Copy-Ready Minimal Contract for GAS

At minimum, universal process should enforce:

- target maturity declared
- required gates declared
- objective pass/fail criteria per gate
- evidence links per gate
- deferred items with owner/date
- explicit approval decision

Without those six elements, completion is not done-done.
