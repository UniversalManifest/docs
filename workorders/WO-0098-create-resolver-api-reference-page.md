# WO-0098 — Create Resolver API Reference Page on the Public Site

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Project Completeness and Vision Audit (2026-03-01), Gaps 7, 23, Recommended Action P1-9
**Tags:** [site], [docs]
**Blocks:** External adopter ability to integrate with the resolver
**Dependencies:** None
**Estimated effort:** 3-4 hours

## Objective

Consolidate resolver documentation from multiple sources into a single, authoritative "Resolver API Reference" page on the public site.

## Why this work matters

The completeness audit found that resolver documentation is split across `docs/DOMAIN-ARCHITECTURE.md`, `services/myum-resolver/CONTRACT.md`, and `site/src/content/docs/conformance/resolver.md` with no single authoritative external reference. An external adopter who wants to integrate with the resolver has to piece together information from multiple files.

## Scope

### Source files to consolidate

1. **`docs/DOMAIN-ARCHITECTURE.md`** — Domain split rationale and resolver behavior
2. **`services/myum-resolver/CONTRACT.md`** — Resolver contract details
3. **`site/src/content/docs/conformance/resolver.md`** — Resolver conformance requirements

### New site page

**`site/src/content/docs/reference/resolver-api.md`** (or similar path)

### Content to include

1. **Endpoint reference** — `GET myum.net/{UMID}` with request/response format
2. **Lookup contract** — Deterministic lookup rules
3. **Error semantics** — Error codes and responses
4. **Health endpoint** — `GET myum.net/health`
5. **Caching behavior** — Cache headers, TTL interaction
6. **Domain architecture** — Why spec hosting and runtime resolution are separate
7. **Rate limiting** — If applicable
8. **Examples** — curl examples for common operations

### Sidebar integration

Add to the site navigation, potentially under a new "Reference" section or under "Conformance."

## Acceptance criteria

- [ ] Single API reference page exists on the public site.
- [ ] All resolver endpoints are documented with request/response formats.
- [ ] Error codes are listed with explanations.
- [ ] At least 3 curl examples are included.
- [ ] Page is linked from the conformance resolver page and the getting started section.
- [ ] `cd site && npm run build:clean` succeeds.

## Validation commands

- `cd site && npm run build:clean`
- Manual review of API reference completeness.
