# EliteCoach — Local Development Setup

## Overview

EliteCoach is a premium AI business coach SaaS application built with:

- **Frontend:** React 19 + TypeScript + Tailwind CSS 4 + Framer Motion
- **Backend:** Express 4 + tRPC 11 (end-to-end type safety)
- **Database:** MySQL / TiDB (via Drizzle ORM)
- **Auth:** Manus OAuth (or swap with any OAuth provider)
- **Payments:** Stripe (subscriptions, $8/month Premium tier)
- **AI:** Built-in LLM integration (OpenAI-compatible)

---

## Prerequisites

| Tool | Version | Install |
|------|---------|---------|
| Node.js | ≥ 22 | https://nodejs.org |
| pnpm | ≥ 10 | `npm install -g pnpm` |
| MySQL | ≥ 8 | https://dev.mysql.com/downloads/ |

---

## Quick Start

### 1. Clone / extract the project

```bash
cd elite-coach-app
```

### 2. Install dependencies

```bash
pnpm install
```

### 3. Configure environment variables

Create a `.env` file in the project root:

```env
# ── Database ──────────────────────────────────────────────────────────────────
DATABASE_URL=mysql://root:password@localhost:3306/elitecoach

# ── Auth (Manus OAuth) ────────────────────────────────────────────────────────
# Replace with your own OAuth provider credentials if not using Manus
JWT_SECRET=your-super-secret-jwt-key-min-32-chars
VITE_APP_ID=your-manus-app-id
OAUTH_SERVER_URL=https://api.manus.im
VITE_OAUTH_PORTAL_URL=https://manus.im
OWNER_OPEN_ID=your-owner-open-id
OWNER_NAME=Your Name

# ── Stripe ────────────────────────────────────────────────────────────────────
STRIPE_SECRET_KEY=sk_test_...
VITE_STRIPE_PUBLISHABLE_KEY=pk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...

# ── LLM (OpenAI-compatible) ───────────────────────────────────────────────────
BUILT_IN_FORGE_API_URL=https://api.openai.com/v1
BUILT_IN_FORGE_API_KEY=sk-...
VITE_FRONTEND_FORGE_API_KEY=sk-...
VITE_FRONTEND_FORGE_API_URL=https://api.openai.com/v1

# ── App ───────────────────────────────────────────────────────────────────────
VITE_APP_TITLE=EliteCoach
```

> **Tip:** For Stripe local testing, install the [Stripe CLI](https://stripe.com/docs/stripe-cli) and run:
> ```bash
> stripe listen --forward-to localhost:3000/api/stripe/webhook
> ```
> Copy the webhook signing secret it outputs into `STRIPE_WEBHOOK_SECRET`.

### 4. Set up the database

```bash
# Generate migration SQL from schema
pnpm drizzle-kit generate

# Apply migrations (reads from drizzle/ folder)
pnpm drizzle-kit migrate
```

### 5. Start the development server

```bash
pnpm dev
```

The app will be available at **http://localhost:3000**

---

## Project Structure

```
elite-coach-app/
├── client/                     # React frontend
│   ├── index.html              # HTML entry point (fonts loaded here)
│   └── src/
│       ├── pages/
│       │   ├── Home.tsx        # Landing page (6 sections)
│       │   ├── Onboarding.tsx  # 3-step onboarding flow
│       │   ├── Dashboard.tsx   # Main dashboard (XP, quests, streak)
│       │   ├── Roadmap.tsx     # 14-day roadmap (4 phases)
│       │   ├── QuestDetail.tsx # Quest step-by-step + complete button
│       │   ├── Upgrade.tsx     # Premium paywall page
│       │   └── UpgradeSuccess.tsx
│       ├── components/         # Reusable UI components (shadcn/ui)
│       ├── contexts/           # ThemeContext
│       ├── lib/trpc.ts         # tRPC client binding
│       ├── App.tsx             # Routes
│       ├── index.css           # Global dark theme + gold accents
│       └── main.tsx            # React entry point
│
├── server/
│   ├── routers.ts              # All tRPC procedures
│   ├── db.ts                   # Database query helpers
│   ├── products.ts             # Stripe product/price config
│   ├── stripeWebhook.ts        # Stripe webhook handler
│   ├── roadmap.test.ts         # Gamification tests
│   ├── subscription.test.ts    # Subscription tests
│   └── _core/                  # Framework internals (OAuth, tRPC, LLM)
│
├── shared/
│   ├── roadmapData.ts          # 14-day roadmap + 26+ quests data
│   └── const.ts                # Shared constants
│
├── drizzle/
│   ├── schema.ts               # Database schema (Drizzle ORM)
│   └── *.sql                   # Generated migration files
│
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README_LOCAL.md             # This file
```

---

## Key Features

### 14-Day Roadmap (4 Phases)

| Phase | Days | Focus |
|-------|------|-------|
| Idea & Research | 1–3 | Niche selection, market research, business model |
| Validation | 4–6 | Customer interviews, demand validation, offer testing |
| Build | 7–10 | Content creation, product build, personal brand setup |
| Monetization | 11–14 | Outreach, posting offers, closing first sales |

### Gamification System

- **XP:** 10–50 XP per quest completed
- **Levels:** Beginner (0 XP) → Builder (200 XP) → Seller (500 XP) → Founder (1000 XP)
- **Streaks:** Daily login + quest completion tracking
- **Progress bars:** Per-day and overall roadmap completion

### Subscription Tiers

| Feature | Free | Premium ($8/mo) |
|---------|------|-----------------|
| Roadmap access | Days 1–3 | All 14 days |
| Quests | 6 starter quests | 26+ quests |
| AI feedback | — | ✓ |
| Personalized plan | — | ✓ |
| Advanced strategies | — | ✓ |
| Premium badge | — | ✓ |

---

## Running Tests

```bash
pnpm test
```

Tests cover:
- Roadmap data integrity (all 14 days, quest structure, XP ranges)
- Gamification logic (XP calculation, level progression, streak tracking)
- Subscription system (status checks, tier gating, webhook handling)

---

## Building for Production

```bash
pnpm build
pnpm start
```

---

## Stripe Test Cards

| Card | Result |
|------|--------|
| `4242 4242 4242 4242` | Successful payment |
| `4000 0000 0000 9995` | Payment declined |

Use any future expiry date and any 3-digit CVC.

---

## Customization

### Change the price
Edit `server/products.ts` — update the `unitAmount` (in cents) and `priceId` fields.

### Add more quests
Edit `shared/roadmapData.ts` — follow the existing `Quest` interface structure.

### Modify XP thresholds
Edit the `LEVELS` array in `shared/roadmapData.ts`.

### Change theme colors
Edit the CSS variables in `client/src/index.css` under `:root` and `.dark`.

---

## Support

For issues or questions, open an issue in the project repository.
