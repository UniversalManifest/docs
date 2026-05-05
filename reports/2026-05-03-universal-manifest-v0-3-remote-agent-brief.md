# Universal Manifest v0.3 Remote Agent Brief

Date: 2026-05-03

Audience: a remote strategy, specification, architecture, and design agent with no access to private preview servers, no access to the current browser, and no guaranteed access to private working state beyond what is written here.

Primary instruction: produce a detailed Universal Manifest v0.3 design/spec/build proposal after reading this brief. Do not implement code. Do not patch docs. Do not create work orders yet. Your output should be a concrete proposal that the project owner can review before any implementation work begins.

Hard warning: do not drift into vague aspirational language. Universal Manifest already has a published v0.2, a repo, a public site, conformance fixtures, a resolver contract, a done-done framework, and a current deployment blocker. Treat v0.3 as a standards design problem with migration, conformance, governance, implementer, privacy, trust, and public-reader consequences. Every recommendation should say what becomes normative, what stays guidance, what is deferred, what files/routes would change, what evidence would prove it, and what risk it reduces.

## Objective

Design the serious v0.3 path for Universal Manifest.

Universal Manifest is a standard/specification for a portable signed context envelope. It is not a product, not a hosted backend replacement, not a wallet replacement, not a DID method, and not a universal database. A Universal Manifest carries enough bounded, signed, receiver-evaluable context for systems that do not share one backend to make a trust and projection decision.

Current core envelope idea:

- identity references: who or what the manifest is about
- claims: assertions, entitlements, roles, or verification state the receiver can evaluate
- permissions and consents: what the receiver may show, store, share, or request
- pointers: references to canonical sources, assets, credentials, pods, stores, resolvers, or runtime endpoints
- proof: signatures, claim proof material, attestation references, trust-tier evidence
- validity: issued and expiry windows, plus optional status/revocation/freshness metadata

The receiving system should evaluate the manifest before projection. It verifies what it supports, applies local policy, follows only allowed pointers, projects only allowed or supported context, and leaves authoritative data where it belongs. Large, mutable, private, or domain-specific data may remain in external systems, wallets, pods, issuer stores, asset stores, runtime services, or subject-controlled agents. UM's job is the inspectable envelope and exchange boundary, not ownership of every source of truth.

The remote agent's task is to determine what v0.3 should specify and how it should be built into the existing system. The expected result is a proposal, not code. The proposal should be implementation-aware enough that follow-on work orders can be created without re-litigating the conceptual model.

## Current State

Universal Manifest v0.2 exists and has been published. The publication evidence pack records all done-done gates as passing for early-adopter v0.x maturity. The v0.2 GitHub release is public at `https://github.com/grigb/universal-manifest/releases/tag/spec-v0.2`. The local source of truth for the evidence pack is `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-30-v0-2-publication-evidence-pack.md`.

Important nuance: publication and deployment are not the same current fact. v0.2 was released and the repo contains the v0.2 publication surfaces, but the public deployment may still be stale until the gated Cloudflare deploy succeeds. Work order `WO-0255` is blocked because GitHub Actions deploy reaches Cloudflare and fails with `Invalid access token [code: 9109]`. Do not assume production currently reflects the redesigned local site or the latest repo state.

Current latest repo/CI facts:

- Current commit in this working copy: `98404ba17df72e029c34bbab76bf00a5cc38f83d` (`fix(site): retarget dead getting started links`).
- That commit retargeted dead `/getting-started/` links to `/getting-started/implement/`.
- GitHub `verify` passed for that commit: `https://github.com/grigb/universal-manifest/actions/runs/25269311596`.
- GitHub `CI/CD Pipeline` passed for that commit: `https://github.com/grigb/universal-manifest/actions/runs/25269311600`.
- The last known gated deploy failure remains `https://github.com/grigb/universal-manifest/actions/runs/25253991767`, with failure at Cloudflare auth rather than at site build/test.

Current public-front-door state:

- `WO-0253` completed a design direction package for the homepage cluster on 2026-05-02.
- `WO-0254` implemented the approved homepage-cluster redesign locally across `/`, `/use-cases/`, `/explorer/`, `/how-it-works/`, and `/standards-fit/`.
- Local build and local route checks passed during `WO-0254`, but local verification is not public deployment verification.
- `WO-0255` must verify the public route/deployment state after Cloudflare credentials are fixed.
- `WO-0256` must run real external-reader validation only after production routes are verified and a real reader cohort/process exists. Simulated reader validation is forbidden as completion evidence.

Current spec posture:

- v0.1 established the basic manifest shape, unknown-field tolerance, fixtures, and early conformance scaffolding.
- v0.2 made signatures real: JCS (RFC 8785) canonicalization plus Ed25519 signatures, with `signature` required for strict v0.2.
- v0.2 added or documented the trust-layer concerns around claim proof, the Bag of Claims vulnerability, Tier 0 and Tier 1 trust posture, and future promotion paths for stronger identity binding.
- v0.2 keeps revocation/status metadata optional and extension-lane oriented.
- v0.2 supports two privacy paths as guidance: projection-derived manifests and encrypted inline facets, with projection as the normative broad interoperability path and encrypted inline facets as optional guidance.
- v0.2 conformance includes valid and invalid fixtures, TTL/replay/security rejection cases, signature failure cases, and a standalone conformance package layout.

Current project maturity model:

- `docs/DONE-DONE-DEFINITION.md` defines gates G1 through G7: contract completeness, conformance testability, integrity/trust profile, interoperability proof, publishing/discoverability, governance/change control, and operational realism.
- v0.2 is early-adopter ready, not world-ready.
- "World-ready" requires independent implementations, security and compatibility hardening, long-term governance, migration reliability, and broader adversarial conformance coverage.

## Non-negotiable Constraints

1. Do not assume a private preview route. Do not tell anyone to inspect a local preview server. A remote agent cannot access it.

2. Do not assume production is current. Public URLs are useful source references, but the current deployment is blocked by Cloudflare GitHub Actions credentials. Production may still be stale until `WO-0255` passes.

3. Do not treat v0.3 as a marketing rewrite. v0.3 must be a standards/specification proposal with schema, conformance, migration, implementation, public-reader, and governance consequences.

4. Do not implement immediately. The required remote-agent output is a v0.3 design/spec/build proposal. Implementation should come only after review and work-order creation.

5. Do not overclaim UM. UM is a portable signed context envelope. It does not replace authoritative stores, credential wallets, DID methods, identity providers, object storage, resolvers, payment rails, or backend policy engines.

6. Preserve the v0.2 release truth. v0.3 can change the future direction, but it must explain migration from published v0.2, keep durable v0.2 source paths meaningful, and respect unknown-field tolerance unless explicitly proposing a breaking change.

7. Every recommendation needs a status category: normative v0.3, non-normative guidance, conformance profile, public documentation, implementation helper, or deferred future work.

8. The public reader path matters. If v0.3 creates new concepts but first-time readers cannot understand what UM is and where to start, adoption will fail. Public route verification and real reader validation are still blocked prerequisites for trustworthy external feedback.

9. Use absolute repo paths for local sources. A human or agent receiving this brief should not need to infer the repository root.

10. Avoid "generic interoperability" claims. Say exactly what crosses a boundary, what is verified, what remains authoritative elsewhere, what is projected, and what the receiver must do.

## Existing System Map

The repo path is `/Users/grig/work/repo/universalmanifest`.

### Project authority and status docs

- Documentation index: `/Users/grig/work/repo/universalmanifest/docs/README.md`
- Project vision: `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- Current status: `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
- Critical path: `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`
- Done-done definition: `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-DEFINITION.md`
- Decision log: `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- Early bootstrap worklogs: `/Users/grig/work/repo/universalmanifest/docs/WORKLOG-2026-02-11.md` and `/Users/grig/work/repo/universalmanifest/docs/WORKLOG-2026-02-12.md`

Key vision facts from these docs:

- UM is pointer-first and storage-neutral.
- UM uses a composite stack framing: trust layer, data layer, interaction layer.
- A subject-controlled active runtime can be a valid implementation pattern, but it is non-normative architecture guidance, not a requirement that all conformant systems ship the same runtime.
- A future Record primitive is already captured as vision direction: records may be leaf or container records, may declare their own schema/standards context, and should support push and request/pull exchange.
- User journeys mapped to executable tests are treated as proof, not decoration.

### v0.2 spec artifacts

- Overview: `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`
- Signature profile: `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md`
- Conformance: `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
- JSON Schema: `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.json`
- JSON-LD context: `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.jsonld`

v0.2 required fields are `@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`, and `signature`. Optional top-level arrays include `facets`, `claims`, `consents`, `devices`, and `pointers`. The v0.2 schema constrains the signature profile and leaves most domain payloads extensible.

v0.2 signature baseline:

- `signature.algorithm` must be `Ed25519`.
- `signature.canonicalization` must be `JCS-RFC8785`.
- Signing input removes the top-level `signature` property, then canonicalizes the rest with JCS.
- `signature.value` is base64url-encoded Ed25519 signature bytes.
- `signature.keyRef` and/or `signature.publicKeySpkiB64` identifies verification material.
- `signature.statusRef` and `signature.revocationCursor` are optional revocation/freshness metadata when the extension lane is used.

### Conformance and proof surfaces

- Standalone suite root: `/Users/grig/work/repo/universalmanifest/conformance/README.md`
- Conformance expected outcomes: `/Users/grig/work/repo/universalmanifest/conformance/v0.1/expected.json` and `/Users/grig/work/repo/universalmanifest/conformance/v0.2/expected.json`
- Canonical examples: `/Users/grig/work/repo/universalmanifest/examples/v0.1/` and `/Users/grig/work/repo/universalmanifest/examples/v0.2/`
- Journey proof runner: `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`
- Journey docs index: `/Users/grig/work/repo/universalmanifest/docs/journeys/README.md`

The publication evidence pack reports `npm test` passing with 49 valid fixtures accepted, 26 invalid fixtures rejected, 26 integration-lane fixtures accepted as non-normative evidence, and 11 GPC proof checks passing. It also reports 27 executable journeys passing.

### Package/reference surfaces

- TypeScript helper package: `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/`
- Package README: `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/README.md`
- Public package API source: `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/src/index.ts`
- Helper package guidance: `/Users/grig/work/repo/universalmanifest/docs/TS-HELPER-PACKAGE.md`
- Adopter implementation guide: `/Users/grig/work/repo/universalmanifest/docs/IMPLEMENTING-UM.md`

The repo-local TypeScript package provides types and assertions for v0.1 and v0.2, including v0.2 Ed25519/JCS verification when `publicKeySpkiB64` is embedded. It intentionally does not provide DID/key resolution, a full SDK, or resolver clients. The package remains private/internal in the current policy; the published adoption contract is the spec plus fixtures plus conformance suite, not one official SDK.

There is also a standalone TypeScript reference implementation repository at `https://github.com/grigb/um-typescript`. The spec repo treats that as implementation #1, not "the official implementation."

### Resolver/runtime surfaces

- Resolver contract: `/Users/grig/work/repo/universalmanifest/services/myum-resolver/CONTRACT.md`
- Public resolver docs source: `/Users/grig/work/repo/universalmanifest/site/src/content/docs/reference/resolver-api.md`
- Runtime host: `https://myum.net`
- Standards/docs host: `https://universalmanifest.net`

The resolver contract is currently minimal and public-read-only:

- `GET /health`
- `GET /.well-known/myum-resolver.json`
- `GET /.well-known/security.txt`
- `GET /openapi.json`
- `GET /{UMID_PATH}`

Resolver responses include `X-UM-Resolver-Contract: myum-resolver/v0.1` and `X-UM-Resolver-Source: runtime | kv | fallback_fixture`. The resolver distinguishes HTTP cache behavior from manifest TTL: consumers must enforce `expiresAt` for use regardless of HTTP cache headers. Private/authenticated resolution is explicitly out of scope for the current runtime and should be designed only as an explicit future profile.

### Public site and reader surfaces

Current redesigned homepage-cluster implementation exists locally in:

- `/Users/grig/work/repo/universalmanifest/site/src/pages/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/use-cases/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/explorer/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/how-it-works/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/standards-fit/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/data/home-cluster.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/styles/public-surface.css`

The redesigned homepage copy states the core message clearly: "A portable signed context envelope for systems that do not share a backend." It also names the anatomy: identity, claims, permissions, pointers, proof, and validity.

Current public discovery files:

- `/Users/grig/work/repo/universalmanifest/site/public/.well-known/universal-manifest.json`
- `/Users/grig/work/repo/universalmanifest/site/public/llms.txt`
- `/Users/grig/work/repo/universalmanifest/site/public/agent/fixture-catalog.json`
- `/Users/grig/work/repo/universalmanifest/site/public/agent/sandbox-scenarios.json`

Agent-facing public support is read-mostly. The public hosts support reading docs, fetching versioned artifacts, enumerating public fixtures/scenarios, using browser tooling surfaces, and resolving UMIDs read-only. They do not support A2A task lifecycle, authenticated write APIs, public MCP service behavior, or agent task claiming.

### Current work orders and blockers

The work-order index is `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`.

Relevant v0.3-adjacent stubs from Phase 19:

- `WO-0245`: Tier 2 cryptographic identity-binding research package
- `WO-0246`: Tier 3 multi-party ceremony research package
- `WO-0247`: Data Integrity / RDF profile decision package
- `WO-0248`: Additional integrity-profile registry decision package
- `WO-0249`: Revocation-as-normative decision package
- `WO-0250`: Encrypted inline facet promotion decision
- `WO-0251`: Broader cross-DID binding tier scope decision

Relevant active blockers:

- `WO-0255`: blocked by invalid Cloudflare token in GitHub Actions; required for public route/deployment verification.
- `WO-0256`: blocked by `WO-0255` plus real external-reader cohort/process.

## v0.3 Candidate Design Themes

The remote agent should analyze these themes seriously. Do not assume all should become normative in v0.3. The task is to decide the right v0.3 scope and explain the boundary.

### 1. v0.3 thesis and maturity target

v0.2 made UM verifiable with a pragmatic JCS + Ed25519 baseline. v0.3 needs a thesis. Possible thesis: "v0.3 turns the signed envelope from a verifiable packet into a policy-aware, privacy-aware, revocation-aware exchange profile without making UM a backend."

The proposal should decide whether v0.3 targets:

- a focused early-adopter increment,
- a production-candidate step toward Maturity B,
- or a research-heavy pre-standard package that should not yet be versioned as v0.3.

Do not default to "more features." Pick a release shape that can pass done-done gates.

### 2. Schema and context design

v0.2 leaves `facets`, `claims`, `consents`, `devices`, and `pointers` mostly open. That flexibility is useful, but v0.3 may need clearer extension grammar so implementers converge.

Questions to resolve:

- Should v0.3 introduce a formal Record primitive, or keep Record at vision/guidance level?
- Should facets, claims, consents, pointers, and devices get stronger internal schemas?
- Should projection metadata become a first-class shape?
- Should `claims[].claimProof`, `requiredTrustTier`, and cross-DID binding conventions graduate into the JSON-LD context or stay conventions?
- What must remain unknown-field tolerant for forward compatibility?
- Which terms belong in `spec/v0.3/schema.jsonld` versus a registry or integration profile?

### 3. Privacy, projection, and encrypted facets

The accepted privacy ADR says v0.2 supports two valid paths: projection-derived manifests and encrypted inline facets. Projection is the normative broad path; encrypted inline facets are optional guidance.

v0.3 needs to decide whether to formalize either path further.

Required analysis:

- Define exactly what a projection is: derived manifest, subset view, independent signature, independent TTL, receiver-specific scope.
- Define how projection regeneration works when consumer scope changes.
- Define whether projection metadata must include source manifest reference, derivation timestamp, audience, purpose, permission basis, and invalidation expectations.
- Decide whether encrypted inline facets need a named profile, a required envelope shape, key reference semantics, recipient list structure, encryption algorithm suite, and decrypt-after-verify ordering.
- Preserve partial-visibility behavior: consumers without keys should still verify the cleartext envelope and report protected facets as opaque/unreadable, not silently treat them as absent.

### 4. Revocation, freshness, and status

v0.2 separates authenticity/integrity from freshness/invalidation. `statusRef` and `revocationCursor` help answer whether a signed manifest has later been revoked or superseded. They do not replace signature verification and they do not participate in the signing input.

v0.3 should decide whether revocation remains optional, becomes a named conformance mode, or becomes normative for some manifest/profile classes.

Questions to resolve:

- Is there a v0.3 `revocation-aware` conformance level?
- What is the status response shape at `statusRef`?
- How should `revocationCursor` monotonicity be defined?
- How do offline/local-first receivers honestly report status: `valid-signature`, `fresh-by-ttl`, `revocation-unchecked`, `revoked`, `status-unavailable`, `stale-status`?
- When should consumers fail open, fail closed, or downgrade trust?
- How does resolver HTTP `410 Gone` relate to manifest-level status metadata?
- How does manifest `expiresAt` interact with status endpoint freshness and HTTP cache headers?

### 5. Trust tiers and identity binding

v0.2 documents the Bag of Claims vulnerability: a signed manifest proves the signer produced the packet, but does not automatically prove the signer controls every subject or that every claim was issued by its stated issuer.

Current tiers:

- Tier 0: signature-only, self-asserted claims
- Tier 1: attested or claimProof-backed claims
- Tier 2: cryptographic binding, deferred to v0.3
- Tier 3: multi-party ceremony, deferred to v0.4+

v0.3 should decide whether Tier 2 is actually ready to specify, or whether v0.3 should instead tighten Tier 1 semantics and produce a research package for Tier 2.

Required analysis:

- What evidence must bind `subject`, signer, issuer, and claim?
- Should multi-signature binding or proof-of-control over multiple DIDs be a v0.3 profile?
- Can the project specify Tier 2 without picking a DID method or requiring VC ecosystem lock-in?
- How should privacy-preserving pairwise identifiers coexist with cross-DID binding?
- Should relying parties declare required trust tiers in policy only, or can manifests declare `requiredTrustTier` as issuer guidance?

### 6. Resolver contracts and active runtime boundaries

The current `myum.net` resolver is public-read-only and minimal. It is useful, but it is not the whole runtime story.

v0.3 should clarify:

- whether resolver behavior remains non-normative reference-runtime guidance,
- whether a resolver profile belongs in v0.3 conformance,
- whether private/authenticated resolution gets a design-only profile,
- how subjects, wallets, agents, or local-first runtimes request projection updates,
- how pointer resolution failure affects receiver decisions,
- how source provenance headers and resolver source indicators should be surfaced to humans and agents.

Do not accidentally turn UM into a hosted resolver product. If resolver profiles are proposed, define them as interoperable contracts that other implementations can adopt.

### 7. Conformance expansion

v0.2 conformance validates structure, TTL, signature profile, invalid signature cases, and some extension lanes. v0.3 should define an expanded conformance matrix before implementation.

Candidate conformance buckets:

- v0.3 baseline structural acceptance/rejection
- projection-derived manifests
- encrypted inline facets and partial-visibility processing
- revocation-aware status resolution and stale cursor handling
- claimProof and trust-tier downgrade behavior
- resolver-agnostic status and resolution behavior
- pointer target integrity or freshness metadata if adopted
- migration fixtures showing v0.2 consumers encountering v0.3 fields safely
- adversarial fixtures for signature stripping, stale projection replay, unauthorized facet disclosure, fake claimProof, unsupported profile spoofing, and resolver provenance confusion

The proposal should name expected valid and invalid fixtures, not just say "add tests."

### 8. Agent-facing use and public machine-readable surfaces

UM already exposes `llms.txt`, a well-known descriptor, fixture catalogs, scenario catalogs, and agent onboarding docs. These are read-mostly public supports, not an agent task service.

v0.3 should consider whether agent-facing guidance needs to become more formal:

- How should external agents discover the current spec, schema, conformance suite, fixtures, and resolver contract?
- How should agents report whether they verified a manifest, merely parsed it, or relied on stale public pages?
- Should manifests carry agent delegation pointers or agent authority claims beyond the current non-normative convention?
- What anti-fabrication language should public agent docs include so agents do not invent unsupported APIs?
- Should v0.3 include a machine-readable conformance/status declaration format for implementations and agents?

The public agent path must remain honest. Do not imply authenticated write behavior, task lifecycle behavior, or public MCP behavior unless those systems actually exist.

### 9. Implementer ergonomics

External implementers should be able to build a conformant implementation without TypeScript and without insider knowledge. The current system has a standalone conformance suite, fixtures, docs, and a TypeScript reference path.

v0.3 should propose:

- which implementation guide updates are required,
- whether the private `packages/universal-manifest` helper should remain private or become publishable,
- what API surface a reference implementation should expose for v0.3,
- how adapters in other languages should prove conformance,
- what report format implementers should publish,
- how to avoid public SDK drift from the spec.

### 10. Migration from v0.2

v0.3 must have a migration plan. At minimum:

- v0.2 durable route remains durable.
- `/spec/latest/` eventually points to v0.3 only after v0.3 is published and verified.
- v0.2 consumers should either safely ignore v0.3 extensions or reject v0.3 when strict version policy requires.
- v0.3 issuers need guidance for dual-emitting v0.2/v0.3 during transition if necessary.
- breaking changes must be named with rollback and deprecation policy implications.
- v0.3 schema/context artifact URLs and hashes need release evidence.

### 11. Public reader path and adoption validation

The v0.3 proposal should not be isolated from public comprehension. UM adoption depends on a first-time reader understanding the envelope model before deep spec material.

Do not claim v0.3 public readiness until:

- Cloudflare deployment credentials are fixed,
- `WO-0255` verifies required public routes,
- `WO-0256` runs real external-reader validation,
- the homepage cluster and spec paths agree on current version posture,
- discovery descriptors and `llms.txt` reflect the same story.

## Required Outputs From Remote Agent

The remote agent should produce one detailed Markdown proposal with the following outputs:

1. v0.3 executive thesis: one clear paragraph explaining what v0.3 is for and what it is not for.

2. Scope decision: list what should be normative v0.3, what should be non-normative guidance, what should be a conformance profile, and what should be deferred.

3. Normative delta map: field-by-field or behavior-by-behavior changes from v0.2, including schema/context implications.

4. Privacy design: projection and encrypted-facet decision package with receiver behavior, issuer behavior, lifecycle rules, and conformance fixtures.

5. Trust design: trust-tier and identity-binding proposal, including whether Tier 2 is ready for v0.3.

6. Revocation/freshness design: statusRef, revocationCursor, TTL, resolver, offline behavior, failure-state vocabulary, and conformance implications.

7. Resolver/runtime boundary: what belongs in the UM standard versus resolver guidance versus reference runtime.

8. Conformance plan: concrete valid/invalid fixture categories, expected outcomes, runner changes, report schema updates, and journey proof additions.

9. Migration plan: v0.2 to v0.3 lifecycle, compatibility behavior, public route changes, docs changes, and release evidence requirements.

10. Build plan: ordered implementation waves across `spec/`, `examples/`, `conformance/`, `packages/`, `site/`, `docs/`, `services/myum-resolver/`, and public discovery artifacts.

11. Proposed work orders: review-ready WO candidates with objective, files, constraints, dependencies, and acceptance criteria.

12. Risk register: concrete risks and mitigations, especially around crypto overreach, privacy leakage, public route staleness, and vague messaging.

13. Open questions: only questions that block a decision. Do not ask for context that is already included in this brief.

## Proposed Work Orders To Create After Review

These are not active work orders yet. They are candidate work orders to create after the remote proposal is reviewed and accepted.

- v0.3 Scope and Release Thesis Decision Package: define the v0.3 maturity target, release boundary, normative/guidance split, and done-done gate expectations.

- v0.3 Schema and JSON-LD Context Design: draft `spec/v0.3/schema.json`, `spec/v0.3/schema.jsonld`, and README deltas, including Record/projection/trust terms if accepted.

- Projection and Encrypted Facet Profile Package: decide what becomes normative versus guidance, then produce lifecycle docs and fixture expectations.

- Revocation and Freshness Profile Package: decide whether revocation-aware verification becomes a v0.3 conformance level, then define status shape, cursor semantics, failure states, and fixtures.

- Trust Tier and Identity Binding Package: evaluate Tier 2 readiness, refine Tier 1, and decide what identity-binding vocabulary is safe for v0.3.

- Resolver and Runtime Boundary Package: define what resolver behavior is reference guidance, what can be resolver-agnostic conformance, and what private/authenticated resolution profile remains future work.

- v0.3 Conformance Matrix and Fixture Expansion: create valid/invalid fixture plan, expected outcome schema, runner changes, and language-neutral adapter expectations before implementation.

- Implementer Ergonomics and Reference Surface Update: update implementation guides, package policy, reference implementation expectations, and conformance report publishing guidance.

- v0.2 to v0.3 Migration and Governance Package: create migration guide, breaking-change analysis, release route plan, changelog plan, artifact hash policy, and rollback notes.

- Public Reader Path and Discovery Alignment Package: after `WO-0255` and `WO-0256`, update public docs, `llms.txt`, well-known descriptors, and first-time reader path for v0.3 without overstating production state.

- Agent-Facing Verification and Anti-Fabrication Package: define how external agents should cite, validate, and report UM capabilities without inventing unsupported APIs or relying on stale public pages.

## Suggested Acceptance Criteria

A v0.3 design/spec/build proposal is acceptable only if it satisfies all of the following:

- It is self-contained enough for a project owner to review without opening private preview routes or private browser state.
- It names the v0.3 thesis in concrete standards language.
- It maps every proposed change to a source surface: spec, schema, context, conformance, examples, package, resolver, site, governance, or public discovery.
- It distinguishes normative requirements from guidance and deferred research.
- It explains migration from published v0.2, including strict consumers, dual-version consumers, and public route/version behavior.
- It defines concrete conformance fixture categories with expected accept/reject behavior.
- It addresses privacy, revocation/freshness, trust tiers, resolver boundaries, agent-facing discovery, and implementer ergonomics.
- It does not claim public deployment success until `WO-0255` is unblocked and verified.
- It does not claim external reader validation until `WO-0256` has real cohort evidence.
- It uses the done-done gates as release criteria rather than treating a proposal as completion.
- It includes proposed work orders that can be executed independently after review.
- It includes a risk register with mitigations and clear deferrals.

## Risks/Anti-Patterns

- Vague interoperability rhetoric: "works across systems" is not enough. Say what crosses, what verifies, what remains elsewhere, and what the receiver does.

- Product drift: do not turn UM into a backend, wallet, hosted identity service, resolver monopoly, or SDK-first product.

- Crypto overreach: do not standardize Tier 2, ZK, Data Integrity, post-quantum, BBS+, SD-JWT, or multi-party ceremony behavior without evidence and implementer cost analysis.

- Privacy false safety: encrypted facets and projection can both leak if lifecycle, key rotation, recipient scoping, and stale copy handling are vague.

- Revocation confusion: a valid signature is not proof of current permission. A revoked or stale manifest can still verify cryptographically.

- Resolver authority confusion: `universalmanifest.net` is standards/docs; `myum.net` is resolver/runtime. Do not collapse their roles.

- Public route hallucination: public production may be stale while Cloudflare deploy is blocked. Do not cite a public page as current unless route verification has passed after deploy.

- Conformance theater: adding docs without fixtures, expected outcomes, and runner/report changes does not prove interoperability.

- Agent-facing inflation: public agent surfaces are read-mostly. Do not imply task execution, write APIs, public MCP, or authenticated agent services.

- Migration silence: v0.3 cannot be credible if it breaks v0.2 consumers without a documented transition path.

- Homepage/design detour: v0.3 specification work should not re-open homepage design unless it affects public-reader comprehension, version posture, or adoption flow.

## Source Pack

Use this source pack as the initial read order. The context above is intended to be enough to begin analysis, but these paths are the authoritative local artifacts.

Primary project state:

- `/Users/grig/work/repo/universalmanifest/docs/README.md`
- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
- `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`
- `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-DEFINITION.md`
- `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`

v0.2 source of truth:

- `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.json`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.jsonld`
- `/Users/grig/work/repo/universalmanifest/docs/VERSION-DIFFERENCES-V01-V02.md`
- `/Users/grig/work/repo/universalmanifest/docs/guides/MIGRATION-V01-V02.md`
- `https://github.com/grigb/universal-manifest/releases/tag/spec-v0.2`

Current blockers and homepage reader path:

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0253-homepage-cluster-design-direction-package.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0254-implement-approved-homepage-cluster-redesign.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0255-public-route-and-deployment-verification-v0-2-reader-path.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0256-external-reader-validation-execution.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`

v0.3-adjacent decision reports:

- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-30-v0-2-publication-evidence-pack.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-01-wo-0143-private-encrypted-inline-facets-vs-projection-adr.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-22-revocation-cursor-and-status-contract.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-22-conformance-suite-ttl-replay-and-security-expansion.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-15-agent-discovery-and-machine-readable-entrypoints-report.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-15-external-agent-onboarding-and-adoption-memo.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-15-agent-facing-publication-gates-framework.md`

Implementation and conformance surfaces:

- `/Users/grig/work/repo/universalmanifest/conformance/README.md`
- `/Users/grig/work/repo/universalmanifest/conformance/v0.2/expected.json`
- `/Users/grig/work/repo/universalmanifest/examples/v0.2/`
- `/Users/grig/work/repo/universalmanifest/examples/v0.2/invalid/`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/README.md`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/src/index.ts`
- `/Users/grig/work/repo/universalmanifest/docs/IMPLEMENTING-UM.md`
- `/Users/grig/work/repo/universalmanifest/docs/TS-HELPER-PACKAGE.md`

Resolver and public discovery:

- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/CONTRACT.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/reference/resolver-api.md`
- `/Users/grig/work/repo/universalmanifest/site/public/.well-known/universal-manifest.json`
- `/Users/grig/work/repo/universalmanifest/site/public/llms.txt`
- `/Users/grig/work/repo/universalmanifest/site/public/agent/fixture-catalog.json`
- `/Users/grig/work/repo/universalmanifest/site/public/agent/sandbox-scenarios.json`

Current local public-site implementation:

- `/Users/grig/work/repo/universalmanifest/site/src/pages/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/use-cases/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/explorer/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/how-it-works/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/standards-fit/index.astro`
- `/Users/grig/work/repo/universalmanifest/site/src/data/home-cluster.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/styles/public-surface.css`

Public URLs that are useful but must be treated with deployment caveats:

- `https://universalmanifest.net/`
- `https://universalmanifest.net/spec/latest/`
- `https://universalmanifest.net/spec/v0.2/`
- `https://universalmanifest.net/.well-known/universal-manifest.json`
- `https://universalmanifest.net/llms.txt`
- `https://myum.net/.well-known/myum-resolver.json`
- `https://myum.net/openapi.json`

Again: public URLs are not a substitute for the repo source pack while the Cloudflare deploy is blocked. The v0.3 proposal should be source-grounded, deployment-aware, and specific enough to turn into reviewed work orders.
