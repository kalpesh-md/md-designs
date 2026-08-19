# Design Rationale — 9 Variations Across 3 Portals

Each portal gets three variations that share the same layout skeleton conventions and the
same token system ([../02-tokens/design-tokens.md](../02-tokens/design-tokens.md)) but explore
a different personality and palette:

- **Variation A · Palette A "Modern Cool"** — safest, most conventional modern SaaS look
- **Variation B · Palette B "Warm Wellness"** — most emotionally differentiated, wellness-first
- **Variation C · Palette C "Professional Depth"** — most premium/data-confident, navy heritage

Open [../03-mockups/index.html](../03-mockups/index.html) in a browser to compare all nine.

---

## Client Portal (landing page)

### A — "Modern Minimalist"
- **Thesis:** the current landing crams 10 sections, 7 accent colors, and heavy animation
  into the first scroll. Design A removes everything that doesn't drive the two conversions
  that matter (book a session / take assessment).
- **Mobbin patterns used:** minimal hairline cards (2.2), greeting-free centered hero,
  status pills for therapist availability (2.4).
- **Key improvements over current:** one accent color instead of seven; Fraunces display serif
  finally delivers the serif-heading intent that Playfair was supposed to provide; 96px section
  rhythm replaces inconsistent spacing; trust markers moved directly under the hero CTA where
  decision anxiety is highest.
- **Color psychology:** refined blue keeps the existing brand recognition while desaturating
  the "corporate alarm" edge of the current `hsl(221 83% 53%)`.
- **Risk:** lowest. Closest to current brand, fastest to implement.

### B — "Immersive Wellness"
- **Thesis:** MoodScale is a mental-health product but the current site looks like a booking
  SaaS. Design B makes the *feeling* the product: soft organic motion, layered floating cards
  showing the actual in-product experience (mood check-in, session card, streak).
- **Mobbin patterns used:** overlapping depth cards (2.1 adapted), avatar-first session
  preview (2.5), emotional journey timeline.
- **Key improvements:** the floating product cards *show* the app instead of describing it;
  the journey timeline reframes therapy from "transaction" to "progression"; sage green
  inherits the therapist portal's green heritage, unifying brand across portals.
- **Color psychology:** sage + warm stone reads calm and organic; the peach accent is
  reserved exclusively for encouragement moments (streaks, milestones) so it stays meaningful.
- **Risk:** highest visual ambition; needs care to keep animation subtle (all motion ≤ gentle
  12s float loops, honors `prefers-reduced-motion`).

### C — "Data-Driven Clarity"
- **Thesis:** the biggest conversion blocker for first-time therapy users in India is
  skepticism. Design C answers it with proof: outcome charts, credentials, comparison table,
  verified reviews.
- **Mobbin patterns used:** sparkline/chart-in-card (2.7), trust strip, segmented CTAs.
- **Key improvements:** the anonymized PHQ-9 outcome chart in the hero is a claim no
  competitor's landing makes; the comparison table converts "why not offline therapy?"
  objections directly; segmented CTAs stop forcing individuals, couples, and companies
  through one funnel.
- **Color psychology:** existing brand navy at AAA contrast signals institutional
  trustworthiness; violet accent kept strictly for data highlights.
- **Risk:** medium — needs real (anonymizable) outcome data to be honest.

---

## Therapist Portal (dashboard)

### A — "Professional Dashboard"
- **Thesis:** therapists are professionals mid-workday; the dashboard should read like a
  well-organized desk. Metrics → today's sessions → pending work, in strict priority order.
- **Mobbin patterns used:** greeting + context header (2.6), avatar-first rows (2.5),
  status pills (2.4), minimal stat cards (2.2).
- **Key improvements over current:** the greeting line answers "what does today look like?"
  in one sentence; the next-up session gets an inline Join button (currently buried);
  pending notes get a due-date warning pill instead of hiding in a subpage.

### B — "Engagement-Focused"
- **Thesis:** therapy is emotionally taxing work; the dashboard can reflect impact back to
  the therapist. Bento grid celebrates progress (streaks, milestones, client mood trends)
  without becoming a game.
- **Mobbin patterns used:** bento grid (2.1), sparkline cells (2.7), mood-dot check-in chips.
- **Key improvements:** "Today's focus" cell kills the scan-the-whole-table problem — the
  single next session is physically the largest thing on screen; client check-in chips give
  a between-session signal the current portal has nowhere to surface.
- **Gamification restraint:** streaks and milestones are informational, never pressuring —
  no loss-aversion mechanics (deliberate ethical choice for a clinical tool).

### C — "Task-Oriented"
- **Thesis:** a therapist's day is a timeline, not a table. The schedule *is* the interface;
  everything else collapses behind progressive disclosure.
- **Mobbin patterns used:** progressive disclosure (2.3), time-block timeline, contextual
  hover actions, color-coded session types.
- **Key improvements:** free time between sessions becomes visible (helps note-writing
  planning); "Clients needing attention" surfaces rising PHQ-9 scores proactively — clinical
  value the current dashboard doesn't attempt; collapsed sections keep density without noise.

---

## Admin Portal (dashboard)

### A — "Command Center"
- **Thesis:** an admin's first question is "is everything okay and what changed?" Eight KPIs,
  system health, and alerts answer it in one screen without scrolling.
- **Key improvements over current:** current admin home is a decorative splash page — this
  replaces it with an actual overview; system health strip and incident alerts don't exist
  anywhere in the current UI; deltas on every KPI replace bare numbers.

### B — "Focused Metrics"
- **Thesis:** dashboards fail when everything shouts. Design B is the anti-overload option:
  a single 960px column that literally tells you "3 items need your attention" and puts
  those three first with one action each.
- **Mobbin patterns used:** needs-attention card pattern, sparkline metrics (2.7),
  event timeline, quick-action row.
- **Key improvements:** decision fatigue drops — the admin reads top-to-bottom once and is
  done; only 4 metrics, each with a 30-day sparkline so "is this good?" needs no report.

### C — "Visual Analytics"
- **Thesis:** for an admin making growth decisions, trends matter more than snapshots.
  Chart-first layout: 12-month dual-line hero, acquisition funnel, revenue donut,
  health gauges.
- **Key improvements:** the acquisition funnel (visited → signed up → assessed → first
  session → retained) makes the platform's leaky bucket visible for the first time;
  gauges compress uptime/quality/NPS into glanceable arcs.
- **Risk:** heaviest to implement (chart work); best paired with Recharts already present
  in the admin portal's dependencies.

---

## Accessibility notes (all 9)

- All body text ≥ 16px, all palettes AA-checked (Palette C brand is AAA at 10.4:1).
- Status pills always pair a dot with a text label — never color alone.
- Every interactive element has a visible 2px focus ring.
- All decorative animation is disabled under `prefers-reduced-motion`.

## Recommendation

If choosing one direction today: **Client B (Immersive Wellness), Therapist A or C,
Admin B** — this pairs the most differentiated public face with the most workmanlike
internal tools. But the palette can be mixed independently of the layout: any layout can
be re-skinned to any of the three palettes in minutes because everything runs on tokens.
