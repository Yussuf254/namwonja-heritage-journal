# Dashboard Fix — Story Performance & Quick Action Cards + Dashboard Icon

## Plan Steps
- [ ] Fix Dashboard module icon (`bi-gauge-high` doesn't exist in Bootstrap Icons 1.11.3 → use `bi-speedometer2`)
- [ ] Restructure Story Performance widget markup in `admin.html` (table → rich list container)
- [ ] Restructure Quick Actions widget markup in `admin.html` (stacked buttons → rich action rows)
- [ ] Rewrite `renderStoryPerformance()` in `js/admin.js` to render rich rows (rank + thumb + title + bar + views)
- [ ] Add new CSS for `.story-perf` and `.admin-quick` widgets in `css/admin.css`
- [ ] Bump cache-busting versions (`css/admin.css?v=2.2`, `js/admin.js?v=2.2`)
- [ ] Verify in browser

## Previous: Admin edits reflecting on main website — Fix Plan Status
- [x] `js/blog.js`: DB-first rendering
- [x] `js/stories.js`: DB-driven grids + cache-busting
- [x] `api/_lib/supabase.js`: no-store cache headers
- [x] Backfill SQL modal (admin)
- [ ] Run `backfill-story-content.sql` in Supabase SQL Editor (manual data step)

