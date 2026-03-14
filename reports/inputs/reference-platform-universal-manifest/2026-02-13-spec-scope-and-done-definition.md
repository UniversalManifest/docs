# Universal Manifest Spec Scope + Done Definition

Date: 2026-02-13  
Work Order: `WO-reference implementation-universal-manifest-spec-scope-and-done-definition`  
Status: COMPLETE

## 1) Scope Definition (What the spec is responsible for)

Universal Manifest is a portable state-capsule specification. It is responsible for:

- document identity and lifecycle (`@id`, `manifestVersion`, `issuedAt`, `expiresAt`)
- subject binding (`subject`)
- composable state slices (`facets`)
- machine-actionable state sections (`claims`, `consents`, `devices`, `pointers`)
- optional signature (`signature`, profile-versioned)
- compatibility semantics (unknown-field tolerance, extension points, version policy)

In-scope normative surfaces:

- `spec/v0.1/schema.jsonld`
- `spec/v0.1/schema.json`
- `spec/v0.1/README.md`
- `spec/v0.1/CONFORMANCE.md`
- `spec/v0.1/REGISTRY.md`

In-scope but required-to-adopt surfaces:

- `examples/v0.1/`
- `integrations/reference-runtime.md`
- `integrations/social.md`
- `docs/PUBLISHING-AND-VERSIONING.md`
- `docs/DOMAIN-ARCHITECTURE.md`

Explicitly out of scope for current phase:

- full resolver implementation (`myum.net`) as production service
- final trust-distribution model and revocation network
- full DID method standardization or profile-locking
- long-horizon restoration/recovery workflows

## 2) Done-Done Criteria

### D1. Contract completeness

- Required fields stable and normatively specified.
- Consumer/issuer required behavior is explicit and testable.
- Versioning and compatibility rules are explicit.

### D2. Conformance readiness

- Valid and invalid fixtures cover baseline + failure modes.
- A reference validator/harness proves pass/fail expectations.
- TTL/freshness semantics are enforceable by adopters.

### D3. Integrity profile clarity

- Signature profile is either finalized for release or clearly marked draft with migration path.
- Canonicalization expectations are explicit where signatures are normative.

### D4. Publishability

- Canonical public URLs and hosting policy documented.
- Release process and artifact immutability policy defined.
- “Read this first” pathway exists for new adopters.

### D5. Integration viability

- At least one real integration path demonstrates consumption with ID references and bounded caching.
- Integration docs separate spec contract from implementation specifics.

## 3) Current Progress Against Done-Done

Current status (evidence in scorecard and crosswalk reports):

- D1 Contract completeness: mostly complete (v0.1 shape and behavior defined)
- D2 Conformance readiness: partially complete (baseline strong; deeper edge/security cases pending)
- D3 Integrity profile clarity: partially complete (v0.2 direction exists; not finalized)
- D4 Publishability: partially complete (docs and domain architecture defined; production hosting flow not yet fully operationalized in this repo)
- D5 Integration viability: complete for stub-level reference implementation integration

Overall completion estimate for “spec + adoption-ready documentation package”: **~72%**.

### What “done done” means now

The current body of work is enough for early adopters and controlled integration pilots.  
It is not yet “foundation-grade finalized” until signature profile hardening, conformance deepening, and production publishing guarantees are closed.

## 4) Gap-Closure Sequence (ordered)

1. Finalize signature/canonicalization profile for v0.2 and migration notes.
2. Expand conformance suite for TTL edge cases, replay/misuse cases, and signature-failure cases.
3. Stand up production publication flow for `universalmanifest.net` with immutable versioned artifacts.
4. Publish resolver skeleton contract for `myum.net/[UMID]` (interface-first, minimal service).
5. Freeze v0.1.x and produce a concise adopter implementation checklist.

## 5) Foundational Inputs Used

- `/Users/grig/work/repo/reference-platform/UNIVERSAL-MANIFEST.md`
- `/Users/grig/work/repo/reference-platform/docs/decisions/2026-02-11-universal-manifest-integration-decisions.md`
- `/Users/grig/work/repo/reference-platform/docs/decisions/2026-02-12-universal-manifest-queue-decisions.md`
- `/Users/grig/work/repo/reference-platform/.dev/ai/handoffs/2026-02-11-20-45-58Z-universal-manifest-handoff.md`
- `/Users/grig/work/repo/reference-platform/.dev/ai/reports/2026-02-12-universal-manifest-status-report.md`
- `docs/STATE-OF-THE-PROJECT.md`
- `docs/DEPTH-AND-SCOPE.md`
- `docs/DECISIONS.md`
- `spec/v0.1/CONFORMANCE.md`
- `/Users/grig/.agents/knowledge-sources/INDEX.md`
- `/Users/grig/Downloads/INBOX-markdown/universal-manifest/`
