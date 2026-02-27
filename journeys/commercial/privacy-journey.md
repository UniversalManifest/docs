# The Privacy-Conscious Individual

**Persona:** Riley Torres, privacy advocate. Uses multiple platforms but is careful about what data goes where. Currently manages privacy settings in 15 different apps individually.

---

I keep a spreadsheet. It has fifteen rows -- one for each platform I use -- and columns for every privacy toggle I care about. Profile visibility. Search indexing. Analytics. Location sharing. Face recognition. Data retention. Cross-platform sharing. I update it whenever a platform changes their settings page, which happens constantly. Last month, three platforms redesigned their privacy dashboards. Two of them reset my preferences to defaults. One of them added a new "personalization" toggle that was opted-in by default and buried three menus deep.

I spend more time managing my privacy settings than I do using some of these platforms.

When I first hear about Universal Manifest, I am skeptical. Another identity layer. Another place to put my data. But when I read the spec, one sentence stops me: "Default-deny -- anything not explicitly allowed is blocked." That is the opposite of every platform I have ever used. Every platform defaults to "we take everything unless you find the off switch." UM defaults to "nothing is shared unless you say yes."

I create my manifest. I set the bare minimum in my publicProfile shard: my professional name and a link to my personal website. Nothing else. Then I set my consents. I go through the list deliberately:

- `publicDisplay`: denied.
- `analytics.proofOfPlay`: denied.
- `social.profilePublic`: denied.
- `ar.recording.faceVisible`: denied.
- `ar.recording.voiceAllowed`: denied.
- `ar.profile.autoSharePublic`: denied.

Everything is off. This is my starting point. I will open individual doors when I trust the room on the other side.

I set the TTL to 48 hours. My manifest expires every two days and auto-renews with the same settings. If any system caches my manifest, it becomes invalid after 48 hours. They have to come back and get a fresh copy -- which means they get my latest consent settings every time.

---

I sign up for a new professional networking app using my UMID. The app fetches my manifest and reads my publicProfile shard -- just my name and website link. The app checks for `social.profilePublic` consent. It finds the value set to `denied`. My profile is created but not visible to other users. I can browse the platform, but nobody can find me or see my information. The app does not push back or nag me about "completing my profile." It respects what the manifest says.

I decide this platform is trustworthy after a week of using it. I open my manifest and flip one toggle: `social.profilePublic: allowed`. I sync. Within the hour -- on the next TTL refresh cycle -- the app picks up the change. My profile becomes visible. One toggle, one place, one change. Not a fifteen-step privacy wizard. Not a cookie banner. One consent value in my manifest.

---

I attend a technology conference. The venue has smart glasses stations for attendees to try AR demos. The glasses run UM-compatible software. When I walk into the demo area, the glasses scan for nearby attendees' UMIDs via a local beacon. They find mine and fetch my manifest.

The glasses check `ar.recording.faceVisible`. My manifest says denied. The AR system immediately applies a privacy filter: my face is blurred in real-time on the glasses' display. Other attendees wearing the glasses see a blurred shape where I am standing. My voice is not captured either -- `ar.recording.voiceAllowed: denied`. I am a ghost in the augmented layer, exactly as I chose to be.

I notice a colleague, Dana, who is standing nearby and fully visible in the AR layer -- sharp face, name tag floating above her head, professional title displayed. She set her consents to allowed. We made different choices. The same system respects both.

---

After the conference, I pull up my manifest's activity log. The resolver tracks which systems fetched my manifest and when. I can see the professional networking app checking every 48 hours on the TTL cycle. I can see the conference venue's AR system making a single fetch during the demo session. I can see a third platform I forgot about -- a music streaming service I signed up for months ago -- still checking on its refresh cycle. Everything is transparent.

I examine the music service's access pattern and decide I no longer want them to have access at all. I could revoke their access specifically, but with UM's architecture, I do not need a per-platform revocation mechanism. I simply ensure my manifest continues to deny the consents that service would need. The next time they check, they get nothing useful. And when my manifest TTL expires in 48 hours, whatever they cached becomes invalid. The short TTL is my data retention policy, enforced by the protocol.

Months later, I look back at that spreadsheet I used to maintain. I have not updated it in ten weeks. I do not need to. My privacy preferences live in one place -- my manifest -- and every system that interacts with me checks that manifest before doing anything. When I change my mind, I change it once. When I want something denied, I simply do not allow it, and the default-deny model handles the rest.

> **Aha moment:** "I set my privacy preferences once. Every app, every device, every platform checks my manifest before doing anything. I am in control everywhere, not just in one app's settings page."

---

## How UM Works Here

**Default-deny consent model:** UM's consent architecture treats the absence of an explicit `allowed` value as a denial. Riley's manifest starts with everything denied. Consumers check the `consents` array for specific consent names; if a name is not present or its value is not `allowed`, the consumer must not perform that action. This inverts the typical platform pattern where everything is allowed unless the user finds the opt-out.

**Consent entries as explicit toggles:** Each consent entry in the manifest has a `@type` of `um:Consent`, a `name` (e.g., `ar.recording.faceVisible`, `social.profilePublic`), and a `value` (`allowed`, `denied`, or `restricted`). Riley controls each toggle independently. Consumers read specific consent names relevant to their function.

**Smart glasses consent enforcement:** AR-capable devices fetch nearby attendees' manifests via UMID resolution and check AR-specific consent entries (`ar.recording.faceVisible`, `ar.recording.voiceAllowed`). When these are denied, the device applies privacy filters in real-time (face blurring, voice exclusion). The AR policy is modeled through an `arPolicyPack` shard with a default stance of `deny-if-missing-consent`.

**TTL as a privacy guarantee:** Riley sets a 48-hour TTL (`expiresAt` = `issuedAt` + 48 hours). Consumers must re-fetch before expiry. Expired manifests must be rejected per the conformance spec -- no consumer may continue to use an expired manifest to grant permissions or render state. This ensures that no system retains valid permissions beyond the TTL window.

**UMID-based access transparency:** The resolver logs which systems fetched Riley's manifest and when. This is not behavioral tracking -- it is access auditing. Riley can see the fetch pattern and decide whether to continue allowing access.

**Consent revocation propagation:** When Riley changes a consent value (e.g., flipping `social.profilePublic` from `denied` to `allowed`), the updated manifest syncs to the resolver. Consumers pick up the change on their next TTL-driven refresh. No per-platform revocation API is needed; the manifest is the single source of truth.

**UM capabilities demonstrated:** Default-deny consent enforcement, AR consent toggles, TTL as data retention control, UMID resolution for consent checking, consent change propagation via TTL refresh, audit transparency.
