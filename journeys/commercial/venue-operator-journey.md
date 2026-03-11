# The Venue Operator

**Persona:** Jordan Park, runs Sunset Gallery -- a mid-size art gallery with digital displays. Needs to curate content, manage devices, and respect artist preferences. Currently spends hours onboarding each new artist.

---

It is Monday morning and I have three new artists confirmed for this weekend's group show. In the old days, this meant three separate email threads, three different file formats, three rounds of "can you resend that in higher resolution," and at least an hour of manually entering bios into our display system. Last month I onboarded a single artist and it took forty-five minutes of copy-pasting between a PDF, a Google Doc, and our content management tool.

Today, I have three UMIDs. Three short strings of text, sent to me in a single group chat message.

I paste the first UMID into our gallery management system. The system reaches out to myum.net, fetches the manifest, and runs validation. The manifest is structurally sound -- all required fields present, types correct, timestamps valid. The TTL checks out: the manifest was issued yesterday and does not expire until next week. The system then reads the venue policy facet from our own gallery manifest -- PG-13 content rating, no nudity, no hate symbols -- and compares it against the artist's content tags. Everything passes. Within thirty seconds, the artist's name, bio, and featured work appear in our content queue, ready for display.

I paste the second UMID. Same process, same speed. This artist has allowed public display and proof-of-play analytics. Their work loads into the queue alongside the first.

The third UMID is different. This artist has consented to public display but has denied analytics tracking entirely. The system notes this and flags it clearly in my dashboard: "Analytics: denied. Proof-of-play events will not be emitted for this artist's content." I do not need to configure anything. The system read the consent toggles and adjusted automatically.

Three new artists. Zero forms. Zero file uploads. Their work is on my preview screens in under five minutes.

---

After lunch, a delivery arrives: a new 55-inch display for the east wall alcove. My technician plugs it in, connects it to the gallery's local network, and boots it up. The display runs our standard client software, which immediately looks for the gallery's edge node. It finds it via local network discovery, fetches the gallery's venue manifest, and reads the device enrollment information. The display registers itself -- its hardware model, capabilities, preferred resolution -- and appears in my device list as "Display East-03, enrolled, trust: local."

I tap "enroll" in the dashboard. The device's trust level changes from "local" to "enrolled." It begins pulling content from the queue -- the same three artists I onboarded this morning. The new display is showing art within ten minutes of being unpacked. No configuration files. No manual IP address entry. No remote desktop sessions. The display read the venue manifest, understood the enrollment process, and joined the network.

---

The show opens on Friday. People walk through the gallery, and the screens rotate through each artist's featured work. Everything is running smoothly. I pull up the activity log on my tablet. I can see exactly which manifests were resolved today, when they were last refreshed, and which consent toggles were checked. Artist one: public display allowed, analytics allowed. Artist two: same. Artist three: public display allowed, analytics denied. The log is clean and auditable.

Saturday evening, I notice something on the dashboard. Artist two's manifest has gone amber -- the TTL is approaching expiration. The manifest was issued five days ago with a seven-day window. If the artist does not renew, the manifest will expire tomorrow evening. I send a quick message: "Your manifest expires tomorrow -- want to renew for next week?"

No response. Sunday evening, the manifest expires. Our system does exactly what the spec requires: it stops rendering the artist's content. The screens that were showing their work gracefully transition to the remaining two artists. No placeholder images. No error screens. No stale content lingering on the wall. The expired manifest is retained in our logs by its ID for audit purposes, but the full payload is purged from the active cache. The system cleaned itself up.

On Monday morning I review the weekend's activity. Six manifests resolved across the weekend -- three artists, refreshed on cycle. Fourteen consent checks logged. One expiration handled automatically. Zero manual interventions.

> **Aha moment:** "Three new artists, zero forms, zero uploads. Their work was on my screens in minutes. And when the TTL expired, it cleaned itself up."

---

## How UM Works Here

**Venue manifest:** Sunset Gallery operates its own `um:Manifest` with a `venueIdentity` facet (name, locale, timezone), a `venuePolicy` facet (content rating rules, curation preferences, safety mode), and an `edgeNode` facet (local network discovery, edge base URL). This manifest defines the gallery's identity and rules for content display.

**Artist onboarding via UMID resolution:** When Jordan pastes an artist's UMID, the gallery system sends an HTTP GET to `myum.net/{UMID}` and receives the artist's manifest. It runs `assertUniversalManifestV01` to validate structure (required fields, type checks, ISO date-time format), then confirms the TTL window is valid (`issuedAt <= now <= expiresAt`).

**Content policy matching:** The system compares the artist's content metadata against the gallery's `venuePolicy` facet -- checking safety mode compatibility, content rules (no nudity, no hate symbols), and preferred media types. Only content that passes the policy gate enters the display queue.

**Device enrollment:** New displays discover the gallery's edge node via local network service discovery (`_um-edge._tcp.local`). The display fetches the venue manifest, reads the `edgeNode` facet for the edge base URL, and registers itself with a `deviceIdentity` facet containing hardware model, capabilities, and resolution. Trust level starts at `local` and is promoted to `enrolled` by the operator.

**Consent enforcement:** Before emitting analytics events, the system checks each artist's `consents` array. If `analytics.proofOfPlay` is set to `allowed`, proof-of-play events are emitted keyed by the manifest `@id`. If denied, no events are emitted. This check happens per-artist, per-render cycle.

**TTL enforcement and automatic cleanup:** The system monitors each artist manifest's `expiresAt` timestamp. When a manifest expires, the system stops rendering that artist's content, purges the full manifest from the active cache, and retains only the manifest `@id` in logs. No stale content is ever displayed.

**UM capabilities demonstrated:** Venue manifest with policy facets, UMID-based artist onboarding, device enrollment and trust levels, content policy matching, per-artist consent enforcement, TTL-driven automatic cleanup.
