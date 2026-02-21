# Claude Code Prompt: SnapStats Landing Page (/about)

## What You're Building

Build a conversion-focused landing page at `/about` for SnapStats (snapstats.app), a multi-sport SaaS platform for game stat tracking. This is the primary sales page. Every section should move a visitor closer to clicking "Start Free Trial." The page lives inside an existing Next.js + Tailwind project.

---

## Design System (Non-Negotiable)

Follow these specs exactly. Do not improvise colors, fonts, or spacing.

### Colors
```
--navy:          #0F1B2D   (primary background)
--navy-800:      #1A2942   (elevated surfaces, cards)
--navy-700:      #253754   (hover states)
--lime:          #BFFF00   (accent, CTAs, highlights)
--lime-dark:     #99CC00   (hover on lime buttons)
--slate-500:     #64748B   (secondary text)
--slate-300:     #CBD5E1   (body text on dark)
--slate-200:     #E2E8F0   (borders on light)
--surface:       #F8FAFC   (light sections)
--alert:         #EF4444   (live indicators)
--success:       #22C55E   (positive callouts)
--warning:       #F59E0B   (warnings)
```

### Typography
- Headlines: Inter, weight 700-800
- Body: Inter, weight 400-500
- Stats/numbers: JetBrains Mono, weight 400-700
- Import both from Google Fonts

### Buttons
- Primary CTA: `bg-[#BFFF00] text-[#0F1B2D] font-bold` with hover `bg-[#99CC00]`
- Secondary: transparent with slate border, white text on dark
- Border radius: 8px on everything
- Minimum button padding: py-3 px-6
- CTAs should be uppercase for short labels (2 words or less)

### General
- Dark mode is the default for this page. Navy background throughout.
- Lime is an accent flash, not a flood. Use it only for CTAs, key highlights, and small badges.
- No serif fonts. No decorative fonts. No gradients on text.
- Mobile-first. Design for 375px width first, scale up.
- Max content width: 1280px, centered.
- Section padding: py-20 on mobile, py-24 on desktop.

---

## Page Structure

Build these sections in this exact order. Each section has a specific conversion job.

### 1. Navigation Bar (sticky)

- Left: SnapStats wordmark ("Snap" in lime, "Stats" in white, Inter ExtraBold)
- Right: "Log In" text link + "Start Free Trial" lime CTA button
- Background: navy, transitions from transparent to solid on scroll
- Mobile: hamburger menu

### 2. Hero Section

**Job: Hook them in 3 seconds.**

- Headline (text-4xl mobile, text-5xl desktop, Inter ExtraBold, white):
  "Every sport. Every stat. Every play."
- Subhead (text-lg, slate-300, max-w-2xl):
  "Track game stats live or from recorded video. Sync to film. See what the scoreboard can't tell you. One platform for 15+ sports, from club teams to college programs."
- Primary CTA: "START FREE TRIAL" (lime button, large)
- Secondary CTA: "See How It Works" (ghost button, scrolls to demo section)
- Below CTAs: Small trust line in slate-500, e.g. "No credit card required. Set up in under 5 minutes."
- Visual: Abstract stat bars or a mockup of the dark-mode dashboard on a tablet/phone. Use a placeholder div styled as a device frame with fake stat UI inside it if no real screenshot exists yet. Make it look real.

### 3. Sport Grid Section

**Job: Show breadth. "Wait, it does MY sport?"**

- Section label (lime, uppercase, text-sm, tracked): "EVERY SPORT, ONE PLATFORM"
- Headline (text-3xl, white): "From water polo to wrestling. And everything in between."
- Grid of sport cards (4 columns desktop, 2 columns mobile):
  - Water Polo, Basketball, Football, Soccer, Volleyball, Lacrosse, Field Hockey, Ice Hockey, Baseball, Softball, Wrestling, Tennis, Rugby, Swimming, Track & Field, More Coming
- Each card: navy-800 background, sport name in white, subtle icon or emoji, rounded-lg
- The "More Coming" card should have a lime border and say "Request a sport" as a subtle CTA
- Below grid: "New sports added through configuration, not code. If you play it, we can track it."

### 4. How It Works Section

**Job: Make it feel dead simple.**

- Section label: "HOW IT WORKS"
- Headline: "From signup to stats in under 5 minutes."
- 4 steps in a horizontal flow (vertical on mobile):
  1. "Sign Up" — "Create your club account and pick your sport."
  2. "Build Your Roster" — "Add players, invite coaches and stat trackers."
  3. "Track the Game" — "Tap to log plays live at the game or later from recorded video. Your schedule."
  4. "Review and Analyze" — "Scrub through stats synced to film. Export reports. Track progression."
- Each step: Number in lime (large, JetBrains Mono), title in white bold, description in slate-300
- Connecting line or arrow between steps (lime, subtle)
- CTA at bottom: "START FREE TRIAL"

### 5. Film Sync Feature Section

**Job: Sell the killer feature.**

- Section label: "FILM SYNC"
- Headline: "Every stat, timestamped to the video."
- Body: "Log a goal, an assist, a steal. SnapStats timestamps it to the exact moment in your game film. During review, tap any stat and jump straight to that play. No more scrubbing through hours of footage."
- Visual: A mockup showing a stat list on the left and a video player on the right with a timestamp indicator. Build this as a styled component with fake data, not an image. Use JetBrains Mono for the stat numbers and timestamps.
- Callout badge: "Track live or post-game" in a lime-bordered pill
- CTA: "START FREE TRIAL"

### 6. Built for the Sideline Section

**Job: Show the mobile-first UX advantage.**

- Section label: "MOBILE FIRST"
- Headline: "Designed for game day. Not the office."
- Body: "Big tap targets. Instant undo. Works on any phone or tablet. Whether you're on the pool deck, the sideline, or your couch after the game, SnapStats is built for how you actually track stats."
- Visual: A phone mockup showing large stat tracking buttons (build a fake UI component with buttons like "GOAL", "ASSIST", "STEAL", "FOUL", "SHOT" in a grid layout, dark theme, lime accents on active states)
- Feature bullets (2 columns on desktop):
  - "48px+ tap targets for zero mis-taps"
  - "Instant undo on every action"
  - "Works offline, syncs when connected"
  - "Track from your phone, tablet, or laptop"

### 7. Pricing Section

**Job: Remove the money objection.**

- Section label: "PRICING"
- Headline: "Less than a tournament entry fee."
- Subhead: "Start free. Upgrade when you're ready."
- Toggle: Monthly / Yearly (yearly shows "Save 28%" badge in lime)

**4 pricing cards in a row (stack on mobile):**

**Starter — Free**
- "Try SnapStats with zero commitment"
- 14-day Pro trial included
- 1 team, 1 sport
- 3 games per month
- Basic stat tracking
- CTA: "START FREE TRIAL" (lime button)

**Pro — $29/mo or $249/yr**
- "Everything a team needs"
- Unlimited games
- Film sync
- Analytics dashboards
- CSV and PDF export
- Up to 3 stat trackers
- CTA: "START FREE TRIAL" (lime button)
- Badge: "MOST POPULAR" (lime background, navy text, top of card)

**Program — $79/mo or $699/yr**
- "For multi-team programs and athletic directors"
- Everything in Pro
- Unlimited teams and sports
- Unlimited stat trackers
- Player profiles
- Season trends and progression
- Priority support
- CTA: "START FREE TRIAL" (secondary button style)

**Enterprise — Custom**
- "For colleges and large athletic departments"
- Everything in Program
- SSO and API access
- White-label options
- Dedicated onboarding
- CTA: "CONTACT US" (secondary button, links to mailto:hello@snapstats.app)

- Pro card should be visually elevated (slightly larger, lime top border or glow)
- All prices show monthly by default, switch to yearly on toggle
- Below pricing: "All plans include a 14-day free trial of Pro features. No credit card required."

### 8. Coming Soon / Parents Section

**Job: Build excitement for what's next. Get parents invested.**

- Background shift: navy-800 to differentiate from other sections
- Section label: "COMING SOON"
- Headline: "For the parents in the stands."
- Subhead: "We're building features that keep the whole family connected to the game."
- 3 teaser cards (navy-700 background, lime accent icon area):
  1. "Public Player Profiles" — "Showcase your athlete's stats, highlights, and progression. Built for college recruiting."
  2. "Live Game Feed" — "Follow the game in real time from anywhere. See every play as it happens, even when you can't be there."
  3. "Season Highlight Reels" — "Auto-generated video highlights pulled from your timestamped stats. Every big moment, compiled for you."
- Each card: "Coming Soon" pill badge (lime border, lime text, small)
- CTA: "Get Notified" button that triggers an email capture input (just the email field + submit, nothing complex). Store submissions or just wire to a mailto for now.
- Tone: Warm, inclusive, exciting. This section is talking to parents, not coaches.

### 9. Social Proof / Trust Section

**Job: Handle objections.**

- Since there are no testimonials yet, use trust-building stat callouts instead:
  - "15+ Sports Supported"
  - "Set Up in Under 5 Minutes"
  - "No Sales Call Required"
  - "No Credit Card to Start"
- Display as 4 large stat blocks in a row (numbers in JetBrains Mono, large, lime; labels in white)
- Below: "Trusted by coaches and programs building the future of youth sports analytics."

### 10. Final CTA Section

**Job: Last chance to convert.**

- Full-width section with navy background
- Headline (text-3xl, white): "Ready to track like the pros?"
- Subhead: "Sign up in 30 seconds. Start tracking your next game."
- Large lime CTA: "START FREE TRIAL"
- Below: "No credit card required. Cancel anytime."

### 11. Footer

- 4 columns on desktop, stacked on mobile:
  - **Product**: Features, Pricing, Sports, How It Works (anchor links to sections above)
  - **Company**: About, Contact (hello@snapstats.app), Blog (placeholder)
  - **Legal**: Privacy Policy (placeholder), Terms of Service (placeholder)
  - **Connect**: @snapstatsapp links for Twitter/X, Instagram, LinkedIn
- Bottom bar: "© 2026 SnapStats. All rights reserved." + snapstats.app

---

## Technical Requirements

- Next.js page component at `/about` (or `/app/about/page.tsx` depending on router)
- Tailwind CSS only. No component libraries. No external CSS.
- Responsive: Mobile (375px), Tablet (768px), Desktop (1280px+)
- Smooth scroll behavior for anchor links
- Intersection Observer for subtle fade-in animations on scroll (one section at a time, not staggered individual elements). Keep animations under 300ms.
- Pricing toggle is client-side state (useState for monthly/yearly switch)
- "Get Notified" email capture: just collect the email in a form. Console.log it for now or wire to a simple API route. Do not over-engineer this.
- All "Start Free Trial" buttons link to `/signup` (even if that page doesn't exist yet)
- "Contact Us" links to mailto:hello@snapstats.app
- Semantic HTML throughout. Proper heading hierarchy (one h1, h2s for sections, h3s for cards).
- Images: Use placeholder divs styled to look like device mockups and app UI. Do not use external image URLs or stock photos. Build fake UI components that look like the real product.

---

## Pricing Architecture and Subscription System

This is not just a landing page. The pricing model needs to be built into the application's data layer so that feature gating, plan enforcement, and payment processing are ready to wire up. Build this alongside the landing page.

### Plan Definitions

Create a central pricing config file (e.g. `lib/pricing.ts` or `config/plans.ts`) that is the single source of truth for all plan data. The landing page pricing section, the app's feature gates, and the future Stripe integration all read from this one file.

```typescript
// This is the structure. Implement it exactly.

export type PlanId = 'starter' | 'pro' | 'program' | 'enterprise';
export type BillingInterval = 'monthly' | 'yearly';

export interface PlanFeatures {
  maxTeams: number;           // -1 for unlimited
  maxSports: number;          // -1 for unlimited
  maxGamesPerMonth: number;   // -1 for unlimited
  maxStatTrackers: number;    // -1 for unlimited
  filmSync: boolean;
  analyticsDashboards: boolean;
  csvExport: boolean;
  pdfExport: boolean;
  playerProfiles: boolean;
  seasonTrends: boolean;
  prioritySupport: boolean;
  sso: boolean;
  apiAccess: boolean;
  whiteLabel: boolean;
  dedicatedOnboarding: boolean;
}

export interface Plan {
  id: PlanId;
  name: string;
  tagline: string;
  monthlyPrice: number;       // in cents. 0 for free. -1 for custom/contact us.
  yearlyPrice: number;        // in cents. 0 for free. -1 for custom/contact us.
  features: PlanFeatures;
  highlighted: boolean;       // true for Pro (the "MOST POPULAR" card)
  ctaLabel: string;
  ctaAction: 'signup' | 'contact';
  trialDays: number;          // 14 for all plans with a trial
  stripePriceIdMonthly?: string;   // filled in when Stripe is connected
  stripePriceIdYearly?: string;    // filled in when Stripe is connected
}
```

### Plan Data

```typescript
export const PLANS: Plan[] = [
  {
    id: 'starter',
    name: 'Starter',
    tagline: 'Try SnapStats with zero commitment',
    monthlyPrice: 0,
    yearlyPrice: 0,
    features: {
      maxTeams: 1,
      maxSports: 1,
      maxGamesPerMonth: 3,
      maxStatTrackers: 1,
      filmSync: false,
      analyticsDashboards: false,
      csvExport: false,
      pdfExport: false,
      playerProfiles: false,
      seasonTrends: false,
      prioritySupport: false,
      sso: false,
      apiAccess: false,
      whiteLabel: false,
      dedicatedOnboarding: false,
    },
    highlighted: false,
    ctaLabel: 'START FREE TRIAL',
    ctaAction: 'signup',
    trialDays: 14,  // 14-day trial of Pro features
  },
  {
    id: 'pro',
    name: 'Pro',
    tagline: 'Everything a team needs',
    monthlyPrice: 2900,       // $29.00
    yearlyPrice: 24900,       // $249.00 (save ~28%)
    features: {
      maxTeams: 1,
      maxSports: 1,
      maxGamesPerMonth: -1,
      maxStatTrackers: 3,
      filmSync: true,
      analyticsDashboards: true,
      csvExport: true,
      pdfExport: true,
      playerProfiles: false,
      seasonTrends: false,
      prioritySupport: false,
      sso: false,
      apiAccess: false,
      whiteLabel: false,
      dedicatedOnboarding: false,
    },
    highlighted: true,
    ctaLabel: 'START FREE TRIAL',
    ctaAction: 'signup',
    trialDays: 14,
  },
  {
    id: 'program',
    name: 'Program',
    tagline: 'For multi-team programs and athletic directors',
    monthlyPrice: 7900,       // $79.00
    yearlyPrice: 69900,       // $699.00 (save ~26%)
    features: {
      maxTeams: -1,
      maxSports: -1,
      maxGamesPerMonth: -1,
      maxStatTrackers: -1,
      filmSync: true,
      analyticsDashboards: true,
      csvExport: true,
      pdfExport: true,
      playerProfiles: true,
      seasonTrends: true,
      prioritySupport: true,
      sso: false,
      apiAccess: false,
      whiteLabel: false,
      dedicatedOnboarding: false,
    },
    highlighted: false,
    ctaLabel: 'START FREE TRIAL',
    ctaAction: 'signup',
    trialDays: 14,
  },
  {
    id: 'enterprise',
    name: 'Enterprise',
    tagline: 'For colleges and large athletic departments',
    monthlyPrice: -1,         // custom pricing
    yearlyPrice: -1,
    features: {
      maxTeams: -1,
      maxSports: -1,
      maxGamesPerMonth: -1,
      maxStatTrackers: -1,
      filmSync: true,
      analyticsDashboards: true,
      csvExport: true,
      pdfExport: true,
      playerProfiles: true,
      seasonTrends: true,
      prioritySupport: true,
      sso: true,
      apiAccess: true,
      whiteLabel: true,
      dedicatedOnboarding: true,
    },
    highlighted: false,
    ctaLabel: 'CONTACT US',
    ctaAction: 'contact',
    trialDays: 0,
  },
];
```

### Feature Gating System

Build a feature gate utility that checks the current user's plan against the feature they're trying to use. This is used throughout the app to show/hide UI elements and enforce limits.

```typescript
// lib/features.ts

export function canAccess(
  userPlan: PlanId,
  feature: keyof PlanFeatures
): boolean {
  const plan = PLANS.find(p => p.id === userPlan);
  if (!plan) return false;
  const value = plan.features[feature];
  if (typeof value === 'boolean') return value;
  if (typeof value === 'number') return value !== 0;
  return false;
}

export function getLimit(
  userPlan: PlanId,
  feature: keyof PlanFeatures
): number {
  const plan = PLANS.find(p => p.id === userPlan);
  if (!plan) return 0;
  const value = plan.features[feature];
  if (typeof value === 'number') return value;
  return 0;
}

export function isAtLimit(
  userPlan: PlanId,
  feature: keyof PlanFeatures,
  currentCount: number
): boolean {
  const limit = getLimit(userPlan, feature);
  if (limit === -1) return false; // unlimited
  return currentCount >= limit;
}

export function getUpgradePlan(currentPlan: PlanId): PlanId | null {
  const order: PlanId[] = ['starter', 'pro', 'program', 'enterprise'];
  const idx = order.indexOf(currentPlan);
  if (idx === -1 || idx >= order.length - 1) return null;
  return order[idx + 1];
}
```

### Subscription Database Schema

Add these fields to the existing club/organization table in Supabase (or create a subscriptions table):

```sql
-- Add to clubs table or create subscriptions table
-- This is the target schema. Implement as a Supabase migration.

create table if not exists subscriptions (
  id uuid primary key default gen_random_uuid(),
  club_id uuid references clubs(id) not null,
  plan_id text not null default 'starter',
  status text not null default 'trialing',
  billing_interval text default 'monthly',
  trial_start timestamptz default now(),
  trial_end timestamptz default (now() + interval '14 days'),
  current_period_start timestamptz,
  current_period_end timestamptz,
  stripe_customer_id text,
  stripe_subscription_id text,
  stripe_price_id text,
  cancel_at_period_end boolean default false,
  canceled_at timestamptz,
  created_at timestamptz default now(),
  updated_at timestamptz default now(),
  unique(club_id)
);

create index idx_subscriptions_club on subscriptions(club_id);
create index idx_subscriptions_stripe on subscriptions(stripe_customer_id);
```

### Subscription State Helper

```typescript
// lib/subscription.ts

export type SubscriptionStatus = 'trialing' | 'active' | 'past_due' | 'canceled' | 'unpaid';

export interface Subscription {
  planId: PlanId;
  status: SubscriptionStatus;
  billingInterval: BillingInterval;
  trialEnd: Date | null;
  currentPeriodEnd: Date | null;
  cancelAtPeriodEnd: boolean;
}

export function isTrialing(sub: Subscription): boolean {
  if (sub.status !== 'trialing') return false;
  if (!sub.trialEnd) return false;
  return new Date() < sub.trialEnd;
}

export function isActive(sub: Subscription): boolean {
  return sub.status === 'active' || isTrialing(sub);
}

export function isPastDue(sub: Subscription): boolean {
  return sub.status === 'past_due';
}

export function daysLeftInTrial(sub: Subscription): number {
  if (!isTrialing(sub) || !sub.trialEnd) return 0;
  const diff = sub.trialEnd.getTime() - Date.now();
  return Math.max(0, Math.ceil(diff / (1000 * 60 * 60 * 24)));
}

export function effectivePlan(sub: Subscription): PlanId {
  // During trial, user gets Pro features regardless of plan
  if (isTrialing(sub)) return 'pro';
  if (!isActive(sub)) return 'starter'; // fallback to free on lapsed
  return sub.planId;
}
```

### Upgrade/Downgrade UI Components

Build these components that will be used throughout the app:

**UpgradeBanner** — A dismissible banner shown when a user hits a feature limit.
- "You've used 3 of 3 games this month. Upgrade to Pro for unlimited games."
- Lime accent border on the left, navy-800 background, upgrade CTA button
- Shows contextually (e.g. on the games list when at limit, on the export button when export is locked)

**PlanBadge** — A small badge showing the user's current plan.
- Shown in the sidebar or account settings
- Starter: slate outline, "Starter" text
- Pro: lime background, navy text, "Pro"
- Program: lime outline, lime text, "Program"
- Enterprise: white outline, "Enterprise"

**TrialCountdown** — Shows remaining trial days.
- "5 days left in your Pro trial"
- Shown in the sidebar or top bar when trialing
- When 3 days or fewer: amber/warning color
- When trial expires: prompt to upgrade or fall back to Starter

**PaywallModal** — Shown when a user tries to access a locked feature.
- "Film Sync is a Pro feature"
- Brief explanation of the feature
- Current plan vs. what they need
- "Upgrade to Pro" CTA (lime) and "Maybe Later" dismiss
- Do NOT block the entire app. Just gate the specific feature.

**PricingTable** — Reusable component that renders the pricing cards.
- Used on the /about landing page AND in an in-app /settings/billing page
- Reads from the central PLANS config
- Highlights the user's current plan when shown in-app
- Monthly/yearly toggle
- This is a shared component, not duplicated code

### Stripe Integration Prep

Do NOT integrate Stripe yet. But structure the code so it's ready:

1. **Environment variables placeholder:**
```env
# .env.local (do not populate yet)
STRIPE_SECRET_KEY=
STRIPE_PUBLISHABLE_KEY=
STRIPE_WEBHOOK_SECRET=
STRIPE_PRO_MONTHLY_PRICE_ID=
STRIPE_PRO_YEARLY_PRICE_ID=
STRIPE_PROGRAM_MONTHLY_PRICE_ID=
STRIPE_PROGRAM_YEARLY_PRICE_ID=
```

2. **API route stubs** — Create these files with TODO comments and the expected request/response shapes:
- `app/api/stripe/create-checkout/route.ts` — Creates a Stripe Checkout session for a plan upgrade
- `app/api/stripe/create-portal/route.ts` — Creates a Stripe Customer Portal session for managing subscription
- `app/api/stripe/webhook/route.ts` — Handles Stripe webhook events (subscription created, updated, deleted, payment failed)

3. **Webhook event handlers to stub out:**
- `checkout.session.completed` — Activate subscription, update plan in database
- `customer.subscription.updated` — Handle plan changes, interval changes
- `customer.subscription.deleted` — Mark as canceled, downgrade to Starter
- `invoice.payment_failed` — Mark as past_due, trigger email notification
- `customer.subscription.trial_will_end` — Trigger email 3 days before trial expires

4. **Checkout flow (stubbed):**
- User clicks "Upgrade to Pro" anywhere in the app
- App calls `/api/stripe/create-checkout` with planId and billingInterval
- API creates Stripe Checkout session (stubbed: just return a placeholder URL)
- User is redirected to Stripe Checkout (when live) or shown a "Coming soon" message (for now)
- On success, Stripe webhook fires and updates the subscription in Supabase

5. **Customer portal flow (stubbed):**
- User clicks "Manage Subscription" in settings
- App calls `/api/stripe/create-portal`
- User is redirected to Stripe Customer Portal where they can update payment, switch plans, cancel

### Feature Gating in the UI

When a feature is locked by the user's plan, the UI should:
1. Show the feature as visible but disabled (not hidden). Users should know what they're missing.
2. Show a lock icon or "Pro" / "Program" badge next to the feature name.
3. On click/tap of a locked feature, open the PaywallModal with the relevant upgrade path.
4. Never show a blank wall or generic "upgrade" page. Always tell them specifically what they'll unlock.

Examples of where feature gates apply:
- **Games list**: If at maxGamesPerMonth limit, show UpgradeBanner and disable "New Game" button
- **Film sync toggle**: If filmSync is false, show lock icon, clicking opens PaywallModal
- **Export buttons**: If csvExport/pdfExport is false, show lock icon
- **Add team**: If at maxTeams limit, show UpgradeBanner
- **Invite stat tracker**: If at maxStatTrackers limit, show UpgradeBanner
- **Player profiles tab**: If playerProfiles is false, show "Pro" badge and paywall
- **Season trends view**: If seasonTrends is false, show "Program" badge and paywall
- **Analytics dashboards**: If analyticsDashboards is false, show paywall

---

## Voice and Tone Reminders

- Short sentences. Active voice. Lead with verbs.
- No buzzwords: never use "revolutionary," "disruptive," "game-changing," "cutting-edge," "next-gen," or "leverage."
- Write like a coach talks. "Track it live. Watch it back." Not "Our platform enables real-time statistical data capture."
- Address the reader as "you" and "your team."
- Sport language is good (courtside, film room, game day). Tech jargon is bad (webhook, API, sync conflict).
- The parent section can be warmer and more emotional. The rest should be confident and direct.

---

## What Success Looks Like

A visitor lands on this page and within 10 seconds understands:
1. What SnapStats does (track game stats for any sport)
2. What makes it different (film sync, every sport, affordable)
3. What to do next (start free trial)

The page should feel fast, athletic, modern, and trustworthy. It should look like it belongs next to Strava or ESPN, not like a template from a website builder. Every pixel should earn its place.
