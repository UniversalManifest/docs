# Proximity Credential and Presentation Profile Assessment

Date: 2026-03-06  
Work order: `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0134-proximity-credential-and-presentation-profile-assessment.md`

## 1. Executive answer

Universal Manifest should not model the live mechanics of proximity-triggered credential exchange.

The correct boundary is:

- UM carries holder-controlled policy context, consent scope, freshness expectations, preferred proof-format hints, and post-exchange evidence references.
- OpenID4VP, W3C Digital Credentials API, wallet/OS mediation, QR/deep-link/NFC/BLE handoff, nonce/state handling, response delivery, and proof verification stay outside the UM document model.
- The current standards stack is mature enough to define a non-normative boundary profile for same-device and cross-device web-mediated flows.
- The stack is not mature enough for Universal Manifest to publish a broad public integration lane claiming full proximity support across offline or device-to-device transports.

Decision:

- `No UM core schema change`.
- `No transport semantics in UM`.
- `Public integration lane: deferred for now`.
- `Allowed near-term scope: internal examples and boundary-only guidance`, not a broader adopter-facing lane, until executable proof exists.

That conclusion is driven by the promotion gate already adopted in `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-protocol-volatility-proximity-and-federation-research-first-decision-package.md`: the repository still lacks fixture/journey proof for a proximity request/presentation flow.

## 2. Standards checkpoint as of 2026-03-06

### 2.1 OpenID4VP

Status:

- OpenID for Verifiable Presentations 1.0 is `Final`, published `2025-07-09`.
- Source: [OpenID4VP 1.0 Final](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html)

Why it matters:

- It is the most mature standards-track presentation protocol in the current web and wallet ecosystem.
- It explicitly supports both same-device and cross-device presentation patterns.
- It supports multiple credential formats in one transaction, including VC Data Model credentials, ISO mdoc, and SD-JWT VC.
- It already defines a browser/API variant through its Digital Credentials API appendix.

Key signals from the specification:

- The protocol “defines a mechanism to request and present Credentials” and includes a separate mechanism where messages are sent over the Digital Credentials API instead of redirects/HTTPS browser flow.
- Same-device flow is defined as the Verifier and Wallet interaction occurring on the same device.
- Cross-device flow is defined as the Verifier interaction occurring on a different device from the Wallet.
- `direct_post` exists specifically to support flows where the Wallet and Verifier are on different devices or where payload size makes redirect fragments impractical.
- The Verifier must still perform its own security checks on returned credentials and presentations; it must not rely on the Wallet to enforce Verifier-side constraints.

### 2.2 OpenID4VCI

Status:

- OpenID for Verifiable Credential Issuance 1.0 is `Final`, published `2025-09-16`.
- Source: [OpenID4VCI 1.0 Final](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0-final.html)

Why it matters here:

- `WO-0134` is about presentation, not issuance, but issuance matters for freshness, reissuance, multiple credential instances, and unlinkability strategy.
- The spec explicitly allows credential refresh, but how the issuer signals refresh to the wallet is out of scope.
- That matters because UM can reasonably carry freshness and policy expectations, but not the issuer-to-wallet refresh signaling protocol itself.

### 2.3 W3C Digital Credentials API

Status:

- W3C Digital Credentials is `Working Draft`, published `2026-03-05`.
- Source: [W3C Digital Credentials API](https://www.w3.org/TR/digital-credentials/)

Why it matters:

- It is the emerging browser/user-agent mediation layer for wallet-backed issuance and presentation.
- It does not replace presentation protocols; it passes protocol-specific request data to wallet providers and mediates user permission at the browser/OS layer.
- It introduces important privacy and permission concepts that overlap with, but do not replace, UM consent semantics.

Key signals from the draft:

- A `DigitalCredentialGetRequest` specifies a `protocol` and `data`; the browser/user agent forwards protocol-specific request data to the wallet.
- User mediation is mandatory for DigitalCredential operations.
- Cross-origin request support exists via the `digital-credentials-get` permissions policy.
- The draft is still explicit that “permission” is not the same thing as legal or business “consent”.
- Several important privacy and permission sections remain work in progress, which means this is not yet a closed standards surface.

### 2.4 SD-JWT VC

Status:

- SD-JWT VC is still an `Internet-Draft` (`draft-ietf-oauth-sd-jwt-vc-15`, February 2026; expires 2026-08-30).
- Source: [IETF SD-JWT VC draft](https://datatracker.ietf.org/doc/draft-ietf-oauth-sd-jwt-vc/)

Why it matters:

- It is one of the strongest current selective-disclosure candidates for wallet ecosystems.
- It is directly referenced by OpenID4VP, OpenID4VCI, and HAIP.
- It still carries privacy and metadata-governance risk that UM should not hide under a simplistic “selective disclosure solved” narrative.

Key signals from the draft:

- Privacy considerations explicitly call out unlinkability concerns, especially around holder-binding material.
- `vct` values are ecosystem-defined and can themselves leak more information than intended if poorly chosen.
- Key Binding JWT payloads use verifier audience and nonce, reinforcing that replay protection and audience binding are live protocol concerns, not manifest concerns.

### 2.5 HAIP

Status:

- OpenID4VC High Assurance Interoperability Profile 1.0 is `Final`, published `2025-12-24`.
- Source: [HAIP 1.0 Final](https://openid.net/specs/openid4vc-high-assurance-interoperability-profile-1_0-final.html)

Why it matters:

- HAIP is the strongest current signal that the ecosystem is moving toward profiled interoperability rather than raw unprofiled optionality.
- It profiles OpenID4VCI, OpenID4VP, Digital Credentials API, SD-JWT VC, and ISO mdoc together.
- It is useful evidence that high-assurance interoperable web-mediated flows are becoming concrete.

Critical limitation for this work:

- HAIP explicitly leaves offline presentation protocols, such as BLE-based offline presentation, out of scope.
- That is decisive for Universal Manifest: any claim that UM now has a complete proximity strategy across device-to-device/offline interactions would overstate reality.

## 3. Current overlap with existing Universal Manifest work

The repository already has the right architectural posture.

Existing repo position that overlaps correctly:

- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md`
- `/Users/grig/work/repo/universalmanifest/integrations/did-vc.md`
- `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.1/REGISTRY.md`

What that posture already gets right:

- A subject-controlled runtime is the natural place for live consent mediation and exchange coordination.
- The manifest remains pointer-first and storage-neutral.
- Bridge adapters and closed-surface behavior are implementation detail, not normative UM contract.
- Credential and proof material can be referenced without forcing a single credential stack into the core schema.
- Runtime-authoritative state with optional document-level evidence projection is already an accepted repo pattern, demonstrated most clearly by the GPC integration.

Relevant existing UM primitives:

- `portableIdentity.proofBundle`
- `metaverse.preferencesBundle`
- `metaverse.transaction.complianceShare`
- `metaverse.credentials.presentation`
- `prefs.credentials.*`
- sync/freshness guidance in `/Users/grig/work/repo/universalmanifest/site/src/content/docs/guides/mum-synchronization-profile.md`

Relevant existing proof precedent:

- The repo already tests consent enforcement, pairwise privacy, revocation-aware behavior, and runtime-authoritative GPC projection.
- It does not yet test a proximity-triggered credential request/presentation journey.

## 4. The boundary Universal Manifest should adopt

## 4.1 What belongs outside UM

These concerns remain live presentation-protocol or wallet/runtime concerns and should not be represented as core UM semantics:

- QR, deep-link, NFC, BLE, or local-radio invocation mechanics.
- Request URI fetching and request object validation.
- `state`, `nonce`, `response_uri`, `redirect_uri`, and `expected_origins` handling.
- Wallet invocation routing and browser/OS mediation.
- Verifier authentication details and request signing rules.
- Response transport mode selection (`fragment`, `direct_post`, `dc_api`, `dc_api.jwt`, etc.).
- Presentation proof construction and verifier-side validation.
- Replay defense and session fixation defense.
- Credential-format-specific handover/session transcript rules.
- Device discovery beacons or stable local broadcast identifiers.

If UM tries to carry these directly, it stops being a portable document model and starts impersonating a live transport/session protocol.

## 4.2 What UM can safely carry

UM can safely carry four bounded categories of information for a proximity-aware credential flow.

### A. Holder disclosure policy and consent scope

Examples:

- whether credential-derived claims may be presented at all in a given context,
- whether presentation reuse is allowed,
- whether a class of verifier or surface is allowed,
- whether transaction/compliance proof references may be shared.

Applied example:

- A venue kiosk asks for age-over-threshold proof.
- The wallet/runtime checks `metaverse.credentials.presentation=allowed` and a holder policy facet saying retail age-verification is allowed only for in-person sessions.
- If absent or denied, nothing is presented.

### B. Freshness and trust posture expectations

Examples:

- local policy requiring short-lived requests,
- requirement for trusted verifier metadata before disclosure,
- requirement for revocation/status freshness before presenting proof-derived results,
- requirement for runtime verification before honoring a request.

Applied example:

- A wallet sees an OpenID4VP request from a kiosk but holder policy says: only proceed if verifier metadata is signed or otherwise trusted and the request is fresh.
- That holder policy can be represented in a non-normative policy facet or pointer, but the actual request freshness check stays in the runtime.

### C. Preference and capability hints

Examples:

- preferred proof families,
- preferred wallet behavior,
- audience-specific disclosure preferences.

Applied example:

- A person prefers a selective-disclosure format when available. UM can carry `prefs.credentials.preferredFormat=sd-jwt-vc` as a preference hint.
- The runtime may use that hint when several proof options exist, but the actual protocol selection still happens at runtime against verifier capabilities.

### D. Post-exchange evidence and audit references

Examples:

- proof-result reference,
- audit log pointer,
- authorization/change-log pointer,
- verifier-policy snapshot reference.

Applied example:

- After a successful age check, the runtime stores an audit record behind a pointer such as `portableIdentity.proofBundle` or a new non-normative audit object, keyed to a short-lived event record rather than embedding the raw SD-JWT or mdoc presentation in the manifest.

## 4.3 What UM should not carry even as a convenience

UM should not be used to persist the following as standard practice:

- raw live presentation requests,
- response envelopes,
- verifier nonces or session secrets,
- device discovery tokens,
- stable beacon identifiers,
- raw credential copies that are reused across verifiers,
- browser/DC API permission artifacts that belong to the user-agent layer.

Applied example:

- A museum kiosk displays a QR code to request proof of adult status.
- The QR payload, request URI, verifier challenge, and response transport mode must remain outside the manifest.
- UM can contribute only the holder's policy context and optional post-exchange audit reference.

## 5. Flow-by-flow application of the boundary

## 5.1 Same-device web or app flow

Reference shape:

- Website or app triggers OpenID4VP redirect flow or Digital Credentials API request on the same device.
- Browser/user agent mediates permission and wallet selection.
- Wallet/runtime evaluates UM-based policy and consent.
- Wallet presents only what the verifier requested and what the holder approved.
- Verifier validates returned proofs itself.
- Runtime may record a short-lived proof-result reference or audit pointer.

What UM contributes:

- consent gate,
- preference hint,
- freshness/trust policy pointer,
- optional audit reference after exchange.

What UM does not contribute:

- the request payload,
- the DCQL query,
- the `expected_origins` list,
- browser permission state,
- the returned VP Token.

Applied example:

- A concert website on a phone requests proof that the visitor is over 18.
- The browser invokes `navigator.credentials.get()` with `protocol` and protocol-specific `data`.
- The wallet checks UM holder policy, sees that age-over-threshold disclosure is allowed for event admission, and returns the minimum proof.
- The manifest remains unchanged except for an optional pointer to the resulting audit event.

## 5.2 Cross-device verifier-to-phone-wallet flow

Reference shape:

- A kiosk or desktop page displays a QR code or deep link carrying an OpenID4VP request URI.
- The holder uses a phone wallet on a different device.
- The wallet fetches the request object, validates verifier information, checks holder policy, and returns the presentation with `direct_post` or another allowed response mode.
- The verifier validates the proof and applies local policy.

What UM contributes:

- disclosure permission,
- policy pointer for allowed verifier class or context,
- freshness expectation for proof or status checks,
- post-exchange reference.

What UM does not contribute:

- QR structure,
- request URI transport,
- response URI,
- session fixation defenses,
- response correlation tokens.

Applied example:

- A venue entrance kiosk asks a visitor to prove regional age eligibility.
- The phone wallet scans the QR code, retrieves the OpenID4VP request, verifies that the verifier is trusted enough for this policy, and returns a minimal proof.
- The holder's manifest can later reference an audit record for the completed interaction, but the live exchange never becomes manifest content.

## 5.3 Device-to-device or offline in-person flow

Reference shape:

- Wallet and verifier exchange proof directly using transport/profile rules outside the common web redirect model.
- This may include local radio or offline handover patterns.

Current answer:

- UM can still supply holder-side policy, consent, freshness expectations, and audit-reference semantics.
- UM should not publish guidance that implies the transport is standardized at the UM layer.
- For now, this remains `Research-First` for public guidance.

Why:

- HAIP explicitly keeps offline BLE presentation out of scope.
- OpenID4VP does not solve every device-to-device or offline presentation pattern.
- The Digital Credentials API is not the answer for offline/direct wallet-to-verifier proximity exchange.

Applied example:

- A staff member uses a handheld inspection device with no browser session and intermittent connectivity.
- UM can still say “presentation allowed only under staff-audited in-person policy, with an audit pointer recorded afterward.”
- UM cannot currently standardize how the handheld device and wallet perform the live handover.

## 6. Privacy and anti-correlation analysis

This is the most important section for deciding whether proximity belongs in the manifest or outside it.

## 6.1 Risks that exist in the current standards landscape

### A. Repeated request or silent probing leakage

Relevant standards signals:

- OpenID4VP warns that even `values` matching can leak information if the wallet distinguishes between mismatch and non-consent.
- Digital Credentials API is explicitly concerned with credential availability leakage and prompt abuse.

UM implication:

- UM must not offer any stable field that lets nearby verifiers probe whether a subject possesses a credential or would satisfy a credential rule without explicit user mediation.

Applied example:

- A store should not be able to scan nearby manifests and infer who likely has an age credential before asking.
- UM can expose policy only through the runtime after a real request, not through public static credential-availability flags.

### B. Verifier-to-verifier linkability

Relevant standards signals:

- OpenID4VP explicitly notes that SD-JWT and mdoc presentations can still be linkable because of issuer signatures or credential-bound public keys.
- SD-JWT VC privacy sections also call out unlinkability concerns.

UM implication:

- UM should not encourage durable reuse of the same proof artifacts across verifiers.
- Any audit or proof-result reference stored in UM must be verifier-scoped or event-scoped and preferably behind a protected pointer.

Applied example:

- A retail verifier and an event verifier should not both receive or later re-fetch the same durable proof pointer from the manifest.
- The runtime should create short-lived verifier-specific evidence instead.

### C. Type and metadata leakage

Relevant standards signals:

- SD-JWT VC warns that ecosystem-defined `vct` values can reveal more than intended.
- Digital Credentials API warns that incidental metadata in authentic presentations can still reidentify the user.

UM implication:

- Public UM data should not advertise sensitive credential-type inventory.
- Preference hints may exist, but concrete credential inventories and proof capabilities should remain private runtime knowledge.

Applied example:

- Public UM should not expose that a person holds a regulated health credential or a country-specific identity credential.
- At most, private holder policy can say which disclosure classes are allowed.

### D. Browser, OS, and multi-agent permission confusion

Relevant standards signals:

- Digital Credentials API says permission is not the same as consent.
- The draft also notes that multiple cooperating software layers may be involved and that overprompting or prompting without context can create exploitable confusion.

UM implication:

- UM consent cannot be treated as a replacement for browser or OS permission.
- The runtime must compose three distinct checks:
  - user-agent permission,
  - wallet/business consent,
  - UM holder policy.

Applied example:

- A browser may allow a DC API request to proceed to wallet selection, but the wallet still blocks disclosure because UM policy denies this verifier class.

### E. Session fixation and response hijacking risk in cross-device flows

Relevant standards signals:

- OpenID4VP says `direct_post` is susceptible to session fixation if not strengthened.
- Same-device fragment flows avoid some of these issues; cross-device has fewer built-in session guarantees.

UM implication:

- Session and replay defenses must stay at the presentation protocol and verifier/runtime layers.
- UM should not create a false impression that TTL or manifest signatures solve session-level handoff risk.

Applied example:

- A signed manifest and fresh `expiresAt` do not make a cross-device `direct_post` flow safe if verifier session handling is weak.

## 6.2 UM-specific guardrails that should be preserved

The existing repo privacy direction should be preserved and applied explicitly to proximity work:

- pairwise or audience-scoped identifiers where feasible,
- deny-biased disclosure defaults,
- short TTL and freshness checks,
- pointer-first audit/evidence references rather than raw proof persistence,
- no stable proximity beacon semantics in the manifest,
- no public credential inventory exposure,
- runtime-authoritative mediation before any disclosure.

## 7. Should any current UM concept be replaced?

Answer: `No`.

Nothing in the current standards stack replaces the need for:

- subject-controlled consent state,
- pointer-first externalization,
- freshness policy,
- audience/context policy,
- document-level portability.

What changes is only the integration boundary.

What should be adopted from the standards instead of invented locally:

- request/presentation session semantics from OpenID4VP,
- browser mediation semantics from the Digital Credentials API where applicable,
- proof-format-specific privacy assumptions from SD-JWT VC or ISO mdoc ecosystems,
- ecosystem profiles like HAIP where an adopter needs stricter interoperable subsets.

What should not be replaced:

- UM consent architecture,
- UM pointer model,
- UM subject/runtime separation,
- UM TTL/freshness posture.

## 8. Can proximity be integrated directly as a facet?

Answer: `No, not as the primary design`.

A facet can carry:

- holder-side policy metadata,
- preferred proof family hints,
- verifier-class constraints,
- audit references,
- proof-result references.

A facet should not be used as:

- the transport envelope,
- the verifier request object,
- the wallet response body,
- the handover/session transcript carrier.

Applied example:

- A `presentationPolicy` facet could say:
  - adult-status proofs may be shown to trusted in-person venue verifiers,
  - background or silent requests are disallowed,
  - reuse across verifier classes is disallowed,
  - results should be logged by pointer only.
- The actual OpenID4VP or mdoc session still occurs outside the facet.

## 9. GPC-style precedent: where it helps and where it does not

The repo’s GPC integration is a useful precedent, but only partially.

What maps cleanly:

- live state is runtime-authoritative,
- optional manifest projection can be evidence or descriptive metadata,
- provenance and observation time matter,
- the static document must not override live protocol facts.

What does not map cleanly:

- GPC is a simple preference signal; proximity presentation is a full multi-party protocol exchange.
- For GPC, a consent-style projection is often enough as evidence.
- For proximity presentation, projecting the raw proof or session details back into the manifest would create privacy and replay problems.

Correct adaptation:

- Use the GPC precedent only for `runtime-authoritative, optional evidence projection`.
- Do not use it to justify turning live credential exchange into a manifest facet.

## 10. Decision on future guidance

### 10.1 Public integration lane

Recommendation: `Defer public integration lane for now`.

Reason:

- The architecture boundary is now clear enough.
- But the repository still lacks the promotion evidence already required by repo policy: executable same-device and cross-device proof coverage.
- Publishing a public lane now would invite readers to assume a broader support claim than the project can currently prove.

### 10.2 Internal examples

Recommendation: `Allowed`.

Reason:

- The repo can safely use internal examples or future fixtures to show the boundary in practice.
- Those examples should be narrow and explicit that transport remains external to UM.

### 10.3 Core schema work

Recommendation: `Not justified`.

Reason:

- The gap is not core document structure.
- The gap is proof of an integration boundary plus executable journey evidence.

## 11. Final assessment against the work-order acceptance criteria

### Acceptance criterion 1

Criterion:

- The report clearly separates UM document semantics from live presentation transport semantics.

Result:

- `Satisfied`.

### Acceptance criterion 2

Criterion:

- Same-device and cross-device flows are both addressed.

Result:

- `Satisfied`.

### Acceptance criterion 3

Criterion:

- Privacy and anti-correlation risks are documented.

Result:

- `Satisfied`.

### Acceptance criterion 4

Criterion:

- The result explicitly states whether a UM integration lane should be created, deferred, or limited to examples.

Result:

- `Satisfied`.
- Explicit answer: `defer public integration lane; allow only limited internal examples/boundary guidance until executable proof exists`.

## 12. Sources

Primary standards sources reviewed:

- [OpenID for Verifiable Presentations 1.0 Final](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html)
- [OpenID for Verifiable Credential Issuance 1.0 Final](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0-final.html)
- [W3C Digital Credentials API Working Draft 2026-03-05](https://www.w3.org/TR/digital-credentials/)
- [IETF SD-JWT VC draft-ietf-oauth-sd-jwt-vc-15](https://datatracker.ietf.org/doc/draft-ietf-oauth-sd-jwt-vc/)
- [OpenID4VC High Assurance Interoperability Profile 1.0 Final](https://openid.net/specs/openid4vc-high-assurance-interoperability-profile-1_0-final.html)

Key repo sources aligned in this assessment:

- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md`
- `/Users/grig/work/repo/universalmanifest/integrations/did-vc.md`
- `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.1/REGISTRY.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/guides/mum-synchronization-profile.md`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/src/index.ts`
- `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/metaverse-mum-compliance-transaction-manifest.jsonld`
