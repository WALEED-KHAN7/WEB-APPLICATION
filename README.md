# MAJU Carpool

Karachi Campus carpool matching app for MAJU students. Built with TanStack Start (React 19 + Vite 7), Tailwind CSS v4, and Lovable Cloud (Supabase) for auth, database, and storage.

## Tech stack
- **Frontend**: React 19, TanStack Start/Router, Tailwind v4, shadcn/ui, Framer Motion
- **Backend**: Lovable Cloud (Supabase) — Postgres, Auth, Storage, RLS
- **Deploy target**: Cloudflare Workers (via `@cloudflare/vite-plugin` + Wrangler)

## Prerequisites
- Node.js 20+ and [Bun](https://bun.sh) (or npm/pnpm)
- A Supabase project (free tier works) — needed for auth & database

## Setup

```bash
# 1. Install dependencies
bun install      # or: npm install

# 2. Create your env file
cp .env.example .env
# then fill VITE_SUPABASE_URL / VITE_SUPABASE_PUBLISHABLE_KEY
# with your Supabase project values (Settings → API)

# 3. Apply database migrations
# Open your Supabase SQL editor and run every file in supabase/migrations/
# in chronological filename order.

# 4. Start the dev server
bun run dev      # http://localhost:8080 (or printed port)
```

## Build / preview

```bash
bun run build       # production build
bun run preview     # serve the production build locally
```

## Deploy
- **Cloudflare Workers**: `npx wrangler deploy` (config in `wrangler.jsonc`)
- **Lovable**: click Publish in the Lovable editor

## Project layout
```
src/
  routes/              # file-based routes (TanStack Router)
  components/          # UI + shadcn primitives
  integrations/supabase # generated Supabase client (do not edit)
  lib/                 # hooks, helpers, server functions
supabase/
  migrations/          # SQL migrations (run in order)
  config.toml          # Supabase project ref
```

## Admin access
The first admin email is `sp26bscs0066@maju.edu.pk`. Sign up with that email, then the
`user_roles` migration grants admin. Visit `/admin` to manage drivers / passengers.

## Notes
- Only `@maju.edu.pk` emails can sign up.
- Forgot-password flow at `/auth` → "Forgot password?" sends a reset link.
- No one can read existing passwords — they are one-way hashed in Supabase Auth.
