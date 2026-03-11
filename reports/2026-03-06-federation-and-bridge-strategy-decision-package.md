# Federation and Bridge Strategy Decision Package

Date: 2026-03-06  
Work order: `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0135-federation-and-bridge-strategy-decision-package.md`

## 1. Executive answer

Universal Manifest should not adopt a single canonical federation or bridge substrate.

The correct strategy is role-based:

- keep the **subject-controlled runtime** as the canonical private-state authority,
- allow multiple attachable substrates to fill bounded roles,
- make refresh, trust, and failure behavior explicit,
- keep closed-surface bridge adapters non-normative,
- and refuse to let any single substrate redefine UM itself.

Decision summary:

- `No UM core schema change`.
- `No single external substrate is normative for UM`.
- `Federation must be described by role, not by vendor or protocol family alone`.
- `Closed-surface adapters remain implementation detail`.
- `Follow-on guidance work is justified`, but it should land first in shared runtime/synchronization guidance, and only secondarily in substrate-specific or ecosystem-specific integration docs.

The strongest current role alignment is:

- **Canonical private state authority**: subject-controlled runtime first; Solid and DWN only as attachable examples.
- **Public projection broker**: AT Protocol is a strong bounded example for public projection and broad public sync, not for private canonical state.
- **Trust federation gatekeeper**: OpenID Federation is the strongest current standards-family fit for verifier/issuer trust establishment, but it does not solve subject-state portability or sync.
- **Relay/sync coordinator**: no single winner; use UM's push-intent plus pull-fetch model and attach substrate-specific mechanisms only where they fit.
- **Closed-surface bridge adapter**: always non-normative.

## 2. Why this decision package is needed

The repo already had the right direction but not the final comparison frame.

What already existed:

- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md` correctly defines a subject-controlled runtime and pointer-first architecture.
- `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md` correctly defines bridge adapters as implementation detail.
- `/Users/grig/work/repo/universalmanifest/docs/guides/MUM-SYNCHRONIZATION-PROFILE.md` already defines authoritative source, change log, snapshot, staleness checks, deterministic retry, and offline behavior.
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-protocol-recommendation-governance-and-standards-currency-matrix.md` already prevents accidental overpromotion of Solid, DWN, AT Protocol, and OpenID Federation.

What was missing:

- a role taxonomy,
- an explicit explanation of which substrate fills which role,
- a statement of what happens when the substrate is unavailable or stale,
- a clear answer to “what is the actual source of truth?”

## 3. Role taxonomy Universal Manifest should use

The following roles are the correct federation/bridge vocabulary for the project.

### 3.1 Canonical private state authority

Definition:

- The place where the subject's current consent, pointer routing, current preferred references, and authoritative state decisions are governed.

UM answer:

- This role belongs to the subject-controlled runtime first.
- An external substrate may store or replicate state for the runtime, but it does not replace the runtime's authority to decide what is current and shareable.

Applied example:

- A person's wallet/client decides that `social.profilePublic=denied`, rotates a pointer, and updates the current authoritative manifest state.
- Solid or DWN may store the underlying state, but the runtime remains the control point for disclosure and refresh.

### 3.2 Public projection broker

Definition:

- A surface that republishes or distributes allowed public-facing subsets of state to consumers.

UM answer:

- This is a projection role, not a source-of-truth role.
- A public social substrate, a public scene package, or a world-specific profile surface can all fill this role.

Applied example:

- A creator's public profile projection is emitted to a public social network while private consents and restricted proof references remain under runtime control.

### 3.3 Trust federation gatekeeper

Definition:

- The mechanism used to establish whether issuers, verifiers, relying parties, or service entities are trusted enough to participate.

UM answer:

- This is separate from subject-state storage or sync.
- Trust federation may be attached to UM, but it is not the same thing as UM portability.

Applied example:

- A verifier presents a trust chain or federation metadata that the wallet/runtime uses before disclosing proof-derived results.

### 3.4 Relay/sync coordinator

Definition:

- The mechanism that propagates updates, resynchronizes stale consumers, and recovers from missed changes.

UM answer:

- UM already has the right generic model: authoritative source, change log, snapshot, TTL, and deterministic conflict rules.
- External substrates can implement or support this, but they must not replace the generic model.

Applied example:

- A display or world cache sees a change-log event, checks `authoritativeSource`, fetches a fresher manifest, validates it, applies merge rules, and either updates or restricts operations.

### 3.5 Edge availability custodian

Definition:

- The component responsible for bounded offline behavior, last-known-good state, and safe degradation.

UM answer:

- This is usually an edge, display, client cache, or local relay role.
- It is not solved by the choice of substrate alone.

Applied example:

- A venue edge continues to use an unexpired cached manifest but blocks sensitive actions when trust freshness cannot be revalidated.

### 3.6 Closed-surface bridge adapter

Definition:

- A bridge that maps UM-controlled policy and projections into a proprietary or constrained platform.

UM answer:

- This role is always non-normative.
- It must still honor consent, TTL, trust posture, and pointer-first behavior.

Applied example:

- A game or commerce platform receives only the reduced view it is permitted to consume; the bridge adapter performs format conversion, not authority substitution.

## 4. Evaluation criteria the project should apply

A substrate is only useful to UM guidance if it can be evaluated against explicit criteria.

Required criteria:

- `Role coverage`: which role or roles can it actually fill safely?
- `Source-of-truth clarity`: does it define or support where authority really lives?
- `Refresh model`: how do updates propagate, and how does a stale consumer recover?
- `Failure behavior`: what happens when the substrate is offline, delayed, inconsistent, or malicious?
- `Consent compatibility`: can the runtime still remain the authority for disclosure decisions?
- `Pointer-first fit`: can the substrate be used without forcing UM to embed large or live payloads?
- `Lock-in risk`: would adopting it make UM appear dependent on one ecosystem?
- `Public/private fit`: is the substrate fundamentally better for private state, public distribution, trust, or relay?

## 5. Official-source substrate review

## 5.1 Solid Protocol

Current source status:

- Solid Protocol is published by the Solid Community Group and the latest published report is modified `2024-05-12`.
- It explicitly says it is not a W3C Standard and not on the W3C Standards Track.
- Source: [Solid Protocol](https://solidproject.org/TR/protocol)

What the source says:

- Solid provides secure and permissioned access to externally stored data in an interoperable way.
- It defines storage resources, reading and writing resources, Linked Data Notifications, Live Update, WebID, Solid-OIDC, and authorization surfaces such as Web Access Control.

Role fit:

- Strongest fit: `canonical private state substrate example`.
- Secondary fit: `resource notification / live-update support`.
- Weak fit: `broad trust federation`.
- Weak fit: `large-scale public relay`.

Why it fits UM:

- Solid is a clean example of an external storage target that preserves pointer-first architecture.
- It supports permissioned external state while keeping that state outside the manifest itself.

Why it does not solve everything:

- It is not standards-track final in the W3C sense.
- It does not by itself solve verifier/issuer trust federation.
- It does not provide a universal large-scale public event fan-out model comparable to a public social relay protocol.

Applied example:

- The runtime stores the authoritative private profile and consent resources in a Solid storage.
- The manifest carries pointers to those resources.
- Consumers still treat the runtime and current authoritative pointers as the decision authority, not the storage substrate alone.

Failure behavior expectation:

- If Solid storage is unavailable, use only unexpired last-known-good cache.
- Do not upgrade permissions based on stale cached state.
- Sensitive actions must degrade to restricted mode when freshness cannot be confirmed.

UM recommendation level:

- Keep as `architecture-context example only`.
- Do not present as a recommended canonical store.

## 5.2 Decentralized Web Node (DWN)

Current source status:

- DWN is a `DRAFT` specification under active development within DIF.
- Source: [DIF Decentralized Web Node](https://identity.foundation/decentralized-web-node/spec/)

What the source says:

- DWN is a data storage and message relay mechanism for data related to a DID.
- An entity may operate multiple nodes that sync to the same state across one another.
- The design explicitly aims to avoid dependence on location- or provider-specific infrastructure.
- DWN protocols can define types, structure, roles, object capabilities, and enforced limitations.
- DWN supports encryption at the individual message level.

Role fit:

- Strongest fit: `canonical private state substrate candidate`.
- Strongest fit: `relay/sync coordinator candidate`.
- Weak fit: `public projection broker at broad public-network scale`.
- Weak fit: `standards-final trust federation`.

Why it fits UM:

- It maps closely to the project's active-runtime, subject-controlled, sync-aware direction.
- It is the clearest current example of a substrate that tries to combine subject-controlled data, replication, relay, and protocol-shaped interaction.

Why it does not solve everything:

- It is still draft-stage.
- The project would risk overcommitting if it promoted DWN into adopter-facing recommendation today.
- It is a substrate candidate, not a replacement for UM's runtime and policy model.

Applied example:

- The runtime writes authoritative preference and consent records to multiple user-controlled DWN nodes.
- A relying-party bridge receives only a verifier-scoped or world-scoped projection via a policy-governed process.
- The manifest continues to carry pointer and consent semantics rather than raw DWN protocol behavior.

Failure behavior expectation:

- Replicated nodes may diverge temporarily.
- Consumers must still validate currentness, conflict rules, and revocation posture before trusting the result.
- A node being reachable does not by itself prove the data is the current authority.

UM recommendation level:

- Keep as `research-only substrate candidate`.
- Do not promote to adopter-facing guidance yet.

## 5.3 AT Protocol

Current source status:

- AT Protocol has active production sync and repository specifications.
- Source: [AT Protocol Sync](https://atproto.com/specs/sync), [AT Protocol Repository](https://atproto.com/specs/repository)

What the source says:

- Synchronization of public data between independent network participants is a defining feature.
- Full repository exports plus real-time firehose streams together provide a complete, live-updated, authenticated copy of network data.
- Firehose updates can be aggregated by relays.
- Repository data synchronized over the firehose is self-certifying and signed.
- Larger binary media are referenced by content hash instead of being stored directly in repositories.

Role fit:

- Strongest fit: `public projection broker`.
- Strongest fit: `public relay/sync substrate`.
- Weak fit: `canonical private state authority`.
- Weak fit: `trust federation for verifier/issuer ecosystems`.

Why it fits UM:

- It is a strong example of how public-facing projections and event distribution can work at network scale.
- Its pointer-heavy and signed-public-state characteristics align well with UM's projection model.

Why it does not solve everything:

- The sync design is explicitly about public data distribution.
- It is not the right general answer for private consent state, verifier-gated proof policy, or subject-private canonical runtime state.

Applied example:

- A creator's public social identity projection is emitted through an AT-compatible surface while the authoritative private state remains under the runtime.
- The manifest points to the public profile or account handle, but the runtime does not treat AT Protocol as its private source of truth.

Failure behavior expectation:

- Public projection lag is tolerable within policy limits.
- It must not silently become the authority for private state if the canonical private store is unavailable.
- Consumers must distinguish “public projection is fresh enough” from “private authority is current.”

UM recommendation level:

- Keep as `architecture-context example` for public projection and public sync only.
- Do not present it as a general federation substrate for UM.

## 5.4 OpenID Federation

Current source status:

- OpenID Federation 1.0 is `Final`, published `2026-02-17`.
- Source: [OpenID Federation 1.0 Final](https://openid.net/specs/openid-federation-1_0-final.html)

What the source says:

- It describes how entities establish trust through a trust anchor.
- It only concerns itself with how entities in a federation get to know about each other.
- It defines trust infrastructure building blocks for OpenID Connect and OAuth contexts and can be used by other application protocols for trust establishment.

Role fit:

- Strongest fit: `trust federation gatekeeper`.
- Weak fit: `canonical private state authority`.
- Weak fit: `relay/sync coordinator`.
- Weak fit: `public projection broker`.

Why it fits UM:

- It is the cleanest currently-final standards-family answer for issuer/verifier/relying-party trust relationships.
- It can strengthen wallet and verifier trust decisions without distorting UM into a federation registry itself.

Why it does not solve everything:

- It is explicitly about entity discovery and trust establishment.
- It does not solve subject-state storage, subject-state portability, public projection, or live synchronization.

Applied example:

- A wallet receives an OpenID4VP request from a verifier and uses a federation trust chain to decide whether this verifier class is eligible for disclosure under local policy.
- The wallet still relies on UM consent and runtime policy for what to disclose.

Failure behavior expectation:

- If trust-chain resolution fails or cannot be validated, disclosure should fail closed or restrict to a lower-risk path.
- A valid trust chain does not override UM consent or runtime disclosure rules.

UM recommendation level:

- Safe for `bounded current guidance` as trust-federation context.
- Not a solution for “UM federation” in the broader state-portability sense.

## 5.5 Spatial-fabric and scene-network surfaces

Current source status:

- The fresh spatial-fabric crosscheck is recorded at `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-omb-wiki-spatial-fabric-crosscheck.md`.

What that report established:

- The current UM core boundary remains correct.
- The real gap is source completeness and integration-doc depth, not missing required core schema.
- Spatial-fabric material is best understood as projection, composition, and runtime-service context, not as the canonical private state substrate.

Role fit:

- Strongest fit: `public projection broker` for spatial topology and scene attachment references.
- Strongest fit: `closed/open world composition surface`.
- Weak fit: `canonical private state authority`.

UM implication:

- Spatial-fabric surfaces should continue to receive pointer/facet-based treatment.
- Stronger RP1/MSF bridge guidance should wait for the recommended primary-source refresh.

## 5.6 Closed-surface adapters

Current source status:

- This is a repo architecture pattern, not a named standards family.
- Primary repo sources: `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md` and `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md`

What the repo says:

- Closed-surface adapters and automation bridges are implementation detail.
- They must still honor consent, TTL, pointer-first behavior, and forward compatibility.

Role fit:

- Strongest fit: `closed-surface bridge adapter` only.

Applied example:

- A proprietary commerce or game platform accepts a reduced JSON mapping produced by an adapter.
- The adapter reads UM-controlled state, transforms it, and pushes only the allowed subset to the closed API.
- The closed platform never becomes the authority for the original state.

Failure behavior expectation:

- If bridge mapping or refresh fails, stale or overprivileged data must not continue indefinitely.
- The adapter should fall back to minimal, last-known-good, or no-disclosure modes depending on policy risk.

## 6. Source-of-truth, refresh, and failure-mode expectations

The project should standardize its language here even if it does not standardize one substrate.

## 6.1 Source of truth

Required answer:

- The subject-controlled runtime is the authoritative decision point for current subject state.
- External substrates are attached stores, relay planes, trust planes, or projection planes.
- A consumer should treat any external substrate as authoritative only through the runtime's declared `authoritativeSource` or equivalent pointer model.

Consequence:

- A consumer must never infer that “reachable storage” equals “current authority”.
- A public projection endpoint must never silently substitute for the current private authority.

## 6.2 Refresh model

Required answer:

- Use the existing UM synchronization profile model:
  - authoritative source pointer,
  - optional change log,
  - optional snapshot,
  - TTL and freshness checks,
  - deterministic conflict resolution,
  - retry with bounded degradation.

Consequence:

- Different substrates may provide different eventing or transport mechanisms, but they should all map back to the same authoritative refresh contract.

## 6.3 Failure behavior

Required answer:

- Validation failure: hard stop.
- Signature or trust failure: hard stop for sensitive actions.
- Source unavailable: degrade to unexpired last-known-good where policy allows.
- Authority conflict: deny-biased merge or hold previous authoritative state until reconciled.
- Public projection lag: tolerable only for public or low-risk views.
- Closed-surface bridge failure: do not continue using stale privileged state indefinitely.

Applied example:

- A world client can continue showing a cached public avatar while offline if the manifest is unexpired.
- The same client cannot continue granting commerce or compliance actions if the trust or consent state can no longer be refreshed.

## 7. Replacement and integration questions

### 7.1 Should any current UM concept be replaced by one substrate?

Answer: `No`.

What should not be replaced:

- subject-controlled runtime,
- pointer-first manifest contract,
- consent-first disclosure,
- TTL/freshness posture,
- optional-facet extensibility.

What should be adopted from external sources instead of re-invented locally:

- storage and permission patterns from Solid where a web storage substrate is desired,
- replicated node/message-relay patterns from DWN research when DID-centered private replication is being evaluated,
- public sync and projection patterns from AT Protocol where public distribution is the actual role,
- trust-anchor and trust-chain patterns from OpenID Federation where verifier/issuer trust is the actual role.

### 7.2 Can federation or bridge strategy be integrated directly as a facet?

Answer: `No, not as the primary design`.

A facet can safely carry:

- canonical-source pointer metadata,
- public projection references,
- change-log references,
- social/account handles,
- scene package or world package references,
- bridge configuration references for a specific implementation.

A facet should not be treated as:

- the federation protocol itself,
- the live relay/session plane,
- the trust chain carrier of record,
- or the whole synchronization contract.

## 8. Recommendation on follow-on guidance work

Follow-on guidance work is justified.

It should land in this order.

### 8.1 First landing surface: shared runtime and synchronization guidance

Recommended first targets:

- `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md`
- `/Users/grig/work/repo/universalmanifest/docs/guides/MUM-SYNCHRONIZATION-PROFILE.md`

Why:

- These are the correct shared documents for role taxonomy, source-of-truth rules, refresh rules, and closed-surface boundary language.
- They can absorb the decision package without making any one substrate look normative.

### 8.2 Second landing surface: substrate-specific integration updates only when justified

Examples:

- RP1/MSF integration refresh after the primary-source refresh recommended by `WO-0136`.
- A future public-projection lane if the project decides to treat AT-compatible public distribution as worth a dedicated integration page.
- A future trust-federation explainer if verifier/issuer trust chains become a recurring adopter need.

Why:

- Substrate-specific surfaces should only be strengthened after their role is bounded and the supporting sources are current.

### 8.3 Not justified now

Not justified now:

- spec core changes,
- registry changes that imply one substrate is standard,
- adopter-facing language claiming that UM has chosen a universal federation substrate.

## 9. Final assessment against the work-order acceptance criteria

### Acceptance criterion 1

Criterion:

- The decision package is role-based rather than vendor-based.

Result:

- `Satisfied`.

### Acceptance criterion 2

Criterion:

- Source-of-truth, refresh, and failure-mode expectations are explicit.

Result:

- `Satisfied`.

### Acceptance criterion 3

Criterion:

- Closed-surface behavior remains clearly non-normative.

Result:

- `Satisfied`.

### Acceptance criterion 4

Criterion:

- The result states whether follow-on guidance work is justified and where it should land.

Result:

- `Satisfied`.
- Explicit answer: `yes, follow-on guidance work is justified; it should land first in shared runtime/synchronization docs, then in bounded substrate-specific docs only where sources and scope support it`.

## 10. Sources

Primary standards and protocol sources reviewed:

- [Solid Protocol](https://solidproject.org/TR/protocol)
- [DIF Decentralized Web Node](https://identity.foundation/decentralized-web-node/spec/)
- [AT Protocol Sync](https://atproto.com/specs/sync)
- [AT Protocol Repository](https://atproto.com/specs/repository)
- [OpenID Federation 1.0 Final](https://openid.net/specs/openid-federation-1_0-final.html)

Key repo sources aligned in this assessment:

- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md`
- `/Users/grig/work/repo/universalmanifest/docs/guides/MUM-SYNCHRONIZATION-PROFILE.md`
- `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
- `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-protocol-volatility-proximity-and-federation-research-first-decision-package.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-protocol-recommendation-governance-and-standards-currency-matrix.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-omb-wiki-spatial-fabric-crosscheck.md`
- `/Users/grig/work/repo/universalmanifest/research/federation/universal-manifest-workstream.md`
- `/Users/grig/work/repo/universalmanifest/research/reference-platform/interoperability-sync.md`
