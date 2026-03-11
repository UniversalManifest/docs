# Integration Lane Authoring Guide

This guide explains how to create a new Universal Manifest integration lane. It is written for both human contributors and AI agents. Following this guide should produce a complete, valid integration document with zero additional context required.

## When to Create an Integration Lane

Create a new integration lane when:

- **A new domain** needs to use Universal Manifest (e.g., healthcare, education, automotive) and no existing lane covers its data model or consent requirements.
- **A new use-case pattern** emerges within an existing domain that requires distinct facets, pointers, or consent keys not covered by existing lanes.
- **A new consent model** is needed (e.g., a domain with unique privacy regulations like HIPAA, FERPA, or GDPR-specific requirements).
- **A new platform or protocol** wants to integrate with UM and needs guidance on how to map its concepts to manifest fields.

Do **not** create a new lane if an existing lane already covers the domain and use case. Instead, consider proposing amendments to the existing lane.

## Prerequisites

Before starting, ensure you have access to:

1. The integration lane template: `integrations/TEMPLATE.md`
2. The v0.1 specification: `spec/v0.1/`
3. Example fixtures: `examples/v0.1/` (for reference)
4. The test harness: `packages/universal-manifest` (for fixture validation)

## Step-by-Step Process

### Step 1: Copy the Template

```bash
cp integrations/TEMPLATE.md integrations/{your-lane-name}.md
```

Use kebab-case for the filename (e.g., `healthcare-patient-consent.md`, `smart-home.md`, `education-credentials.md`).

### Step 2: Define the Domain and Use Cases

Fill in the **Overview** section with:

- What systems, platforms, or standards this lane targets.
- Why this domain benefits from a portable manifest model.
- What problems UM solves in this domain.

Write 3-5 **use cases** as user stories in the format: "As a {role}, I want to {action} so that {benefit}."

### Step 3: Identify Natural Facets

Facets are named data compartments within the manifest. Ask:

- What distinct categories of data does this domain need to carry?
- What would a consumer need to extract and process independently?

Each facet should have:

- A descriptive `name` (camelCase, e.g., `patientConsent`, `deviceIdentity`).
- A `@type` of `"um:Facet"` (additional domain types are optional).
- An `entity` object with domain-relevant fields.

**Naming convention:** `{domain}{DataCategory}` in camelCase. Examples: `patientConsent`, `academicCredential`, `deviceIdentity`.

### Step 4: Identify Natural Pointers

Pointers are URL references to external systems or resources. Ask:

- What external systems should a manifest reference?
- What canonical data sources exist outside the manifest?

Each pointer should have:

- A `name` using dot-notation: `{domain}.{resourceName}` (e.g., `health.record`, `edu.transcript`).
- A `url` pointing to the external resource.

**Naming convention:** `{domain}.{resourceType}` in dot-notation. Examples: `health.insuranceProvider`, `edu.transcript`, `home.firmwareUpdate`.

### Step 5: Identify Natural Consents

Consents are default-deny permission toggles. Ask:

- What actions require explicit user permission in this domain?
- What data disclosures are sensitive?
- What regulatory requirements apply?

Each consent should have:

- A `name` using dot-notation: `{domain}.{permissionAction}` (e.g., `health.shareRecords`, `edu.verifyDegree`).
- A `value` of `"allowed"` or `"denied"`.
- A default of `"denied"` -- consumers must treat missing consents as denied.

**Naming convention:** `{domain}.{verb}{Object}` in dot-notation. Examples: `health.shareAllergies`, `edu.shareTranscript`, `home.allowRemoteAccess`.

### Step 6: Identify Natural Claims

Claims are role or permission assertions. Ask:

- What roles matter in this domain? (e.g., patient, practitioner, student, device-owner)
- What statuses or attestations need to be carried? (e.g., verified, enrolled, certified)

Each claim should have:

- A `name` using dot-notation: `{domain}.{claimType}` (e.g., `health.role`, `edu.degreeStatus`).
- A `value` with the assertion content.
- An `issuer` DID identifying who made the assertion.

**Naming convention:** `{domain}.{claimCategory}` in dot-notation. Examples: `health.practitionerRole`, `edu.enrollmentStatus`, `home.deviceOwnership`.

### Step 7: Write Consumer and Issuer Behavior

**Consumer behavior** describes how a relying party should process manifests with this integration's fields. Always include:

1. Core UM validation (required fields, TTL check).
2. Integration-specific field extraction and processing.
3. Consent checks before acting on data.
4. Unknown-field tolerance.

**Issuer behavior** describes how to construct manifests. Always include:

1. Setting standard required fields with fresh values.
2. Integration-specific facet, pointer, consent, and claim construction.
3. Signature addition (optional in v0.1, expected in v0.2).

### Step 8: Create an Example Fixture

Write a complete, valid v0.1 JSON-LD manifest that demonstrates the integration in action. Requirements:

- Must include all required fields: `@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`, `facets`.
- `@context` must be `"https://universalmanifest.net/ns/universal-manifest/v0.1/schema.jsonld"`.
- `@id` must be a `urn:uuid:` with a valid UUID.
- `@type` must be `"um:Manifest"`.
- `manifestVersion` must be `"0.1"`.
- `subject` must be a DID or URI.
- `issuedAt` must be a valid ISO 8601 timestamp.
- `expiresAt` must be after `issuedAt`.
- `facets` must be an array (may be empty, but should contain domain-relevant facets for a useful example).
- Each facet must have `@type: "um:Facet"`.

Use realistic but fictional data. Do not use real people, organizations, or identifiers.

### Step 9: Validate the Fixture

Run the validation harness to confirm the fixture is structurally valid:

```bash
cd packages/universal-manifest
npm run test
```

The fixture must pass `assertUniversalManifestV01`. If it does not, fix the structure until it does.

### Step 10: Submit for Review

1. Place the integration file in `integrations/{your-lane-name}.md`.
2. Optionally create a site docs version in `site/src/content/docs/integrations/{your-lane-name}.md` with Starlight frontmatter.
3. Submit for review. Current process: create the file and it will be reviewed by hand. In the future, this may involve a pull request workflow.

## Naming Conventions Summary

| Element | Convention | Examples |
|---|---|---|
| File name | kebab-case | `healthcare-patient-consent.md`, `smart-home.md` |
| Facet name | camelCase, `{domain}{DataCategory}` | `patientConsent`, `academicCredential` |
| Pointer name | dot-notation, `{domain}.{resourceType}` | `health.record`, `edu.transcript` |
| Consent name | dot-notation, `{domain}.{verbObject}` | `health.shareRecords`, `edu.verifyDegree` |
| Claim name | dot-notation, `{domain}.{claimCategory}` | `health.role`, `edu.degreeStatus` |

## Quality Checklist

Before submitting, verify:

- [ ] **Template complete**: All template sections are filled in (no placeholder braces remain).
- [ ] **Fixture validates**: The example fixture passes `assertUniversalManifestV01`.
- [ ] **Consent defaults to deny**: All consent keys specify a default of "denied" in the table and the fixture demonstrates explicit "allowed"/"denied" values.
- [ ] **No normative language**: The document does not use "MUST", "SHALL", "REQUIRED" (RFC 2119 keywords) except when referring to core UM spec requirements. Integration guidance uses "should", "recommended", or "suggested".
- [ ] **Boundary declared**: The Normative Boundary section is present and unmodified.
- [ ] **Use cases concrete**: Each use case is a specific, actionable user story.
- [ ] **Facets well-scoped**: Each facet represents a distinct data compartment, not a dump of all fields.
- [ ] **Pointers reference external systems**: Pointers link to resources outside the manifest, not to facet contents.
- [ ] **Claims are attestations**: Claims represent verifiable assertions, not data fields (data belongs in facet entities).
- [ ] **Consumer behavior is defensive**: Consumer steps include TTL checks, consent checks, and unknown-field tolerance.
- [ ] **Issuer behavior is constructive**: Issuer steps produce a valid manifest from scratch.

## Common Mistakes

- **Putting data in claims instead of facets.** Claims are assertions ("this person has role X"). Data belongs in facet entities ("this person's name is Y").
- **Forgetting the consent default.** Every consent key must default to "denied". A missing consent means denied.
- **Using normative language.** Integration lanes are non-normative guidance. Do not write "The consumer MUST do X" -- write "The consumer should do X" or "Recommended: do X".
- **Invalid fixture structure.** Missing `@context`, wrong `@type`, `issuedAt` after `expiresAt`, or facets not in an array are common fixture errors.
- **Namespace collisions.** Use domain-specific prefixes for all pointer, consent, and claim names to avoid collisions with other lanes.
