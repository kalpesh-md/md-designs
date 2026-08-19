# Design Pattern Research — MoodScale Portal Redesign

Reference sources: [Mobbin](https://mobbin.com/) pattern library conventions and the
[Mental Health Counseling Dashboard](https://project-mental-health-counseling-dashboard-106.magicpatterns.app) reference,
analyzed against the current state of the three MoodScale portals.

---

## 1. Current State Audit (what "feels immature" and why)

| Problem | Where it shows up | Design principle violated |
|---|---|---|
| Flat, undifferentiated cards — every card same size, same weight | Admin & therapist dashboards | No visual hierarchy; the eye has nowhere to land first |
| Hardcoded hex accent colors per nav section (7 different hues) | Client portal header | No cohesive palette; colors compete instead of guiding |
| Headings referenced (Playfair/Raleway) but never loaded — falls back to Inter everywhere | Client portal | Typography hierarchy collapses to one font at different sizes |
| Dense 1000+ line hero with competing animations | Client landing `HeroSection` | Decoration over clarity; slow first paint |
| Default shadcn styling with no brand personality | Admin & therapist | Portals look like an unstyled template |
| No consistent spacing rhythm (mix of p-4, p-6, arbitrary margins) | All three | Layouts feel "off" without users knowing why |
| Splash page (admin) / hard redirect (therapist) as home | Admin & therapist `page.tsx` | Missed opportunity for orientation and status-at-a-glance |

---

## 2. Mobbin Patterns Selected for Adoption

These are the seven patterns from top apps on Mobbin (Headspace, Calm, Notion, Linear,
Stripe Dashboard archetypes) most applicable to MoodScale.

### 2.1 The "Bento Grid" dashboard
- Mixed-size cards on a strict grid: one 2x2 hero metric card, several 1x1 support cards.
- Creates instant hierarchy — the most important number is physically the biggest.
- Adopted in: Admin Design A ("Command Center"), Therapist Design B.

### 2.2 Generous-whitespace minimal cards
- Cards defined by whitespace and a 1px hairline border, not heavy shadows.
- Shadow only on hover/interaction (elevation = affordance, not decoration).
- Adopted in: all Design A variants.

### 2.3 Progressive disclosure
- Show 3 items + "View all" instead of a 20-row table.
- Expandable sections with chevron affordance; details live one click away.
- Adopted in: Therapist Design C ("Task-Oriented"), Admin Design B.

### 2.4 Status pills and micro-feedback
- Small rounded pills with a dot indicator (● Confirmed, ● Pending, ● Cancelled).
- Semantic color used only in the pill, never as the whole card background.
- Adopted in: every dashboard variation.

### 2.5 Avatar-first list rows
- People-centric rows: avatar, name, one line of metadata, one action — nothing more.
- Fits therapy context: sessions and clients are people, not table rows.
- Adopted in: Therapist all variants, Admin activity feeds.

### 2.6 Greeting + context header
- "Good morning, Dr. Mehta — you have 4 sessions today" replaces a generic "Dashboard" H1.
- Warmth + immediate orientation in one line.
- Adopted in: Therapist and Client dashboards, all variants.

### 2.7 Sparkline-in-card metrics
- KPI cards carry a tiny 30-day trend line and a delta chip (+12%), not just a static number.
- Answers "is this good?" without opening a report.
- Adopted in: Admin Designs B and C.

---

## 3. Mental Health / Wellness Design Principles

Drawn from wellness-category leaders (Headspace, Calm, Wysa) and the counseling dashboard reference.

1. **Calm color, low saturation.** Full-saturation blues/reds read as "corporate alert."
   Wellness products desaturate 10–20% and warm the neutrals (stone/sand instead of pure gray).
2. **Soft geometry.** Larger corner radii (12–20px), pill buttons, rounded avatars.
   Sharp corners read as clinical; soft corners read as safe.
3. **One emotional accent.** A single warm accent (sage, teal, or peach) used sparingly
   for moments of encouragement — streaks, progress, positive deltas.
4. **Type warmth.** A humanist serif or rounded sans for display headings paired with a
   clean grotesque for UI. (Current stack intends Playfair + Inter — the intent is right,
   the loading is broken.)
5. **Slow, gentle motion.** 300–400ms ease-out transitions; nothing bounces or flashes.
   Motion should feel like breathing, not notification.
6. **Never alarm without action.** Red only when the user can immediately act on it.
   "Low mood trend" is shown in amber with a supportive tone, not red with a warning icon.
7. **Readable body text.** 16px minimum body, 1.6 line-height, 65–75ch measure on prose.

---

## 4. Accessibility Baseline (applies to all 9 designs)

- WCAG AA contrast: 4.5:1 body text, 3:1 large text and UI borders.
- Focus rings visible on every interactive element (2px offset ring in accent color).
- Semantic status never conveyed by color alone (dot + label text in every pill).
- Touch targets ≥ 44px on mobile layouts.
- `prefers-reduced-motion` disables all decorative animation.

---

## 5. How the 3x3 Variation Matrix Uses This Research

| | Variation A | Variation B | Variation C |
|---|---|---|---|
| **Personality** | Minimal, editorial | Warm, immersive | Dense, data-confident |
| **Mobbin patterns** | 2.2, 2.4, 2.6 | 2.1, 2.5, 2.6 | 2.3, 2.7, 2.4 |
| **Palette** | Modern Cool (refined brand blue) | Warm Wellness (sage/teal) | Professional Depth (brand navy) |
| **Risk profile** | Safest, fastest to build | Most differentiated brand | Best for power users |

Each column keeps the *same theme DNA* (MoodScale blue/navy/green heritage) but treats it
differently — per the decision to compare three color treatments side by side.
