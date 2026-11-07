---
name: prompt-architect
description: Turns a rough request, idea or task description into a structured, high-quality prompt for Claude or another model. Use when the user asks to write, improve, restructure or optimize a prompt, system prompt, CLAUDE.md, agent instruction or skill, or says "give me a better prompt", "make this prompt clearer" or "prompt for".
---

# Prompt Architect

Turn a vague request into a prompt that gets the right result the first time. The output is a prompt the user can paste or save, plus a short note on the choices made.

---

## Step 1: Gather what's missing

Before writing, identify the gaps. Ask only for what's needed to write a good prompt. Usually that is:

- **Goal**: what the output is for, and what "done" looks like
- **Audience or consumer**: a human reader, another model, a script
- **Inputs**: what context, files, data or examples the model will receive
- **Constraints**: length, format, tone, language, things to avoid
- **Failure modes**: what a bad result looks like, which is often the most useful thing to know

If the request is clear enough, skip questions and write the prompt. Note your assumptions at the end so the user can correct them.

---

## Step 2: Choose the structure

Pick the structure that fits the job. Don't force every prompt into the same template.

**Single task prompt** (one clear deliverable):
1. Role or context (one or two sentences, only if it changes the output)
2. The task, stated directly
3. Inputs, marked clearly
4. Output format and length
5. Constraints and things to avoid

**Agent or system prompt** (behaves across many turns):
1. Purpose and scope
2. Operating rules (what to always and never do)
3. Decision rules for ambiguous cases
4. Tool use, if any
5. Output and reporting conventions

**Skill or CLAUDE.md** (loaded automatically, reused often):
1. Frontmatter with a precise `description` that says when to trigger (skills only)
2. Short overview of what it does
3. Step-by-step procedure, with the decision points spelled out
4. Examples of good and bad output
5. A final checklist

**Multi-step pipeline** (several models or agents):
1. Shared context block, reused by each step
2. Per-step prompt with exact inputs and exact output schema
3. Handoff format between steps
4. Validation step before anything is shipped

Choosing between a skill and CLAUDE.md: a skill loads only when its description matches the task, so use one for specialised procedures. Use CLAUDE.md for rules that must govern every session, because a rule the model has to remember on every turn will be missed if it sits in a file that only loads sometimes.

---

## Step 3: Write with these principles

- **Be specific about the output.** "Return a JSON array of objects with `name` and `date` keys" beats "give me the data."
- **Say what to do, then why, when the reason changes behavior.** Explaining the reason helps the model handle cases the rules didn't anticipate.
- **Use examples for format and judgment.** One good example and one bad example usually do more than a paragraph of description.
- **Put inputs in clearly marked blocks** (XML tags or fenced sections) so they can't be confused with instructions.
- **State the scope boundary.** What is in, what is out, and what to do when unsure (usually: ask, or flag and continue).
- **Avoid vague intensifiers.** "Very thorough," "extremely important" and "make sure to always" add little. Concrete criteria work better.
- **Don't repeat yourself.** One clear rule beats the same rule stated three ways.
- **Match the target model.** Shorter, plainer prompts suit fast models. Complex, multi-constraint tasks suit the more capable ones and benefit from explicit steps.

---

## Step 4: Check before returning

- [ ] The goal and the definition of done are stated
- [ ] Every input the model needs is present or referenced
- [ ] The output format is specific enough to check automatically
- [ ] Constraints are concrete and testable
- [ ] There is a rule for ambiguous cases
- [ ] No rule contradicts another
- [ ] Length is proportional to the task; nothing is padded
- [ ] Any placeholders are marked, e.g. `[PROJECT NAME]`

---

## Output format

Return:

1. **The prompt**, in a fenced block, ready to copy
2. **Assumptions**, a short list of anything inferred that the user should confirm
3. **Optional variants**, only if the task has a real fork (e.g. a short and a detailed version)

Keep the surrounding commentary brief. The prompt is the deliverable.

---

## Improving an existing prompt

When the user supplies a prompt to improve:

1. Identify what it is trying to do, in one sentence
2. List the specific failure points: ambiguity, missing inputs, conflicting rules, unclear output, excess length
3. Rewrite, preserving the user's intent and any rules they clearly care about
4. Summarize the changes in a short list, one line each, so the user can see what moved and why
