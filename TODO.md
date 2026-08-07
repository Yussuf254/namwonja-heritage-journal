# Donation Projects — Implementation Plan

## Goal
Add admin-managed donation projects (e.g. "Building the Mausoleum for Chief Mukudi") that link to M-Pesa donations and reflect on the public support site with a target amount + progress bar.

## Plan Steps
- [x] Create `donation-projects.sql` (DB migration: table + columns + RLS + seed)
- [x] Create `api/donation-projects.js` (public GET active projects + admin CRUD)
- [x] Edit `api/stkpush.js` (store projectId/projectName on donation)
- [x] Edit `support.html` (projects section + donation modal)
- [x] Edit `js/mpesa.js` (fetch projects, render cards, modal flow, pass projectId)
- [x] Edit `css/about-magazine.css` (project cards, progress bar, modal styling)
- [x] Edit `admin.html` (nav item, section, project editor modal, payments header)
- [x] Edit `js/admin.js` (project CRUD, payments project column, stats)
- [x] Edit `css/admin.css` (project table/modal styles)
- [x] Bump cache-busting versions (`?v=2.3`)
- [ ] Run `donation-projects.sql` in Supabase SQL Editor (manual data step)
- [x] Redeploy serverless functions and verify end-to-end

## Previous: Admin edits reflecting on main website
- [x] `js/blog.js`: DB-first rendering
- [x] `js/stories.js`: DB-driven grids + cache-busting
- [x] `api/_lib/supabase.js`: no-store cache headers
- [x] Backfill SQL modal (admin)
- [ ] Run `backfill-story-content.sql` in Supabase SQL Editor (manual data step)
