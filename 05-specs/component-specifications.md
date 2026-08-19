# Component Specifications & Implementation Notes

How each of the 9 designs maps to the existing codebases. All three portals already ship
shadcn/ui + Radix + Framer Motion + TanStack Query, so most of this is styling and
composition work, not new dependencies.

---

## 0. Prerequisites (one-time, before any variation is built)

| Task | Where | Notes |
|---|---|---|
| Load Fraunces + keep Inter | All 3 `layout.tsx` | `next/font/google`; fixes the broken Playfair/Raleway references in `md-latest/tailwind.config.ts` |
| Add shared tokens | All 3 `globals.css` | Port [tokens.css](../02-tokens/tokens.css) values into Tailwind v4 `@theme` (admin/therapist) and CSS vars (client, until Tailwind v4 upgrade) |
| Decide palette | — | Layouts and palettes are independent; any A/B/C layout can wear any palette by swapping the token block |

---

## 1. Shared primitives (used by all 9 designs)

### StatusPill
- Composition: existing shadcn `Badge` restyled — pill radius, dot span, semantic tint tokens.
- Variants: `success | warning | danger | info | brand`. Dot is mandatory (a11y: never color-only).
- Tailwind: `inline-flex items-center gap-1.5 rounded-full px-3 py-1 text-xs font-semibold`.

### StatCard
- Props: `label`, `value`, `delta?`, `icon?`, `sparkline?`.
- Structure: uppercase 12px label (ink-tertiary) → 36px semibold value → delta StatusPill.
- Base: shadcn `Card` with `rounded-2xl border shadow-none hover:shadow-lg transition-shadow duration-300`.

### AvatarRow (list row for people)
- avatar (initials fallback via existing shadcn `Avatar`) + name/meta stack + right slot (pill or button).
- Hover: `hover:bg-[--brand-soft]`, 150ms.

### SectionHeading (landing)
- Small uppercase tracked label + Fraunces H2 (`font-display text-4xl`).

### Buttons
- Restyle shadcn `Button`: `rounded-full`, primary = `bg-[--brand] hover:bg-[--brand-strong] hover:-translate-y-px hover:shadow-lg`, 150ms `ease-[cubic-bezier(0.25,0.6,0.3,1)]`.

---

## 2. Client portal (`md-latest`)

Current `src/app/page.tsx` composes ~10 section components; each design replaces that composition.

### Design A — Modern Minimalist
| Piece | Reuse | New |
|---|---|---|
| Nav | Existing `Header.tsx` simplified | Remove per-section hex accents; hairline border + blur |
| Hero | — | New `HeroMinimal` (centered, max-w-[800px]); replaces the ~1000-line `HeroSection` |
| Services grid | Existing `ServiceSection` data | `ServiceCardMinimal` (icon tile + 2-line copy + ghost link) |
| Steps | — | `HowItWorksSteps` — numbered circles + hairline connector |
| Therapist cards | Existing therapist query | `TherapistCardMinimal` + availability StatusPill |
- Effort: **smallest**. Mostly deletion + restyle. Framer Motion: fade-up on scroll only (`whileInView`, 300ms, stagger 80ms).

### Design B — Immersive Wellness
- New `HeroImmersive`: CSS blob backgrounds (`border-radius` morph keyframes, 12s loops, `will-change: transform`, disabled under `prefers-reduced-motion`).
- New `FloatingProductCard` (3 instances: mood check-in, session, streak) — absolute positioned, Framer Motion float variants with staggered delays.
- New `JourneyTimeline`: center dashed SVG path + alternating cards, `whileInView` reveal.
- Overlapping service cards: negative margins + `hover:z-10 hover:rotate-0` transitions.
- Effort: **largest** for client; the floating cards should reuse real dashboard card markup so marketing matches product.

### Design C — Data-Driven Clarity
- New `OutcomeChart`: Recharts `LineChart` (add recharts to md-latest, or inline SVG as in mockup) with anonymized PHQ-9 trend.
- New `ComparisonTable`: static table, brand-soft highlighted column, `overflow-x-auto` on mobile.
- New `TrustStrip`, `SegmentedCTAs` (3 cards, distinct hrefs for individual/couples/corporate funnels).
- Effort: medium. Content dependency: real stats and certifications must be verified before launch.

---

## 3. Therapist portal (`md-therapist`)

Replaces `src/app/therapist/dashboard/page.tsx` content inside the existing `TherapistLayoutClient` shell.

### Design A — Professional Dashboard
- 4× `StatCard` grid (`grid-cols-2 lg:grid-cols-4`).
- `TodaysSessions` card: `AvatarRow` list; next-up row gets inline Join `Button` (session join URL already exists in sessions service).
- `QuickActions` (3 ghost buttons), `PendingItems` (compact warning rows).
- Data: existing TanStack Query hooks for sessions/clients cover everything; pending-notes count may need one new endpoint aggregation.

### Design B — Engagement-Focused
- `BentoGrid`: CSS grid `grid-cols-4 auto-rows-[140px]`, hero cell `col-span-2 row-span-2`; collapses to single column under `lg`.
- Cells: `TodaysFocusCell` (next session, gradient bg), `SparklineCell` (inline SVG or Recharts `Tiny` area), `StreakCell` (accent-soft bg), `MilestoneCell`, `CheckinChipsRow`.
- New data needs: client check-in events and streak computation — confirm these exist before choosing this design.

### Design C — Task-Oriented
- `ScheduleTimeline`: vertical list of `TimeBlockCard`s with 4px colored left border by session type; free-time spacer rows computed from gaps between sessions.
- Hover quick-actions: `opacity-0 group-hover:opacity-100` icon buttons (Join / Notes / Reschedule).
- Right rail: 3 collapsible sections — use existing shadcn `Collapsible` (Radix) with chevron rotate 150ms; "Clients needing attention" driven by assessment-score deltas (needs a `score_delta` query on assessments).
- Segmented Day/Week/Month control: shadcn `Tabs` restyled to pill segment.

---

## 4. Admin portal (`md-admin-02-Nov-2025`)

Replaces `src/app/admin/dashboard/page.tsx` inside `AdminLayoutClient`. Also: replace the
decorative splash at `src/app/page.tsx` with a redirect to login (mirror therapist portal).

### Design A — Command Center
- 8× `StatCard` (`grid-cols-2 xl:grid-cols-4`).
- `SystemHealthStrip`: slim card, 5 inline service statuses — needs a `/api/health` aggregate endpoint (new).
- `AlertCard` (warning/info variants, colored left border), `ActivityFeed` (`AvatarRow` + type icons), `TopTherapists` (ranked rows + relative volume bar `div` widths).

### Design B — Focused Metrics
- `NeedsAttentionCard`: 3 rows, one action button each — the queries (pending approvals, incidents, refund requests) all exist in current admin services.
- 4× `StatCard` with `sparkline` prop — Recharts `AreaChart` 40px tall, no axes.
- `EventTimeline`: dot+line vertical list; severity dot colors from status tokens.
- Layout: **no sidebar** — this variation uses a top navbar + 960px centered column; implement as an alternate layout branch or keep the sidebar and center the content (decide at implementation).

### Design C — Visual Analytics
- Hero `DualLineChart` (12-month sessions + revenue): Recharts `ComposedChart`, gradient `Area` fills, annotation label on peak month.
- `FunnelChart`: horizontal CSS bars with width % + conversion labels (simpler and more legible than a Recharts funnel).
- `DonutChart`: Recharts `PieChart` innerRadius, center label total.
- `Gauge` ×3: SVG arc with `stroke-dasharray` (as in mockup) — small reusable component.
- Effort: **largest** admin option; Recharts and Tremor are already dependencies, so no new packages.

---

## 5. Motion spec (all designs)

| Interaction | Duration | Easing |
|---|---|---|
| Button/row hover | 150ms | gentle cubic-bezier(0.25, 0.6, 0.3, 1) |
| Card hover lift | 300ms | gentle |
| Scroll-reveal (landing) | 300ms, 80ms stagger | gentle, `whileInView` once |
| Collapsible expand | 200ms | ease-out |
| Decorative blobs/floats (Client B) | 8–12s loops | ease-in-out |
| Skeleton shimmer | 1.5s loop | linear |

All decorative motion gated behind `prefers-reduced-motion: no-preference`.

## 6. Responsive breakpoints

- 375px: single column, sidebars hidden (existing mobile drawer patterns reused), touch targets ≥ 44px.
- 768px: 2-col grids, sidebar as drawer.
- 1024px+: full sidebar, 3–4 col grids.
- 1440px: max content width 1280px (dashboards) / 1200px (landing), centered.

## 7. Suggested build order (post-approval)

1. Prerequisites (fonts + tokens) — half day.
2. One dashboard variation (therapist or admin) to validate tokens in real code — 1–2 days.
3. Client landing variation — 2–3 days (B is +1 day over A/C).
4. Remaining portal — 1–2 days.
