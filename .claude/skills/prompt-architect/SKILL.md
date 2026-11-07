---
name: prompt-architect
description: Turns a rough request, idea or task description into a structured, high-quality prompt for Claude or another model. Use when the user asks to write, improve, restructure or optimize a prompt, system prompt, CLAUDE.md, agent instruction or skill, or says "give me a better prompt", "make this prompt clearer" or "prompt for".
---

# Prompt Architect

Turn a rough idea, or an existing prompt that isn't working well, into a structured, specific prompt. Follow these four steps in order.

## Step 1 — Gather what's missing

Figure out: the goal (what should the output actually accomplish), the audience (who or what reads/uses the output — a person, another model, an automated pipeline), the inputs available, the constraints (length, format, tone, things to avoid), and the likely failure modes (what would make this go wrong).

If the request is already clear on these points, skip asking and state the assumptions you're making instead. Only ask when something is genuinely ambiguous and guessing wrong would waste the user's time.

## Step 2 — Pick a structure

Match the shape to the job:

- **Single task prompt** — a one-off request with a clear input and output, no persistence needed.
- **Agent or system prompt** — defines ongoing behavior/role for an agent across a session or many invocations.
- **Skill or CLAUDE.md** — use a *skill* for a specialized procedure that should load on demand when relevant, keeping it out of the default context otherwise. Use *CLAUDE.md* for rules that must apply in every session regardless of task, with no loading step.
- **Multi-step pipeline** — a task that genuinely decomposes into ordered stages, each depending on the last.

Say which structure you picked and why in one line before writing it.

## Step 3 — Write it

- Be specific rather than vague — "under 200 words, bullet list, no jargon" beats "keep it concise."
- Explain the *reason* behind a rule where it isn't obvious, so the reader (human or model) can judge edge cases the rule didn't anticipate.
- Give at least one concrete example when the desired output shape isn't self-evident from a description alone.
- Mark inputs clearly (e.g., fenced blocks, explicit placeholders) so it's unambiguous what's data versus instruction.
- State scope boundaries explicitly — what this prompt is NOT responsible for, especially if it sits next to other prompts/agents that cover adjacent ground.
- Avoid vague intensifiers ("very," "really," "make sure to really nail") that add length without adding instruction.

## Step 4 — Check it

Before handing back the result, verify:

- Goal is stated, not just implied.
- Required inputs are named.
- Output format is explicit (length, structure, medium).
- Constraints are complete (tone, exclusions, hard limits).
- Ambiguity-handling rule exists (what to do when the input is unclear or incomplete) — don't leave the reader guessing.
- No internal contradictions (two rules that can't both be satisfied).
- Length is proportionate to the task — a one-line request doesn't need a 50-line prompt back.
- No leftover placeholders or template scaffolding that should have been filled in.

## Output format

Return the finished prompt in a single fenced code block, then list the assumptions made below it (if any were needed in Step 1).

**For an existing prompt being improved**: first state its apparent intent in one line, then list the specific failure points found against the Step 4 checklist, then give the rewritten version in a fenced block, then a short summary of what changed and why.
