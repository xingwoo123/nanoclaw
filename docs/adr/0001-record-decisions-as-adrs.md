# ADR-0001: Record project decisions as ADRs

**Status:** accepted
**Date:** 2026-11-07
**Deciders:** xingwoo (the owner)
**Supersedes / superseded by:** none

## Context

Decisions on this project are made in chat, in grill sessions, in specs, and in PR threads. Without a record, the reasons behind a structure or a process rule are lost, and the same question gets reopened later.

## Decision

We will record every decision about architecture, process, tooling and dependencies, and scope as an ADR in `docs/adr/`, following `docs/adr/README.md` and `docs/adr/_template.md`. Small, easy-to-reverse choices are exempt.

## Consequences

- Decisions have a findable home and a clear status.
- Each new decision costs a short document and a PR. That cost is accepted.
- `CLAUDE.md`, the spec process, and the governance memory point to this rule, so the rule applies to agents too.
- The rule is not enforced by CI yet. The reviewer checks for an ADR when a PR contains a decision.

## Alternatives considered

- **Decisions only in specs:** rejected. Specs cover features, not structure, and decisions outside a feature would have no home.
- **Decisions only in PR descriptions:** rejected. PR text is hard to find once merged and cannot be superseded cleanly.
- **An ADR only for big decisions:** rejected for now. The owner asked for every decision, and the threshold is written into `docs/adr/README.md` so it can be narrowed later.
