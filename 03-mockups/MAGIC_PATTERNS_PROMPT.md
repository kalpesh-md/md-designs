# Magic Patterns prompt — MoodScale client Home + Bookings

Copy this into Magic Patterns chat. Attach the repo (or these subfolders) first.

## Setup in Magic Patterns (do this once)

1. Open the editor → **+** → **Connect Github**.
2. Attach this repo. Narrow folders so the agent stays focused:
   - `md-latest/src` — live client product (existing dashboard, booking widgets, retreats)
   - `design-explorations/02-tokens` — navy `#1E3A5F`, mid `#2D5A8B`, sky `#0EA5E9`, emerald
   - `design-explorations/03-mockups` — **this is the restructure to restyle**
3. Optional: screenshot `client-a-modern-minimalist.html` and `client-a-bookings.html` in a browser and attach the images.
4. Work **one page at a time**. Use **Select Mode** (⌥ + S) on a single card. Use `/Polish` after each pass. Do **not** ask it to redesign the whole product in one prompt.

Magic Patterns generates a **high-fidelity prototype**. It reads your code for look-and-feel. It does not write to the repo. Treat the output as a design spec, then we port the look back into these HTML mockups / `md-latest`.

---

## Prompt 1 — Home (paste first)

Keep the same pages and the same blocks. You **may reshape each component** — layout inside the card, hierarchy, typography, illustration, motion, chip/button treatment — to make it more attractive and easier to use. Do not invent new product features or move Bookings widgets onto Home.

**Pages to keep:**
- Home = `design-explorations/03-mockups/client-a-modern-minimalist.html` (also B and C variants)
- Bookings = `design-explorations/03-mockups/client-a-bookings.html` (do Bookings in a later prompt)

**Live product to match visually:** `md-latest/src/app/(protected)/dashboard/page.tsx` and cards in `md-latest/src/components/dashboard/` — rounded-2xl white cards, `shadow-[0_2px_8px_rgba(0,0,0,0.08)]`, navy `#1E3A5F` primary buttons, Inter, pill status badges.

**Home must keep these blocks in this order of importance:**
1. Greeting (“Good morning, {name}” + date)
2. Upcoming appointment — therapist avatar, name, specialty, date/time, video, 50 min, countdown, Join + Reschedule + Add to calendar, later-this-week row
3. MoodSync check-in — 8 moods: happy, focused, calm, low, anxious, stressed, excited, tired + optional note + “Share with my therapist”
4. Check-in streak (7-day dots)
5. Mood this week (7 coloured bars by mood type)
6. Wellness snapshot — mood score, sleep hours, steps + last Spotify track + “Open MoodSync”

**Do not add** booking widgets on Home (earliest slots, assessments, book-with-therapist, AI match, nature retreats). Those live on Bookings.

**Visual direction:** Calm clinical SaaS, not generic emoji dashboard. Generous whitespace, hairline borders, soft shadow. Upcoming session is the visual hero. Mood chips should feel tactile. Streak uses a warm peach/orange accent only for encouragement. Keep brand navy `#1E3A5F`. You may reshape cards (split, stack, bento, hero, compact) if it reads better — as long as every listed block is still present.

Style Design A first (clean 2-column). Then apply the same components to Design B (bento / gradient hero) and Design C (compact 70/30) without changing content.

---

## Prompt 2 — Bookings (after Home looks good)

Keep the same widgets. You **may reshape each widget** to look more attractive. Do not replace them with generic “booking option” cards or invent new booking types.

**Keep these blocks:**
1. AI match banner (“Find Your Perfect Therapist”) — reference idle state in `md-latest/src/app/(protected)/dashboard/page.tsx`
2. Earliest Booking — date chips + pager + time chips (same behaviour as live dashboard)
3. Quick Assessment — BFI-10 / GAD-7 / PHQ-9 FREE vs PREMIUM tiles
4. Book with a Therapist — therapist cards with avatar, spec, video/phone pills, rating, match reason, “View availability”
5. Nature Retreats — latest 3 (cover, category, location, date, price onwards) + View all → `/dashboard/retreats`

**Visual direction:** Same tokens as Home. Date chip selected = navy border + brand-soft fill. Therapist cards should feel premium on hover. Retreat covers can be richer (photo, overlay, taller crop). Reshape freely inside each widget. Do not drop any of the five blocks.

---

## Prompting rules (Magic Patterns docs)

- Be specific: name the component (“upcoming appointment card”), not “make it nicer”.
- Select Mode on one card, then prompt that card.
- `/Polish` for spacing/alignment after a pass.
- `/Inspiration` only if you want 4 visual alternatives of **one** component.
- Fork or restore if it starts changing structure.
- Attach a screenshot of the current HTML mockup as the starting point.
