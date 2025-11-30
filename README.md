# Spotless — Booking + Real-time Chat

## What this repo contains
- `index.html` — Main site for customers (booking form, map, chat widget)
- `inbox.html` — Cleaner/admin dashboard (view bookings, chat per booking)

## Setup (Supabase)
1. In Supabase console, run the SQL in **SQL editor**:

```sql
create table if not exists bookings (
  id bigint generated always as identity primary key,
  name text,
  email text,
  service text,
  date text,
  time text,
  duration text,
  address text,
  price text,
  status text,
  created_at timestamptz default now()
);

create table if not exists messages (
  id bigint generated always as identity primary key,
  booking_id bigint references bookings(id) on delete cascade,
  sender text,
  text text,
  created_at timestamptz default now()
);
```

2. Copy your **Project URL** and **anon public** key from Supabase → Project Settings → API.
3. In both `index.html` and `inbox.html` make sure the `SUPABASE_URL` and `SUPABASE_KEY` constants are set to your values.

## Publish to GitHub Pages
1. Push this repo to GitHub.
2. In the repository → Settings → Pages, set source branch: `main` and folder: `/ (root)`.
3. Wait a minute — your site will be published at:
   `https://<your-github-username>.github.io/<repo-name>/`

## Notes
- GitHub Pages provides HTTPS (required for geolocation).
- The `anon` key is safe to include client-side; DO NOT expose your `service_role` key.
- If you want email notifications or authentication (so the inbox is private), we can add those later.
