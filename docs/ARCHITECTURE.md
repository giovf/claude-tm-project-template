# <Project name> — Architecture

> Derived from `.taskmaster/docs/prd.md`. This file holds the *stable*
> architectural decisions and is loaded into every Claude session via
> CLAUDE.md. When the PRD changes, update **this** file — not `CLAUDE.md`.
> Volatile detail (full data model, phasing, open questions) stays in the PRD;
> this is the always-loaded summary.

<!-- SETUP: fill in every section during /setup, based on the approved PRD.
     Delete sections that don't apply. Keep the whole file skimmable — it costs
     context tokens in every session. -->

## What we're building
<!-- SETUP: 2-4 sentences — the product, the users, the launch scope. -->

## Repo layout
<!-- SETUP: top-level directories and what lives in each. -->

## Stack
<!-- SETUP: framework(s), language, key libraries (state, forms, data
     fetching), and the reasoning only where it's non-obvious. -->

## Backend & data
<!-- SETUP: where data lives, auth model, access-control rules, migrations
     policy. Delete if there is no backend. -->

## External services
<!-- SETUP: payments, analytics, error tracking, notifications — and the
     abstraction seams around each (interfaces/adapters), if any. -->

## Compliance & accessibility
<!-- SETUP: applicable privacy law, data residency, accessibility target,
     i18n stance. Delete if genuinely not applicable. -->

## Out of scope for v1 (do not scope-creep without re-baselining)
<!-- SETUP: the explicit not-now list from the PRD. -->
