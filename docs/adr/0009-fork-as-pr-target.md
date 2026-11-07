# ADR-0009: Pull requests target the owner's fork, not upstream

**Status:** accepted
**Date:** 2026-11-07
**Deciders:** xingwoo (the owner)
**Supersedes / superseded by:** none

## Context

The checkout has `origin` pointing at the upstream NanoClaw project and `fork` pointing at the owner's copy. Upstream contributions follow CONTRIBUTING.md, which the owner has not yet agreed to use for this work.

## Decision

PRs for this work target `xingwoo123/nanoclaw` (the fork), base `main`. Upstream PRs are a separate later decision.

## Consequences

- Work stays in the owner's copy until it is ready for upstream.
- Upstream CONTRIBUTING.md rules (one change per PR, labels, the PR template checks) are followed where they apply, but no upstream PR is opened.

## Alternatives considered

- **PRs to upstream now:** rejected for now. Not yet reviewed by the owner for upstream.
