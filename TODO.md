# Admin edits reflecting on main website — Fix Plan Status

## ✅ Analyzed
Root cause: Public story pages are static `.html` files with hardcoded content. `js/blog.js` only replaces the article body from the DB when `content_html` is non-empty, so old stories whose DB rows lack `content_html` keep showing stale static text — admin edits don't appear.

## Completed
- [x] `js/blog.js`: Make rendering DB-first — always render title/excerpt/date/author/image from DB, and always replace the article body from `content_html` (or show a clear "no content" state) so stale hardcoded text is never shown.
- [x] `js/blog.js`: Added fallbacks for the profile pages (different hero markup) — updates the first H1, meta description, and the hero/figure `<img>` + og:image when the standard `storyTitle`/`storyFigureImg` ids are absent.
- [x] `js/stories.js`: Keep grids fully DB-driven and only fall back to static cards on a genuine API failure (not masking DB edits). Added cache-busting to `/api/stories` so grids never show stale DB content.
- [x] `api/_lib/supabase.js`: Added `Cache-Control: no-store` + `Pragma: no-cache` + `Expires: 0` to all API responses so Vercel doesn't serve stale cached stories after admin edits.

## Prerequisite (data) — READY TO PASTE
- [x] Created **`backfill-story-content.sql`** — a clean, paste-ready SQL file using dollar-quoting that backfills `content_html` for all 12 stories.
- [ ] Open Supabase → SQL Editor → paste the **entire** contents of `backfill-story-content.sql` → Run.

## Follow-up
- [ ] Deploy and hard-refresh public pages.
- [ ] Verify an admin edit to an old story now reflects its body on the main site.
