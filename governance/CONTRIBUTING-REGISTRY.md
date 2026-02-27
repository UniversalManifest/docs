# Contributing to the Universal Manifest Registry

> **Note**: The registry system is planned for future implementation. This document defines the contribution process in preparation for registry launch.

This guide explains how external contributors can propose registry entries for Universal Manifest, including capability definitions, protocol extensions, and other registry-based extensions.

## What is the Registry?

The Universal Manifest registry will be a collection of standardized definitions that extend the core specification:

- **Capability Types**: Standard capability definitions (e.g., `"image-generation"`, `"text-analysis"`)
- **Protocol Extensions**: Additional interaction patterns beyond core spec
- **Integration Patterns**: Canonical integration templates
- **Schema Extensions**: Optional field definitions for specific use cases

Registry entries are **semi-normative**: they provide standard definitions that implementations can adopt for interoperability, but they are not required by the core specification.

## Before Contributing

1. **Check existing registry**: Once launched, review the registry to avoid duplicates
2. **Open a discussion**: Create a GitHub Discussion to gather feedback before formal submission
3. **Validate use case**: Ensure your registry entry solves a real adoption need
4. **Review guidelines**: Follow the contribution guidelines in [CONTRIBUTING.md](../../CONTRIBUTING.md)

## Registry Entry Requirements

All registry contributions must include:

### 1. Definition Document

A markdown file with:

- **Name**: Unique identifier (kebab-case)
- **Category**: capability-type | protocol-extension | integration-pattern | schema-extension
- **Purpose**: One-paragraph description
- **Specification**: Detailed definition with examples
- **Validation Rules**: How to validate conformance
- **References**: Links to related standards or prior art

### 2. JSON Schema (if applicable)

For schema extensions, provide:

- JSON Schema definition
- Valid examples
- Invalid examples with explanations

### 3. Conformance Tests

For capability types and protocol extensions:

- Valid usage fixture
- Invalid usage fixture
- Edge case coverage

### 4. Implementation Proof

At least one of:

- Working reference implementation
- Integration guide showing real-world usage
- Link to production deployment using the registry entry

## Submission Process

### Step 1: Fork and Branch

```bash
git clone https://github.com/WebOfTrustInfo/universal-manifest.git
cd universal-manifest
git checkout -b registry/your-entry-name
```

### Step 2: Create Registry Entry

When the registry launches, you will add your entry to the appropriate category:

```
docs/registry/
├── capability-types/
│   └── your-capability.md
├── protocol-extensions/
│   └── your-extension.md
├── integration-patterns/
│   └── your-pattern.md
└── schema-extensions/
    └── your-extension.md
```

### Step 3: Add Tests and Examples

Add conformance fixtures:

```
packages/universal-manifest/tests/fixtures/registry/
└── your-entry-name/
    ├── valid/
    │   └── example-1.json
    └── invalid/
        └── example-1.json
```

### Step 4: Update Registry Index

When the registry launches, add your entry to the registry index:

```markdown
### [Your Entry Name](./category/your-entry.md)

**Category**: capability-type
**Status**: Proposed
**Author**: Your Name

Brief description of the registry entry.
```

### Step 5: Submit Pull Request

```bash
git add .
git commit -m "registry: add [your-entry-name]"
git push origin registry/your-entry-name
```

Open a pull request with:

- **Title**: `registry: add [your-entry-name]`
- **Description**: Summary, motivation, and implementation proof
- **Checklist**: Complete the PR template checklist

## Review Process

1. **Community Review** (7 days minimum)
   - Open discussion and feedback
   - Address questions and concerns
   - Update proposal based on feedback

2. **Maintainer Review**
   - Technical review of definition
   - Validation of conformance tests
   - Assessment of implementation proof

3. **TSC Decision** (for significant extensions)
   - Final approval or rejection
   - Integration plan if approved

4. **Merge and Publish**
   - Entry added to registry
   - Documentation updated
   - Announced in release notes

## Registry Entry Status

- **Proposed**: Under review, not yet approved
- **Accepted**: Approved and available for use
- **Stable**: Widely adopted, unlikely to change
- **Deprecated**: Superseded, marked for removal

## Naming Conventions

### Capability Types

Use descriptive, action-oriented names:

- `"image-generation"`
- `"sentiment-analysis"`
- `"real-time-translation"`

### Protocol Extensions

Use clear protocol naming:

- `"request-response"`
- `"streaming-updates"`
- `"bidirectional-sync"`

### Schema Extensions

Use qualified field names to avoid conflicts:

- `"x-vendor-specific-field"`
- `"ext-custom-namespace"`

## Best Practices

### 1. Start Small

Begin with a minimal viable registry entry. You can always expand later.

### 2. Provide Real Examples

Include working examples from real integrations, not hypothetical use cases.

### 3. Document Tradeoffs

Explain design decisions and alternatives considered.

### 4. Test Thoroughly

Ensure conformance tests cover edge cases and failure modes.

### 5. Maintain Compatibility

Avoid changes that break existing adopters of your registry entry.

## Examples

### Minimal Capability Type Entry

```markdown
# Capability: Text Summarization

**Name**: `text-summarization`
**Category**: capability-type
**Status**: Proposed
**Author**: Jane Developer

## Purpose

Defines a standard capability type for text summarization services.

## Specification

Agents declaring `"text-summarization"` capability can:

- Accept text input of arbitrary length
- Return concise summaries
- Preserve key information and intent

## Usage Example

\`\`\`json
{
  "@context": "https://universalmanifest.net/v0.2",
  "@type": "Manifest",
  "@id": "urn:uuid:...",
  "capabilities": ["text-summarization"],
  "input": {
    "accepts": ["text/plain", "text/markdown"]
  },
  "output": {
    "produces": ["text/plain"]
  }
}
\`\`\`

## Validation

Valid implementations MUST:
- Support minimum 1000 character input
- Return output shorter than input
- Preserve semantic meaning

## References

- Related: `text-analysis` capability
```

## Contact

Questions about registry contributions?

- **GitHub Discussions**: [Universal Manifest Discussions](https://github.com/WebOfTrustInfo/universal-manifest/discussions)
- **Email**: registry@universalmanifest.net
- **Issue Tracker**: [Registry Issues](https://github.com/WebOfTrustInfo/universal-manifest/issues?q=label%3Aregistry)

---

Thank you for contributing to Universal Manifest's ecosystem!
