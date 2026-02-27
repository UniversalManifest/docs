# RFC Template

Use this template when proposing specification changes. Submit as a GitHub Issue with the `rfc` label.

---

## RFC: [Concise Title]

**RFC Number**: [Assigned by maintainers]
**Author(s)**: [Your Name / GitHub handle]
**Status**: DRAFT | REVIEW | ACCEPTED | REJECTED | WITHDRAWN
**Created**: YYYY-MM-DD
**Updated**: YYYY-MM-DD

## Summary

One paragraph summary of the proposed change.

## Motivation

What problem does this solve? Why should we make this change?

Include:
- User pain points or adoption blockers
- Interoperability issues
- Inconsistencies or ambiguities in current spec
- Real-world use cases that aren't well-supported

## Current Behavior

Describe how the specification currently handles this area (if applicable).

## Proposed Change

Detailed description of the proposed specification change.

Include:
- New or modified schema fields
- Semantic changes to existing behavior
- Validation rules
- Examples of valid and invalid usage

### Specification Updates

List specific sections of the specification that would change:

- `spec/v0.X.md` - Section Y: [describe change]
- `schemas/manifest.schema.json` - [describe schema change]

## Examples

### Valid Example

```json
{
  "@context": "https://universalmanifest.net/v0.2",
  "@type": "Manifest",
  "@id": "urn:uuid:550e8400-e29b-41d4-a716-446655440000",
  "example-field": "example-value"
}
```

### Invalid Example

```json
{
  "@context": "https://universalmanifest.net/v0.2",
  "@type": "Manifest",
  "invalid-usage": "explanation of why this is invalid"
}
```

## Impact Analysis

### Breaking Changes

Is this a breaking change? If yes, describe:
- What existing implementations would break
- Migration path for adopters
- Deprecation timeline (if applicable)

### Backward Compatibility

How does this affect:
- Existing v0.X manifests?
- Consumers parsing older versions?
- Producers generating current version?

### Interoperability

How does this affect:
- Cross-platform adoption?
- Integration with adjacent standards?
- Registry-based extensions?

## Implementation

### Reference Implementation

Link to prototype or reference implementation (if available):

- Repository: [URL]
- Branch: [branch-name]
- Status: [proof-of-concept / production-ready]

### Conformance Tests

What new conformance tests are needed?

- Valid fixture: [description]
- Invalid fixture: [description]
- Edge cases: [description]

### Documentation Updates

What documentation needs to change?

- Integration guides
- Migration guides
- API reference
- Examples

## Alternatives Considered

What other approaches were considered? Why was this approach chosen?

1. **Alternative 1**: [description] — Rejected because [reason]
2. **Alternative 2**: [description] — Rejected because [reason]

## Open Questions

List unresolved questions or areas needing further discussion:

1. [Question 1]
2. [Question 2]

## References

Link to related issues, discussions, or external standards:

- Issue #123: [related issue]
- Discussion: [link]
- Related RFC: [RFC-XXX]
- External standard: [URL]

## Feedback Period

Minimum 7-day community review period required before TSC decision.

**Review Deadline**: [YYYY-MM-DD]

---

## Decision Log

**TSC Decision**: [Date] — [APPROVED / REJECTED / DEFERRED]

**Rationale**: [Brief explanation of decision]

**Implementation Tracking**: Issue #[number]
