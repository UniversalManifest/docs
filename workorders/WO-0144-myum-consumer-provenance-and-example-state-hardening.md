# WO-0144 — myum Consumer Provenance and Example-State Hardening

**Status:** IN_PROGRESS
**Created:** 2026-03-10
**Updated:** 2026-03-10
**Priority:** P0
**Owner:** Platform / Runtime UX
**Source:** Live production QA pass after WO-0124 closeout

## Objective

Remove remaining live-vs-stub ambiguity from the `myum` consumer resolver experience and make production example states representative enough to exercise the real contract surface.

## Problem Statement

Live production QA found that the main successful resolver example is served by a built-in fallback fixture in the Worker, but the consumer page presents it as a generic live resolver response and gives a plain safe-to-use verdict without calling out its demo provenance. Production also lacks public redirect and revoked demo records, so the consumer page cannot exercise all advertised response states against the live runtime.

## Scope

In scope:
- add explicit runtime provenance signaling for resolver responses
- surface provenance in the consumer resolver UI
- reduce misleading verdict language for fallback-fixture responses
- seed and verify live demo redirect/revoked records if remote KV access allows it
- add quick example entry points for available live contract states

Out of scope:
- private/authenticated resolver profiles
- write/registration APIs
- non-resolver frontend redesign work

## Acceptance Criteria

- [ ] Resolver responses distinguish built-in fallback fixture responses from KV-backed responses.
- [ ] Consumer resolver UI visibly labels response provenance and does not present fallback fixture data as ordinary authoritative live publisher data.
- [ ] Production consumer flow can exercise at least `200`, `404`, and, if seeding succeeds, `307` and `410` against live runtime.
- [ ] Browser verification completed on production resolver page after changes.
