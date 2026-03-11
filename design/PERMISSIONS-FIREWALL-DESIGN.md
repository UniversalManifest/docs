# Personal Data Firewall -- Permissions Architecture for Universal Manifest

**Status**: Draft design proposal (2026-03-01)
**Source**: `.dev/INBOX/permissions-system.md` (rough concept note)
**Inspiration**: [Little Snitch](https://www.obdev.at/products/littlesnitch/index.html) network firewall permission model
**Relates to**: `spec/v0.1/REGISTRY.md` (consent names), `docs/PROJECT-VISION.md` (permission model direction), `integrations/smart-glasses.md`, `integrations/healthcare-patient-consent.md`

---

## 1. The Core Idea

**A Universal Manifest is not just a document you hand over. It is a document you *control*.**

The manifest carries your identity, claims, consents, and pointers across system boundaries. But without a permission model that puts the subject in control, the manifest becomes a liability -- a packet of personal data that any consumer can read in full.

The proposal: treat the manifest's consent layer as a **personal data firewall**. Like Little Snitch controls which applications can make which network connections, the manifest's permission system controls which consumers can access which pieces of your portable state.

The firewall metaphor is precise:

| Network Firewall (Little Snitch) | Data Firewall (Universal Manifest) |
|---|---|
| Application wants to connect to a server | Consumer wants to read a facet or claim |
| Rule: allow/deny by app + destination + port | Rule: allow/deny by consumer + data-type + context |
| Default: deny all (zero trust) | Default: deny all (consents absent = denied) |
| First connection triggers a prompt | First access request triggers a consent decision |
| Rule remembered for future connections | Consent recorded in manifest for future presentations |
| Noise decreases as rules accumulate | Consent prompts decrease as preferences stabilize |
| Profiles for different networks (home/work/public) | Profiles for different contexts (personal/professional/public/emergency) |

---

## 2. What Already Exists in the Spec

The Universal Manifest v0.1 already has the **foundation** for this model. The `consents[]` array is designed as a default-deny permission system:

```json
{
  "consents": [
    { "@type": "um:Consent", "name": "publicDisplay", "value": "allowed" },
    { "@type": "um:Consent", "name": "ar.recording.faceVisible", "value": "denied" },
    { "@type": "um:Consent", "name": "health.shareAllergies", "value": "restricted" }
  ]
}
```

**Current model strengths:**
- Default-deny: if a consent name is absent, the consumer SHOULD treat it as denied
- Simple vocabulary: `allowed`, `denied`, `restricted` as values
- Domain-namespaced keys: `ar.*`, `health.*`, `social.*` etc.
- Already integrated into journey proofs (journey-08: smart glasses consent enforcement)

**Current model gaps (what this design addresses):**
- No concept of *who* is requesting access (consumer identity)
- No concept of *conditional* access (allowed for hospitals, denied for employers)
- No concept of *context-dependent* rules (different rules at home vs. in public)
- No concept of *temporal* consent (allowed for this session, not permanently)
- No mechanism for rule *learning* or progressive refinement
- No standard for how a subject *manages* their consent rules over time

---

## 3. Specification vs. Implementation Boundary

This is the critical architectural decision. The design splits cleanly into two layers:

### Layer 1: Specification (normative -- lives in `spec/`)

The spec defines **what a consent rule looks like** and **what a consumer MUST do when it encounters one**. The spec is the *wire format* and the *enforcement contract*.

The spec answers:
- What is the shape of a consent rule?
- What values are valid?
- What does "deny by default" mean precisely?
- How do conditional rules (audience-scoped consents) get expressed?
- How does a consumer match itself against a rule?

### Layer 2: Implementation (non-normative -- lives in `integrations/` and adopter surfaces)

Implementation defines **how the subject creates and manages their rules** and **how the experience feels**. The implementation is the *firewall UI* and the *rule management system*.

Implementation answers:
- How does the subject get prompted for new consent decisions?
- How do rules accumulate and reduce noise over time?
- How does the subject review and modify their rules?
- How do profiles/contexts switch?
- How does monitoring/observability work?

### The Boundary Principle

> **The spec defines the language. Implementations speak it.**
>
> A consent rule in the manifest is like a firewall rule in a packet header.
> The spec defines the header format. Implementations decide how rules get created,
> managed, and displayed to the user.

This means:
- Two completely different implementations (a mobile app and a CLI tool) can produce manifests with identical consent rules
- A consumer does not need to know *how* the subject decided on their rules, only *what* the rules say
- The firewall UX (progressive disclosure, noise reduction, profiles) is an implementation concern, not a spec concern

---

## 4. Specification-Level Design

### 4.1 Consent Rule Structure (proposed extension to `um:Consent`)

The current v0.1 consent is a simple name/value pair. The firewall model extends this with optional structured fields while remaining backward-compatible:

**v0.1 (current, still valid):**
```json
{ "@type": "um:Consent", "name": "publicDisplay", "value": "allowed" }
```

**Extended consent rule (proposed):**
```json
{
  "@type": "um:Consent",
  "name": "health.shareAllergies",
  "value": "allowed",
  "audience": {
    "@type": "um:Audience",
    "match": "accreditation",
    "value": "healthcare.provider"
  },
  "context": "emergency",
  "expires": "2026-06-01T00:00:00Z",
  "notes": "Allow any accredited healthcare provider to see allergies in emergency contexts"
}
```

#### New optional fields:

| Field | Type | Spec/Impl | Description |
|-------|------|-----------|-------------|
| `audience` | `um:Audience` | **Spec** | Who this rule applies to (consumer matching criteria) |
| `context` | string | **Spec** | Context tag for when this rule applies |
| `expires` | ISO 8601 | **Spec** | When this specific consent rule expires (independent of manifest TTL) |
| `scope` | string | **Spec** | What level of data this rule covers (`section`, `facet`, `field`) |
| `notes` | string | **Spec** | Human-readable rationale (already exists in some integration lanes) |

#### Backward compatibility:

A consent without `audience`, `context`, or `expires` behaves exactly as v0.1: a blanket allow/deny for all consumers in all contexts, valid for the manifest's TTL. Extended fields are additive; consumers that do not understand them MUST fall back to the base `value`.

### 4.2 Audience Matching

The `audience` field answers the question: **who is allowed to access this data?**

This is the firewall-rule equivalent of "which application on which destination." In the data firewall model, the "application" is the consuming system, and the "destination" is the data section being accessed.

**Proposed audience match types:**

| Match type | Meaning | Example |
|---|---|---|
| `any` | Any consumer | Public data; no restrictions beyond consent value |
| `accreditation` | Consumer must present a recognized accreditation | `"healthcare.provider"`, `"education.institution"` |
| `relationship` | Consumer must have a declared relationship to the subject | `"employer"`, `"family"`, `"friend"` |
| `identity` | Specific consumer identity (DID or URI) | `"did:web:hospital.example"` |
| `domain` | Consumer's domain matches | `"*.nhs.uk"`, `"university.edu"` |

**Matching semantics (normative):**

- If `audience` is absent, the consent applies to **all consumers** (equivalent to `match: "any"`).
- If `audience` is present and the consumer cannot prove it matches, the consent MUST be treated as `"denied"` regardless of `value`.
- Multiple consents with the same `name` but different `audience` values are valid. The **most specific matching rule wins** (same precedence model as Little Snitch).

### 4.3 Context Tags

Contexts answer: **when does this rule apply?**

This maps to Little Snitch's "Profiles" concept -- different rule sets for different situations.

**Proposed well-known context values:**

| Context | Meaning |
|---|---|
| `default` | Applies when no other context is active (fallback) |
| `public` | Subject is in a public setting (venue, event, public space) |
| `private` | Subject is in a private setting (home, personal device) |
| `professional` | Subject is in a work context |
| `emergency` | Emergency access (may override other denials) |
| `event:<name>` | Named event or venue context |

**Context semantics (normative):**

- If `context` is absent, the consent applies in **all contexts** (equivalent to `"default"`).
- If multiple consents match the same `name` + `audience` but differ by `context`, the consumer MUST use the rule matching its current context, falling back to `"default"` if no specific match exists.
- Context identification is a consumer responsibility. The spec defines the vocabulary; implementations decide how context is determined.

### 4.4 Scope Granularity

Consents can apply at different levels of the manifest:

| Scope | Applies to | Example consent name |
|---|---|---|
| `section` | An entire top-level section | `"publicDisplay"` (governs all rendering) |
| `facet` | A specific facet by name | `"facet:allergyAlerts"` (governs one facet) |
| `field` | A specific field within a facet | `"facet:publicProfile.field:dateOfBirth"` |

**Scope semantics (normative):**

- If `scope` is absent, it is inferred from the consent `name`:
  - Names without `:` prefix are section-level (current v0.1 behavior)
  - Names starting with `facet:` are facet-level
  - Names containing `.field:` are field-level
- More specific scopes override less specific ones (a facet-level deny overrides a section-level allow for that facet).

### 4.5 Default-Deny Formalization

The current v0.1 spec recommends but does not mandate default-deny. The firewall model makes this normative:

**Proposed normative requirement (for conformant consumers at Tier 2+):**

> A consumer that respects consent semantics MUST treat the absence of a consent
> entry for a given data section, facet, or field as equivalent to `"denied"`.
> Explicit consent is required for access. This is the **default-deny** principle.

**Exception: Tier 0 and Tier 1 consumers** (parse-only and pointer-consumers from the adoption tiers) are not required to enforce consent semantics, as they do not interpret payload content.

### 4.6 Consent Precedence Rules

When multiple consent rules could apply, specificity determines which rule wins. This directly mirrors Little Snitch's rule precedence:

**Precedence hierarchy (most specific wins):**

1. Field-level consent (`facet:publicProfile.field:dateOfBirth`)
2. Facet-level consent (`facet:publicProfile`)
3. Section-level consent (`publicDisplay`)
4. Audience-specific rule over audience-general rule
5. Context-specific rule over context-general rule
6. Explicit `"denied"` over `"allowed"` at the same specificity level (deny wins ties)
7. Absent consent = `"denied"` (default-deny fallback)

---

## 5. Implementation-Level Design

Everything below is **non-normative guidance** for implementations that want to provide the full "personal data firewall" experience.

### 5.1 Progressive Consent Gathering (The "Learning" Phase)

Inspired by Little Snitch's Alert Mode, implementations SHOULD support a "learning" phase:

1. **Initial state**: The manifest starts with minimal or no consent rules.
2. **First-access prompts**: When a consumer requests data that has no consent rule, the issuing system (wallet, agent, or app) prompts the subject: *"[Consumer X] is requesting access to your [employment history]. Allow or deny?"*
3. **Rule creation**: The subject's decision creates a consent rule that is embedded in future manifest issuances.
4. **Noise reduction**: Over time, the subject has answered most common requests. New prompts only appear for genuinely novel consumer/data combinations.

**Implementation pattern:**

```
New access request arrives
  │
  ├── Matching consent rule exists?
  │     ├── Yes, value = "allowed" → Grant access
  │     ├── Yes, value = "denied"  → Deny access
  │     └── Yes, value = "restricted" → Apply audience/context checks
  │
  └── No matching rule?
        ├── Prompt subject for decision
        │     ├── "Allow always" → Create permanent consent (value: "allowed")
        │     ├── "Allow once"   → Grant access, no rule created
        │     ├── "Allow for this session" → Create temporary consent (with expires)
        │     └── "Deny always"  → Create permanent consent (value: "denied")
        │
        └── Subject unavailable?
              └── Default-deny applies → Deny access
```

### 5.2 Rule Management Interface

Implementations SHOULD provide a way for subjects to review and modify their consent rules. Conceptual design:

**Dashboard view (analogous to Little Snitch's rule list):**

```
┌─────────────────────────────────────────────────────────────────┐
│  My Data Firewall                                               │
│                                                                 │
│  Active Profile: [Personal]  ▼                                  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │ RULE                         │ AUDIENCE    │ STATUS        ││
│  ├─────────────────────────────────────────────────────────────┤│
│  │ Public profile display       │ Anyone      │ ● Allowed     ││
│  │ Employment history           │ Accredited  │ ◐ Restricted  ││
│  │ Allergy information          │ Healthcare  │ ● Allowed     ││
│  │ Date of birth                │ Government  │ ◐ Restricted  ││
│  │ Social graph sharing         │ Anyone      │ ○ Denied      ││
│  │ Face visibility (smart glasses)         │ Anyone      │ ○ Denied      ││
│  │ Location history             │ Anyone      │ ○ Denied      ││
│  └─────────────────────────────────────────────────────────────┘│
│                                                                 │
│  Recent activity: 3 new requests this week                      │
│  [Review pending requests]                                      │
└─────────────────────────────────────────────────────────────────┘
```

### 5.3 Context Profiles

Implementations MAY support switchable profiles (like Little Snitch's network profiles):

| Profile | Active rules | Use case |
|---|---|---|
| **Personal** | Generous sharing with friends/family, restricted for institutions | Day-to-day life |
| **Professional** | Employment claims visible, personal data restricted | Work contexts |
| **Public event** | Public display allowed, analytics allowed, personal details restricted | Venues and events |
| **Emergency** | Healthcare data allowed for any medical provider | Medical emergencies |
| **Lockdown** | Everything denied except identity verification | Maximum privacy |

When a profile is active, the implementation selects the appropriate `context` value when issuing manifests, and includes only the consent rules matching that context.

### 5.4 Observation and Monitoring

Implementations SHOULD provide visibility into what data has been accessed:

- **Access log**: Which consumers accessed which data, when (analogous to Little Snitch's Network Monitor)
- **Rule coverage**: Which data sections have explicit consent rules vs. relying on default-deny
- **Anomaly alerts**: Unusual access patterns (a consumer suddenly requesting data types it has not requested before)

### 5.5 Rule Groups

Implementations MAY support grouping consent rules by domain (like Little Snitch's Rule Groups):

- **Healthcare rules**: `health.shareAllergies`, `health.shareRecords`, `health.shareEmergencyInfo`
- **Social rules**: `social.profilePublic`, `social.graphShare`, `ar.recording.faceVisible`
- **Professional rules**: `employment.history`, `education.credentials`, `verification.status`

Groups allow bulk enable/disable operations and make the rule set manageable as it grows.

---

## 6. Integration with Existing Manifest Sections

### 6.1 Consents Governing Facets

A consent rule can gate access to a specific facet. The consumer checks the consent before reading the facet:

```json
{
  "consents": [
    {
      "@type": "um:Consent",
      "name": "facet:allergyAlerts",
      "value": "allowed",
      "audience": { "@type": "um:Audience", "match": "accreditation", "value": "healthcare.provider" }
    }
  ],
  "facets": [
    {
      "@type": "um:Facet",
      "name": "allergyAlerts",
      "entity": {
        "@type": "health:AllergyList",
        "allergies": ["penicillin", "shellfish"]
      }
    }
  ]
}
```

**Consumer behavior**: A consumer reads `facet:allergyAlerts`, checks for a consent named `facet:allergyAlerts`, verifies it can satisfy the audience requirement (it is an accredited healthcare provider), and only then processes the facet data.

**Key design question**: Should the facet data even be *present* in the manifest if the consent is `"denied"`? Two valid approaches:

1. **Declarative model** (spec-level): The facet is always present; the consent governs whether the consumer is *permitted* to use it. The data is visible in the JSON but access is policy-controlled.
2. **Selective inclusion model** (implementation-level): The issuing system omits facets that the intended audience is not permitted to access, producing a *projection* of the manifest tailored to the consumer. The consent rules describe the policy; the issuing system enforces it at generation time.

**Recommendation**: Both models are valid. The spec should define the consent semantics (model 1). Implementations may additionally use selective inclusion (model 2) as an optimization. A consumer MUST NOT assume that the absence of a facet means the subject does not have that data -- it may mean the consent was `"denied"` for this consumer.

### 6.2 Consents Governing Pointers

Pointers can be similarly gated:

```json
{
  "consents": [
    {
      "@type": "um:Consent",
      "name": "pointer:solidPod.creatorCanonical",
      "value": "restricted",
      "audience": { "@type": "um:Audience", "match": "relationship", "value": "collaborator" }
    }
  ],
  "pointers": [
    { "name": "solidPod.creatorCanonical", "url": "https://pod.example/creator/profile" }
  ]
}
```

A consumer that is not a recognized collaborator SHOULD NOT follow the pointer.

### 6.3 Consents Governing Claims

Claims themselves may be consent-gated (e.g., only reveal employment role to certain audiences):

```json
{
  "consents": [
    {
      "@type": "um:Consent",
      "name": "claim:employment.role",
      "value": "allowed",
      "audience": { "@type": "um:Audience", "match": "domain", "value": "*.employer.example" }
    }
  ],
  "claims": [
    { "@type": "um:Claim", "name": "employment.role", "value": "senior-engineer" }
  ]
}
```

### 6.4 Consents and the Signature

All consent rules are part of the signed manifest content. Changing a consent rule invalidates the signature. This is correct behavior: consent changes require re-issuance (a new manifest with a new `@id`, new `issuedAt`, and new signature).

This means the subject's firewall rules are tamper-evident. A consumer cannot silently upgrade a `"denied"` consent to `"allowed"`.

---

## 7. Capsule-Pod Visual Mapping

The data firewall concept maps naturally to the Capsule-Pod visual system:

### Firewall as the Shell

The pod's outer **shell** is the firewall boundary. The shell determines what passes through.

```
      ╭────────╮
     ╱  ╭────╮  ╲       Shell = data firewall boundary
    │   │ UM │   │       Gap   = consent verification layer
     ╲  ╰────╯  ╱       Core  = protected data (facets, claims, pointers)
      ╰────────╯
```

### New Animation States

| State | Visual | Description |
|---|---|---|
| **Access request** | Shell pulses with incoming arrow | A consumer is requesting data |
| **Consent check** | Gap illuminates amber while checking rules | Firewall is evaluating the request against consent rules |
| **Access granted** | Gap glows green; specific facet emerges through shell opening | Consent matched; data flows to consumer |
| **Access denied** | Gap flashes red; shell stays sealed | Consent check failed; no data released |
| **New rule prompt** | Gap pulses with question mark | No matching rule exists; subject must decide |

These states extend (not replace) the existing Capsule-Pod animation states from `docs/design/CAPSULE-POD-DESIGN.md`.

---

## 8. Relationship to Existing Integration Lanes

### Smart Glasses (`integrations/smart-glasses.md`)

The smart-glasses lane already defines consent keys like `ar.recording.faceVisible` and `ar.profile.autoSharePublic`. The firewall model enriches these with audience-scoped rules:

```json
{
  "name": "ar.recording.faceVisible",
  "value": "allowed",
  "audience": { "@type": "um:Audience", "match": "relationship", "value": "friend" },
  "context": "public"
}
```

*"My face is visible in smart glasses recordings made by friends, but not by strangers, when I'm in public."*

### Healthcare (`integrations/healthcare-patient-consent.md`)

The healthcare lane already defines consent-gated facets (`health.shareAllergies` gates `allergyAlerts`). The firewall model formalizes this:

```json
{
  "name": "facet:allergyAlerts",
  "value": "allowed",
  "audience": { "@type": "um:Audience", "match": "accreditation", "value": "healthcare.provider" },
  "context": "emergency"
}
```

*"Any accredited healthcare provider can see my allergies in an emergency."*

### Metaverse (`integrations/metaverse.md`)

Cross-world identity sharing gets granular control:

```json
{
  "name": "facet:crossWorldProfile",
  "value": "restricted",
  "audience": { "@type": "um:Audience", "match": "domain", "value": "*.trustedworlds.example" },
  "notes": "Only share my metaverse profile with verified world operators"
}
```

---

## 9. Open Questions

### 9.1 Audience Verification

How does a consumer *prove* it matches an audience requirement? Options:

- **Self-declaration** (low assurance): Consumer claims its accreditation in the request. Suitable for low-stakes scenarios.
- **Verifiable credential** (high assurance): Consumer presents a VC proving its accreditation. Suitable for healthcare, government, and financial contexts. Requires VC infrastructure.
- **DID resolution** (medium assurance): Consumer's DID document contains relevant service endpoints or capability declarations.

This is likely a v0.3+ concern. The spec can define the audience structure now; verification mechanisms can be profiled later (similar to how v0.1 defined the signature structure permissively and v0.2 locked down the algorithm).

### 9.2 Rule Synchronization

If a subject has multiple devices or agents managing their manifest, how do consent rules stay synchronized? This is an implementation concern, but the spec may need to define a rule-version or rule-hash mechanism to detect conflicts.

### 9.3 Emergency Override

Should the spec define a standard mechanism for emergency access that bypasses normal consent rules? The `context: "emergency"` approach lets the *subject* pre-authorize emergency access. But what about scenarios where the subject is incapacitated and hasn't pre-configured emergency rules?

This is a policy question with ethical dimensions. The spec can define the mechanism; implementations and jurisdictions define the policy.

### 9.4 Consent Delegation

Can a subject delegate consent management to a trusted agent (parent, guardian, legal representative)? The spec should probably define a delegation mechanism in a future version, but should not block the core firewall model on it.

### 9.5 Retroactive Consent Changes

If a subject changes a consent from `"allowed"` to `"denied"`, does this affect data already shared? The manifest model is inherently temporal (manifests have TTLs), so old manifests with old consent rules expire naturally. But the implementation may need to send revocation signals for high-sensitivity data.

---

## 10. Proposed Spec Evolution Path

### Phase 1: v0.1 (current) -- Foundation

- `consents[]` array with simple `name`/`value` pairs
- Default-deny recommended (not mandated)
- Well-known consent names in registry (non-normative)
- **No changes needed** -- the current spec supports the base model

### Phase 2: v0.2 (current draft) -- Signed Consent

- Consent rules are included in the signed manifest content
- Tamper-evidence: consent changes require re-issuance
- **No changes needed** -- the signature already covers `consents[]`

### Phase 3: v0.3 (proposed) -- Audience-Scoped Consent

- Add `audience` field to `um:Consent` (optional, backward-compatible)
- Add `context` field to `um:Consent` (optional, backward-compatible)
- Add `scope` field for facet/field-level granularity
- Formalize default-deny as normative for Tier 2+ consumers
- Define consent precedence rules
- Add `um:Audience` type to JSON-LD context

### Phase 4: v0.4+ (future) -- Verified Audience

- Define audience verification profiles (VC-based, DID-based)
- Add consent delegation mechanism
- Add consent synchronization protocol
- Add emergency override profile

---

## 11. Integration Proposal

### Where the pieces live in the repo:

| Content | Location | Normative? |
|---|---|---|
| Consent rule shape + matching semantics | `spec/v0.3/CONSENT-PROFILE.md` (future) | Yes |
| `um:Audience` type definition | `spec/v0.3/schema.jsonld` (future) | Yes |
| Extended consent names | `spec/v0.1/REGISTRY.md` (add now, non-normative) | No |
| Data firewall UX patterns | `integrations/data-firewall-ux.md` (new) | No |
| Updated healthcare consent examples | `integrations/healthcare-patient-consent.md` (update) | No |
| Updated smart glasses consent examples | `integrations/smart-glasses.md` (update) | No |
| Updated metaverse consent examples | `integrations/metaverse.md` (update) | No |
| Firewall visual mapping | `docs/design/CAPSULE-POD-DESIGN.md` (update) | No |
| This design document | `docs/design/PERMISSIONS-FIREWALL-DESIGN.md` | No |
| Decision record | `docs/DECISIONS.md` (append) | Procedural |
| Stub fixture: firewall-rules manifest | `examples/v0.1/stubs/` (new) | No |

### Lateral integration touchpoints:

1. **Teaching scripts** -- Add a "firewall" scene to the teaching progression: *"Your pod has a shell. That shell is your firewall. Nothing gets in or out without your permission."*
2. **Interactive sandbox** (WO-0060+) -- Add a consent-rule builder to the sandbox UI, demonstrating how rules gate facet visibility
3. **Journey proofs** -- Add a journey proving audience-scoped consent enforcement (e.g., healthcare provider accreditation check)
4. **Animated SVG** -- Produce a "data firewall" explainer SVG using the established animation pipeline
5. **Threat model** (`docs/security/THREAT-MODEL.md`) -- Add consent-bypass and audience-spoofing threats

### Immediate next steps:

1. Record the design direction in `docs/DECISIONS.md`
2. Add extended consent names to `spec/v0.1/REGISTRY.md` (non-normative, backward-compatible)
3. Create a stub fixture demonstrating audience-scoped consent rules
4. Update existing integration lanes with firewall-model examples
5. Write the UX guidance document (`integrations/data-firewall-ux.md`)

---

## Appendix A: Little Snitch Design Pattern Mapping

The design patterns from Little Snitch that directly inform this architecture:

| Little Snitch Pattern | Universal Manifest Adaptation |
|---|---|
| **Deny by default** | Absent consent = denied; explicit rules required for access |
| **Progressive disclosure** | Start with no rules; prompt on first access; accumulate rules over time |
| **Rule specificity precedence** | Field > facet > section; specific audience > any audience; deny wins ties |
| **Profiles** | Context tags (personal, professional, public, emergency) select different rule subsets |
| **Rule groups** | Domain-grouped consents (healthcare, social, professional) for bulk management |
| **Network Monitor** | Access log showing which consumers accessed which data |
| **Temporary rules** | Consent rules with `expires` for session-scoped or time-limited access |
| **Alert Mode / Silent Mode** | Learning phase (prompt for decisions) vs. steady state (rules handle everything) |

## Appendix B: Comparison with Other Permission Models

| System | Model | UM Adaptation |
|---|---|---|
| **Little Snitch** | App + destination + port + protocol rules | Consumer + data-type + context + audience rules |
| **OAuth 2.0 Scopes** | Pre-defined scope strings granted at auth time | Consent names as scope equivalents, but subject-controlled not app-requested |
| **GDPR Consent** | Purpose-limited, withdrawable, informed | Default-deny, temporal expiry, explicit per-data-type |
| **UMA (User-Managed Access)** | Resource owner controls access to APIs | Similar subject-centricity, but UM is document-level not API-level |
| **Solid WAC/ACP** | Resource-level access control on pods | Complementary: UM consents govern the manifest; Solid WAC governs the pod data the manifest points to |

## Appendix C: Example Manifest with Firewall Rules

```json
{
  "@context": "https://universalmanifest.net/spec/v0.1/schema.jsonld",
  "@id": "urn:uuid:a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "@type": "um:Manifest",
  "manifestVersion": "0.1",
  "subject": "did:key:z6MkPersonalIdentity",
  "issuedAt": "2026-03-01T00:00:00Z",
  "expiresAt": "2026-03-02T00:00:00Z",

  "consents": [
    {
      "@type": "um:Consent",
      "name": "publicDisplay",
      "value": "allowed",
      "notes": "Public profile can be shown on any display"
    },
    {
      "@type": "um:Consent",
      "name": "facet:allergyAlerts",
      "value": "allowed",
      "audience": {
        "@type": "um:Audience",
        "match": "accreditation",
        "value": "healthcare.provider"
      },
      "context": "emergency",
      "notes": "Healthcare providers can see allergies in emergencies"
    },
    {
      "@type": "um:Consent",
      "name": "facet:allergyAlerts",
      "value": "denied",
      "notes": "Default: allergy data is private"
    },
    {
      "@type": "um:Consent",
      "name": "claim:employment.role",
      "value": "allowed",
      "audience": {
        "@type": "um:Audience",
        "match": "domain",
        "value": "*.employer.example"
      },
      "context": "professional"
    },
    {
      "@type": "um:Consent",
      "name": "ar.recording.faceVisible",
      "value": "allowed",
      "audience": {
        "@type": "um:Audience",
        "match": "relationship",
        "value": "friend"
      }
    },
    {
      "@type": "um:Consent",
      "name": "ar.recording.faceVisible",
      "value": "denied",
      "notes": "Strangers cannot capture my face in smart glasses"
    },
    {
      "@type": "um:Consent",
      "name": "social.graphShare",
      "value": "denied",
      "notes": "Never share my social graph"
    }
  ],

  "facets": [
    {
      "@type": "um:Facet",
      "name": "publicProfile",
      "entity": {
        "@type": "schema:Person",
        "name": "Alex",
        "description": "Creator and builder"
      }
    },
    {
      "@type": "um:Facet",
      "name": "allergyAlerts",
      "entity": {
        "@type": "health:AllergyList",
        "allergies": ["penicillin", "shellfish"]
      }
    }
  ],

  "claims": [
    { "@type": "um:Claim", "name": "employment.role", "value": "senior-engineer" },
    { "@type": "um:Claim", "name": "verification.status", "value": "verified" }
  ],

  "pointers": [
    { "name": "solidPod.creatorCanonical", "url": "https://pod.example/alex/profile" }
  ]
}
```

In this example manifest, the consent rules form a coherent firewall:

- **Public profile**: visible to anyone (allowed, no audience restriction)
- **Allergy data**: visible only to healthcare providers in emergencies; denied by default
- **Employment role**: visible only to employer domain, in professional context
- **Face in smart glasses**: visible to friends only; denied for strangers
- **Social graph**: denied to everyone, always
