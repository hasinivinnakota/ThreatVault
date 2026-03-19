# ThreatVault AI — Workspace

## Overview

ThreatVault AI is a premium phishing detection app built as a CEH Module 19 portfolio demo. It uses a rule-based mock ML engine to analyze email text, URLs, and image uploads for phishing indicators.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **Frontend**: React + Vite + Tailwind CSS + shadcn/ui + Framer Motion + Recharts
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)

## Structure

```text
artifacts-monorepo/
├── artifacts/
│   ├── api-server/         # Express API server
│   │   └── src/
│   │       ├── lib/
│   │       │   ├── phishing-analyzer.ts  # Rule-based ML analysis engine
│   │       │   └── rate-limiter.ts       # DB-backed rate limiter (5/min)
│   │       └── routes/
│   │           ├── analysis.ts           # /analyze, /scans, /stats routes
│   │           └── health.ts             # /healthz
│   └── threatvault/        # React + Vite frontend
│       └── src/
│           ├── pages/
│           │   ├── home.tsx      # Landing + triple input cards
│           │   ├── results.tsx   # Results dashboard + radar chart
│           │   ├── auth.tsx      # Login/signup
│           │   └── dashboard.tsx # Scan history analytics
│           └── components/
│               ├── layout.tsx    # Nav + footer
│               └── ui/           # shadcn components + radar chart
├── lib/
│   ├── api-spec/           # OpenAPI spec + Orval codegen config
│   ├── api-client-react/   # Generated React Query hooks
│   ├── api-zod/            # Generated Zod schemas from OpenAPI
│   └── db/
│       └── src/schema/
│           └── scans.ts    # scans + rate_limits tables
└── scripts/
```

## Features

- **Landing Page**: Hero with 12K+ threats badge, triple input (email/URL/image), sample phishing emails, analyze CTA
- **Results Dashboard**: 4 metric cards, interactive radar chart, verdict badge, threat indicators, scan history table, PDF export
- **Auth**: Email/password form with guest option
- **User Dashboard**: Scan history with analytics
- **Dark Neon Theme**: #0a0a0a bg, #00ff88 green + #ff0080 pink accents, glassmorphism cards
- **Animations**: Framer Motion page transitions, animated counters, card hover glows
- **PWA**: manifest.json + theme-color for installability
- **Rate Limiting**: 5 scans per minute per IP
- **Keyboard Shortcuts**: Ctrl+Enter (analyze), Escape (clear), Ctrl+D (dark mode)

## API Endpoints

- `POST /api/analyze` — Analyze email text, URL, image for phishing
- `GET /api/scans` — Paginated scan history (optional sessionId filter)
- `GET /api/scans/:id` — Single scan by ID
- `GET /api/stats` — Aggregate stats
- `GET /api/healthz` — Health check

## Database Tables

- `scans` — stores all scan results (verdict, scores, indicators, email text, URL)
- `rate_limits` — per-IP rate limiting counters

## Footer Credit

Hasini Vinnakota | CEH 2026 | GitHub
