# Task board

## In progress
### 2026-09-16 · Homepage trust-badge row (branch `feature/homepage-trust-badges`)
- [x] Research: local files, uncommitted WIP, assets (10 badges = 2 design sets), live site, Netlify publishing, web best practice, 8 competitor homepages
- [x] Plan approved: Logo4 -> Logo1 -> Logo2 -> Logo3; stash WIP; transparent Logo2.png; phones 2x2 at 120px; keep "Over 50 years" text and flag it
- [x] T0: WIP stashed (`git stash list`) + feature branch created
- [ ] T1: `.claude/` project setup -> commit 1
- [ ] T2: Logo2.png + badge row (index.html, css/index.css) -> commit 2
- [ ] Check: breakpoints + regression page
- [ ] Review: lessons + report

## Backlog — found out of scope (not changed)
- [ ] "Over 50 years of Experience" (index.html, next-project section, >1200px) contradicts the "30 years since 1996" badge — owner to decide.
- [ ] `ACE-WEBSITE-APR18.pdf` (4.1 MB) is publicly downloadable at acecustom.com.
- [ ] `.DS_Store` is tracked in git; the repo has no `.gitignore`.
- [ ] Badge art contrast: white on #ED1C1C = 4.39:1 (< 4.5:1 AA for small text) — designer.
- [ ] "30 Years – Since 1996" goes out of date in 2027 — designer: evergreen "Since 1996" version.
- [ ] Ask the designer for a transparent PNG/SVG export of Logo2 (overwrite images/logos/Logo2.png).
- [ ] Stashed WIP `brand-logo-strip` (Disney/Dole/Exxon/4H): decide whether to drop or revisit.

## Ideas (need approval)
- Rebuild the badges as HTML text + SVG icons (WCAG 1.4.5, sharper, editable).
- Repeat "1-week delivery" / "as few as 25" next to QUOTE buttons and on product pages.
- Measure impact with a GTM event on quote clicks (before/after).
