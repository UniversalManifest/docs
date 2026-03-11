# V-03: Default-Deny Consent

**Duration:** 30–45 seconds
**Format:** Motion graphics / animated explainer
**Audience:** Anyone interested in how UM handles privacy — product managers, privacy advocates, adopters.
**Tone:** Confident, clear, slightly emphatic on the "denied by default" point.
**Concept:** Privacy controls that travel inside the manifest. If a permission is not explicitly granted, it is denied. Consent is embedded in the data layer, not bolted on after the fact.

---

### Scene 1: The Consent Panel (12s)

**Visual:** A Universal Manifest card opens to reveal the consent compartment (teal-colored). Inside, a clean panel of toggle switches appears:

- `publicDisplay` — switch is **green** (allowed). A small open padlock icon beside it.
- `analytics.tracking` — switch is **red** (denied). A small locked padlock icon beside it.
- `ar.recording.faceVisible` — switch is **gray** (not set). A small locked padlock icon beside it, with a label: "not set = denied."

The three states are visually distinct: green glow for allowed, red glow for denied, gray with a lock for unset.

**Narration:** "Every Universal Manifest can carry consent toggles — explicit signals for how data may be used. Green means allowed. Red means denied. And if a permission is not set at all — gray — it defaults to denied. Nothing gets through unless you open the lock."

**On-screen text:** `Green = allowed` | `Red = denied` | `Gray = denied by default`

---

### Scene 2: Consent in Action (15s)

**Visual:** A system (represented by a glowing probe beam from an app icon) approaches the manifest to access data:

- **Probe 1:** The beam reaches for `publicDisplay`. It passes through the green toggle with a clean "access granted" visual — the beam connects. A checkmark appears.
- **Probe 2:** The beam reaches for `analytics.tracking`. It hits the red padlock and deflects with a spark. An X mark appears.
- **Probe 3:** The beam reaches for `ar.recording.faceVisible`. It hits the gray padlock — same result, deflected with a spark. An X mark appears. A small callout: "Not set? Still denied."

The manifest owner (Riley, shown as a silhouette) watches from behind the manifest, arms folded, satisfied.

**Narration:** "When a system requests access, it checks the consent toggles. Allowed? The data flows. Denied or not set? Blocked. The system does not need to ask — the answer is already in the manifest. Privacy travels with the data."

**On-screen text:** `Consent built in. Not bolted on.`

---

### Scene 3: Close (8s)

**Visual:** The consent panel folds back into the manifest card. The card glows steadily. A tagline appears:

**Narration:** "Your data. Your rules. Enforced everywhere, by default."

**On-screen text:** `universalmanifest.net`

---

## Production Notes

- **Key technical accuracy:** Consents are objects in the manifest's `consents` array, each with `@type: "um:Consent"`, a `name` field (e.g., `"publicDisplay"`, `"analytics.tracking"`), and a `value` field (`"allowed"` or `"denied"`). The absence of a consent entry for a given permission is treated as denied — this is the consent-default-deny pattern proven in Journey 10 and the conformance test suite.
- **Critical distinction:** Consent is **structural**, not a UI feature. It lives inside the JSON document itself, not in a cookie banner or a terms-of-service page. Downstream systems read the consent array to determine behavior.
- **Visual palette:** Consent panel is teal (#14b8a6). Toggle states: green (#22c55e) for allowed, red (#ef4444) for denied, gray (#6b7280) for not set. Dark background (#0f172a).
- **Sound design:** Toggle clicks are satisfying mechanical sounds. "Access granted" is a clean chime. "Blocked" is a firm but not aggressive deflection sound.
- **Aspect ratios:** 16:9 (primary), 1:1 (social), 9:16 (stories/reels).
