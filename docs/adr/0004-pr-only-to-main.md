# ADR-0004: Changes land on main only through pull requests, merged by the owner

**Status:** accepted
**Date:** 2026-11-07
**Deciders:** xingwoo (the owner)
**Supersedes / superseded by:** none

## Context

Claude works with broad permissions on this machine and on GitHub. A direct push to `main` would skip review and could not be reviewed afterwards.

## Decision

Claude may read, clone, and push to feature branches. Claude must not push to `main`. Every change goes through a PR. A reviewer pass runs first, and the owner merges. Claude never merges its own PRs.

## Consequences

- Every change has a reviewable record.
- The owner is a bottleneck for merges. That cost is accepted.
- The rule is policy only. Branch protection on `main` is not yet set, so it is not enforced by GitHub.

## Alternatives considered

- **Claude merges after CI passes:** rejected. It removes the owner from the review step.
- **Direct push to `main` allowed:** rejected. No review record.
