# ADR-0005: GitHub Projects as the kanban board

**Status:** accepted
**Date:** 2026-11-07
**Deciders:** xingwoo (the owner)
**Supersedes / superseded by:** none

## Context

Work spans several projects and needs one board. The team's work already lives in GitHub issues and PRs. A separate board tool would need its own login and its own links to PRs.

## Decision

We use GitHub Projects as the single kanban board, linked to issues and PRs, covering all projects. The board is not created yet. Creating it needs the `project` scope on the `gh` login.

## Consequences

- Cards and PRs link without extra work.
- The board depends on GitHub. It is not available offline.
- The existing local Wekan instance is not the source of truth. Whether to stop it is a separate decision.

## Alternatives considered

- **Wekan (local, already running):** rejected as the source of truth. It has no link to PRs and its look was a problem.
- **Notion database:** rejected. It would split work between Notion and GitHub.
- **Markdown files in a repo:** rejected. No drag-and-drop and no PR links.
