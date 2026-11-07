# ADR-0003: Agentic workflow order for new requests

**Status:** accepted
**Date:** 2026-11-07
**Deciders:** xingwoo (the owner)
**Supersedes / superseded by:** none

## Context

Requests arrived as rough ideas, and the first draft often missed assumptions and gave the output the wrong shape or tone.

## Decision

For each new feature or behavior change, run in this order: `grill-me` (surface gaps by being questioned), then `prompt-architect` (structure the request), then `tokenizer-humanizer` (token economy during agentic work, humanized prose for drafted text), then the spec process (ADR-0002). Small changes skip the first three steps. See `docs/specs/README.md`.

## Consequences

- Gaps surface before any spec is written.
- Extra steps add time to features. Small changes are exempt to keep the cost down.
- The skills live in `.claude/skills/` in the repo.

## Alternatives considered

- **Spec directly from the request:** rejected. It skipped the questioning step, which is where the gaps showed up.
- **Apply the order to every change:** rejected. Typo fixes would pay a full interview.
