# Sport Prediction Agent (Web App MVP)

A fully usable **Next.js web app** that:
- fetches fixtures (mock by default),
- stores data in a DB (SQLite via Prisma),
- generates match probabilities + top picks (edge-ranked),
- builds a bet slip with stake suggestion.

> This is a **decision-support** tool (probabilities + edge), not a guarantee engine.

## 1) Run locally

### Prereqs
- Node.js 18+ (recommended 20)
- npm

### Setup
```bash
cp .env.example .env
npm install
npm run prisma:generate
npm run prisma:migrate
npm run dev
```

Open: http://localhost:3000

## 2) Enable real data (recommended)
This MVP ships in mock mode to work immediately.

To use real fixtures:
- Get an API-Football key
- Set `USE_MOCK_DATA=false` and `APIFOOTBALL_KEY=...` in `.env`

Odds integration:
- Add `ODDSAPI_KEY=...`
- Implement resolver in `lib/providers/oddsApi.ts` + `app/api/odds/route.ts`
  (matching events by kickoff + team names or use Odds API as primary event source)

## 3) What’s inside
- `app/` UI + API routes
- `lib/predictor.ts` baseline model (vig-removed market odds blended with simple ELO prior)
- `prisma/` DB schema
- `scripts/cron_daily.ts` fetch → odds → predict batch

## 4) Next upgrades (production)
- Use Postgres (Supabase) + Redis cache
- Add user auth + subscriptions
- Backtesting + metrics (Brier score, ROI sim)
- Better model (XGBoost + calibration)
- Injury/news ingestion + odds movement tracking
- Bookmaker code export (only if you have explicit integration permission)

## Responsible use
This app provides probabilistic analysis. Use within legal frameworks and bet responsibly.


## Deploy
See `DEPLOY.md` for Vercel + Postgres deployment.
