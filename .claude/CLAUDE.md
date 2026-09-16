# ACE Custom website — instructions for Claude

<!-- Keep under ~120 lines (Claude Code docs: < 200). Procedures go in .claude/skills/, history in .claude/notes/. -->

## What this is
- Static HTML/CSS marketing site for acecustom.com (custom belt buckles, medals, coins, pins, plaques...). No build step, package manager or framework.
- Netlify deploys the **repo root** from `main`; the quote form uses Netlify Forms. **A push to `main` is a production deploy.**

## Pitfalls — read before editing
- **Everything committed outside a dot-folder is public** (`https://acecustom.com/README.md` is served). Netlify skips dot-files/folders, so internal docs, notes and AI config live only in `.claude/`. Never commit secrets.
- **`css/index.css` is shared by ~65 pages** (index, products, Products/**, Projects/**, Quotes/home). Add new, uniquely named classes; never edit an existing selector to fix one page. Page-specific sheets: `css/products.css`, `quote.css`, `finishes.css`, `2d3d.css`.
- **index.html duplicates the product markup**: `.grid-container` (desktop) and `.flex-mobile-container` (<=681px). Change both or neither.
- **Match file-name case exactly in `src`/`href`.** This Netlify site happens to serve paths case-insensitively (tested 2026-09-16: `/CSS/INDEX.CSS` -> 200), but git records exact case and other hosts can be case-sensitive.
- **`images/logos/`** holds two alternative badge sets with the same 5 messages (Logo1-5 = set A, Logo6-10 = set B). Commit only files a page uses — committed files are public.

## Conventions
- CSS variables: `--red` rgb(237,28,28), `--yellow` rgb(255,187,0), `--black` #333. Font: Roboto (Google Fonts).
- Breakpoints (`max-width`): 1200, 954, 860, **681** (mobile layout switch), **535** (header stacks), 366.
- 4-space indentation; kebab-case classes; sparse section comments such as `/*TRUST BADGES (homepage)*/`.
- Images: `width` + `height` attributes with CSS `height:auto`; `alt` repeats any text inside the image; no `loading="lazy"` above the fold; `.webp` for photos.
- Non-clickable elements get no hover effect, pointer cursor or animation.

## Workflow — Research -> Plan -> Implement, closed with PDCA (`/rpi-pdca <task>`)
1. **Research:** read this file, the target files and `git status` / `git diff`; open the real assets; use the `web-researcher` agent for best practice and industry examples; verify key claims in primary docs.
2. **Plan:** plan mode is the project default. Show context, exact files and code, trade-offs, verification and rollback; wait for approval.
3. **Implement (Do):** feature branch; one focused task = one `site-implementer` subagent = one commit; minimal diff.
4. **Check:** automated checks + `visual-qa` at 1366/1070/954/768/682/680/535/375/320 and one regression page, before committing.
5. **Act / Review:** the session that ran the checks adds the lesson to `.claude/notes/lessons.md` and updates `.claude/notes/todo.md` (don't relay verified results to a subagent to write); report with evidence.

## Ground rules
- Don't guess. No example, or an ambiguous requirement -> stop and ask.
- Stay in scope: log out-of-scope issues in `todo.md` -> Backlog; don't fix them unasked.
- Never push without an explicit OK (`.claude/settings.json` asks before any `git push`).
- Simplicity first: no new dependencies, build tools or hooks without approval.

## Preview & verify
- Start the `site` preview (`.claude/launch.json`: `python -m http.server 8080`) -> http://localhost:8080/. Pages opened via `file://` in the in-app browser render unstyled.
- Quick DOM checks: `document.documentElement.scrollWidth <= document.documentElement.clientWidth` (no sideways scroll; don't compare with `innerWidth`, which includes the scrollbar on Windows); every `img.naturalWidth > 0`.
- If screenshots time out, the app window is probably minimized: fall back to DOM checks and say so.

## Self-improvement loop
- Every task ends with a lesson: what happened -> why it matters -> rule.
- A lesson that repeats or is critical gets promoted: here (instruction) or to `.claude/settings.json` permissions / a hook (enforcement).

## MCP & tools
- Used now: the Claude desktop app's built-in browser (preview + screenshots). A Netlify MCP connector is available in Claude sessions on this machine — confirm it can see the acecustom site before relying on it.
- Add later when needed (commands verified 2026-09-16):
  - Figma, once a design file exists: `claude plugin install figma@claude-plugins-official` (or `claude mcp add --scope user --transport http figma https://mcp.figma.com/mcp`), then authenticate in `/mcp`.
  - Playwright, for browser checks from a terminal session: `claude mcp add playwright npx @playwright/mcp@latest`.

## Notes
- Task board: `.claude/notes/todo.md` · Lessons: `.claude/notes/lessons.md` · Research records: `.claude/notes/research/`
