# ADR-0002: Spec approved before code for features and behavior changes

**Status:** accepted
**Date:** 2026-11-07
**Deciders:** xingwoo (the owner)
**Supersedes / superseded by:** none

## Context

Features were being built from chat requests with no agreed written scope, so acceptance was unclear and reviews had nothing to check against.

## Decision

We will write a spec in `docs/specs/` and get the owner's approval (an `Approved by:` line) before any code is written for a new feature or behavior change. Bug fixes, typos, and docs-only changes are exempt. See `docs/specs/README.md`.

## Consequences

- Scope and acceptance criteria are agreed before work starts.
- Each feature PR must link its spec, or check "Not required". The `spec-check` workflow enforces this.
- Small changes pay no spec cost.

## Alternatives considered

- **Spec in the PR description only:** rejected. Approval would happen after the code exists.
- **No spec, review after the fact:** rejected. Review then has no agreed target.
