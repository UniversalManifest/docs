# universalmanifest.net — Editorial Style Guide

This style guide defines the voice and structure for Universal Manifest standards documentation.

## Voice

- Professional, neutral, implementer-oriented
- Precise language:
  - use **MUST / SHOULD / MAY** for requirements
  - avoid hand-wavy claims
- No marketing tone; adoption happens through clarity and proof

## Document patterns

### For overview pages

- Problem statement (what fails without this)
- Core concept (portable state capsule)
- Scope boundaries (what is and is not included)
- Links to next steps (getting started, spec, conformance)

### For spec pages

- Required fields and semantics
- Extension rules (unknown-field behavior)
- Compatibility/versioning rules
- Examples + fixture links

### For conformance pages

- Checklist by role (consumer / issuer)
- Mapping: requirement → fixture(s)
- How to run tests (one command)
- Clear failure semantics

### For hosting/publishing pages

- Canonical URLs (versioned)
- Headers and caching policy
- Release process (immutability)
- Migration policy

## Chunking rules

- Keep pages short and scannable:
  - lead with “what to do” and “what it means”
  - provide deeper details on subpages
- Prefer numbered steps for implementer flows
- Every page should link to at least one runnable proof point when possible

## Terminology

- “UMID” refers to the manifest `@id`
- “Resolver” refers to the `myum.net/{UMID}` lookup behavior
- “Standards site” refers to `universalmanifest.net`

