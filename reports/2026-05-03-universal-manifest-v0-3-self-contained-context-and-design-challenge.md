# Universal Manifest v0.3: Self-Contained Context And Design Challenge For A Remote Reasoning Agent

Date: 2026-05-03

Prepared for: a remote high-reasoning strategy/specification/design agent that may have no repository checkout, no localhost access, no browser access, no private chat history, and no ability to ask for missing project context before thinking.

This document is intentionally verbose. Its purpose is to transfer enough context for the remote agent to reason seriously about Universal Manifest v0.3 without flattening the project into a vague interoperability idea.

## 1. The Assignment

The remote agent should work out, in detail, what Universal Manifest v0.3 should become and how it should be built into the existing Universal Manifest system.

The agent should not immediately implement code. The desired output from that agent is a detailed v0.3 design/spec/build proposal that can be reviewed by the project owner and then converted into work orders.

The agent should reason from this document as the source context. It should not assume that a public website is current, that a local preview exists, or that it can inspect private repo files. Absolute file paths are included for traceability, but the core project model and v0.3 challenge are embedded here.

The agent must not produce a meta-document about creating a document. It must make concrete decisions or decision recommendations about v0.3: what should become normative, what should remain guidance, what needs fixtures, what needs conformance, what belongs in the public reader path, what belongs in implementation helpers, and what should be deferred.

## 2. One-Paragraph Project Definition

Universal Manifest is a portable, signed context envelope for systems that do not share one backend. It carries identity references, claims, permissions, pointers, proof, and validity rules so a receiving system can inspect what it may trust, use, request, follow, ignore, reject, or project. It is not a wallet, account system, identity provider, DID method, object store, social graph, payment rail, resolver backend, or product. It is a standard document shape plus an evaluation contract at a system boundary.

## 3. The Core Mental Model

Universal Manifest exists for the moment when one system receives context it did not create.

The important boundary sequence is:

```text
source context -> signed manifest envelope -> receiver inspection -> allowed projection/action
```

A subject, issuer, device, service, runtime, agent, or environment has state somewhere. That state may include identity information, credential facts, profile details, consent settings, asset pointers, runtime capabilities, device registration, social handles, proof-of-personhood references, or domain-specific records. Another system wants to act on some of that context, but it does not share the same backend, data model, account system, or trust infrastructure.

Without Universal Manifest, each receiving system writes custom import logic, asks the user to rebuild state, scrapes a profile, copies more data than needed, trusts stale information, or invents yet another integration-specific consent model.

With Universal Manifest, the receiving system gets a bounded, signed, machine-readable envelope. The receiver can evaluate:

- what subject the envelope is about,
- which claims are being asserted,
- which permissions or consents apply,
- which external pointers are authoritative,
- what proof or signature supports the envelope,
- when the envelope was issued,
- when it expires,
- whether revocation/freshness must be checked,
- which unknown fields it should ignore,
- which supported fields it may project into its local surface.

Universal Manifest should make context portable without pretending that all data must be copied into the manifest. Large, mutable, private, domain-specific, or authoritative data can stay where it belongs. The manifest may carry a pointer, permission, proof, scope, expiry, and processing contract around that data.

## 4. Current Project State

### 4.1 v0.2 is published, but deployment state is not the same as spec state

Universal Manifest v0.2 has been released as the current published version.

Known publication facts:

- Release tag: `spec-v0.2`
- GitHub release: `https://github.com/grigb/universal-manifest/releases/tag/spec-v0.2`
- Published spec route intended: `https://universalmanifest.net/spec/v0.2/`
- Latest spec route intended: `https://universalmanifest.net/spec/latest/`
- Local evidence pack: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-30-v0-2-publication-evidence-pack.md`

Important caveat: public deployment may be stale because gated Cloudflare deployment is blocked by invalid GitHub Actions Cloudflare credentials. The repo and CI have green states for the latest local work, but production may not yet show all local routes. Do not treat current production route behavior as the only source of truth.

### 4.2 Current local/source status

The current local project has:

- v0.2 spec artifacts under `/Users/grig/work/repo/universalmanifest/spec/v0.2/`
- conformance fixtures and runner under `/Users/grig/work/repo/universalmanifest/conformance/`
- a TypeScript helper/reference package under `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/`
- a resolver contract under `/Users/grig/work/repo/universalmanifest/services/myum-resolver/CONTRACT.md`
- public site source under `/Users/grig/work/repo/universalmanifest/site/`
- homepage cluster source under:
  - `/Users/grig/work/repo/universalmanifest/site/src/pages/index.astro`
  - `/Users/grig/work/repo/universalmanifest/site/src/pages/use-cases/index.astro`
  - `/Users/grig/work/repo/universalmanifest/site/src/pages/explorer/index.astro`
  - `/Users/grig/work/repo/universalmanifest/site/src/pages/how-it-works/index.astro`
  - `/Users/grig/work/repo/universalmanifest/site/src/pages/standards-fit/index.astro`
  - `/Users/grig/work/repo/universalmanifest/site/src/data/home-cluster.ts`
  - `/Users/grig/work/repo/universalmanifest/site/src/styles/public-surface.css`

The homepage design/reader path is still actively being corrected. That matters because v0.3 cannot be understood or adopted if the public front door remains unclear.

### 4.3 Current blockers outside v0.3 design

Two blockers matter but should not stop v0.3 thinking:

- `WO-0255`: public route/deployment verification is blocked by Cloudflare credential failure.
- `WO-0256`: external reader validation is blocked until production route verification succeeds and a real external-reader cohort/process exists.

The remote agent should not treat these as reasons to avoid v0.3 design. It should treat them as constraints on evidence collection and public-reader validation.

## 5. v0.1 And v0.2 Baseline

### 5.1 v0.1 baseline

v0.1 established the adoption-friendly minimum shape:

- a JSON-LD-compatible manifest document,
- required fields for identity, type, version, subject, issuance, and expiry,
- TTL/freshness enforcement,
- unknown-field tolerance,
- examples and fixtures,
- conformance expectations for accepting valid fixtures and rejecting invalid fixtures,
- early integration lanes and proof journeys.

The most important v0.1 principle is forward compatibility: consumers must safely ignore fields they do not understand. That principle is core to Universal Manifest because the whole project assumes a multi-domain ecosystem where not every receiver understands every extension.

### 5.2 v0.2 baseline

v0.2 made integrity real.

The v0.2 required fields are:

- `@context`
- `@id`
- `@type`
- `manifestVersion`
- `subject`
- `issuedAt`
- `expiresAt`
- `signature`

The v0.2 signature profile is:

- `signature.algorithm` must be `Ed25519`
- `signature.canonicalization` must be `JCS-RFC8785`
- the signing input removes the top-level `signature` property,
- the remaining object is canonicalized with JCS,
- Ed25519 signs the canonical bytes,
- consumers verify using embedded `signature.publicKeySpkiB64` or key material referenced by `signature.keyRef`,
- consumers reject invalid signatures, unsupported profile pairs, expired manifests, invalid timestamps, and malformed key material.

v0.2 optional/extensible top-level arrays include:

- `facets`
- `claims`
- `consents`
- `devices`
- `pointers`

v0.2 also introduces or documents:

- `claims[].claimProof` as a way to attach or reference proof for a claim,
- optional revocation metadata such as `signature.statusRef` and `signature.revocationCursor`,
- revocation-aware verification as an optional conformance extension,
- Tier 1 assurance obligations when claimed,
- projection-derived manifests as the broad privacy path,
- encrypted inline facets as optional guidance,
- Data Integrity/RDF graph-signing as future, not v0.2.

### 5.3 v0.2 maturity

The v0.2 publication evidence pack says all done-done gates passed for early-adopter maturity:

- G1 Contract completeness
- G2 Conformance testability
- G3 Integrity and trust profile
- G4 Interoperability proof
- G5 Publishing and discoverability
- G6 Governance and change control
- G7 Operational realism

This does not mean UM is world-ready. The project uses three maturity levels:

- Maturity A: early-adopter ready, v0.x
- Maturity B: production-candidate standard
- Maturity C: world-ready standard

v0.2 is an early-adopter-ready release. v0.3 must decide whether it remains a controlled v0.x increment or becomes a push toward production-candidate maturity.

## 6. Non-Negotiable Invariants

v0.3 should not violate these without an explicit, reviewed breaking-change decision.

### 6.1 UM is pointer-first

Universal Manifest should not become a blob container for all user data. It should keep the distinction between:

- context that travels inside the manifest,
- authoritative data that remains external,
- proof material that may be embedded or referenced,
- mutable data that should be fetched or refreshed from a source,
- private data that should be projected or encrypted rather than broadly copied.

### 6.2 UM is provider-neutral

UM must not require one DID method, wallet, identity provider, storage provider, resolver, cloud, ledger, credential stack, app runtime, or implementation language.

It may define profiles that compose with those systems, but baseline conformance should remain possible without adopting a whole external ecosystem.

### 6.3 UM is receiver-evaluable

The manifest must help a receiver decide what to do. Every new v0.3 feature should answer:

- What does the receiver verify?
- What does the receiver trust?
- What does the receiver ignore?
- What does the receiver reject?
- What does the receiver project?
- What does the receiver fetch?
- What does the receiver treat as unchecked?
- What local policy remains local?

### 6.4 UM is not a backend replacement

The resolver, runtime, wallet, pod, issuer, and storage layer can all exist, but UM should not collapse into one official backend model.

### 6.5 Unknown-field tolerance must survive

Receivers should continue to ignore unsupported extension fields safely. v0.3 may define stricter profiles, but it must not destroy the ability for older or narrower consumers to process the parts they understand.

### 6.6 The public reader path is part of the standardization problem

If v0.3 is technically coherent but unreadable to implementers, it fails. A spec version is not just schema files. It includes migration guidance, conformance fixtures, examples, public docs, and a first-time path that explains what changed.

## 7. The Real v0.3 Challenge

v0.3 is not "add more fields."

v0.3 is the point where Universal Manifest must decide how much real-world complexity it can standardize without collapsing under scope. The core problem is context transfer across trust boundaries. The hard parts are not naming fields; the hard parts are preserving meaning, privacy, freshness, proof, and receiver behavior when the manifest crosses systems that do not share:

- the same backend,
- the same identity provider,
- the same wallet,
- the same data model,
- the same policy engine,
- the same trust anchors,
- the same freshness semantics,
- the same privacy expectations,
- the same runtime assumptions.

The agent should think of v0.3 as a release that must choose between three possible shapes:

1. A focused v0.x increment that formalizes one or two high-value areas.
2. A production-candidate step that makes receiver behavior, revocation, projection, and conformance much more complete.
3. A research decision package that says v0.3 is not ready until identity binding, revocation, and privacy profiles are resolved.

The likely best path is not maximal scope. It is a disciplined v0.3 that makes UM more useful at real boundaries while preserving implementability.

## 8. Candidate v0.3 Release Thesis

Recommended thesis to evaluate:

> Universal Manifest v0.3 should turn the signed envelope from a verifiable packet into a policy-aware, privacy-aware, freshness-aware exchange contract, while keeping UM pointer-first and provider-neutral.

That thesis suggests v0.3 should focus on:

- a clearer receiver evaluation model,
- a more formal projection model,
- a revocation/freshness conformance profile,
- a stronger but still optional claim-proof/trust-tier model,
- better extension grammar for records/facets/pointers,
- conformance fixtures that exercise misuse cases,
- migration guidance from v0.2,
- public docs that explain the new trust/privacy model.

The remote agent may reject or refine this thesis, but it should propose an equally concrete thesis.

## 9. Deep Challenge Area: Context Transfer

Context transfer is harder than data transfer.

Data transfer asks: "Can I send bytes from A to B?"

Context transfer asks:

- What do the bytes mean?
- Who said them?
- Who are they about?
- What is the receiver allowed to do with them?
- What changed since they were signed?
- What should remain private?
- What is authoritative elsewhere?
- What proof supports each claim?
- Does the receiver understand this part?
- What if the receiver understands the profile but not the domain extension?
- What if the manifest is valid but stale?
- What if the signature is valid but the claim proof is weak?
- What if the subject uses multiple identifiers?
- What if the issuer and subject are different?
- What if the manifest is audience-specific?
- What if a pointer is valid but the target is unavailable?
- What if a private facet is present but unreadable?

v0.3 must make those questions more explicit without requiring all consumers to solve every possible identity and policy problem.

The most important design move may be to define a receiver decision pipeline:

1. Parse the manifest.
2. Check required fields and version.
3. Check resource limits.
4. Check TTL and timestamp consistency.
5. Identify supported signature/integrity profile.
6. Verify the envelope signature.
7. Classify unknown fields and unsupported profiles.
8. Evaluate revocation/freshness if required by profile or local policy.
9. Evaluate claims and claim proof according to declared/required trust tier.
10. Evaluate permissions and consents.
11. Evaluate pointers and whether following them is permitted.
12. Evaluate private/encrypted/projection metadata.
13. Project only supported, allowed, fresh-enough context.
14. Report acceptance state, downgraded state, unchecked state, opaque state, or rejection state.

v0.3 should consider whether this pipeline becomes normative, profile guidance, or conformance-language structure.

## 10. Deep Challenge Area: Records, Facets, Claims, Consents, Devices, Pointers

The project vision says a Record may become the core primitive. Current v0.2 uses open arrays:

- `facets`: named or typed sections, with optional entity/ref fields,
- `claims`: open objects, optionally with `claimProof`,
- `consents`: open objects,
- `devices`: open objects,
- `pointers`: open objects.

That openness made v0.1/v0.2 adoption easier. It also creates convergence risk. If every adopter invents incompatible shapes inside these arrays, the envelope remains signed but the ecosystem still fragments.

v0.3 must decide how much structure to add.

Key design questions:

- Should `records` become a top-level array?
- Should `facets` remain the main extension unit?
- Are records and facets different, or are facets just records with a role?
- Should each record/facet declare `@type`, `schema`, `namespace`, `visibility`, `audience`, `source`, `proof`, `consent`, and `pointers`?
- Should claims be separate from records, or should claims be records?
- Should consent apply to fields, records, pointers, projections, or whole manifests?
- Should pointers have a standard shape with `name`, `href`, `mediaType`, `integrity`, `authority`, `refresh`, `privacy`, `purpose`, and `fallback`?
- Should devices become a profile rather than a baseline concept?
- Should v0.3 keep the v0.2 arrays and only define recommended sub-shapes to avoid breaking compatibility?

One possible v0.3 approach:

- Keep `facets`, `claims`, `consents`, `devices`, and `pointers` valid for compatibility.
- Introduce a formal optional `records` array as a v0.3 candidate, but do not require all existing use cases to migrate immediately.
- Define a common "portable record" grammar that can be used inside `facets` or `records`.
- Define conformance around receiver behavior, not around understanding every record namespace.

Candidate record shape for discussion, not final spec:

```json
{
  "@id": "urn:uuid:record-123",
  "@type": ["um:Record", "schema:Person"],
  "name": "Public profile projection",
  "namespace": "profile.public",
  "visibility": "public",
  "schemaRef": "https://schema.org/Person",
  "sourceRef": "https://pod.example/alice/profile",
  "audience": "https://gallery.example",
  "purpose": "display-profile",
  "entity": {
    "name": "Alice Example",
    "image": "https://cdn.example/alice/avatar.png"
  },
  "permissions": {
    "show": true,
    "store": false,
    "share": false
  },
  "validity": {
    "issuedAt": "2026-05-03T00:00:00Z",
    "expiresAt": "2026-05-04T00:00:00Z"
  }
}
```

The agent should decide whether this direction is too much for v0.3, exactly right, or better handled as guidance.

## 11. Deep Challenge Area: Projection

Projection may be the central privacy/interoperability concept for v0.3.

A projection is a receiver-appropriate view of broader source context. Instead of sending the whole private source state, the subject/issuer/runtime produces a manifest or record containing only the context that a particular receiver, audience, purpose, or surface is allowed to see.

Projection is already a strong pattern in UM:

- public profile projection,
- metaverse cross-world projection,
- portable identity projection,
- GPC evidence projection,
- RP1/spatial fabric projection,
- education/credential verification projection,
- healthcare/patient consent projection.

The v0.3 challenge is that projection needs lifecycle semantics.

Questions:

- Is a projection a full independent manifest or a record inside a manifest?
- Does every projection need its own signature?
- Does a projection reference the source manifest?
- Does it include derivation metadata?
- Does it declare audience and purpose?
- Does it expire independently?
- How does revocation work when source state changes?
- How does a receiver know whether a projection is stale?
- Can a projection be safely cached?
- What happens when the receiver receives a projection with unknown fields?
- How does projection interact with encrypted facets?

Candidate projection metadata for discussion:

```json
{
  "@type": "um:Projection",
  "sourceManifest": "urn:uuid:source-manifest",
  "derivedAt": "2026-05-03T00:00:00Z",
  "audience": "https://gallery.example",
  "purpose": "display-public-profile",
  "scope": ["profile.name", "profile.avatar", "portfolio.links"],
  "basis": "consent",
  "sourceVersion": "v17",
  "invalidatesAfter": "2026-05-04T00:00:00Z",
  "regeneration": "required-when-consent-or-source-changes"
}
```

Recommended v0.3 question:

Should v0.3 make projection-derived manifests the normative privacy path, with explicit metadata and fixtures, while keeping encrypted inline facets as an optional profile?

This is likely the most adoption-safe direction because it lets simple receivers process clear, bounded manifests without requiring decryption capability.

## 12. Deep Challenge Area: Encrypted Inline Facets

Encrypted inline facets are useful when the envelope should remain one document but some facet content must be unreadable to unauthorized receivers.

v0.2 treats encrypted inline facets as optional guidance. v0.3 must decide whether to promote them.

The hard part is not "can something be encrypted." The hard parts are:

- where key references live,
- how recipients are expressed,
- whether the encrypted payload is included in signature input,
- whether encryption happens before signing or after signing,
- how metadata stays cleartext enough for routing,
- how consumers report opaque/unreadable facets,
- how key rotation works,
- what happens if a receiver can verify the envelope but cannot decrypt a facet,
- what conformance means for consumers that do not implement decryption,
- what algorithms are mandatory, recommended, optional, or out of scope.

Candidate encrypted facet shape for discussion:

```json
{
  "@id": "urn:uuid:facet-private-contact",
  "@type": ["um:Facet", "um:EncryptedFacet"],
  "name": "Private contact data",
  "visibility": "encrypted",
  "encryption": {
    "profile": "HPKE-v1",
    "contentEncryption": "A256GCM",
    "keyAgreement": "X25519",
    "recipients": [
      {
        "kid": "did:web:receiver.example#key-1",
        "encryptedKey": "..."
      }
    ],
    "aad": "manifest:@id + facet:@id"
  },
  "ciphertext": "...",
  "cleartextDescriptor": {
    "purpose": "support-contact",
    "dataClass": "contact",
    "requiredPermission": "contact.read"
  }
}
```

This shape may be too specific for v0.3 if external crypto review is not available. The agent should evaluate whether the right v0.3 move is:

- keep encrypted facets as guidance,
- define only an abstract encrypted facet envelope,
- choose an algorithm profile and create fixtures,
- require only opaque-facet handling by baseline consumers,
- split encrypted facets into a named optional conformance profile.

Recommended caution: do not make encrypted inline facets baseline v0.3 unless the project can produce clear conformance fixtures and security review criteria.

## 13. Deep Challenge Area: Revocation, Freshness, And Status

v0.2 has TTL and optional revocation metadata. TTL says "do not use after this time." Revocation says "even before expiry, this envelope or proof may no longer be valid." Freshness says "this context may be too old for the receiving use case."

These are related but not identical.

v0.3 needs to separate:

- manifest expiry,
- proof expiry,
- claim expiry,
- pointer freshness,
- source version freshness,
- revocation state,
- cache revalidation,
- receiver local freshness policy.

Questions:

- Should `statusRef` become required for v0.3 baseline?
- Should `revocationCursor` become normative?
- Should revocation be a profile: `v0.3-baseline` vs `v0.3-revocation-aware`?
- What status response shape is expected?
- What should a receiver do if status is unavailable?
- Does fail-closed apply only to high-trust contexts?
- Can low-risk receivers accept with `revocation: unchecked`?
- Should conformance fixtures include revoked, stale, unavailable, regressed-cursor, and mismatched-status cases?

Candidate status model:

```json
{
  "manifest": "urn:uuid:manifest-123",
  "status": "valid",
  "cursor": "2026-05-03T00:00:00Z:17",
  "updatedAt": "2026-05-03T00:00:00Z",
  "expiresAt": "2026-05-03T01:00:00Z",
  "reason": null
}
```

Candidate receiver statuses:

- `accepted`
- `accepted-with-revocation-unchecked`
- `downgraded`
- `opaque-partial`
- `rejected-expired`
- `rejected-invalid-signature`
- `rejected-revoked`
- `rejected-status-unavailable`
- `rejected-policy`
- `unsupported-profile`

Recommended v0.3 direction to evaluate:

Make revocation/freshness a named optional conformance profile in v0.3, but make the reporting vocabulary normative. That lets baseline consumers stay simple while preventing them from claiming revocation-aware behavior they did not perform.

## 14. Deep Challenge Area: Claim Proof, Trust Tiers, And Identity Binding

v0.2 has a Tier 1 posture and `claimProof`, but stronger binding is deferred.

The hard problem is the "Bag of Claims" vulnerability: a manifest can collect claims that look impressive, but unless the receiver understands issuer trust, subject binding, audience binding, proof freshness, and cross-identifier relationships, the manifest may imply more trust than it actually has.

v0.3 must decide how far to go.

Possible trust tiers:

- Tier 0: self-asserted or envelope-only integrity. The manifest is signed, but claims may not have external proof.
- Tier 1: claimProof-backed attestation. The receiver can evaluate issuer/attester trust, proof expiry, and audience binding according to policy.
- Tier 2: cryptographic subject binding. Stronger link between subject identifiers and claim subjects, possibly through verifiable presentations, DIDs, keys, or pairwise identifiers.
- Tier 3: multi-party ceremony or higher-assurance binding. Likely future scope, requiring evidence and review beyond v0.3 unless narrowly profiled.

Questions:

- Should v0.3 define a `trustTier` field?
- Should `requiredTrustTier` be a receiver policy, manifest declaration, claim property, or profile requirement?
- Should `claimProof` accept URI references, embedded VP-like objects, or both?
- Should v0.3 define minimal proof metadata without adopting a full VC stack?
- How does a receiver report "signature valid, claim proof unchecked"?
- How do pairwise DIDs and opaque identifiers avoid correlation?
- How can v0.3 avoid requiring DID while still allowing DID/VC integration?
- What fixtures prove rejection of mismatched claim issuer/proof issuer, stale proof, missing audience, wrong subject, or untrusted attester?

Candidate claim shape:

```json
{
  "@id": "urn:uuid:claim-123",
  "@type": "um:Claim",
  "name": "ageOver18",
  "value": true,
  "issuer": "did:web:issuer.example",
  "subject": "did:key:z6Mki...",
  "trustTier": "Tier1",
  "claimProof": {
    "type": "VerifiablePresentationReference",
    "href": "https://issuer.example/presentations/age-over-18/abc",
    "audience": "https://venue.example",
    "expiresAt": "2026-05-04T00:00:00Z",
    "statusRef": "https://issuer.example/status/abc"
  }
}
```

Recommended v0.3 stance to evaluate:

Do not make Tier 2/Tier 3 baseline. Define Tier 1 more rigorously and create fixtures that force receivers to distinguish "manifest signature valid" from "claim proof verified." Treat Tier 2 as a candidate profile if research can define promotion criteria clearly.

## 15. Deep Challenge Area: Integrity Profiles And Data Integrity/RDF

v0.2 uses JCS + Ed25519. That was chosen because it is implementable across languages and does not require JSON-LD/RDF canonicalization.

The future path may include W3C Data Integrity / RDF graph-signing semantics. The agent must reason carefully here.

JCS signs the JSON representation. Data Integrity/RDF signs graph meaning. Those are not the same. A standard can support both, but only if profile identity, signing input, verification behavior, and conformance are explicit.

Questions:

- Does v0.3 need Data Integrity now?
- Is Data Integrity necessary for standards alignment, credential ecosystem compatibility, or graph semantics?
- Does adding it in v0.3 make implementation too hard?
- Should v0.3 define a profile registry without adding a second required profile?
- Should multi-proof support exist?
- Should a manifest be allowed to carry both JCS and Data Integrity proofs?
- How do consumers choose which proof profile is sufficient?
- What does unknown proof profile tolerance mean?

Recommended caution:

The baseline should probably remain JCS + Ed25519 unless there is a strong reason and enough test evidence to add Data Integrity. v0.3 may define the registry/discovery mechanics for future profiles without requiring every consumer to implement RDF canonicalization.

## 16. Deep Challenge Area: Resolver And Distribution Semantics

The current resolver contract is public-read-only and minimal. It separates HTTP cache from manifest TTL. Consumers must enforce manifest `expiresAt` regardless of HTTP cache headers.

v0.3 must decide whether resolver behavior becomes more important to the spec.

Questions:

- Is resolver behavior normative to UM, or a reference/runtime profile?
- Should the spec define resolver response headers?
- Should resolver responses include status/freshness metadata?
- Should private/authenticated resolution remain out of scope?
- How do `statusRef`, `keyRef`, pointers, and resolver endpoints relate?
- Should content addressing or integrity hashes be required for pointers?
- Should `myum.net` remain a reference runtime, not part of baseline UM?

Recommended stance:

Keep resolver baseline small. Define how manifests can reference resolver/status/key/pointer endpoints, and define consumer obligations around TTL, status, and pointer-following. Do not make one hosted resolver part of the normative standard.

## 17. Deep Challenge Area: Conformance And Fixtures

v0.3 should not be accepted without executable evidence.

The conformance system should prove both happy paths and misuse paths.

Candidate fixture categories:

Baseline v0.3:

- valid minimal v0.3 manifest,
- valid v0.3 manifest with projection metadata,
- valid v0.3 manifest with revocation metadata but unchecked status,
- valid v0.3 manifest with Tier 1 claimProof reference,
- valid v0.3 manifest with opaque encrypted facet descriptor,
- valid v0.3 manifest with unknown extension fields safely ignored.

Invalid or rejected:

- expired manifest,
- invalid timestamp,
- missing signature,
- invalid signature,
- unsupported signature profile in strict mode,
- projection with missing audience/purpose when required by profile,
- claimProof issuer mismatch,
- claimProof expired,
- required trust tier not satisfied,
- revoked manifest,
- stale revocation cursor,
- status unavailable under fail-closed policy,
- encrypted facet malformed,
- private facet treated as readable without key,
- pointer followed despite denied permission,
- unknown field causing rejection in baseline consumer.

Conformance must distinguish:

- schema validation,
- signature verification,
- freshness/revocation verification,
- claim-proof verification,
- privacy/projection handling,
- pointer-following policy,
- receiver result reporting.

v0.3 should likely introduce named conformance profiles, for example:

- `v0.3-baseline`
- `v0.3-projection-aware`
- `v0.3-revocation-aware`
- `v0.3-claimproof-tier1`
- `v0.3-encrypted-facet-opaque`
- `v0.3-encrypted-facet-decrypting` if encryption is promoted

The agent should decide if that profile structure is too fragmented or exactly what is needed.

## 18. Deep Challenge Area: Migration From v0.2

v0.3 must not strand v0.2 adopters.

Migration questions:

- Can a v0.2 manifest remain valid as a v0.3-compatible baseline if it includes v0.3 extensions?
- Does `manifestVersion` become `"0.3"` for all v0.3 features?
- Should v0.3 keep the same required fields?
- Are any v0.2 fields renamed?
- Does v0.3 add required fields?
- Are v0.2 consumers expected to ignore v0.3 additions?
- What exact break/non-break classification applies?
- What migration examples must exist?

Recommended migration principle:

Avoid breaking v0.2 unless the release explicitly chooses a production-candidate maturity jump. Prefer additive v0.3 features, named profiles, and clear conformance modes.

Possible migration rule:

- v0.3 baseline keeps the v0.2 required field set plus tighter receiver behavior language.
- Additional v0.3 features appear through additive fields and profiles.
- v0.2 consumers can ignore unknown v0.3 fields but cannot claim v0.3 conformance.
- v0.3 consumers must process v0.2 manifests according to v0.2 rules unless local policy requires v0.3-only behavior.

## 19. Deep Challenge Area: Public Docs And First-Time Comprehension

The public homepage and docs are part of the spec's adoption surface.

v0.3 will introduce concepts that can easily become overwhelming:

- projection,
- trust tiers,
- revocation,
- status,
- claim proof,
- private facets,
- profile registries,
- resolver behavior,
- data integrity profiles.

The public reader path must not dump these concepts into one wall of text.

Recommended public documentation structure:

- Homepage: signed context envelope and boundary inspection.
- Use Cases: where UM matters in real systems.
- Explorer: one lane at a time, showing what travels and what stays authoritative.
- How It Works: envelope anatomy and receiver evaluation.
- Standards Fit: how UM composes with DID, VC, JSON-LD, Data Integrity, storage, resolver, and privacy standards.
- v0.3 Spec: normative contract.
- v0.2 to v0.3 Migration Guide: exactly what changes.
- Conformance v0.3: implementer obligations and fixtures.
- Security/Privacy Profile Guide: revocation, trust tier, projection, encrypted facets.
- Implementation Guide: build path for non-TypeScript implementers.

The agent should include public-reader consequences in the v0.3 proposal, not only schema decisions.

## 20. Deep Challenge Area: Governance

v0.3 should go through explicit decision and work-order structure.

Existing governance surfaces include:

- `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/SPEC-IMPROVEMENT-QUEUE.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/BREAKING-CHANGE-POLICY.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/DEPRECATION-POLICY.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/INCIDENT-RESPONSE.md`
- `/Users/grig/work/repo/universalmanifest/docs/governance/RELEASE-CADENCE.md`

Phase 19 already names the v0.3-adjacent inputs:

- post-publication external-human reader validation,
- adopter-feedback loop against published v0.2,
- Tier 2 cryptographic identity-binding research,
- Tier 3 multi-party ceremony research,
- Data Integrity/RDF profile decision,
- additional integrity-profile registry decision,
- revocation-as-normative decision,
- encrypted inline facet promotion decision,
- broader cross-DID binding tier scope decision.

The remote agent should not simply expand all of those into v0.3. It should rank them, decide dependencies, and identify what evidence is needed before promotion.

## 21. Recommended v0.3 Scope Options

The agent should evaluate at least these three options.

### Option A: Conservative v0.3

Scope:

- receiver evaluation pipeline,
- clearer projection metadata guidance,
- revocation-aware reporting vocabulary,
- migration guide,
- conformance profile naming,
- no new required baseline fields.

Pros:

- implementable,
- low risk,
- preserves v0.2 compatibility,
- improves clarity.

Cons:

- may not solve enough real trust/privacy complexity,
- may feel incremental.

### Option B: Balanced v0.3

Scope:

- receiver evaluation pipeline as normative,
- projection metadata as normative for projection-derived manifests,
- revocation/freshness as named optional conformance profile with required result reporting,
- Tier 1 claimProof obligations strengthened,
- opaque encrypted facet handling required, decryption profile optional,
- profile registry/discovery grammar,
- robust conformance fixtures,
- v0.2 to v0.3 migration.

Pros:

- meaningfully advances real-world use,
- avoids making encryption/Data Integrity/Tier 2 mandatory too soon,
- creates clear implementer paths,
- supports privacy and trust without overbuilding.

Cons:

- still requires careful spec writing and fixtures,
- profile structure may feel complex if docs are poor.

### Option C: Ambitious v0.3

Scope:

- formal Record primitive,
- normative revocation,
- encrypted inline facet lifecycle,
- Data Integrity/RDF proof profile,
- Tier 2 cryptographic binding,
- broader resolver/status contract,
- multi-proof handling.

Pros:

- major maturity jump,
- addresses many deferred concerns.

Cons:

- high risk of overreach,
- needs external security/standards review,
- may exceed v0.x early-adopter maturity,
- could fracture implementability.

Recommended starting stance: Option B, unless the remote agent can prove Option A or C is more appropriate.

## 22. Proposed Normative/Guidance Classification For v0.3

This is a candidate classification for the remote agent to evaluate.

Normative baseline:

- v0.2 required fields retained,
- resource limits retained or clarified,
- receiver evaluation pipeline,
- receiver result vocabulary,
- unknown-field tolerance,
- signature profile identification,
- TTL enforcement,
- strict rejection for invalid envelope signature,
- projection metadata required when a manifest claims to be a projection,
- unsupported private/encrypted facets must be treated as opaque, not as absent.

Named conformance profiles:

- revocation-aware verification,
- Tier 1 claimProof-aware verification,
- projection-aware verification,
- encrypted-facet decrypting profile if promoted,
- additional integrity profiles if accepted.

Non-normative guidance:

- subject-controlled active runtime,
- private source-of-truth architecture,
- specific wallet/pod/agent patterns,
- specific DID methods,
- specific resolver deployments,
- integration-lane examples.

Deferred unless evidence is strong:

- Tier 2 cryptographic binding as baseline,
- Tier 3 multi-party ceremony,
- mandatory Data Integrity/RDF profile,
- mandatory encrypted facet decryption,
- authenticated private resolver profile.

## 23. Concrete Questions The Remote Agent Must Answer

The remote agent should produce answers to these, not avoid them.

1. What is the v0.3 thesis?
2. What maturity target does v0.3 aim for?
3. Which fields and behaviors become normative?
4. Which profiles exist, and how are they named?
5. Does v0.3 introduce `records`?
6. What is the final relationship between records, facets, claims, consents, devices, and pointers?
7. What does a projection-derived manifest require?
8. What is the receiver evaluation pipeline?
9. What result statuses must a receiver report?
10. What does revocation-aware verification require?
11. Does v0.3 require `statusRef` or keep it profile-specific?
12. What does Tier 1 claimProof-aware behavior require?
13. What are Tier 2 promotion criteria?
14. Do encrypted inline facets become normative, profile-specific, or guidance?
15. Does v0.3 add Data Integrity/RDF support or only prepare for it?
16. How does v0.3 preserve v0.2 compatibility?
17. What fixtures prove v0.3 behavior?
18. What invalid fixtures are required?
19. What examples are required?
20. What docs/site routes need updates?
21. What implementation-helper changes are necessary?
22. What governance decisions/RFCs must be recorded before implementation?

## 24. Required Output From The Remote Agent

The remote agent should return a detailed proposal with:

1. Executive recommendation.
2. v0.3 release thesis.
3. Normative scope.
4. Non-normative guidance scope.
5. Deferred scope.
6. Field/schema/context proposal.
7. Receiver behavior proposal.
8. Privacy/projection proposal.
9. Revocation/freshness proposal.
10. Claim proof/trust tier proposal.
11. Encrypted facet proposal.
12. Integrity profile/Data Integrity proposal.
13. Resolver/distribution proposal.
14. Conformance profile and fixture matrix.
15. Migration plan from v0.2.
16. Public docs and homepage impact.
17. Implementation map to repo surfaces.
18. Work-order breakdown.
19. Acceptance criteria.
20. Risk register.

It should explicitly label every recommendation as:

- normative v0.3,
- optional conformance profile,
- implementation helper,
- public documentation,
- governance decision,
- research/deferred.

## 25. Proposed Work Orders After Review

These are candidate work orders to create only after the v0.3 proposal is reviewed.

1. v0.3 scope and thesis decision package.
2. v0.3 schema/context draft.
3. Receiver evaluation pipeline specification.
4. Projection-derived manifest profile.
5. Revocation-aware conformance profile.
6. Tier 1 claimProof verification profile.
7. Encrypted facet handling decision.
8. Integrity profile registry/Data Integrity decision.
9. v0.3 conformance fixture set.
10. v0.3 TypeScript helper updates.
11. v0.2 to v0.3 migration guide.
12. v0.3 public docs and reader-path update.
13. v0.3 release evidence pack template.
14. External implementer review and feedback loop.
15. Security/privacy review for promoted profiles.

## 26. Acceptance Criteria For v0.3

v0.3 should not be considered done unless:

- the release thesis is explicit,
- normative vs guidance boundaries are explicit,
- schema and JSON-LD context align,
- conformance profiles are named and testable,
- valid and invalid fixtures exist,
- receiver behavior is unambiguous,
- projection semantics are testable,
- revocation/freshness behavior is either profile-bound or explicitly deferred,
- claim proof/trust tier behavior is not misleading,
- privacy handling is clear for both projection and opaque/encrypted facets,
- migration from v0.2 is documented,
- public reader docs explain v0.3 without insider language,
- implementation helpers match the spec rather than becoming the spec,
- the done-done gates can be audited with evidence.

## 27. Main Risks And Anti-Patterns

### Risk: turning UM into a backend

If v0.3 requires one resolver, runtime, store, wallet, or identity provider, it violates the core provider-neutral design.

### Risk: over-standardizing before evidence

Tier 2/Tier 3 binding, encrypted facets, and Data Integrity profiles may be valuable, but premature baseline requirements could make UM too hard to adopt.

### Risk: signed but misleading claims

A manifest signature proves envelope integrity. It does not automatically prove that every claim is true, fresh, audience-bound, or backed by a trusted issuer.

### Risk: privacy leakage through identifiers

Stable global subject identifiers can create correlation. v0.3 must preserve pairwise/opaque identifier guidance and avoid turning portability into tracking.

### Risk: stale but valid packets

A signature can remain valid after the real-world state changes. TTL, revocation, status, source version, and receiver local freshness policy must be separated.

### Risk: encrypted data treated as absent

If a consumer cannot decrypt a private facet, it must not pretend the facet does not exist. It should report opaque/unreadable state.

### Risk: profile explosion

Too many profiles can confuse implementers. Too few can force all adopters into a heavy baseline. v0.3 must balance profile clarity with implementability.

### Risk: public docs collapse under complexity

If the public docs expose every technical concept at once, v0.3 will be technically good but adoption-hostile.

## 28. Source Pack Embedded Summary

Traceable local sources:

- Project vision: `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- Critical path: `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`
- Done-done definition: `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-DEFINITION.md`
- v0.2 evidence pack: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-30-v0-2-publication-evidence-pack.md`
- v0.2 overview: `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`
- v0.2 conformance: `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
- v0.2 signature profile: `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md`
- v0.2 schema: `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.json`
- v0.2 context: `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.jsonld`
- work-order index: `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`
- spec improvement queue: `/Users/grig/work/repo/universalmanifest/docs/governance/SPEC-IMPROVEMENT-QUEUE.md`
- reference runtime guidance: `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md`
- runtime profile guidance: `/Users/grig/work/repo/universalmanifest/integrations/runtime-profile.md`
- DID/VC integration: `/Users/grig/work/repo/universalmanifest/integrations/did-vc.md`
- proof-of-personhood integration: `/Users/grig/work/repo/universalmanifest/integrations/proof-of-personhood.md`
- package source: `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/src/index.ts`
- conformance suite: `/Users/grig/work/repo/universalmanifest/conformance/README.md`

Source facts carried into this document:

- UM is pointer-first, provider-neutral, and storage-neutral.
- The manifest is an envelope, not the whole system.
- v0.2 baseline is JCS + Ed25519.
- v0.2 requires signatures for strict verification.
- Unknown-field tolerance is central.
- Projection is currently the safer broad privacy path.
- Encrypted inline facets are optional guidance in v0.2.
- Revocation/status metadata is optional extension-lane behavior in v0.2.
- Claim proof and Tier 1 behavior exist but need stronger treatment.
- Tier 2/Tier 3 identity binding is deferred research/future scope.
- Data Integrity/RDF profile is future, not v0.2.
- v0.3 inputs are already recognized in Phase 19, but not yet promoted.
- Public reader validation remains blocked until deployment and real external-reader process are available.

## 29. Build-Into-The-Existing-System Map

The remote agent should not propose v0.3 as an abstract essay. It should map recommendations into the existing Universal Manifest artifact families.

Current existing artifact families:

- versioned spec artifacts under `/Users/grig/work/repo/universalmanifest/spec/`
- canonical examples under `/Users/grig/work/repo/universalmanifest/examples/`
- implementation-neutral conformance package under `/Users/grig/work/repo/universalmanifest/conformance/`
- TypeScript helper package under `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/`
- public Astro site under `/Users/grig/work/repo/universalmanifest/site/`
- integration guidance under `/Users/grig/work/repo/universalmanifest/integrations/`
- project docs under `/Users/grig/work/repo/universalmanifest/docs/`
- governance and spec improvement queue under `/Users/grig/work/repo/universalmanifest/docs/governance/`

The likely v0.3 build surface is:

- `spec/v0.3/README.md`: version overview, release thesis, normative references, security/privacy posture, and upgrade guidance.
- `spec/v0.3/schema.json`: structural JSON Schema for the v0.3 profile.
- `spec/v0.3/schema.jsonld`: JSON-LD context terms for any new v0.3 vocabulary.
- `spec/v0.3/CONFORMANCE.md`: conformance targets, required behavior, optional profile behavior, fixture list, and failure expectations.
- `spec/v0.3/SIGNATURE-PROFILE.md`: either continuation of JCS + Ed25519 as the baseline or an expanded integrity-profile registry, depending on v0.3 decisions.
- `spec/v0.3/PRIVACY-PROFILE.md`: if privacy/facet/projection behavior becomes too large for the main README, this should define projection, encrypted facets, disclosure, redaction, and unreadable/opaque state rules.
- `spec/v0.3/REVOCATION-AND-STATUS.md`: if revocation/freshness becomes normative or profile-bound, this should define status result shapes, cache rules, fail-open/fail-closed behavior, and receiver reporting.
- `spec/v0.3/TRUST-TIERS.md`: if trust tiers become more central, this should define Tier 0/Tier 1/Tier 2/Tier 3 semantics, claim proof requirements, and downgrade behavior.
- `docs/guides/MIGRATION-V02-V03.md`: human-readable migration guide.
- `docs/VERSION-DIFFERENCES-V02-V03.md`: implementer delta table.
- `examples/v0.3/`: valid and invalid manifests that show every normative v0.3 behavior.
- `conformance/v0.3/`: implementation-neutral fixture mirrors and `expected.json`.
- `packages/universal-manifest/src/index.ts`: reference TypeScript types and assertions for v0.3, but only after the spec shape is clear.
- `site/src/pages/spec/v0.3.astro`: rendered v0.3 spec route.
- `site/src/pages/spec/latest.astro`: latest-spec pointer update after v0.3 release, not before.
- public reader pages: only the small set needed to explain the v0.3 change without overwhelming first-time readers.

The remote agent should classify each proposed artifact as one of:

- Required for v0.3 release.
- Required only if a specific profile is promoted.
- Useful but deferrable.
- Explicitly out of scope.

## 30. v0.3 Field-Level Design Workbench

This section is not a final schema. It is a structured workbench for the remote agent. The agent should use it to decide what fields or concepts belong in v0.3 and what must remain guidance.

### 30.1 Top-level envelope questions

Current v0.2 top-level required fields are:

- `@context`
- `@id`
- `@type`
- `manifestVersion`
- `subject`
- `issuedAt`
- `expiresAt`
- `signature`

Current v0.2 optional top-level payload sections are:

- `facets`
- `claims`
- `consents`
- `devices`
- `pointers`

v0.3 questions:

- Should v0.3 add an explicit top-level `issuer`, `controller`, or `producer`, or should signer identity remain inferred from signature key material and claim issuers?
- Should v0.3 add top-level `audience` or `intendedRelyingParty` semantics, or should audience binding live only inside claim proofs and projections?
- Should v0.3 add top-level `profiles` or `capabilities` so consumers can tell whether the manifest uses privacy, revocation, projection, Data Integrity, or claim-proof profiles?
- Should v0.3 add top-level `status` or `statusRef`, or should status remain signature metadata?
- Should v0.3 add top-level `sourceManifest`, `projectionOf`, or `derivation` fields to make projection lineage machine-readable?
- Should v0.3 add top-level `policy` or `policyRef`, or should policies remain in `consents[]` and domain-specific facets?
- Should v0.3 leave the top-level object nearly unchanged and instead specify profiles that use existing extension tolerance?

Recommended starting bias: minimize required new top-level fields. v0.2's small top-level contract is a strength. Add top-level fields only when receivers need them before safely deciding how to parse, reject, project, or fetch anything else.

### 30.2 Facets and records questions

Current v0.2 facets are flexible named data sections. A facet must include `@type` and may include `@id`, `name`, `description`, `ref`, and `entity`. Additional properties are allowed.

v0.3 questions:

- Should `facet` and `record` become distinct normative concepts, or should "record" remain explanatory architecture language?
- If `Record` is promoted, does it replace `facet`, wrap `facet`, or describe a subtype of facet?
- Should facets/records carry their own `schema`, `mediaType`, `profile`, or `syntax` identifiers?
- Should facets/records carry their own `sourceRef`, `statusRef`, `expiresAt`, or `freshness` metadata?
- Should facets/records carry their own `sensitivity`, `visibility`, `audience`, or `purpose` metadata?
- Should facets/records declare whether they are plaintext, pointer-only, encrypted, redacted, projected, or unresolved?
- Should a consumer be required to preserve unknown facets during projection, or only ignore them safely?
- Should a facet with both `ref` and `entity` define precedence between embedded snapshot and authoritative pointer?
- Should a facet with encrypted payload still expose a cleartext `name`, `@type`, `policy`, and `recipient` metadata?
- Should a facet be allowed to have independent proof material, or should all proof remain manifest-level or claim-level?

Recommended starting bias: if v0.3 introduces `Record`, define it as an interoperability profile for payload sections rather than as a disruptive replacement for `facets[]`.

### 30.3 Claims questions

v0.2 has `claims[]` as flexible objects and adds optional `claimProof` for VP or attestation proof material.

v0.3 questions:

- Should `claims[].issuer` become normative when claim authenticity is asserted?
- Should `claims[].claimProof` become required for any claim above Tier 0?
- Should v0.3 define claim proof result states such as `verified`, `unverified`, `unresolved`, `expired`, `issuer-untrusted`, `audience-mismatch`, and `replayed`?
- Should claim proofs be embedded, pointer-only, or either?
- Should embedded proof size limits from v0.2 guidance become normative?
- Should claims carry `subject` fields distinct from manifest `subject`, or would that invite confusion and spoofing?
- Should claims carry `audience`, `domain`, `challenge`, or nonce requirements for replay resistance?
- Should claims carry `requiredTrustTier`, or should trust-tier policy be receiver-local only?
- Should a consumer be required to degrade unsupported claim proof material rather than rejecting the whole manifest?
- Should a false or forged claim invalidate only the claim, the whole manifest, or the trust tier claimed by the manifest?

Recommended starting bias: make receiver evaluation states explicit. A valid manifest can contain claims that are unverified, unresolved, expired, or outside local trust policy. v0.3 should prevent consumers from treating structural validity as claim truth.

### 30.4 Consents and policy questions

v0.2 already has `consents[]` and a strong privacy direction, but it does not define a complete policy language.

v0.3 questions:

- Should consent objects have a normative minimum shape?
- Should consent values be booleans, state strings, grants/denials, or policy objects?
- Should absence remain default-deny?
- Should consent scope include purpose, audience, context, jurisdiction, data category, retention, onward transfer, and processing mode?
- Should a consent rule have its own `issuedAt`, `expiresAt`, `revokedAt`, or `statusRef`?
- Should the manifest distinguish human consent, legal basis, technical preference signal, and runtime-observed signal?
- Should Global Privacy Control style signals remain helper guidance or become a profile example?
- Should receivers be required to report unsupported consent/policy rules?
- Should policy be advisory only, or should failure to understand a required policy block projection/use?

Recommended starting bias: do not create a general-purpose legal policy engine in v0.3. Define a minimum interoperable consent/policy shape only for decisions receivers must make at the boundary.

### 30.5 Pointers and resolver questions

v0.2 pointers are flexible objects and the resolver contract is separate.

v0.3 questions:

- Should pointers have a normative minimum shape such as `name`, `url`, `rel`, `mediaType`, `profile`, and `integrity`?
- Should pointer dereferencing be in spec scope or remain resolver/runtime guidance?
- Should pointers include authorization hints, or would that leak sensitive information?
- Should pointers include expected hash/digest values for immutable resources?
- Should pointers include freshness or cache controls?
- Should pointer failure be represented as `unresolved`, `forbidden`, `not-found`, `stale`, `integrity-failed`, or `unsupported-profile`?
- Should a pointer to private data be allowed without a matching consent/policy entry?
- Should v0.3 define how a projection handles pointers that were present in the source manifest but withheld from the projection?

Recommended starting bias: define pointer evaluation vocabulary before defining network behavior. The spec should not require one resolver backend, but receivers need common language for what happened.

### 30.6 Signature and integrity questions

v0.2 baseline is JCS + Ed25519. It is intentionally JSON-level rather than RDF graph-level.

v0.3 questions:

- Does v0.3 keep JCS + Ed25519 as the required baseline?
- Does v0.3 add a formal integrity profile registry?
- Does v0.3 allow multiple proofs/signatures on one manifest?
- If multiple proofs exist, can one proof sign the whole manifest while another signs only a claim, facet, or RDF graph?
- How should unknown integrity profiles be handled?
- Should Data Integrity/RDF canonicalization remain future, become optional profile, or become required for JSON-LD-heavy adopters?
- Should v0.3 define signature purpose values, such as issuance, projection, delegation, revocation update, or status assertion?
- Should v0.3 distinguish manifest signer, claim issuer, proof issuer, status issuer, and projection issuer?

Recommended starting bias: keep JCS + Ed25519 as the baseline. Consider an optional profile registry if, and only if, the remote agent can define concrete verifier behavior for unsupported or multiple profiles.

### 30.7 Status, revocation, and freshness questions

v0.2 includes optional `signature.statusRef` and `signature.revocationCursor`. It also requires TTL enforcement.

v0.3 questions:

- Should status checking become required for all strict v0.3 consumers?
- Should revocation remain optional but claimable as a conformance level?
- Should status apply to signature, manifest, claim, facet, projection, pointer, or all of these?
- What is the minimum status response shape?
- What statuses are required: active, revoked, suspended, superseded, expired, unknown, unavailable?
- When status cannot be resolved, does the receiver fail open, fail closed, or follow local policy?
- Should receivers be required to report `unchecked` status when they do not implement status resolution?
- Should `revocationCursor` be generalized into a source version or event cursor?
- Should v0.3 define cache-control interaction and stale status handling?

Recommended starting bias: make status semantics explicit and conformance-level-bound. Do not require network status checks for all contexts, because local-first and offline verification remain important.

### 30.8 Projection questions

Projection is currently the safer privacy path: create a consumer-specific derived manifest containing only allowed data.

v0.3 questions:

- Should projection become a named normative profile?
- Should projected manifests carry `projectionOf`, `projectionPolicy`, `projectionAudience`, or `sourceDigest`?
- Should a projection have a shorter TTL than its source manifest?
- Should a projection be independently signed by the same issuer, by a subject runtime, or by a projection service?
- Should a projection include a digest or reference to withheld sections?
- Should projection preserve unknown fields or intentionally strip them?
- Should projection remove, redact, or mark denied data?
- Should projection lineage be visible to the receiving party?
- Should a receiver be able to determine whether it received a complete manifest or a projection?
- Should v0.3 define projection failure states?

Recommended starting bias: v0.3 should make projection lineage and audience explicit enough to prevent accidental over-disclosure and stale projection acceptance.

## 31. Candidate v0.3 Conformance Matrix

The remote agent should design v0.3 around testable behavior. If behavior cannot be tested by fixtures or an executable conformance runner, it should probably remain guidance.

Candidate conformance targets:

- Issuer: produces structurally valid v0.3 manifests.
- Signer: signs v0.3 manifests under supported integrity profiles.
- Consumer/verifier: validates structure, TTL, signature, and profile support.
- Projection producer: creates consumer-specific derived manifests.
- Projection consumer: detects and evaluates projected manifests.
- Status-aware consumer: resolves or reports revocation/freshness state.
- Privacy-aware consumer: handles plaintext, projected, encrypted, redacted, and opaque sections correctly.
- Claim-proof-aware consumer: evaluates claim proof material and reports verification states.
- Resolver/runtime implementer: dereferences supported pointers or reports precise failure states.

Candidate valid fixtures:

- minimal v0.3 baseline manifest,
- manifest with declared v0.3 profile set,
- manifest with projection lineage,
- manifest with a projection-specific audience,
- manifest with encrypted inline facet treated as opaque by a non-decrypting consumer,
- manifest with encrypted inline facet successfully decrypted by an authorized consumer,
- manifest with status metadata and active status,
- manifest with status metadata but status unchecked by a baseline consumer,
- manifest with Tier 0 self-asserted claims,
- manifest with Tier 1 claimProof-backed claim,
- manifest with pointer metadata and successful pointer evaluation,
- manifest with a private pointer withheld from projection,
- manifest with unknown extension fields that are ignored safely.

Candidate invalid or reject fixtures:

- missing required v0.3 field,
- unsupported required profile,
- unsupported signature profile in strict mode,
- expired manifest,
- issued-after-expires manifest,
- signature mismatch after payload tampering,
- projection with audience mismatch,
- projection claiming lineage without source reference or digest when required by profile,
- encrypted facet whose metadata lies about encryption mode,
- encrypted facet whose ciphertext was modified after signing,
- status-required manifest where status is unavailable under fail-closed policy,
- revoked manifest under status-aware conformance,
- claim requiring Tier 1 but lacking claimProof,
- claimProof with expired proof material,
- claimProof with issuer outside local trust policy,
- pointer integrity mismatch,
- pointer marked required but unresolved under strict profile,
- unknown field that appears in a critical/required extension list but is unsupported.

The remote agent should separate:

- baseline fixture expectations,
- privacy profile fixture expectations,
- projection profile fixture expectations,
- revocation/status profile fixture expectations,
- claim-proof/trust-tier fixture expectations,
- future integrity-profile fixture expectations.

## 32. Failure Mode Inventory For v0.3

v0.3 must be designed against concrete ways receivers can get this wrong.

### Structural failure modes

- A consumer accepts a document that is not a manifest because `@type` is absent or malformed.
- A consumer accepts a v0.2 document as v0.3 without checking `manifestVersion`.
- A consumer rejects a valid manifest because it does not tolerate unknown fields.
- A consumer silently drops unknown fields during projection and thereby destroys future compatibility.

### Signature failure modes

- A consumer verifies the signature over the wrong canonical input.
- A consumer includes `signature` in the signing input and accidentally defines a non-interoperable profile.
- A consumer treats `keyRef` as proof of issuer identity without resolving trust policy.
- A consumer accepts an unsupported algorithm/canonicalization pair as if it were JCS + Ed25519.
- A consumer verifies envelope integrity and then assumes every claim is true.

### Freshness and revocation failure modes

- A consumer checks signature validity but ignores `expiresAt`.
- A consumer treats `signature.created` as a validity window.
- A consumer sees `statusRef` but does not check it and still claims revocation-aware conformance.
- A consumer uses cached active status after the revocation cursor changed.
- A consumer fails open for high-risk data because status endpoint is temporarily unavailable.

### Privacy failure modes

- A sender includes full private data when a projection should have been issued.
- A projection accidentally includes pointers to withheld private data.
- A consumer cannot decrypt a facet and treats it as absent rather than opaque.
- A consumer logs encrypted payloads, claim proofs, pointers, or identifiers in debugging output.
- A global stable subject identifier enables correlation across relying parties.
- A consent rule is present but a consumer treats unsupported policy as permission.

### Claim and trust failure modes

- A forged issuer string is treated as issuer proof.
- A copied claim from another manifest is accepted because the envelope signature is valid.
- A claim proof is valid but audience-bound to another relying party.
- A claim proof is valid but expired.
- A cross-DID binding claim is treated as cryptographic proof when it is only attested.
- A receiver combines multiple weak claims into a high-trust conclusion without explicit policy.

### Resolver and pointer failure modes

- A receiver follows a pointer and trusts returned data without verifying media type, integrity, freshness, or authorization.
- A pointer endpoint returns a newer object, but the manifest intended a snapshot.
- A pointer endpoint returns stale data, but the consumer cannot tell.
- A private pointer leaks the existence of sensitive information.
- A resolver status route becomes a de facto central dependency, violating storage neutrality.

The remote agent should map every v0.3 proposal to the failure modes it reduces, and should identify any new failure modes it creates.

## 33. Decision Record Format The Remote Agent Should Use

For each major v0.3 decision, the remote agent should produce a decision record in this shape:

```markdown
### Decision: [short name]

Recommendation:
[Normative / Optional profile / Guidance / Deferred / Reject]

Problem:
[What breaks or stays ambiguous if this is not addressed.]

Proposed behavior:
[Exact behavior receivers, issuers, or projection producers should implement.]

Spec artifacts affected:
[- spec/v0.3/README.md
 - spec/v0.3/schema.json
 - spec/v0.3/CONFORMANCE.md
 - examples/v0.3/...
 - conformance/v0.3/expected.json
 - packages/universal-manifest/src/index.ts
 - docs/guides/MIGRATION-V02-V03.md]

Compatibility:
[What happens to v0.2 producers and consumers.]

Conformance:
[How this is tested. Include valid and invalid fixtures.]

Security/privacy impact:
[What risks improve or worsen.]

Open questions:
[Only unresolved items that truly require owner or standards decision.]
```

The remote agent should not hide hard choices in prose. If it recommends promoting something to normative status, it must say what tests prove compliance. If it recommends deferring something, it must say what evidence would make it ready later.

## 34. Practical Release Shape To Consider

This is a possible release shape, not a command. The remote agent should challenge it if a better one exists.

### Baseline v0.3

Baseline v0.3 could require:

- all v0.2 baseline structure,
- JCS + Ed25519 signature verification,
- TTL enforcement,
- unknown-field tolerance,
- explicit handling of unsupported profiles,
- precise reporting of structural, signature, expiry, and unsupported-profile failures.

Baseline v0.3 could add:

- optional top-level `profiles` or equivalent profile declaration,
- clearer claim evaluation states,
- clearer projection recognition,
- clearer encrypted/opaque facet handling,
- clearer status reporting language even when active status checks are not performed.

### Projection profile

Projection profile could define:

- how a derived manifest declares it is a projection,
- how audience binding works,
- how source lineage or digest is represented,
- how withheld data is represented or omitted,
- how projection TTL relates to source TTL,
- what a projection producer must sign,
- what a projection consumer must reject.

### Privacy/encrypted-facet profile

Privacy profile could define:

- plaintext facet,
- pointer-only facet,
- encrypted inline facet,
- redacted facet,
- opaque/unreadable facet,
- unsupported encrypted facet behavior,
- key rotation metadata expectations,
- revocation implications for encrypted material.

It should not require all v0.3 consumers to decrypt encrypted facets. It should require them to avoid pretending unreadable content is absent.

### Status/revocation profile

Status profile could define:

- status metadata fields,
- status response shape,
- accepted statuses,
- cursor/cache behavior,
- fail-open/fail-closed policy expression,
- how baseline consumers report unchecked status,
- what conformance claim a status-aware consumer may make.

### Trust-tier/claim-proof profile

Trust-tier profile could define:

- Tier 0 as signature-only/self-asserted,
- Tier 1 as claimProof-backed or attested,
- Tier 2 as cryptographic cross-identifier binding if enough evidence exists,
- Tier 3 as multi-party ceremony, probably deferred,
- required receiver downgrade behavior,
- claim proof verification states,
- local trust-policy hooks.

The remote agent should decide whether Tier 2 is ready for v0.3 or whether v0.3 should only prepare the vocabulary and testable Tier 1 behavior.

## 35. What Must Not Be Lost In Transfer

The remote agent should carry these constraints through every recommendation:

- Universal Manifest is a standard boundary object, not an application.
- The manifest is one envelope, not nested envelopes.
- Facets are payload sections inside the manifest, not independent manifests.
- The signature proves integrity of the manifest as signed; it does not prove all claims are true.
- Unknown-field tolerance is part of forward compatibility.
- Short TTL is a security primitive, not just metadata.
- Offline/local-first verification matters.
- Public docs must teach the idea before exposing all complexity.
- A remote service or resolver can support UM but must not become required for baseline conformance.
- Privacy cannot depend only on honest receivers.
- Projection is useful precisely because it withholds data rather than encrypting everything.
- Encrypted inline facets are useful precisely because receivers can verify the envelope before decryption.
- Revocation and freshness are related but not identical.
- Claim authenticity, subject binding, and envelope integrity are separate ideas.
- Different adopters need different assurance levels.
- v0.3 should be a sharper standard, not a bigger bag.

## 36. Final Instruction To The Remote Agent

Do not make Universal Manifest vague.

Do not make v0.3 a feature bucket.

Do not assume a wallet, DID method, resolver, backend, or runtime can solve the design problem for everyone.

Treat v0.3 as a specification design problem at the boundary where context moves between systems. The output must decide how the envelope carries meaning, proof, permission, freshness, privacy, and projection without becoming the source of truth for everything.

The best proposal will be specific enough that the project owner can say:

- these things become normative,
- these things become optional profiles,
- these things remain guidance,
- these things are deferred,
- these files/routes/tests must change,
- these work orders should be created next,
- these acceptance gates must pass before v0.3 is called done.
