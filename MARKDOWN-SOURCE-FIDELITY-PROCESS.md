# Markdown Source Fidelity Process

**Date:** 2026-04-24  
**Status:** Active project rule  
**Purpose:** Prevent drift between markdown/source documents, rendered public pages, machine-readable files, and agent-facing variants.

Universal Manifest has multiple public and agent-facing surfaces. A page can exist as markdown, rendered HTML, a generated static route, a machine-readable descriptor, or an agent-facing variant. This process keeps those variants aligned.

## Core Rule

When a public content surface changes, update the canonical markdown/source and rendered/public variant together.

If a rendered page has no markdown/source counterpart, create one or document the exception in the relevant report or handoff.

## Required Source Link

Every canonical public reader page should include a bottom-page source block:

```text
Source
- Download Markdown
- View source
- Agent-readable entry
```

Use only the links that exist for that page. If an agent-readable entry does not exist, omit that link or note it in the copy/implementation brief.

## Canonical Source Mapping

Every copy brief or implementation handoff must identify:

- canonical markdown/source path
- rendered route target
- compatibility aliases
- machine-readable files that reference the page or concept
- agent-facing files that reference the page or concept
- required bottom-page source links

Recommended mapping table:

| Surface | Required value |
| --- | --- |
| Canonical markdown/source path | absolute repo path |
| Rendered route target | public route |
| Compatibility routes | routes or `none` |
| Machine-readable references | paths or `none` |
| Agent-facing references | paths or `none` |
| Source-link block required | yes/no |

## Update Workflow

Use this workflow whenever changing public copy, route labels, scenario lanes, audience labels, standards positioning, or agent-facing material.

1. Identify the canonical markdown/source document.
2. Identify the rendered page or generated route.
3. Identify machine-readable and agent-facing references.
4. Edit the markdown/source first.
5. Edit the rendered page or content model to match.
6. Update bottom-page source links.
7. Check compatibility routes and aliases.
8. Check machine-readable descriptors and agent-facing files.
9. Record any deliberate exception in a report or handoff.

## Parity Checklist

- [ ] Markdown/source copy updated.
- [ ] Rendered page or content model updated.
- [ ] Bottom-page `Download Markdown` or `View source` link present.
- [ ] Agent-readable entry checked if one exists.
- [ ] Machine-readable descriptors checked.
- [ ] Compatibility aliases checked.
- [ ] Secondary/support pages checked for drift.
- [ ] Report or handoff records any exception.

## High-Risk Drift Areas

These surfaces require special care because the same concepts appear in multiple forms:

- `Home` cluster pages:
  - `/`
  - `/use-cases/`
  - `/explorer/`
  - `/how-it-works/`
  - `/standards-fit/`
- audience pages:
  - `/audiences/*`
- secondary/support pages:
  - `/about/why-um/`
  - `/about/one-pager/`
  - `/about/standards-landscape/`
- machine-readable files:
  - `/.well-known/universal-manifest.json`
  - `/llms.txt`
  - `/agent/fixture-catalog.json`
  - `/agent/sandbox-scenarios.json`
- agent-facing pages:
  - `/for-agents/`
  - `/for-agents/external-agent-onboarding/`

## Current Approved Labels To Protect

- Global nav: `Home`, `Latest Spec`
- `/explorer/` visible label: `Scenario Explorer`
- Metaverse lane: `Metaverse Portaling and Digital-World Interoperability`
- EU lane: `EU Digital Identity and SSI`
- Credential audience: `Credential Issuers and Verifiers`
- Agent lane: `Agent-to-Agent Transactions`
- Payment lane: `Peer-to-Peer Crypto Payments`
- Privacy lane: `Privacy, Consent, and Bounded Disclosure`

## Current Copy Constraints To Protect

- Do not use standalone venue/spatial framing as an approved top-level lane or audience route.
- Ground EU digital identity / SSI claims in public standards, public specifications, architecture references, or public implementation direction.
- Keep peer-to-peer crypto payment copy abstract and provider-neutral unless a specific provider, chain, wallet, offer protocol, or payment rail is explicitly approved.
- Treat private facets, encrypted data, and attested identifier/control binding as cross-cutting material unless a later approved IA change creates a dedicated route.
- Keep private-data copy aligned with the source distinction: projection is the normative path; encrypted inline facets are optional guidance.
- Keep identity-binding copy aligned with v0.2 trust tiers: `claims[].claimProof` and `identity.crossDidBinding` provide Tier 1 attested/proof-backed support, while stronger cryptographic or multi-party binding is deferred.
- Keep `/about/why-um/`, `/about/one-pager/`, and `/about/standards-landscape/` secondary/supporting unless a future approved IA change gives one of them a distinct canonical role.

## Concept Source Packs

When public copy mentions these concepts, check the corresponding source pack before editing rendered pages or agent-facing summaries:

| Concept | Source pack |
| --- | --- |
| Metaverse portaling / IWPS | `/Users/grig/work/repo/universalmanifest/docs/research/iwps-base-specification-v0.3.md`; `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-11-iwps-um-alignment-analysis.md`; `/Users/grig/work/repo/universalmanifest/docs/handouts/oma3-2026-03-12/07-iwps-integration.md`; `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md` |
| EU digital identity / SSI | European Commission EUDI Wallet implementing regulation; EUDI ARF repository; EUDI standards and technical specifications repository; European Commission Digital Identity Q&A |
| Private facets / encrypted data | `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-01-wo-0143-private-encrypted-inline-facets-vs-projection-adr.md`; `/Users/grig/work/repo/universalmanifest/docs/explainers/facet-encryption-deep-dive.md`; `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`; `/Users/grig/work/repo/universalmanifest/examples/v0.2/encrypted-inline-facets/` |
| Claim proof / attested identifier binding | `/Users/grig/work/repo/universalmanifest/docs/VERSION-DIFFERENCES-V01-V02.md`; `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`; `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.json`; `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`; `/Users/grig/work/repo/universalmanifest/integrations/proof-of-personhood.md`; `/Users/grig/work/repo/universalmanifest/integrations/did-vc.md`; `/Users/grig/work/repo/universalmanifest/examples/v0.2/identity-binding-tier1-cross-did-binding.jsonld` |

## Recommended Implementation Pattern

For future public-site implementation, prefer one of these approaches:

1. Render public content directly from markdown/source files when the site framework allows it.
2. Store canonical copy in structured content data that is also exportable as markdown.
3. If a page must be hand-authored in a component, keep a markdown/source file beside the brief and add a parity note explaining why direct rendering was not used.

Do not make component-local prose the only source of truth for canonical public copy.
