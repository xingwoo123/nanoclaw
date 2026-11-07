# Specs

Spec-driven development: a feature or behavior change is agreed in writing before code is written.

## When a spec is required

- New features and behavior changes: **yes**.
- Bug fixes, typo fixes, and docs-only changes: **no**.

## Process

1. Copy `_template.md` to `docs/specs/<short-slug>.md`.
2. Fill in Goal, Scope, Out of scope, and Acceptance criteria. Keep it short.
3. Open a PR containing only the spec, or put it in the feature's issue. Link it from the PR.
4. The owner approves it explicitly, by writing an approval line in the spec (`Approved by: <name>, <date>`) or in a comment on the issue. A reviewer agent passing a spec is not approval.
5. Only after approval, implement. The implementing PR links the spec and must satisfy its acceptance criteria.

## Rules

- No code for a spec-required change until its approval line exists.
- If implementation shows the spec is wrong, update the spec first and get approval again.
- Specs describe what and why. Implementation detail goes in the PR.
