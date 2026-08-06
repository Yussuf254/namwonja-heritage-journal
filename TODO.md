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

## Admin dashboard: Backfill SQL modal
- [x] Added a "View Backfill SQL" button (Stories section) that opens a modal and loads `backfill-story-content.sql`.
- [x] Added a "Copy SQL" button to copy the full script to the clipboard, with a graceful fallback if the file can't be fetched.
- [x] CSS: `.admin-sql-block` dark monospace code block in `css/admin.css`.
- [x] JS: `initBackfillSql()` wired into `js/admin.js` so the button/modal work.

## Deployed
- [x] Committed changes, pushed to GitHub (`main`, 6ba44fc).
- [x] Deployed to Vercel production: https://namwonja-heritage-journal.vercel.app

## Follow-up (manual data step still required)
- [ ] Run `backfill-story-content.sql` (or `migrate-story-content.sql`) in **Supabase → SQL Editor** so all 12 stories have `content_html` populated. Without this, existing rows have no body content to render.
- [ ] Hard-refresh (Ctrl+Shift+R) the public pages to clear cached static HTML.
- [ ] Verify an admin edit to an old story now reflects its body on the main site.
