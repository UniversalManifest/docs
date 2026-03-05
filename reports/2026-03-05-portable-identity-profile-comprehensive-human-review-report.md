# Portable Identity Profile Program Report (First-Time Reviewer Edition)

Date: 2026-03-05  
Project: Universal Manifest (`/Users/grig/work/repo/universalmanifest`)  
Program scope: Portable Identity Profile workstreams (Go-Now + Research-First)

## 1) What this document is

This is a human-first, context-free briefing and operating report for the Portable Identity Profile program.

If a reviewer has never seen this project before, this document explains:

- what problem this program solves,
- what work is planned now,
- what work needs research before implementation,
- how progress is tracked,
- how this report is updated as work is completed.

This is a living document and should be updated whenever a workstream status changes.

## 2) Essential context in plain language

Universal Manifest (UM) is a portable data envelope for identity-related state (subject identifiers, claims, consent rules, device metadata, and pointers to larger assets).

Portable Identity Profile is the program that ensures UM can support interoperable user presence across XR contexts without hard-coding vendor or platform lock-in.

Two execution tracks are used:

- `Go-Now` = implementation work that can be done immediately with existing UM architecture.
- `Research-First` = areas where we need validated design decisions before broad implementation claims.

## 3) Source documents and authority chain

Primary plan and assessment documents:

- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-portable-identity-profile-gap-and-implementation-report.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-portable-identity-profile-go-now-research-first-execution-plan.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-portable-identity-profile-spec-integration-log.md`

This report summarizes and operationalizes those files for first-time reviewers.

## 4) Status model (living)

Status values used:

- `NOT_STARTED`
- `IN_PROGRESS`
- `BLOCKED`
- `DONE`

Evidence rule:

- A workstream cannot be marked `DONE` without links to concrete evidence artifacts (docs, fixtures, journeys, test output, decision updates).

Last program status refresh: 2026-03-05

## 5) Track A — Go-Now workstreams (implementation-first)

## PIP-GN-01 — Portable Identity Profile XR Integration Lane

Current status: `NOT_STARTED`

Why this exists:

- External adopters need one coherent integration lane explaining how to implement Portable Identity Profile behavior in XR using existing UM primitives.

What it delivers:

- integration doc and site mirror with field mapping, consent behavior, and examples.

What “done” means:

- integration documentation published,
- unknown-field tolerance and default-deny consent made explicit,
- minimum three end-to-end examples included.

Evidence to attach when complete:

- updated integration doc path,
- updated site doc path,
- build/link check output report path.

## PIP-GN-02 — Fixture Pack Expansion

Current status: `NOT_STARTED`

Why this exists:

- Claims in docs are insufficient without executable fixtures that third parties can test against.

What it delivers:

- v0.1/v0.2 fixture set for minimal profile, avatar pointers, consent matrix, pairwise subjects, and revocation metadata.

What “done” means:

- all valid fixtures pass,
- all intentionally invalid fixtures fail,
- fixture intent and usage documented.

Evidence to attach when complete:

- fixture file paths,
- test run artifact path (`npm test`),
- fixture-to-requirement mapping note.

## PIP-GN-03 — Journey Expansion

Current status: `NOT_STARTED`

Why this exists:

- We need executable behavior proofs, not just schema examples.

What it delivers:

- journey docs and runner mappings for onboarding projection, pointer/consent behavior, pairwise DID privacy, and revocation-aware policy checks.

What “done” means:

- journeys are documented with pass/fail logic,
- journey runner includes new IDs,
- journey report artifacts include successful outcomes.

Evidence to attach when complete:

- journey file paths,
- updated runner path,
- journey report artifact path.

## PIP-GN-04 — Registry Expansion

Current status: `NOT_STARTED`

Why this exists:

- Naming drift causes interoperability failures even when formats are technically compatible.

What it delivers:

- non-normative but stable candidate key names for XR-related profile, avatar, translation metadata, and consent families.

What “done” means:

- namespaced keys added,
- clearly marked as non-normative,
- same names used consistently across docs and fixtures.

Evidence to attach when complete:

- registry diff path,
- consistency scan output path.

## PIP-GN-05 — Implementation Guide Addendum

Current status: `NOT_STARTED`

Why this exists:

- Teams need direct implementation instructions and not only concept documentation.

What it delivers:

- adopter-ready guide covering consumer algorithm order, issuer checklist, consent enforcement patterns, revocation tiers, and offline risk handling.

What “done” means:

- guide is complete and cross-linked to fixtures/journeys,
- language remains method-neutral.

Evidence to attach when complete:

- guide path,
- site mirror path,
- link validation report path.

## PIP-GN-06 — Governance and Status Synchronization

Current status: `NOT_STARTED`

Why this exists:

- Program work must be traceable and auditable at project-governance level.

What it delivers:

- synchronized updates to decisions and project status artifacts.

What “done” means:

- decision log updated,
- state-of-project updated,
- critical-path updated when needed,
- no drift between deliverables and governance record.

Evidence to attach when complete:

- updated governance doc paths,
- short change log entry path.

## 6) Track B — Research-First workstreams

## PIP-RS-01 — Encrypted Private Fragment Profile

Current status: `NOT_STARTED`

Why this exists:

- Private data handling is a core requirement but currently lacks one interoperable profile.

Research questions:

- packaging model,
- key distribution model,
- signature/canonicalization interactions with encrypted sections.

What “done” means:

- research brief with compared options,
- recommended option with tradeoffs,
- clear promotion recommendation.

Promotion gate:

- at least two independent runtime feasibility paths.

Evidence to attach when complete:

- research report path,
- option comparison appendix path.

## PIP-RS-02 — Selective Disclosure / ZK Proof Profile

Current status: `NOT_STARTED`

Why this exists:

- Minimal disclosure is a key privacy requirement and currently under-specified.

Research questions:

- best practical proof approach,
- proof binding model in UM,
- replay and privacy guarantees.

What “done” means:

- selected profile recommendation,
- verifier maturity evidence,
- conformance fixture feasibility statement.

Promotion gate:

- stable verifier support in at least two languages and clear mitigation model.

Evidence to attach when complete:

- research report path,
- implementation readiness summary path.

## PIP-RS-03 — Wallet Recovery Profile

Current status: `NOT_STARTED`

Why this exists:

- Recovery is required for real-world resilience, but overreach into wallet internals must be avoided.

Research questions:

- minimum interoperable metadata,
- security pitfalls,
- integration-guidance vs profile candidacy boundary.

What “done” means:

- minimal metadata contract proposal,
- security risk analysis,
- promotion decision.

Promotion gate:

- no mandatory wallet-vendor internal coupling.

Evidence to attach when complete:

- research report path,
- decision note path.

## PIP-RS-04 — Wallet Protocol Binding Profile

Current status: `NOT_STARTED`

Why this exists:

- UM payload portability needs a consistent model across OIDC4VP/OIDC4VCI/DIDComm transport families.

Research questions:

- protocol-agnostic state model,
- mapping consistency,
- cross-protocol error taxonomy.

What “done” means:

- abstract state model,
- at least two concrete binding mappings,
- transport-neutral evidence model.

Promotion gate:

- equivalent semantics across at least two transport families.

Evidence to attach when complete:

- research report path,
- binding model diagram path.

## PIP-RS-05 — Avatar Translation Profile

Current status: `NOT_STARTED`

Why this exists:

- Cross-engine avatar portability requires translation metadata conventions.

Research questions:

- anchor formats and metadata conventions,
- minimum translation shard shape,
- runtime-agnostic viability.

What “done” means:

- schema candidate(s),
- cross-runtime validation notes,
- promotion recommendation.

Promotion gate:

- optional shard representation without UM core-field bloat.

Evidence to attach when complete:

- research report path,
- prototype schema appendix path.

## 7) How this report must be updated during execution

When any workstream changes status:

1. Update the `Current status` line for that workstream.
2. Add completion date and owner line directly below status.
3. Add evidence links under the workstream’s “Evidence to attach” section.
4. Update `Last program status refresh` date in section 4.
5. Mirror critical status changes into:
   - `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
   - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`

## 8) First-time reviewer quick answer

Is this program doable now?

- Yes. Track A is immediately executable and is designed to produce practical adopter artifacts quickly.
- Track B handles high-uncertainty items with promotion gates so we avoid premature standardization claims.

What to watch most closely:

- evidence quality,
- privacy/security profile rigor,
- synchronization between implementation artifacts and governance docs.

## 9) Immediate next operational move

Start `PIP-GN-01`, `PIP-GN-02`, and `PIP-GN-06` first, while opening `PIP-RS-01` and `PIP-RS-02` research briefs in parallel.
