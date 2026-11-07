---
name: tokenizer-humanizer
description: Two jobs. Part A keeps agentic work (search, reads, edits, subagent dispatch) token-efficient. Part B makes drafted prose read as human-written. Use Part A during agentic work and Part B whenever producing prose that should read as human-written, or both.
---

# Tokenizer Humanizer

Two independent jobs. Use Part A whenever doing agentic work (search, reads, edits, subagent dispatch). Use Part B whenever producing prose that should read as human-written. Apply either or both depending on what the task needs.

## Part A — Token economy

The goal is to get the same result for fewer tokens, not to skip work.

**Estimate cost before acting.** Roughly 4 characters per token for English prose, 2-3 characters per token for code, JSON, logs, and Dutch. A 2000-line file read in full is not free — budget for it.

**Search before you read.** Grep for the symbol, string, or pattern first. Only open the specific file(s) and line range that actually matched. Don't read a whole directory to find one function.

**Read with offset and limit.** When a file is long and you only need one section, pass `offset`/`limit` instead of reading the whole thing. Re-read only the part that changed, not the whole file, when checking an edit.

**Don't re-read unchanged files.** If a file was already read earlier in the session and nothing has touched it since, use what's already in context instead of reading it again.

**Smallest unique `old_string` for edits.** Give Edit just enough surrounding context to be unambiguous — not the whole function when three lines identify the spot uniquely.

**Filter command output at the source.** Pipe through `grep`/`head`/`tail`/`wc -l` in the command itself rather than dumping thousands of lines and scanning them in context. Prefer `--quiet`/`-q` flags where they exist.

**Ask subagents for short answers.** When dispatching a subagent or sub-task, state the exact output format wanted ("one paragraph," "a table," "yes/no plus one sentence") rather than leaving it open-ended.

**Lead with the answer.** State the conclusion or result first, then supporting detail — never bury the answer at the end of a long explanation.

**Suggest `/compact` when context is stale.** If a session has accumulated a lot of now-irrelevant tool output or the conversation has drifted far from the current task, say so and suggest compacting rather than continuing to carry the dead weight forward.

## Part B — Humanizing

Goal: text that reads like it was written by a person, not generated. Keep every fact, number, and name exactly as given. Keep whatever register/tone the user asked for (formal, casual, technical).

**Remove these tells:**
- Stock openers/closers ("I hope this helps!", "Let's dive in", "In conclusion", "Great question!").
- Filler vocabulary: "delve," "leverage," "utilize," "robust," "seamless," "landscape," "realm," "furthermore," "moreover" used as connective filler rather than because they're the right word.
- Hedge stacks — piling up "might," "could," "potentially," "in some cases" all in one sentence when one qualifier would do.
- Reflexive triads — three-item lists that appear out of habit rather than because there are genuinely three things ("fast, reliable, and efficient").
- Em-dash overuse — more than one or two per paragraph is a tell; use a period, comma, or parenthetical instead.
- The "not X but Y" construction used reflexively rather than because the contrast is actually the point.
- Repetitive summary sentences that restate what was just said in slightly different words.

**Add these instead:**
- Concrete specifics — a real number, name, or detail beats a vague generality.
- Varied sentence length — short sentences next to longer ones, not a uniform rhythm.
- The sender's own voice — match how this specific person actually talks/writes if there's a sample to go on, rather than defaulting to a generic register.

## Checklist

- [ ] Searched/greped before reading whole files
- [ ] Used offset/limit on long files where only a section was needed
- [ ] Didn't re-read anything already in context
- [ ] Edit calls used the smallest unambiguous `old_string`
- [ ] Command output filtered at the source, not dumped raw
- [ ] Subagent/sub-task prompts stated the exact output format wanted
- [ ] Answer stated up front, detail after
- [ ] Suggested `/compact` if context had gone stale
- [ ] No stock openers/closers in drafted prose
- [ ] No filler vocabulary, hedge stacks, or reflexive triads
- [ ] Em-dashes used sparingly, not as a crutch
- [ ] Facts, numbers, and names unchanged from the source
- [ ] Register matches what the user asked for
