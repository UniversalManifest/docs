# The Freelance Creator

**Persona:** Alex Rivera, mixed-media artist. Creates installations, digital art, and ambient performances. Works across multiple venues, platforms, and virtual worlds. Frustrated with maintaining profiles everywhere.

---

I am sitting in my studio on a Tuesday afternoon, surrounded by half-finished collages and the hum of an audio loop I have been layering for three days. My phone buzzes with a reminder: three gallery applications are due this week, each one asking for the same information I have typed into a hundred forms before. Bio. Artist statement. Portfolio links. Headshot. Social handles. Emergency contact. Every time I apply to a new venue, I rebuild myself from scratch.

Not this time.

I open the Universal Manifest app on my laptop and start building my manifest. I type my name, paste in my artist bio, and link to the portfolio page I already maintain on my own site. I set my display name, add a headshot URL, and tag the media I want venues to feature -- "Corner Store Sunlight," the photo series from last spring, and the ambient video loop "Night Bus Polaroids." I point to my canonical portfolio page as the authoritative source for my work. I am not uploading copies of anything. The manifest just holds a reference -- a pointer -- to where my real work lives.

Then I set my consent toggles. Public display? Allowed. Analytics tracking? Allowed, but only proof-of-play events keyed to my manifest ID, not behavioral profiling. Social profile publishing? Allowed. I leave everything else off. If a system wants something I have not explicitly permitted, the answer is no by default.

The whole process takes eight minutes. My manifest gets a unique identifier -- my UMID -- and syncs to the resolver at myum.net. I copy my UMID and paste it into three gallery application forms. That is it. Three applications, one string of text.

---

Two days later, I get accepted to Sunset Gallery for a weekend show. Jordan, the gallery operator, sends me a message: "Got your UMID. Your work is already on our preview screens." I have never been to Sunset Gallery. I have never met Jordan. But my art is there, on the walls, because the gallery's system fetched my manifest, read my publicCapsule shard, confirmed my consent for public display, and pulled the featured media from the URLs I pointed to. No email attachments. No WeTransfer links. No "can you send that in a different format."

I walk into Sunset Gallery on Friday evening for the first time. The screens in the main room are already showing "Corner Store Sunlight" in a slow rotation. In the corner, a smaller display cycles my bio and headshot. I did not do anything to make this happen. The gallery system read my manifest, followed the pointers to my media, and rendered what I had consented to show.

I stand there for a moment, watching my own work appear in a space I have never visited before, without having filled out a single form for it. That is the moment it clicks.

---

The following week, a new social platform for creators launches and invites me to join. I enter my UMID during signup. The platform reads my publicProfile shard -- name, bio, avatar, links -- and pre-fills my profile page. It checks my consent settings: I have allowed social profile publishing but denied analytics indexing for search. The platform shows my profile to visitors but does not add me to their discovery index. Exactly what I asked for.

A week after that, I notice the platform started running aggressive behavioral analytics on profile views. I open my manifest and flip the analytics consent toggle to "denied." I sync. The next time the platform's system checks my manifest -- which it does on a short interval because of the TTL -- it sees the change. The analytics pipeline stops collecting data on my profile views. I did not file a support ticket. I did not navigate five menus in a settings page. I changed one value in one place.

Then I update my portfolio. I finish a new piece, "Rooftop Signal," and add it to my canonical portfolio page. I do not need to update my manifest at all -- because the manifest holds a pointer to my portfolio URL, not a copy of the portfolio itself. Every system that follows that pointer -- Sunset Gallery, the social platform, a virtual world gallery I joined last month -- sees the new piece the next time they resolve the pointer. One update, everywhere, instantly.

> **Aha moment:** "I updated my portfolio once and it showed up everywhere -- at the gallery, on the social platform, even in the virtual world. I never filled out another form."

---

## How UM Works Here

**Manifest creation:** Alex creates a single `um:Manifest` document containing identity fields (`subject`, display name, bio), a `publicCapsule` shard with featured media references, a `publicProfile` shard for social surfaces, consent toggles (`publicDisplay: allowed`, `analytics.proofOfPlay: allowed`, `social.profilePublic: allowed`), and pointers to canonical data sources (portfolio URL, social handles).

**Resolver sync:** The manifest is published to the myum.net resolver under Alex's UMID. Any system with the UMID can fetch the manifest via a simple HTTP GET to `myum.net/{UMID}`.

**Shard reading:** Sunset Gallery reads the `publicCapsule` shard to extract display-safe media references and profile data. The social platform reads the `publicProfile` shard for web-facing profile fields. Each consumer reads only the shards relevant to its surface.

**Consent enforcement:** Before rendering or processing data, each consumer checks the `consents` array. The gallery checks `publicDisplay: allowed` before showing art on screens. The social platform checks `social.profilePublic` before publishing the profile and respects `analytics.proofOfPlay: denied` by excluding Alex from behavioral tracking. UM operates on a default-deny model: anything not explicitly set to `allowed` is blocked.

**Pointer resolution:** Alex's portfolio URL is stored as a pointer, not embedded content. When Alex adds a new piece to their portfolio, every system that resolves the pointer sees the update without any manifest change. The manifest is the routing layer; the canonical data lives where Alex controls it.

**TTL enforcement:** The manifest has `issuedAt` and `expiresAt` timestamps. Consumers must re-fetch before the TTL expires. When Alex changes a consent toggle, the updated manifest is picked up on the next TTL cycle. Expired manifests are rejected -- no stale permissions persist.

**UM capabilities demonstrated:** Manifest creation, UMID resolution, shard-based data compartments, pointer-based canonical references, default-deny consent enforcement, TTL-driven freshness.
