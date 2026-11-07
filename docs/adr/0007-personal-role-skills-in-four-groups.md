# ADR-0007: Thirteen role skills as personal skills, in four groups

**Status:** proposed
**Date:** 2026-11-07
**Deciders:** xingwoo (the owner), pending approval
**Supersedes / superseded by:** none

## Context

The owner wants expert roles (backend, frontend, security, architecture, product, quality) available to Claude Code on this machine.

## Decision

Create four personal skills in `~/.claude/skills/`: `engineering`, `platform-security`, `architecture`, `product-quality-ux`. They hold the 13 roles. Roles advise, review, refine backlog items, create architecture, and write code on request, under the governance in ADR-0002 and ADR-0004. The detail is in `docs/specs/role-skills.md` (PR #3).

## Consequences

- The roles are available in every Claude Code session on this machine.
- The skill files live outside git, so a copy in `docs/roles/` is a separate decision.
- Roles can edit any repo they are asked to. Governance limits this to PR-based changes.

## Alternatives considered

- **One skill per role (13 skills):** rejected. A long skill list.
- **Skills in the repo:** rejected for now. Would be shared with anyone who clones the repo, which is not wanted yet.
- **Skills in NanoClaw agent containers:** rejected. Changes what the agents know, and needs more care.
