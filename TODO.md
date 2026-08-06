# Admin Dashboard Fix Plan — Status

## ✅ Completed

### 1. Rich-text editor + Preview for story content
- Replaced plain HTML `<textarea>` with a WYSIWYG toolbar + contenteditable editor (`storyContentRte`).
- Added **Preview/Edit** toggle to see rendered content before publishing.
- Editor syncs back into hidden `storyContent` textarea on save; stores HTML in `content_html`.
- CSS: `.rte-wrap`, `.rte-toolbar`, `.rte-btn`, `.rte-editor`, `.rte-preview` added.

### 2. CSV Export for all data tables
- Added **Export CSV** buttons to Stories, Comments, Messages, and Donations sections.
- Implemented client-side CSV generation + download (`exportCSV` / `initExports`).

### 3. Label estimated analytics honestly
- Added an **"estimated" badge** to the Today's Visitors KPI with a tooltip clarifying no analytics backend is connected.

### 4. Keyboard shortcuts
- `Ctrl+N` = New Story.
- `Ctrl+1..4` = jump to Dashboard/Stories/Comments/Messages.

### 5. Real backend for placeholder modules (Authors, Contributors, Users, Roles, Settings)
- Created `/api/admin-data.js` handling these against Supabase tables (with graceful fallback to empty arrays / localStorage when tables are missing).
- Added schema tables to `fix-supabase-schema.sql`: `authors`, `contributors`, `admin_users`, `admin_roles`, `site_settings`, `audit_log` + default role seeding + RLS.
- Updated `admin.js` to fetch from the API with localStorage fallback.

### 6. Fixed seed-stories.sql column/value mismatch
- Reverted the heritage-story entry to the 8-column INSERT (matching the 8-column column list).
- Added a separate `UPDATE ... SET content_html = $story$...$story$` (dollar-quoted) for the heritage-story so the editor shows real content.

## Follow-up (for the user)
- Run `fix-supabase-schema.sql` in Supabase SQL Editor (creates admin support tables).
- Run `seed-stories.sql` to seed stories + populate heritage-story content.
- Test the admin dashboard in a browser.
</content>
