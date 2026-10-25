# CalGrid AI

**AI-powered data analytics for small businesses.**
Upload a spreadsheet and get plain-English insights, trends, forecasts, and a report you can share, no analyst required.

🔗 **Live:** [calgridai.com](https://calgridai.com)
👤 **Built by:** Mohammed Bello Ibrahim, sole founder and developer (Dec 2025 to present)

> The production codebase is private. This repo documents the product, architecture, and engineering decisions.

---

## The Problem

Small businesses sit on sales sheets, inventory logs, and customer data but can't afford a data analyst. Generic BI tools are too complex; generic chatbots don't understand their numbers.

## The Solution

CalGrid AI ingests a business's own data, detects what each column means, runs the analysis, and explains the results in language an owner can act on.

![CalGrid AI landing page](screenshots/landing.png)

<!-- Next: add screenshots/onboarding.png and screenshots/report.png -->

---

## Features

| Feature | Details |
|---|---|
| Guided onboarding | 4 quick questions (industry, goal, decision) so the report is written for that business |
| Automatic data cleaning | Fixes numbers stored as text, drops unusable columns, scores data quality |
| Local-first processing | Files are parsed and profiled in the browser; raw data never leaves the user's device |
| AI insights | Plain-English findings generated with the Claude API |
| Multi-file analysis | Analyze several datasets together (Premium) |
| Google Sheets import | Connect a sheet directly, no export needed |
| Forecast cards | Forward-looking trend projections |
| Industry presets | One-click context for common business types |
| Shareable reports | Public report links for partners or investors |
| Email summaries | Automated insight digests |
| Insight feedback | Users rate insights to improve quality |

## Architecture

```
User ──► Next.js 16 / React 19 app (Vercel)
           ├── Auth: Clerk (email + Google OAuth)
           ├── Data: Supabase (Postgres)
           ├── Analysis engine: column typing → measure detection → trends/forecasts
           ├── LLM layer: Claude API for narrative insights
           ├── Billing: Stripe (Single / Pro / Premium)
           ├── Email: Resend
           └── Charts & exports: Chart.js, jsPDF
```

## Engineering Highlights

- **Shipped solo to production:** auth, payments, data pipeline, LLM layer, and deployment owned end to end
- **Auth migration:** moved to Clerk production auth with Google OAuth
- **Privacy by design:** parsing, cleaning, and profiling run client-side, so raw business data isn't uploaded
- **Secrets hygiene:** all API keys kept out of source control, with a placeholder-only `.env.example`
- **Tiered monetization:** three Stripe plans with feature gating per tier
- **Security audit (Oct 2026):** reviewed authentication, authorization, secret handling, and API exposure
- **Data quality problem solving:** found that survey ranking columns named like "price" were being misread as money values; redesigning measure detection and trend logic to fix it

## Roadmap

- [ ] Smarter measure detection for survey and ranking data
- [ ] Per-session chat history
- [ ] PDF ingestion for businesses without spreadsheets
- [ ] White-label PDF reports for agencies
- [ ] Progressive Web App

## Validation

Early user testing with a local small business owner in Peterborough, Ontario shaped the onboarding and insight format.

---

📫 [LinkedIn](https://www.linkedin.com/in/mohammed-bello-ibrahim-7521b62a2/) · [Portfolio](https://mohammed-bello-ibrahim.vercel.app)
