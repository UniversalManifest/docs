# The Enterprise Integrator

**Persona:** Morgan Williams, senior engineer at a company that builds software for venue management. Their clients need interoperability between artist platforms, display systems, and trust services.

---

I build venue management software for a living. Our platform, VenueOS, powers forty-three galleries, performance spaces, and public art installations across the northeast. Every one of our clients has the same problem: they need to pull artist profiles from one system, push content to display hardware from another, verify trust credentials from a third, and manage consent and privacy for all of it. We have built custom integrations for nine different platforms. Each one is a maintenance liability. Each one speaks a different data format. Each one breaks independently.

When our product lead drops a link to the Universal Manifest spec in our engineering channel, I expect another proprietary standard with a heavy SDK and a licensing conversation. Instead, I find a JSON-LD schema, a JSON Schema for structural validation, a set of test fixtures, and a TypeScript assertion library. I open the spec and read it in twenty minutes. I run the test fixtures against the assertion function and they all pass. I look at the schema and count the required fields: seven. `@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`. That is it.

I write a UM consumer for VenueOS in a single afternoon.

---

The consumer is straightforward. When a venue operator enters an artist's UMID, VenueOS sends a GET to the resolver, receives the manifest, and runs structural validation. I use the published JSON Schema for initial validation and add the TTL check on top -- is `now` between `issuedAt` and `expiresAt`? If the manifest passes, VenueOS reads the relevant facets. For artists, that means `publicCapsule` or `publicProfile`. For venues, that means `venueIdentity` and `venuePolicy`. For devices, that means `deviceIdentity` and `venueAssociation`.

The first thing I notice is that I did not have to write a parser for each type. The manifest envelope is the same whether it describes an artist, a venue, or a display device. The `@type` tells me what it is. The `facets` array tells me what data it carries. The `consents` array tells me what the subject permits. The `pointers` array tells me where the canonical data lives. Same structure, different content. One consumer, multiple use cases.

Two hundred and twelve lines of code. No SDK. No API key. No OAuth client registration.

---

I add device enrollment next. Our clients use a mix of display hardware -- Shield TV units, Raspberry Pi kiosks, commercial digital signage panels. Currently, each device type requires a separate enrollment flow with manual configuration. With UM, I model each device as its own manifest with a `deviceIdentity` facet (hardware model, capabilities, resolution) and a `venueAssociation` facet (linking the device to its parent venue). When a new device connects to the venue's local network, it discovers the venue's edge node, fetches the venue manifest, and registers itself. VenueOS reads the device manifest, validates it, and adds the device to the venue's device roster with an initial trust level of `local`. The operator promotes it to `enrolled` with one click.

We roll this out to three client venues as a pilot. The first venue enrolls four new displays in under an hour. The facility manager sends a message to our support channel: "Is that it? I just plug them in?" That is it.

---

Then our enterprise clients start asking for trust verification. One gallery chain wants to verify that artists have been reviewed by a trust service before their content appears on screens. Another wants proof-of-personhood checks for online submissions.

I look at how OMATrust attestations are represented in UM fixtures. The trust signal is modeled as claims within the manifest -- `omatrust.policy.trustMode` indicates whether the trust is `proof-based` or `trusted-attester`. Supporting claims carry attestation details: linked identifier verification, key binding status, review scores. The attestation metadata lives in a facet (`omaTrustReputation`) with a pointer to the external verification endpoint.

I add trust checking to VenueOS in a day. When a venue's content policy requires trust verification, VenueOS reads the artist's manifest, looks for OMATrust claims, checks the trust mode, and follows the pointer to the attestation endpoint to confirm the attestation is still valid. If the trust check fails, the content does not enter the display queue.

The following week, a different client asks about proof-of-personhood. I look at the multi-provider personhood fixtures in the UM examples. Proof-of-personhood is modeled the same way: claims in the manifest with references to the credential provider. Worldcoin, BrightID, Idena -- each one represented as a claim with a `name`, `value`, `issuer`, and a pointer to the verification endpoint. Same envelope. Same consumer logic. I add personhood checking to VenueOS in four hours, reusing the claim verification code I wrote for OMATrust.

I step back and count. Profiles. Device enrollment. Trust attestations. Proof of personhood. Consent management. Audit logging. Six different capabilities. All of them read from the same manifest format. Every new integration was faster than the last because the consumer logic is the same -- fetch the manifest, validate the structure, read the relevant facets and claims, check the consents, follow the pointers.

> **Aha moment:** "We added six different capabilities -- profiles, devices, trust, personhood, consent, and audit -- and it is all the same format. Every new integration was faster than the last."

---

After the pilot succeeds, I write an integration guide for our engineering team and contribute a venue-management integration lane template back to the UM project. The template includes the consumer implementation pattern, the facet names VenueOS uses, the consent names it checks, and the claim verification flow. Other venue management platforms can use it as a starting point. The ecosystem grows by contribution, not by committee.

Our CTO asks me how long the UM integration took, total. I check the git log. First commit to production deployment: eleven working days. Nine platforms' worth of custom integrations replaced by one consumer that reads one format. The maintenance burden dropped by an order of magnitude. When the v0.2 signature spec stabilizes, I will add signature verification. It is one function call: `assertUniversalManifestV02`. The consumer stays the same.

---

## How UM Works Here

**Consumer implementation:** Morgan builds a single UM consumer that validates incoming manifests using the published JSON Schema and the `assertUniversalManifestV01` function from the TS helper package. The consumer handles artists, venues, and devices through the same validation and reading path -- the manifest envelope (`@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`) is identical across all entity types.

**Device enrollment facets:** Display devices are modeled as manifests with `deviceIdentity` facets (hardware model, capabilities such as WebGL2 support, max resolution, preferred render resolution) and `venueAssociation` facets (linking the device to a venue by reference). Trust levels (`local`, `enrolled`) are tracked in the `devices` array. New devices self-register by discovering the venue's edge node and fetching the venue manifest.

**OMATrust claims integration:** Trust attestations are represented as `um:Claim` entries with names like `omatrust.policy.trustMode` (values: `proof-based`, `trusted-attester`), `omatrust.attestation.linkedIdentifier`, and `omatrust.attestation.keyBinding`. A pointer named `omatrust.reputation.attestation` links to the external verification endpoint. VenueOS reads these claims and pointers to gate content display behind trust verification.

**Multi-provider personhood credentials:** Proof-of-personhood is modeled using the same claim structure. Each credential provider (Worldcoin, BrightID, Idena) is represented as a claim with a specific `name`, `value`, and `issuer`. The consumer reads personhood claims using the same code path as trust claims -- no separate integration required.

**Content policy facets:** Venue manifests contain `venuePolicy` facets with content rules (safety mode, content rating, allowed/blocked content types, curation preferences). The consumer compares incoming artist content against these policy rules before adding content to the display queue.

**Integration template contribution:** Morgan contributes a reusable integration lane template back to the UM project, documenting the facet names, consent names, and claim verification patterns used by venue management platforms. This follows the project's extensibility model: well-known names in the registry, not hard-coded types in the schema.

**UM capabilities demonstrated:** Consumer implementation from spec, device enrollment via manifests, OMATrust attestation claims, multi-provider personhood credentials, venue content policy facets, consent enforcement, pointer-based external verification, integration template contribution.
