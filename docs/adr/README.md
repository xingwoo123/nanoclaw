# Architecture Decision Records (ADRs)

Every decision that shapes this project gets an ADR. An ADR records what was decided, why, and what else was considered, so the reasoning survives after the chat or the person is gone.

## What counts as a decision

An ADR is required for decisions about:
- **Architecture:** components, data stores, interfaces, module boundaries, and runtime (host, containers, providers).
- **Process:** how work is planned, reviewed, approved, merged, or released (for example, the spec gate or the workflow order).
- **Tooling and dependencies:** a new library, service, CI system, credential gateway, or board tool.
- **Scope:** what a feature does or deliberately does not do, when that choice affects more than one change.

Small, easy-to-reverse choices (naming a variable, picking a log message, a one-off script) do not need an ADR. When in doubt, write one.

## Process

1. Copy `_template.md` to `docs/adr/NNNN-<short-slug>.md`, using the next number.
2. Fill in Context, Decision, Consequences, and Alternatives considered. Keep it short.
3. Set Status to `proposed`. Open a PR with the ADR.
4. The owner approves it, by setting Status to `accepted` and adding the date and approver.
5. Later decisions that replace an ADR set the old one to `superseded` and link to the new one. Do not edit an accepted ADR's decision in place.

## Statuses

- `proposed`: drafted, not yet approved. Do not act on it.
- `accepted`: approved. This is the decision in force.
- `superseded`: replaced by a later ADR, which is linked.
- `rejected`: considered and declined. Keep it, so the same question is not reopened without new facts.

## Index

| ADR | Decision | Status |
|---|---|---|
| [0001](0001-record-decisions-as-adrs.md) | Record project decisions as ADRs | accepted |
| [0002](0002-spec-gate-before-code.md) | Spec approved before code for features and behavior changes | accepted |
| [0003](0003-workflow-order.md) | Agentic workflow order for new requests | accepted |
| [0004](0004-pr-only-to-main.md) | Changes land on main only through PRs, merged by the owner | accepted |
| [0005](0005-github-projects-as-board.md) | GitHub Projects as the kanban board | accepted |
| [0006](0006-single-local-dashboard.md) | One local dashboard for the board and running agents | proposed |
| [0007](0007-personal-role-skills-in-four-groups.md) | Thirteen role skills as personal skills, in four groups | proposed |
| [0008](0008-confirm-before-host-state-changes.md) | Owner confirms deletes and host-state changes first | accepted |
| [0009](0009-fork-as-pr-target.md) | Pull requests target the owner's fork, not upstream | accepted |
| [0010](0010-github-identity.md) | Claude uses its own GitHub identity, ShinChanWooBot | accepted |

## Relation to specs

A spec says what a feature should do. An ADR says why a structural choice was made. A feature that needs a new architectural decision gets an ADR first, then a spec that refers to it.
