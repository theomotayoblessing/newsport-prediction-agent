# Deploy as a Direct Website (No Docker)

This turns the app into a **live website** using:
- Vercel (hosting)
- Supabase or Neon (Postgres DB)

## A) Create a Postgres database (Supabase recommended)
1) Create a Supabase project
2) Get the **DATABASE_URL** connection string (use the "Connection string" / "URI")
3) Ensure SSL is enabled (Supabase typically requires sslmode=require)

## B) Create The Odds API key (live odds)
1) Create an account at the-odds-api.com
2) Copy your API key

## C) Deploy on Vercel
1) Create a GitHub repo and push this project
2) On vercel.com → New Project → Import repo
3) Add Environment Variables:
   - DATABASE_URL = your Postgres URL
   - USE_MOCK_DATA = false
   - ODDSAPI_KEY = your key
   (Optional: APIFOOTBALL_KEY)
4) Deploy

## D) Run DB migration (IMPORTANT)
After first deploy, run Prisma migration once.

Best way (Vercel):
- Install Vercel CLI locally:
  npm i -g vercel
- Pull env:
  vercel env pull .env.production.local
- Run:
  npx prisma migrate deploy

## E) Daily refresh (optional)
This repo includes Vercel Cron:
- /api/cron/daily runs at 07:00 UTC daily (see vercel.json)

## Notes
- SQLite is not suitable for serverless hosting. Postgres is required for a stable website.
