# Lessons learned

Format: date · task — **what happened** -> why it matters -> **rule**. Promote repeated or critical rules to CLAUDE.md (instruction) or settings/hooks (enforcement).

## 2026-09-16 · Homepage trust-badge row
1. **The "logos" were trust badges in 2 alternative design sets** (10 files = 5 messages x 2 styles) -> they can't be picked or laid out correctly without looking -> **Open the actual assets during Research.**
2. **An earlier, non-matching attempt sat uncommitted** in index.html / index.css -> building on it would mix two tasks in one commit -> **Run `git status` / `git diff` first; stash unrelated WIP with a label.**
3. **css/index.css is shared by ~65 pages** -> a "homepage" tweak can silently move every page -> **Additive, uniquely named classes only; regression-check another page.**
4. **Netlify publishes the repo root** (`/README.md` is live) **but skips dot-folders** (`/.DS_Store` -> 404) -> a root CLAUDE.md or notes file would be public -> **Internal docs live in `.claude/`.**
5. **A research subagent returned wrong Claude Code syntax** (invented permission format, wrong Playwright package) -> configs would silently fail -> **Verify subagent findings against primary docs before using them.**
6. **The in-app browser renders `file://` pages unstyled, and screenshots time out while the app window is minimized** -> misleading "before" evidence -> **Use the `site` preview server; fall back to DOM checks.**
7. **A new badge claim ("30 years") contradicted existing copy ("Over 50 years")** -> mixed claims hurt trust -> **Check new claims against existing page text.**
8. **Logo2 was a JPG with a white background among transparent PNGs** -> a white square on the grey page -> **Check the format and transparency of every asset; ask the designer for a proper export; flood-fill from the edges only as a stop-gap.**
9. **My own overflow check was wrong**: `scrollWidth === innerWidth` failed on the live site at 1366px although nothing overflowed (`innerWidth` 1366 includes the 15px Windows scrollbar; `clientWidth` was 1351) -> false alarms teach people to ignore checks -> **Compare `scrollWidth` with `clientWidth`, and prove every new check on a known-good page before trusting it.**
10. **products.html looked 6px shorter locally than live** (5425 vs 5431px) because it was measured before fonts and images finished loading -> a false regression -> **Wait for `document.fonts.ready` and every image before comparing sizes; attribute a difference by deleting the new CSS rules in the page and re-measuring.**
11. **Asking the emulator for a 681px viewport produced 681.x px** (`innerWidth` 682), so `max-width: 681px` did not match -> a breakpoint test that silently checks the wrong side -> **Test boundaries at 680 and 682 and confirm with `matchMedia()` / `visualViewport.width`.**
12. **An untested claim reached CLAUDE.md**: "Netlify URLs are case-sensitive" came from a subagent and was committed without a test, but the live site serves `/CSS/INDEX.CSS` with 200 -> a wrong rule misleads every future session -> **Test or cite every factual statement before it goes into CLAUDE.md.**
13. **The permission classifier blocked a subagent from writing "all PASS" into todo.md** because it was relaying results it had not produced -> notes are only trustworthy from whoever verified -> **The session that ran the checks writes notes and CLAUDE.md; subagents implement and commit site code.**
