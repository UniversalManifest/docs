# Canonical Home-Cluster Sitemap for Approval

**Date:** 2026-04-22  
**Status:** Approval draft  
**Purpose:** Freeze the sitemap and page-boundary decision before any more homepage rewriting.

## Non-negotiable rule

No more homepage or public-site rewriting should happen before the sitemap and copy architecture are approved.

The site should be treated as downstream implementation of this document, not the place where the sitemap is figured out.

## Global public navigation

The top-level public menu stays:

- `/` — `Home`
- `/spec/latest/` — `Latest Spec`

This should not widen.

## Home cluster

The `Home` surface is a five-page cluster:

1. `/` — `Overview`
2. `/use-cases/` — `Use Cases`
3. `/explorer/` — `Explorer`
4. `/how-it-works/` — `How It Works`
5. `/standards-fit/` — `Standards Fit`

## Role of each page

### `Overview`

Job:

- define UM in plain language
- make the fragmentation problem concrete
- route to explorer and spec

Must not become:

- a giant homepage summary
- an audience taxonomy
- a standards matrix

### `Use Cases`

Job:

- show the strongest scenario families in narrative form

### `Explorer`

Job:

- let the reader inspect one concrete lane at a time
- keep the interaction use-case-first rather than audience-first

### `How It Works`

Job:

- explain the envelope model simply
- explain pointers, TTL, policy, and what stays authoritative elsewhere

### `Standards Fit`

Job:

- explain what UM is and is not relative to adjacent standards

## Audience family

Audience pages should exist one layer down from the home cluster:

- `/audiences/metaverse/`
- `/audiences/eu-ssi/`
- `/audiences/platforms/`
- `/audiences/privacy-and-consent/`
- `/audiences/venues-and-spatial/`
- `/audiences/credential-and-personhood/`

These are secondary entry points, not top-level menu items and not homepage clutter.

## Support surfaces

These remain available but are not the primary onboarding family:

- `/docs/`
- `/about/why-um/`
- `/about/one-pager/`
- `/learning/`
- `/sandbox/`
- `/workbench/`
- `/proof/*`

## What the homepage must not do

- explain the site architecture
- reassure the reader repeatedly that the spec is easy to find
- collapse every audience into one page
- carry all standards-fit, conceptual, and scenario detail at once
- drift into internal maintainership language

## Required approval sequence

1. Approve the sitemap.
2. Approve the copy brief for each page in the home cluster.
3. Approve the first audience-page briefs.
4. Only then rewrite the homepage and related routes.

## Review surface

Browser review page:

- `/review/home-cluster-sitemap/`
