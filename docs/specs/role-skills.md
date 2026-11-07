# Spec: senior role skills (13 roles in 4 skills)

**Status:** draft
**Owner:** xingwoo (the user)
**Issue / PR:** this PR

## Goal

Give Claude Code on this machine 13 expert roles it can switch into: engineering, architecture, security and platform, quality, product and UX. Each role advises, reviews, refines backlog items, creates architecture, and writes code when asked. The roles follow the team's governance: PRs only, spec before code.

## Decisions taken in the grill

- **Location:** personal skills in `~/.claude/skills/`, available in every Claude Code session on this machine. Not in the repo, and not in NanoClaw agent containers.
- **Packaging:** 4 skills, each holding several roles. Invoking a skill loads the roles it holds, and the user names which role to act as.
- **Behavior:** each role advises, reviews, refines PBIs and stories, creates architecture, and writes code when asked. Writing code follows the governance in `orchestrator-governance` (branch, PR, reviewer pass, user merges).

## Proposed grouping

| Skill | Roles |
|---|---|
| `engineering` | senior backend engineer, senior frontend engineer, data engineer |
| `platform-security` | network engineer, infrastructure engineer, security engineer, security architect |
| `architecture` | solution architect, enterprise architect |
| `product-quality-ux` | senior product owner, senior UX designer, frontend test engineer, backend test engineer |

Open point for approval: the grouping above. Change it here if a role belongs elsewhere.

## Scope

Each role section in its skill covers:
- **Mandate:** what the role owns and what it does not.
- **Advise:** the questions it asks first and the trade-offs it names.
- **Review:** a checklist for the artifact type it reviews (code, architecture, backlog items, test plans, threat models).
- **Refine:** for product roles, how it rewrites backlog items into stories with acceptance criteria.
- **Create:** the artifacts it drafts (ADRs, architecture diagrams, threat models, test plans, UX flows, data models).
- **Write code:** only on request, inside a repo, on a feature branch, following the spec gate and PR rules.

Every skill states the governance rules once: no push to `main`, no merge by the role, specs approved by the user before code.

## Out of scope

- Writing these skills into `container/skills/` or any NanoClaw agent container.
- Changing the governance rules themselves.
- Tools or integrations the roles would need beyond what Claude Code already has.

## Acceptance criteria

- [ ] `~/.claude/skills/` contains 4 skills: `engineering`, `platform-security`, `architecture`, `product-quality-ux`, each with a `SKILL.md` that has `name` and `description` frontmatter.
- [ ] All 13 roles are present, named exactly as in the table above, and each has a Mandate, Advise, Review, and Create section.
- [ ] Product and UX roles include a Refine section with a story template that has acceptance criteria.
- [ ] Each skill's Write code section requires a feature branch, a PR, and an approved spec, and forbids pushing to `main`.
- [ ] No skill contains a secret, a personal path, or the user's email address.
- [ ] Each skill loads in a fresh Claude Code session and answers a sample request for one of its roles (checked by hand, with the result recorded in the PR).

## Risks and open questions

- **Personal skills are not in git.** `~/.claude/skills/` lives outside the repo, so this PR holds only the spec. The skill files are not reviewable in a PR, and a machine loss loses them. Mitigation: copy the final files into this repo under `docs/roles/` as a backup, in a later PR, if the user wants it.
- **Skill size.** Four large skills load a lot of text. Mitigation: each skill states which roles it covers in its description, so the right one loads.
- **Overlap:** solution architect and enterprise architect, and security engineer and security architect, can give conflicting advice. Mitigation: each skill names which role decides on which kind of question.
- **Writing code from personal skills:** the roles can edit any repo on this machine if asked. Mitigation: the Write code rule is restricted to repos the user names, and the governance still applies.

---

Approved by: (pending the owner)
