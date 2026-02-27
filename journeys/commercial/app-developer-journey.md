# The App Developer

**Persona:** Sam Chen, building a social platform for creators. Tired of building custom profile import for every other platform. Wants portable profiles that users control.

---

I have been building Artboard for six months -- a social platform where creators share process videos, studio shots, and collaborate on projects. The product is solid. The onboarding is not. Every new user hits the same wall: a blank profile page with twelve empty fields. Name. Bio. Avatar. Links. Location. Tags. Most people fill out three fields and abandon the rest. The profiles look thin. The network feels empty.

I have tried importing profiles from other platforms. I built a scraper for one service, an OAuth integration for another, and a CSV importer for a third. Each one took two weeks of engineering time. Each one breaks when the upstream platform changes their API. Each one captures a frozen snapshot that goes stale the moment the user updates their profile elsewhere. I am tired of building import tools for data that users already have somewhere.

Then I read about Universal Manifest.

I install the `universal-manifest` TypeScript package from npm. It is a single file -- types, validators, and assertion functions. No SDK wrapper. No API keys. No OAuth dance. I add one endpoint to my signup flow: "Have a UMID? Enter it here."

On the backend, when a user provides their UMID, my server sends a GET request to `myum.net/{UMID}`. The response is a JSON-LD document. I pass it through `assertUniversalManifestV01` -- the assertion function checks that all required fields are present (`@context`, `@id`, `@type` including `um:Manifest`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`), validates the date-time formats, and confirms the TTL window has not expired. If anything is wrong, the function throws with a specific error. If it passes, I know I have a structurally valid, non-expired manifest.

I deploy on a Thursday. The first user with a UMID signs up on Friday.

---

Her name is Jules. She enters her UMID in the signup field and taps "continue." My app fetches her manifest, validates it, and reads the `publicProfile` shard. Her display name, bio, avatar URL, and social links flow into her profile page. The twelve empty fields are now eight filled fields. Her profile looks real. She did not type a single character.

But the interesting part is the consents. Jules's manifest says `social.profilePublic: allowed` -- she has explicitly permitted platforms to publish a public profile view derived from her manifest. Good. But I also check for analytics consent, and there is no entry for search indexing. Under UM's default-deny model, the absence of an explicit `allowed` means the answer is no. My app renders her profile for visitors but does not add her to the public search index.

I did not write special case logic for this. I wrote a generic consent checker: look up the consent name in the `consents` array, return the value if present, return `denied` if absent. Five lines of code. Default-deny handled.

---

Three weeks later I add v0.2 signature verification. The v0.2 spec locks down the signature profile: Ed25519 algorithm, JCS (RFC 8785) canonicalization, base64url-encoded signature value, and either an inline public key (`publicKeySpkiB64`) or a key reference (`keyRef`). I call `assertUniversalManifestV02` instead of the v0.1 variant. The function validates the structure, extracts the signature, strips it from the manifest, canonicalizes the remaining document using JCS, and verifies the Ed25519 signature against the public key.

The first v0.2 manifest I verify belongs to a creator named Marco. His profile loads, and next to his name my app now shows a small checkmark -- "Verified manifest." The profile data has not been tampered with since Marco signed it. No certificate authority. No centralized trust service. Just a cryptographic proof that the manifest is intact.

---

A month in, something happens that I did not plan for but that the system handled anyway. A user named Priya signed up with her UMID, and her profile had been live for three weeks. Then she revoked consent. She opened her manifest, set `social.profilePublic` to `denied`, and synced.

My app periodically re-fetches manifests before their TTL expires. On the next cycle, it pulled Priya's updated manifest, ran the consent check, and found that `social.profilePublic` was now denied. Her profile page was automatically hidden from public view. No support ticket. No moderation queue. No delete request form. The user changed their mind, the manifest reflected it, and my app respected it.

I sit back and think about what I did not have to build. I did not build a profile importer. I did not build a scraper. I did not build an OAuth integration. I did not build a data deletion workflow. I did not build a consent management dashboard. All of that complexity lives in the manifest, controlled by the user, and my app just reads it.

> **Aha moment:** "My users brought their own profiles. I did not build a single scraper or import tool. And when they revoked consent, the system just worked."

---

## How UM Works Here

**TS helper integration:** Sam installs the `universal-manifest` npm package and uses `assertUniversalManifestV01` to validate incoming manifests. The function checks all required fields (`@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`), validates ISO date-time formats, confirms `@type` includes `um:Manifest`, and verifies shard structure. It throws typed errors for any validation failure.

**UMID resolution:** The app fetches manifests by sending an HTTP GET to `myum.net/{UMID}`. The resolver returns the manifest as `application/ld+json` with short cache headers (`max-age=60`). The app re-fetches on a TTL-driven cycle to detect updates and consent changes.

**Shard reading:** The app reads the `publicProfile` shard to extract profile fields (name, bio, avatar, links). Each shard has a `@type` of `um:Shard` and a `name` field for lookup. The app ignores unknown shards per the v0.1 conformance requirement -- forward compatibility is built in.

**Consent checking:** The app checks the `consents` array for specific consent names (`social.profilePublic`, analytics toggles). Each consent entry has a `name` and `value` (`allowed` or `denied`). If a consent name is absent from the array, the app treats it as denied (default-deny). This five-line check replaces an entire consent management subsystem.

**Signature verification (v0.2):** When a v0.2 manifest arrives, the app calls `assertUniversalManifestV02`, which validates the Ed25519 signature. The function strips the `signature` field, canonicalizes the remaining document with JCS (RFC 8785), and verifies the signature using the `publicKeySpkiB64` from the signature envelope. A valid signature proves the manifest has not been modified since signing.

**TTL re-validation:** The app checks `expiresAt` on every access using `assertUniversalManifestV01Fresh`. Expired manifests are rejected. Periodic re-fetching before TTL expiry ensures the app always has current consent and profile data. When a user revokes consent, the change is picked up on the next fetch cycle.

**UM capabilities demonstrated:** TS helper validation, UMID resolution, shard-based profile reading, default-deny consent model, Ed25519 signature verification (v0.2), TTL-driven freshness enforcement, consent revocation handling.
