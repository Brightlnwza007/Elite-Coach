# Elite Business Coach - Project TODO

## Phase 2: Database & Backend
- [x] DB schema: userProfile, questProgress, userStats tables
- [x] Backend routers: onboarding, quests, progress, gamification
- [x] Seed data: 14-day roadmap with all quests (shared/roadmapData.ts)

## Phase 3: Design System
- [x] Dark theme CSS variables (black/deep gray, gold accents)
- [x] Google Fonts (Inter + Playfair Display)
- [x] Glassmorphism utility classes
- [x] Smooth animations with framer-motion

## Phase 4: Onboarding
- [x] Multi-step onboarding form (goal, time/day, skill level)
- [x] Save onboarding data to DB
- [x] Redirect to dashboard after onboarding

## Phase 5: Dashboard
- [x] XP bar with level display (Beginner → Builder → Seller → Founder)
- [x] Streak counter
- [x] Today's quests list
- [x] Overall progress bar (14-day)
- [x] Next milestone highlight

## Phase 6: Roadmap & Quest Detail
- [x] 14-day roadmap view with 4 phases
- [x] Phase cards with lock/unlock state
- [x] Quest detail page: step-by-step, time, outcome, XP, difficulty
- [x] Mark quest as complete button
- [x] Day summary after completing all quests

## Phase 7: Premium/Free Tier
- [x] Free tier: Days 1-3 only
- [x] Premium lock overlay on Days 4-14
- [x] Upgrade prompt UI
- [x] Progress summary on dashboard

## Phase 8: Polish & Delivery
- [x] Smooth page transitions (framer-motion)
- [x] Loading states
- [x] Mobile responsive layout
- [x] Vitest tests (24 tests passing)
- [x] Checkpoint & delivery

## Subscription System
- [x] Stripe integration (webdev_add_feature)
- [x] DB schema: subscriptions table (userId, stripeCustomerId, stripeSubscriptionId, status, currentPeriodEnd)
- [x] Backend routers: createCheckoutSession, handleWebhook, getSubscriptionStatus, cancelSubscription
- [x] Premium Paywall page (/upgrade) - dark luxury design, gold accents
- [x] Free vs Premium comparison table
- [x] Strong headline: "Start making real money"
- [x] Monthly price: $8/month display
- [x] Urgency message: "Most users quit before earning. Premium users don't."
- [x] Premium badge on dashboard/nav for premium users
- [x] Locked feature preview overlays (blur + lock icon + upgrade CTA)
- [x] Upgrade button in nav and dashboard
- [x] Success/cancel redirect pages after Stripe checkout
- [x] Webhook handler for subscription lifecycle events
- [x] Tests for subscription logic (16 tests)

## Landing Page & Upgrade Flow
- [x] Rebuild Home.tsx: Hero, Problem, Solution, Features, Pricing, CTA sections
- [x] Upgrade to Premium button in nav and hero (smooth Stripe redirect)
- [x] Post-payment: mark user as premium via webhook (already wired)
- [x] Smooth scroll navigation between sections
- [x] Mobile responsive landing page
