# ADR-0006: One local dashboard for the board and running agents

**Status:** proposed
**Date:** 2026-11-07
**Deciders:** xingwoo (the owner), pending approval
**Supersedes / superseded by:** none

## Context

The board and the running agents are in separate tools. Checking what is planned and what is running means switching between them.

## Decision

We will build one local web page on this server. It shows the GitHub Projects board (drag-to-move writes back to GitHub) and a read-only panel of NanoClaw agents and sessions. It binds to `127.0.0.1` only. The detail is in `docs/specs/dashboard.md` (PR #2).

## Consequences

- One place to see plan and activity.
- Needs a GitHub token with `project` scope, stored outside the repo.
- Stopping or configuring agents stays in the CLI.

## Alternatives considered

- **Use the NanoClaw dashboard skill for agents, board separate:** rejected. Two tools again.
- **Publish as a claude.ai artifact:** rejected. Agent data would leave the server.
