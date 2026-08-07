 
 # Donation Project Fixes — Implementation Plan

## Goal
Fix non-persistent donation modal data (admin edits not reflecting) and the New Project CTA not opening a form.

## Root Cause
- `js/admin.js` & `admin.html` already contain full project CRUD, but the deployed snapshot (`deployed-admin.js`) predates it and browsers may serve cached `?v=2.3` scripts without the project code.
- `js/mpesa.js` only loads projects once on initial page load and embeds the full project JSON into a `data-project` attribute (fragile), so admin edits don't reflect on the public donation modal.

## Plan Steps
- [x] Bump cache-busting versions (`?v=2.3` → `?v=2.4`) in `admin.html` and `support.html`
  - [x] `admin.html`: `css/admin.css`, `js/admin.js`, `css/about-magazine.css`
  - [x] `support.html`: `js/mpesa.js`, `css/about-magazine.css`
- [x] Refactor `js/mpesa.js`:
  - [x] Store fetched projects in memory
  - [x] Use `data-project-id` attribute + lookup instead of embedding full JSON
  - [x] Refresh projects on `pageshow` and `visibilitychange` so admin edits reflect live
- [x] Update `TODO.md` checkboxes
- [x] Redeploy (`vercel --prod`) and verify end-to-end

## Manual data step
- [ ] Run `donation-projects-setup.sql` in Supabase SQL Editor (if not already done) — self-contained, includes `mpesa_transactions` table + project columns
