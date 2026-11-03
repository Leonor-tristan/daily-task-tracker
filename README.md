# TaskFlow – Daily Task Tracker

A productivity dashboard built with **React + Vite + Supabase** (email/password login, per-user tasks).

## Features

- Login / Sign up (Supabase Auth) with protected pages
- Dashboard: stat cards, today's tasks, upcoming, overdue, daily progress ring, recent activity
- My Tasks: add / edit / delete, search, filter by category / priority / status, sort
- Categories: School, Personal, Work, Others
- Priority levels: Low, Medium, High
- Daily Planner: weekly board, **drag and drop** tasks between days
- Calendar: month view with a day panel
- Completed Tasks: undo or clear
- Progress Tracker: daily %, weekly report chart, streak, category breakdown
- Recurring tasks (daily / weekly) – completing one creates the next automatically
- Reminders (in-app toast + optional browser notification while the app is open)
- Dark mode

## Setup (step by step)

1. **Install Node.js** (v18 or newer) from https://nodejs.org
2. **Create a Supabase project** at https://supabase.com
3. In Supabase open **SQL Editor → New query**, paste everything from `supabase/schema.sql`, click **Run**.
   This creates the `tasks` table and the security rules (each user only sees their own tasks).
4. *(Easier testing)* In Supabase go to **Authentication → Providers → Email** and turn **off**
   "Confirm email". Otherwise you must click the link in the confirmation email before logging in.
5. Copy `.env.example` to `.env` and fill in your keys from **Project Settings → API**:
   ```
   VITE_SUPABASE_URL=https://xxxx.supabase.co
   VITE_SUPABASE_ANON_KEY=your-anon-public-key
   ```
6. In this folder run:
   ```bash
   npm install
   npm run dev
   ```
7. Open the address shown in the terminal (usually http://localhost:5173), sign up, and add your first task.

## Project structure

```
src/
  components/  Sidebar, Navbar, Layout, TaskCard, TaskForm, StatCard, ProgressRing, EmptyState
  pages/       Login, Dashboard, MyTasks, Planner, Calendar, Completed, Progress, Settings
  context/     AuthContext, TaskContext, PrefsContext, ModalContext
  hooks/       useReminders
  lib/         supabase.js
  utils/       dates.js
supabase/
  schema.sql   table + Row Level Security
```

## Deploying

`npm run build` creates a `dist/` folder you can host on Netlify or Vercel. Add the same two
`VITE_SUPABASE_*` variables in the host's environment settings. For single-page routing, add a rewrite
of all paths to `/index.html` (Netlify: a `_redirects` file containing `/* /index.html 200`).

## Install on your phone (PWA)

The app is installable. It must be hosted online with HTTPS first (localhost only works on your computer).

1. Put the project on GitHub, or use the Netlify / Vercel CLI.
2. On Vercel or Netlify, create a new project from the repo (Vite is detected automatically).
3. Add the environment variables `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` in the host's settings, then deploy.
4. In Supabase go to Authentication -> URL Configuration and set **Site URL** to your hosted address.
5. Open the hosted address on your phone:
   - **Android (Chrome):** menu (three dots) -> **Install app** / **Add to Home screen**.
   - **iPhone (Safari):** Share button -> **Add to Home Screen**.
