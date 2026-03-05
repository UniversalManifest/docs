# Metaverse Standards Forum Relationship — Universal Manifest

This document records Universal Manifest's relationship with the Metaverse Standards Forum (MSF), covering historical lineage, current status, and future direction.

---

## 1. MUM Lineage — How UM Originated in the MSF

Universal Manifest is explicitly descended from the **Metaverse Universal Manifest (MUM)** concept document, version 1.0. The MUM concept was created within the MSF working group repository:

- **Source document:** `Metaverse Universal Manifest (MUM) concept source document (Metaverse Standards Forum working group archive)`

The MUM concept proposed a portable manifest format for metaverse cross-world identity, asset portability, and social graph exchange. It defined the foundational idea of a single document that could carry identity references, capability claims, and consent controls between virtual worlds.

Universal Manifest took the MUM concept and broadened it into a **cross-domain standard**. The key evolution:

- **MUM** was scoped to metaverse applications: cross-world identity, avatar portability, inventory references, and social graph sharing.
- **UM** generalizes the same document shape to work across any domain boundary: social platforms, IoT/edge devices, smart glasses, spatial computing, proof of personhood, healthcare, education, supply chain, and more.

The lineage is recorded in three project source-of-truth documents:
- [`docs/PROJECT-VISION.md`](PROJECT-VISION.md) — Section "Lineage and expansion direction (2026-02-20)"
- [`docs/DECISIONS.md`](DECISIONS.md) — Decision "2026-02-20 — Directive: codify MUM lineage + metaverse/RP1/smart-glasses integration lanes"
- [`integrations/metaverse.md`](../integrations/metaverse.md) — "Lineage note (source of truth)" section

The decision record explicitly states the strategic direction: "Keep metaverse portability as a first-class integration lane while positioning Universal Manifest as a broader cross-domain standard."

---

## 2. Current Relationship — UM's Status Relative to the MSF

### Organizational status

There is **no active formal organizational relationship** between the Universal Manifest project and the Metaverse Standards Forum. The UM project is an independent open-source specification developed in its own public GitHub repository under the Apache-2.0 license.

### Technical status

Metaverse applications remain a **first-class integration lane** in the UM project. This is not a token acknowledgment -- the metaverse lane has:

- A dedicated integration document: [`integrations/metaverse.md`](../integrations/metaverse.md)
- Published site documentation at `/integrations/metaverse/`
- Suggested pointer names (`metaverse.profile`, `metaverse.avatar`, `metaverse.inventory`, `metaverse.socialGraph`, `metaverse.reputation`)
- Suggested consent keys (`metaverse.profilePublic`, `metaverse.socialGraphShare`, `metaverse.voiceCapture`, `metaverse.recording.faceVisible`)
- A cross-world profile fixture: `examples/v0.1/stubs/metaverse-crossworld-profile-manifest.jsonld`
- A rich manifest example in the AI briefing demonstrating cross-world identity with claims, consents, pointers, and shards

The metaverse integration lane follows the same architecture as all other UM integration lanes: domain-specific data lives in shards, pointers, and consent keys, while the core manifest envelope remains stable and domain-neutral.

### What the MSF is today

The Metaverse Standards Forum is a venue for standards-related cooperation between organizations building metaverse, spatial computing, and virtual world interoperability standards. It hosts working groups, facilitates discussion, and produces exploratory documents and recommendations. The MSF does not itself publish binding standards -- it coordinates between standards bodies (W3C, Khronos, IEEE, etc.) and industry participants.

---

## 3. Future Plans — Contributing UM Back to the MSF

### Current intent

There are **no active plans** to submit Universal Manifest to the MSF or contribute it back to MSF working groups.

### Conditions under which contribution would make sense

Contributing UM to the MSF would be appropriate if:

1. **The metaverse integration lane matures** to the point where there are multiple independent implementations of metaverse-specific manifest consumption (cross-world profile resolution, avatar portability, inventory exchange).

2. **MSF working groups express interest** in a standardized portable state capsule format for cross-world identity and data exchange. UM's manifest shape is directly applicable to the MSF's interoperability mission.

3. **UM achieves broader adoption** that gives the metaverse lane credibility. Contributing a specification that has proven adoption across multiple domains (not just metaverse) would be more valuable to the MSF than contributing a metaverse-only format.

4. **The MSF's process accommodates the contribution.** The MSF is a coordination body, not a standards-publishing organization. Contribution might take the form of a working group input document, a liaison relationship, or a joint work item, depending on what MSF process supports.

### What contribution would look like

If contribution is pursued, it would likely involve:

- Presenting UM's metaverse integration lane to the relevant MSF working group(s)
- Sharing the metaverse-specific fixture manifests and integration guidance as working group input
- Exploring whether UM's manifest envelope could become a recommended format for MSF interoperability use cases
- Maintaining the UM specification's independence (UM would not become an MSF-governed standard; it would be referenced or recommended by MSF work products)

### Relationship to broader standardization

The MSF relationship is one component of UM's overall standards positioning. For the full picture of UM's relationship to all standards bodies and organizations, see [`docs/STANDARDS-POSITIONING.md`](STANDARDS-POSITIONING.md).

---

## References

- [`docs/PROJECT-VISION.md`](PROJECT-VISION.md) — MUM lineage statement and strategic direction
- [`docs/DECISIONS.md`](DECISIONS.md) — MUM lineage codification decision (2026-02-20)
- [`integrations/metaverse.md`](../integrations/metaverse.md) — Metaverse integration lane with lineage note
- [`docs/STANDARDS-POSITIONING.md`](STANDARDS-POSITIONING.md) — Standards positioning (all bodies)
- [`docs/UNIVERSAL-MANIFEST-BRIEFING.md`](UNIVERSAL-MANIFEST-BRIEFING.md) — Full AI briefing including metaverse integration lane
