# SnapStats Design System
## snapstats.app

This is the single source of truth for all design decisions across the SnapStats platform. Every UI component, page, and screen should reference this document. When in doubt, refer back here.

---

## Brand Overview

SnapStats is a multi-sport SaaS platform for game stat tracking. Coaches record their games, upload the video, then track every stat frame by frame on their desktop with pause, rewind, and precision you'd never get live. Every stat is timestamped to the video. Click any stat and the video jumps right to that moment. The platform serves youth clubs, middle school, high school, and college programs across 15+ sports.

**Primary domain:** snapstats.app
**Social handle:** @snapstatsapp (all platforms)

---

## Color Palette

### Primary Colors

| Token | Name | Hex | RGB | Usage |
|-------|------|-----|-----|-------|
| `--color-primary` | Deep Navy | #0F1B2D | 15, 27, 45 | Primary background, dark UI base, nav bars, headers |
| `--color-accent` | Electric Lime | #BFFF00 | 191, 255, 0 | Primary CTA buttons, active states, highlights, badges |
| `--color-secondary` | Cool Slate | #64748B | 100, 116, 139 | Secondary text, labels, borders, muted UI elements |
| `--color-surface` | Off-White | #F8FAFC | 248, 250, 252 | Light mode backgrounds, card surfaces, content areas |
| `--color-alert` | Signal Red | #EF4444 | 239, 68, 68 | Live game indicators, errors, fouls, destructive actions |

### Extended Palette

| Token | Name | Hex | Usage |
|-------|------|-----|-------|
| `--color-primary-light` | Navy 800 | #1A2942 | Card backgrounds on dark, elevated surfaces |
| `--color-primary-lighter` | Navy 700 | #253754 | Hover states on dark backgrounds, secondary panels |
| `--color-accent-dark` | Lime Dark | #99CC00 | Accent hover state, pressed buttons |
| `--color-accent-muted` | Lime Faded | #BFFF0033 | Accent backgrounds at 20% opacity, subtle highlights |
| `--color-success` | Green | #22C55E | Success states, positive stat changes, wins |
| `--color-warning` | Amber | #F59E0B | Warnings, caution states, close games |
| `--color-surface-dark` | Slate 900 | #0F172A | Dark mode surface, near-black panels |
| `--color-surface-mid` | Slate 100 | #F1F5F9 | Alternating rows, subtle section breaks |
| `--color-text-primary` | White | #FFFFFF | Primary text on dark backgrounds |
| `--color-text-secondary` | Slate 300 | #CBD5E1 | Secondary text on dark backgrounds |
| `--color-text-dark` | Slate 900 | #0F172A | Primary text on light backgrounds |
| `--color-text-muted` | Slate 500 | #64748B | Muted text, placeholders, captions |
| `--color-border` | Slate 700 | #334155 | Borders and dividers on dark backgrounds |
| `--color-border-light` | Slate 200 | #E2E8F0 | Borders and dividers on light backgrounds |

### Dark Mode (Default for the app)

SnapStats defaults to dark mode. It gives the interface a film room / scoreboard feel, reduces eye strain during long video review sessions, and looks modern and athletic.

- Background: `--color-primary` (#0F1B2D)
- Elevated surfaces: `--color-primary-light` (#1A2942)
- Text: `--color-text-primary` (#FFFFFF) and `--color-text-secondary` (#CBD5E1)
- Accent: `--color-accent` (#BFFF00)
- Borders: `--color-border` (#334155)

### Light Mode (Marketing site, docs, exports)

- Background: `--color-surface` (#F8FAFC)
- Elevated surfaces: #FFFFFF with subtle shadow
- Text: `--color-text-dark` (#0F172A) and `--color-text-muted` (#64748B)
- Accent: `--color-accent` (#BFFF00) on dark buttons/badges
- Borders: `--color-border-light` (#E2E8F0)

### Color Usage Rules

1. Never place Electric Lime text on white or light backgrounds. It fails contrast. Always use lime on dark backgrounds.
2. For CTAs on light backgrounds, use a Deep Navy button with white text, not lime.
3. The lime accent should feel like a flash, not a flood. Use it for the one thing you want someone to look at.
4. Signal Red is reserved for live indicators, errors, and fouls. Do not use red for branding or decoration.
5. When a sport-specific color is needed (team colors, sport icons), overlay it on the navy base. Never let team colors replace the SnapStats palette.

---

## Typography

### Font Stack

| Role | Font | Fallback | Weight | Usage |
|------|------|----------|--------|-------|
| Headlines | Inter | system-ui, sans-serif | 700 (Bold), 800 (ExtraBold) | Page titles, section headers, hero text |
| Body | Inter | system-ui, sans-serif | 400 (Regular), 500 (Medium) | Paragraphs, descriptions, UI labels |
| Data / Stats | JetBrains Mono | monospace | 400, 500, 700 | Stat numbers, scores, timestamps, data tables |

### Why Inter

Inter is optimized for screens, free, widely supported, and has tabular figures built in. It reads cleanly at all sizes and has enough geometric character to feel modern and sporty without being decorative.

### Why JetBrains Mono for Stats

Stats are numbers. Numbers need to align in columns. JetBrains Mono has consistent character widths, clear distinction between similar characters (0 vs O, 1 vs l), and looks sharp in data-dense interfaces. It gives stat displays that live scoreboard feel.

### Type Scale

Use a modular scale based on 16px root. All sizes in rem.

| Token | Size | Line Height | Weight | Usage |
|-------|------|-------------|--------|-------|
| `--text-xs` | 0.75rem (12px) | 1rem | 400 | Captions, timestamps, fine print |
| `--text-sm` | 0.875rem (14px) | 1.25rem | 400, 500 | Secondary labels, helper text, table cells |
| `--text-base` | 1rem (16px) | 1.5rem | 400, 500 | Body text, form inputs, buttons |
| `--text-lg` | 1.125rem (18px) | 1.75rem | 500 | Emphasized body, card titles |
| `--text-xl` | 1.25rem (20px) | 1.75rem | 600 | Section subheaders |
| `--text-2xl` | 1.5rem (24px) | 2rem | 700 | Section headers |
| `--text-3xl` | 1.875rem (30px) | 2.25rem | 700 | Page titles |
| `--text-4xl` | 2.25rem (36px) | 2.5rem | 800 | Hero headlines |
| `--text-5xl` | 3rem (48px) | 1 | 800 | Marketing hero, big stat numbers |
| `--text-stat` | 3.75rem (60px) | 1 | 700 | Large stat display (score, player number) |

### Typography Rules

1. Headlines can be uppercase for short phrases (3 words or less). Longer headlines use title case.
2. Body text is always sentence case.
3. Never use italic for emphasis in the UI. Use font weight (Medium or Bold) instead.
4. Stat numbers always use JetBrains Mono regardless of context.
5. Line height for large display text (text-4xl and above) should be tight (1 or 1.1). Body text gets breathing room (1.5).
6. Letter spacing: Headlines at -0.02em (slightly tighter). Body at 0 (default). Uppercase headlines at 0.05em (slightly wider).
7. Maximum line length for body text: 65 characters. Use max-w-prose or equivalent.

---

## Spacing and Layout

### Spacing Scale

Based on 4px increments. Use Tailwind spacing tokens directly.

| Token | Value | Common Usage |
|-------|-------|--------------|
| 1 | 4px | Tight gaps between inline elements |
| 2 | 8px | Icon padding, tight component spacing |
| 3 | 12px | Small card padding, compact list items |
| 4 | 16px | Default component padding, form field gaps |
| 5 | 20px | Medium gaps |
| 6 | 24px | Section padding on mobile, card padding |
| 8 | 32px | Section gaps, large card padding |
| 10 | 40px | Section padding on tablet |
| 12 | 48px | Large section breaks |
| 16 | 64px | Page section padding on desktop |
| 20 | 80px | Hero section padding |
| 24 | 96px | Major page sections |

### Grid

- Marketing site: 12-column grid, max-width 1280px, centered
- App dashboard: Full-width fluid, sidebar + main content area
- Stat tracking UI: Full-width, no max-width, every pixel counts on mobile

### Breakpoints

| Token | Width | Target |
|-------|-------|--------|
| `sm` | 640px | Large phones landscape |
| `md` | 768px | Tablets portrait |
| `lg` | 1024px | Tablets landscape, small laptops |
| `xl` | 1280px | Desktops |
| `2xl` | 1536px | Large desktops |

Desktop-first. The stat tracking interface is designed for desktop/laptop use where users have screen space for video and stat panel side by side. The marketing site and dashboards should be responsive but prioritize the desktop experience. Mobile layouts should work but are secondary.

---

## Border Radius

| Token | Value | Usage |
|-------|-------|-------|
| `--radius-sm` | 4px | Small chips, tags, badges |
| `--radius-md` | 8px | Buttons, inputs, small cards |
| `--radius-lg` | 12px | Cards, panels, modals |
| `--radius-xl` | 16px | Large cards, hero sections |
| `--radius-full` | 9999px | Avatars, circular buttons, pills |

Keep it consistent. Most UI elements use radius-md (8px). Cards use radius-lg (12px). Do not mix rounded corners sizes within the same component.

---

## Shadows

Dark mode uses subtle shadows. Light mode uses more pronounced shadows for elevation.

| Token | Value (Dark Mode) | Value (Light Mode) |
|-------|-------------------|-------------------|
| `--shadow-sm` | 0 1px 2px rgba(0,0,0,0.3) | 0 1px 2px rgba(0,0,0,0.05) |
| `--shadow-md` | 0 4px 6px rgba(0,0,0,0.4) | 0 4px 6px rgba(0,0,0,0.07) |
| `--shadow-lg` | 0 10px 15px rgba(0,0,0,0.5) | 0 10px 15px rgba(0,0,0,0.1) |
| `--shadow-xl` | 0 20px 25px rgba(0,0,0,0.5) | 0 20px 25px rgba(0,0,0,0.1) |

In dark mode, rely more on background color changes for elevation than shadows. A lighter navy (#1A2942) on top of the base navy (#0F1B2D) communicates elevation without heavy shadows.

---

## Iconography

Use Lucide icons (lucide.dev) as the primary icon set. They are clean, consistent, open source, and work well at small sizes.

| Property | Value |
|----------|-------|
| Default size | 20px (w-5 h-5) |
| Small size | 16px (w-4 h-4) |
| Large size | 24px (w-6 h-6) |
| Stroke width | 2px (default) |
| Color | Inherits text color |

For sport-specific icons (basketball, soccer ball, etc.), create a custom set using simple filled shapes on the navy/lime palette. Keep them geometric and minimal.

---

## Component Patterns

### Buttons

**Primary (CTA):**
- Dark mode: Electric Lime background, Deep Navy text, bold weight
- Light mode: Deep Navy background, white text
- Hover: Slightly darker shade (lime-dark or navy-light)
- Padding: 12px 24px (py-3 px-6)
- Border radius: radius-md (8px)
- Font: text-base, weight 600
- Uppercase for short labels (TRACK, SYNC, EXPORT). Sentence case for longer labels.

**Secondary:**
- Dark mode: Transparent with slate border, white text
- Light mode: Transparent with slate border, navy text
- Hover: Subtle background fill
- Same padding and radius as primary

**Ghost:**
- No border, no background
- Text color only, with hover underline or subtle background
- Use for tertiary actions, inline links in dense UI

**Destructive:**
- Signal Red background, white text
- Use sparingly: delete team, remove player, cancel subscription

### Cards

- Dark mode: #1A2942 background, #334155 border (1px), radius-lg, shadow-sm
- Light mode: #FFFFFF background, #E2E8F0 border (1px), radius-lg, shadow-md
- Padding: 24px (p-6)
- Always have a clear content hierarchy: title, subtitle/meta, body, actions

### Forms and Inputs

- Height: 44px minimum (touch-friendly)
- Dark mode: #1A2942 background, #334155 border, white text, slate placeholder
- Light mode: #FFFFFF background, #E2E8F0 border, navy text, slate placeholder
- Focus state: Electric Lime border (2px), subtle lime glow
- Error state: Signal Red border, red error text below
- Border radius: radius-md (8px)
- Padding: 12px horizontal

### Navigation

**Sidebar (app):**
- Deep Navy background
- Active item: Electric Lime left border accent (3px), slightly lighter navy background
- Icons + text labels
- Collapsible on mobile to bottom tab bar

**Top bar (marketing site):**
- Transparent on hero, transitions to navy on scroll
- Logo left, nav links center or right, CTA button far right

### Tables and Data

- Use JetBrains Mono for all numeric data in tables
- Alternating row backgrounds: base navy and navy-light in dark mode
- Header row: Bold, slightly smaller text, uppercase, wider letter spacing
- Cell padding: 12px vertical, 16px horizontal
- Horizontal dividers only (no vertical cell borders for cleaner look)
- Sortable columns get a subtle chevron icon

### Live Game Indicators

- Pulsing red dot (Signal Red) with animation for live games
- "LIVE" badge: Signal Red background, white text, radius-sm, uppercase, text-xs
- Animation: CSS pulse keyframe, subtle scale from 1 to 1.15 and back, 2-second loop

```css
@keyframes pulse-live {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.7; transform: scale(1.15); }
}
```

### Stat Tracking Buttons (Courtside UI)

These are the most important interactive elements in the entire app. They need to be large, easy to tap, and impossible to mis-tap.

- Minimum touch target: 48px x 48px (preferably larger, 56-64px)
- Clear visual distinction between stat types (color-coded or icon-coded)
- Active/pressed state: immediate visual feedback (scale down slightly, color change)
- Undo: always accessible, prominent, forgiving. Users will mis-tap. Make undo effortless.
- Spacing between buttons: minimum 8px gap to prevent mis-taps
- Group related stats visually (offensive stats, defensive stats, etc.)

---

## Motion and Animation

Keep it fast and functional. This is a sports app, not a portfolio site.

| Property | Duration | Easing |
|----------|----------|--------|
| Hover states | 150ms | ease-out |
| Panel transitions | 200ms | ease-in-out |
| Modal open/close | 250ms | ease-out |
| Page transitions | 300ms | ease-in-out |
| Data loading skeletons | 1.5s loop | ease-in-out |
| Live pulse animation | 2s loop | ease-in-out |

Rules:
1. No animation should be longer than 300ms except looping indicators.
2. Reduce motion for users who prefer it (prefers-reduced-motion media query).
3. Stat tracking UI should feel instant. No transition delays on tap-to-track buttons.
4. Loading states use skeleton screens, not spinners, wherever possible.

---

## Tailwind Configuration

Here is the base Tailwind config to align with this design system. Extend as needed but do not override these foundational values.

```javascript
// tailwind.config.js
const defaultTheme = require('tailwindcss/defaultTheme')

module.exports = {
  darkMode: 'class',
  content: [
    './src/**/*.{js,ts,jsx,tsx}',
    './app/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {
      colors: {
        navy: {
          DEFAULT: '#0F1B2D',
          800: '#1A2942',
          700: '#253754',
        },
        lime: {
          DEFAULT: '#BFFF00',
          dark: '#99CC00',
          muted: '#BFFF0033',
        },
        slate: {
          50: '#F8FAFC',
          100: '#F1F5F9',
          200: '#E2E8F0',
          300: '#CBD5E1',
          500: '#64748B',
          700: '#334155',
          900: '#0F172A',
        },
        alert: '#EF4444',
        success: '#22C55E',
        warning: '#F59E0B',
      },
      fontFamily: {
        sans: ['Inter', ...defaultTheme.fontFamily.sans],
        mono: ['JetBrains Mono', ...defaultTheme.fontFamily.mono],
      },
      fontSize: {
        'stat': ['3.75rem', { lineHeight: '1' }],
      },
      borderRadius: {
        sm: '4px',
        md: '8px',
        lg: '12px',
        xl: '16px',
      },
      animation: {
        'pulse-live': 'pulse-live 2s ease-in-out infinite',
      },
      keyframes: {
        'pulse-live': {
          '0%, 100%': { opacity: '1', transform: 'scale(1)' },
          '50%': { opacity: '0.7', transform: 'scale(1.15)' },
        },
      },
    },
  },
  plugins: [],
}
```

---

## Logo Guidelines

Until a final logo is designed, use the wordmark "SnapStats" set in Inter ExtraBold with these rules:

- "Snap" in Electric Lime, "Stats" in White (on dark backgrounds)
- "Snap" in Deep Navy, "Stats" in Cool Slate (on light backgrounds)
- Always one word, no space: SnapStats (capital S, capital S)
- Minimum size: 24px font height
- Clear space around the wordmark: minimum 1x the height of the "S" on all sides

**App icon direction:**
- Simple geometric mark that works at 1024px and 16px
- Suggested concept: Abstract upward-trending pulse line or stat bar chart
- Colors: Electric Lime mark on Deep Navy background
- No text in the app icon (it won't be legible at small sizes)

---

## Writing Style in the UI

- Lead with verbs: Track, Sync, Review, Export, Invite, Create
- Short sentences. Active voice. No jargon.
- Button labels: 1-2 words preferred. "Start Tracking" not "Click here to begin tracking stats"
- Error messages: Say what happened and what to do. "Couldn't save. Check your connection and try again." Not "Error 500."
- Empty states: Encouraging, not blank. "No games yet. Create your first game to get started."
- Confirmation dialogs: Be specific. "Delete this game? Stats and film links will be removed. This can't be undone." Not "Are you sure?"
- Use "you" and "your team." Never "the user" or "our customers."
- Sport terms are fine (roster, assist, turnover). Tech terms are not (sync conflict, webhook, payload).

---

## Image and Media Direction

- Photography style: Real game moments, coaches reviewing film on laptops, video review sessions. Not stock photo perfection. Gritty, authentic, in-the-moment.
- Avoid: Posed team photos, overly polished studio shots, corporate imagery.
- Screenshots: Use dark mode app screenshots as the default for marketing. They look better and match the brand.
- Video: Short, punchy demo clips. Show the tap-to-track flow in real time. 15-30 seconds max for social clips.
- Illustrations: Minimal. If needed, use simple geometric line illustrations in lime on navy. Not cartoon-style.

---

## Accessibility

- All text must meet WCAG 2.1 AA contrast ratios (4.5:1 for normal text, 3:1 for large text).
- Electric Lime (#BFFF00) on Deep Navy (#0F1B2D) passes AA for large text. Verify all combinations.
- Never use color alone to convey information. Pair with icons, labels, or patterns.
- All interactive elements need visible focus states (lime outline).
- Touch targets: 44px minimum, 48px recommended.
- Support prefers-reduced-motion and prefers-color-scheme media queries.
- Alt text on all images. Aria labels on all icon-only buttons.
- Keyboard navigable: every action reachable without a mouse.

---

## File Naming Conventions

- Components: PascalCase (GameCard.tsx, StatButton.tsx)
- Utilities: camelCase (formatStat.ts, useGameTimer.ts)
- Pages/routes: kebab-case (game-detail, player-profile)
- Assets: kebab-case with descriptors (icon-basketball.svg, hero-film-review.jpg)
- CSS/style files: Match component name (GameCard.module.css)

---

## Quick Reference: Do and Don't

**Do:**
- Default to dark mode in the app
- Use lime sparingly as an accent, never as a background fill for large areas
- Make tap targets huge on the tracking UI
- Show stats in monospace
- Keep the UI fast and minimal, every second matters during video review
- Support undo everywhere in the tracking flow
- Write like a coach talks, not like a software company markets

**Don't:**
- Use serif or decorative fonts anywhere
- Use red for anything other than live indicators, errors, and fouls
- Add animations that slow down the tracking experience
- Put lime text on light backgrounds (contrast failure)
- Use "revolutionary," "disruptive," "game-changing," or similar startup buzzwords
- Make the parent volunteer feel like they need a training course to use this
- Forget that long video review sessions need comfortable, low-strain UI

---

*Last updated: February 2026*
*Version: 1.0*
*Brand: SnapStats (snapstats.app)*
