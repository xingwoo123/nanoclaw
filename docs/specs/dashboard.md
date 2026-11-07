# Spec: single local dashboard (kanban + running agents)

**Status:** draft
**Owner:** xingwoo (the user)
**Issue / PR:** this PR

## Goal

One local web page on this server shows the work board and the running agents together, so the user sees what is planned, what is in review, and which agents are active, without switching tools.

## Scope

- **Board panel:** columns and cards from one GitHub Projects board, read through the GitHub API. Each card shows its title, linked issue or PR, and status. Opening a card links to GitHub.
- **Board write:** the user can drag a card to another column. The change is written back to GitHub Projects. No other fields are editable.
- **Agents panel (read-only):** each NanoClaw agent group, its active sessions, and whether its container is running, with the last activity time. Read from the NanoClaw central and session databases on this server.
- **Hosting:** served on `127.0.0.1` only, on a port set in `.env`. No external hosting.
- **Refresh:** the page refreshes on a fixed interval (default 30 seconds) and shows the time of the last update.

## Out of scope

- Stopping, restarting, or configuring agents from the dashboard. Those stay in the `ncl` CLI.
- Creating, renaming, or deleting board columns or projects.
- Editing card text, labels, or assignees.
- Replacing Wekan. Wekan keeps running until the user decides to stop it (a separate decision).
- Access from other machines, or any login system beyond localhost binding.

## Acceptance criteria

- [ ] `pnpm run dashboard` (or the equivalent script) starts the page, and it answers on `127.0.0.1:<port>`.
- [ ] The board panel lists every column of the configured GitHub Projects board with its cards.
- [ ] Dragging a card to another column updates its status in GitHub Projects. A reload shows the new column, and GitHub shows the same column.
- [ ] A failed GitHub write shows an error on the card and leaves the card in its original column.
- [ ] The agents panel lists each agent group with its running containers and active sessions, matching `ncl sessions list`.
- [ ] Stopping an agent container in the NanoClaw CLI is reflected in the agents panel within one refresh interval.
- [ ] The page is not reachable from another machine on the network.
- [ ] No secret (GitHub token, API key) is rendered in the page or written to the page's HTML or logs.
- [ ] Tests cover the GitHub read and write paths and the agent-status read, with the GitHub API mocked.

## Risks and open questions

- **GitHub token scope:** the current `gh` login lacks `project` scope. The user must run `gh auth refresh -s project,read:project` before implementation.
- **Board identity:** which GitHub Projects board (owner and number) is the source of truth. Needed before implementation.
- **Stale data:** the agents panel reads the database, so it can lag by one refresh interval. Accepted for a first version.
- **Two writers:** GitHub Projects may be edited in the GitHub UI at the same time. The dashboard uses the latest state on each refresh and never caches card positions.
- **Wekan:** left running. If the dashboard covers the board, the user may stop Wekan later.

---

Approved by: (pending the owner)
