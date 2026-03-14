# WO-0101 — Add Changelog and Release Notes Page to the Public Site

**Status:** COMPLETED
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Project Completeness and Vision Audit (2026-03-01), Gap 29, Recommended Action P1-14
**Tags:** [site]
**Blocks:** External adopter confidence (need to track changes)
**Dependencies:** None
**Estimated effort:** 2-4 hours

## Objective

Add a changelog or release notes page to the public `universalmanifest.net` site that allows external adopters to track what has changed between versions.

## Why this work matters

The completeness audit identified that there is no changelog or release notes page on the public site. External adopters need to track changes to the specification, conformance fixtures, and tooling. Without a public changelog, adopters must browse git history or commit messages to understand what has changed.

## Scope

### New site page

**`site/src/content/docs/publishing/changelog.md`** (or `about/changelog.md`)

### Content structure

1. **Version-based entries** — organized by spec version and date
2. **Categories per entry** — Spec changes, fixture changes, tooling changes, site changes
3. **Breaking changes** highlighted prominently
4. **Links to relevant documents** — spec versions, migration guides

### Source content

- Git commit history
- `docs/RELEASING.md` — release process documentation
- `docs/PUBLISHING-AND-VERSIONING.md` — versioning policy

### Maintenance plan

Document how the changelog is maintained (manual entry at release time, or automated from git tags).

## Acceptance criteria

- [ ] Changelog page exists on the public site.
- [ ] At least the current spec versions (v0.1, v0.2) have entries.
- [ ] Breaking changes are visually distinguished.
- [ ] The page is linked from the Publishing section of the site navigation.
- [ ] A maintenance process for updating the changelog is documented.
- [ ] `cd site && npm run build:clean` succeeds.

## Validation commands

- `cd site && npm run build:clean`
- Manual review of changelog content.
