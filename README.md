# SaaS Platform Foundation

A foundational multi-tenant SaaS platform scaffold featuring:

- Next.js 15 (App Router, TypeScript strict)
- Prisma + Postgres
- Multi-tenant models (Organization → Project → Environment → Feature Flags)
- Basic Feature Flag evaluation utility
- NextAuth (JWT sessions; Credentials + GitHub OAuth placeholder)
- Stripe billing webhook scaffold
- OpenTelemetry bootstrap (optional via env)
- Pino structured logging
- Vitest testing setup
- CI (lint, typecheck, test, build, prisma migrate)
- Docker dev environment
- CDK infrastructure skeleton
- Conventional commit tooling

## Quick Start

```bash
pnpm install
cp .env.example .env
# edit DATABASE_URL etc.
pnpm prisma:generate
pnpm prisma:migrate dev
pnpm seed
pnpm dev
```

Visit http://localhost:3000

## Auth

Using NextAuth with JWT strategy:
- Simpler setup (no session table required).
- Credentials provider expects a hashed password (seed user currently has none).
- GitHub OAuth placeholder ready (add client ID/secret).

To enable credential login:
1. Add a hashed password to a user (e.g. via a small script using bcryptjs).
2. Supply credentials at /api/auth/signin.

## Differences from DB Session Strategy

We intentionally removed database sessions for lower friction at this stage. If you later want persistent server-invalidatable sessions:
- Add the Session model migrations and Prisma Adapter
- Switch `session.strategy` to `database`