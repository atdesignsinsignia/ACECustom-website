---
name: rpi-pdca
description: Research -> Plan -> Implement -> Check -> Act/Review workflow for any change to the ACE Custom website. Use at the start of every website task (new section, style change, content or image update, bug fix).
argument-hint: <task description>
---

# RPI + PDCA workflow for: $ARGUMENTS

Work through the gates in order. Don't start a gate until the previous one is done.

## 1. Research (read-only)
- [ ] Read .claude/CLAUDE.md, the target files and `git status` / `git diff` (any uncommitted work?).
- [ ] Open the real assets (images, copy) the task uses.
- [ ] Find what else shares the files you will touch (e.g. `css/index.css` -> ~65 pages).
- [ ] Best practice + industry examples via the `web-researcher` agent; verify key claims in primary docs.
- [ ] List what only the user can decide and ask. No example or case? Stop and ask.

## 2. Plan (plan mode)
- [ ] Context, confirmed decisions, exact files and code, verification steps, rollback, out-of-scope list.
- [ ] Get explicit approval.
- [ ] Add the task to .claude/notes/todo.md.

## 3. Implement (Do)
- [ ] Feature branch (never `main`).
- [ ] One focused task = one `site-implementer` subagent = one commit; minimal, scoped diff.

## 4. Check
- [ ] Automated checks from the plan (numbers, not impressions).
- [ ] `visual-qa` at 1366/1070/954/768/682/681/535/375/320 plus one regression page.
- [ ] `git diff --stat` shows only planned files. Then commit (no push).

## 5. Act / Review
- [ ] Append a lesson to .claude/notes/lessons.md: what happened -> why it matters -> rule.
- [ ] Repeated or critical lesson -> promote it to CLAUDE.md (instruction) or settings/hook (enforcement).
- [ ] Update todo.md (done items + backlog of out-of-scope findings).
- [ ] Report to the user: what changed, evidence (screenshots), commits, open items.
