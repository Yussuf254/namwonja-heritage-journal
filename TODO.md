# Donation Projects — Implementation Plan

## Goal
Add admin-managed donation projects (e.g. "Building the Mausoleum for Chief Mukudi") that link to M-Pesa donations and reflect on the public support site with a target amount + progress bar.

## Plan Steps
- [ ] Create `donation-projects.sql` (DB migration: table + columns + RLS + seed)
- [ ] Create `api/donation-projects.js` (public GET active projects + admin CRUD)
- [ ] Edit `api/stkpush.js` (store projectId/projectName on donation)
- [ ] Edit `support.html` (projects section + donation modal)
- [ ] Edit `js/mpesa.js` (fetch projects, render cards, modal flow, pass projectId)
- [ ] Edit `css/about-magazine.css` (project cards, progress bar, modal styling)
- [ ] Edit `admin.html` (nav item, section, project editor modal, payments header)
- [ ] Edit `js/admin.js` (project CRUD, payments project column, stats)
- [ ] Edit `css/admin.css` (project table/modal styles)
- [ ] Bump cache-busting versions (`?v=2.3`)
- [ ] Run `donation-projects.sql` in Supabase SQL Editor (manual data step)
- [ ] Redeploy serverless functions and verify end-to-end

## Previous: Admin edits reflecting on main website
- [x] `js/blog.js`: DB-first rendering
- [x] `js/stories.js`: DB-driven grids + cache-busting
- [x] `api/_lib/supabase.js`: no-store cache headers
- [x] Backfill SQL modal (admin)
- [ ] Run `backfill-story-content.sql` in Supabase SQL Editor (manual data step)
