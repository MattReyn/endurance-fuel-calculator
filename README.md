# Endurance Fuel Calculator

Plan your race fueling from the gels and drink mixes you actually have.

Enter your activity, how long it lasts, how much fluid you carry, the products you own and your carb goal. The calculator tells you what to carry and when to take it, in real units:

> **1 Maurten Gel 160 every 35 min**, alternating with **SiS Beta Fuel**, plus **2 scoops** of drink mix in your 500 ml bottle. Achieved 88 g/h against a goal of 90 g/h.

Built for running first, but it works for any endurance sport.

> **Status:** in design. See the design doc for milestones 1 to 3.

## Features (planned through milestone 3)

- Carb plans from your own products, with gel types alternating
- Adjustable plan: change the interval between gels ("2 gels at 45 min") or the share of carbs from drink mix
- Drink mix capped by what your bottle can actually hold
- Actual g/h after rounding, with warnings when you're short
- Sodium and caffeine totals
- A searchable catalog of 60 to 80 gels, chews and drink mixes, each value linked to its source

Later: accounts with an inventory that updates when you complete an activity, refill stations, and sodium and caffeine targets.

## Architecture

| Part | Tech | Role |
| --- | --- | --- |
| Web | React, Vite, Tailwind on Vercel | Planner UI; runs the fueling engine in the browser for instant updates |
| Engine | TypeScript package | Pure, deterministic plan math shared by web and API |
| API | Fastify, Zod on Fly.io | Product catalog search |
| Database | PostgreSQL on Neon, Drizzle ORM | Brands, products, nutrition history |

```
apps/web        React single-page app
apps/api        Fastify REST API, migrations, seed script
packages/engine Fueling engine and CLI
packages/schemas Shared Zod schemas and types
data/products   Sourced product seed data
e2e             Playwright end-to-end tests
```

## Development workflow

- `dev` is the default branch. All work goes through pull requests from feature branches.
- Every PR runs lint, typecheck, unit and property tests, integration tests against a real Postgres, Playwright end-to-end tests and seed data validation. All of them must pass before merging.
- Merging a release PR from `dev` into `production` deploys automatically: build, migrate, deploy the API and web app, smoke test, and roll back if the smoke tests fail.

## Getting started

_Setup instructions will be added with milestone 1._

## Disclaimer

Plans are general guidance, not medical advice. Test your fueling in training before race day.
