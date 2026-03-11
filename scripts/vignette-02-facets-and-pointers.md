# V-02: Facets and Pointers

**Duration:** 30–45 seconds
**Format:** Motion graphics / animated explainer
**Audience:** Someone who knows what a Universal Manifest is and wants to understand the internal structure.
**Tone:** Clean, instructive, modern.
**Concept:** Modular data compartments (facets) with lightweight external references (pointers) that keep the manifest small and the data fresh.

---

### Scene 1: Open the Envelope (10s)

**Visual:** A Universal Manifest card floats on a dark canvas. It opens like a briefcase to reveal its interior. Inside, modular compartments slide into view, each a different accent color:

- **Blue:** `publicProfile` — a name tag, bio text, and avatar thumbnail.
- **Amber:** `claims` — a badge with a role label ("creator") and a verification stamp.
- **Teal:** `consents` — a panel of toggle switches (shown briefly, detailed in V-03).
- **Violet:** `deviceRegistration` — a small screen icon with a serial number.

Each compartment has a label tab, like folders in a filing cabinet.

**Narration:** "Inside a Universal Manifest, data is organized into facets — named compartments, each carrying different information. A profile facet for social apps. A claims facet for credentials. A device facet for hardware. Each system reads only the facets it needs."

**On-screen text:** `Facets: modular, named data sections`

---

### Scene 2: Pointers — References, Not Copies (15s)

**Visual:** A fifth compartment slides out — coral-colored, labeled `pointers`. But unlike the others, it does not contain data. Instead, it holds small arrow icons, each pointing outward with a URL label:

- `metaverse.avatar` → arrow points to a 3D model icon (50 MB) floating outside the manifest.
- `portfolio.gallery` → arrow points to a grid of artwork thumbnails floating outside.
- `rp1.fabric` → arrow points to a spatial scene icon floating outside.

The manifest card itself is visibly small — a size comparison appears: "Manifest: ~2 KB" versus the 3D model: "Asset: 50 MB." The manifest stays lightweight while the arrows reach the full-size data.

**Narration:** "Pointers are the key to keeping manifests lightweight. Instead of embedding a 50-megabyte 3D avatar or an entire portfolio, the manifest stores a URL pointing to the authoritative source. Consuming systems follow the pointer to fetch the real data. The manifest stays under a few kilobytes — small enough to send by API, Bluetooth, or QR code."

**On-screen text:** `Pointers: URLs to authoritative data, not copies`

---

### Scene 3: The Benefit (10s)

**Visual:** A quick split view. Left: a traditional system trying to pass a massive data blob between two platforms — it is slow, the connection strains, versions go stale. Right: the UM approach — a tiny manifest card zips instantly between platforms, and each platform follows pointers to fetch only what it needs, always getting the latest version.

The Universal Manifest wordmark appears below.

**Narration:** "Lightweight, modular, always current. Facets organize the data. Pointers keep it fresh."

**On-screen text:** `universalmanifest.net`

---

## Production Notes

- **Key technical accuracy:** Facets are objects in the manifest's `facets` array, each with a `name` field (e.g., `"publicProfile"`, `"deviceRegistration"`). Pointers are objects with `name` and `url` fields. Pointers reference external authoritative data — they never embed the content. Typical manifest size is 1–3 KB.
- **Visual palette:** Dark background (#0f172a). Each facet type has its own accent color (blue, amber, teal, violet, coral) consistent across all vignettes.
- **Sound design:** Compartments slide in with soft "click" sounds. Pointers extending outward have a "whoosh" sound. Size comparison has a subtle "ding."
- **Aspect ratios:** 16:9 (primary), 1:1 (social), 9:16 (stories/reels).
