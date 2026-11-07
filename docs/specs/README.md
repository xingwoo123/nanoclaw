# Specs

Spec-driven development: a feature or behavior change is agreed in writing before code is written.

## Agentic workflow order

This is the one place the workflow is written down. `CLAUDE.md` and the governance memory point here.

For each new feature or behavior change (the same scope as the spec rule), in this order:

1. **Grill me first.** Run the `grill-me` skill (`.claude/skills/grill-me/`) on the request or its draft document. Answer the questions, so gaps and unlabeled assumptions surface before work starts.
2. **Then prompt-architect.** Run the `prompt-architect` skill (`.claude/skills/prompt-architect/`) to turn the answered request into a structured prompt or spec draft.
3. **Then tokenizer-humanizer.** Run the `tokenizer-humanizer` skill (`.claude/skills/tokenizer-humanizer/`). Apply Part A (token economy) to the agentic work that follows, and Part B (humanized prose) to any drafted text that should read as human-written.
4. Continue with the process below: spec approval, then implementation.

Bug fixes, typos, and docs-only changes skip steps 1 to 3. They still follow Part A for token economy during agentic work.

## Enforcement

The `spec-check` workflow (`.github/workflows/spec-check.yml`) fails a PR unless its Spec section is either checked "Not required", or links a spec in `docs/specs/` that has an `Approved by: <name>, <YYYY-MM-DD>` line. The check verifies that the approval line exists. It does not verify who approved it, so the owner still reviews the spec.

## When a spec is required

- New features and behavior changes: **yes**.
- Bug fixes, typo fixes, and docs-only changes: **no**.

## Process

1. Copy `_template.md` to `docs/specs/<short-slug>.md`.
2. Fill in Goal, Scope, Out of scope, and Acceptance criteria. Keep it short. For a rough request, draft it with the `prompt-architect` skill (`.claude/skills/prompt-architect/`), then check the result against the template.
3. Open a PR containing only the spec, or put it in the feature's issue. Link it from the PR.
4. The owner approves it explicitly, by writing an approval line in the spec (`Approved by: <name>, <date>`) or in a comment on the issue. A reviewer agent passing a spec is not approval.
5. Only after approval, implement. The implementing PR links the spec and must satisfy its acceptance criteria.

## Rules

- No code for a spec-required change until its approval line exists.
- If implementation shows the spec is wrong, update the spec first and get approval again.
- Specs describe what and why. Implementation detail goes in the PR.
