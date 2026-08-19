# MoodScale Shared Design Token System

Single source of truth for all 9 design variations. Implemented in [tokens.css](tokens.css)
(used directly by the HTML mockups) and designed to translate 1:1 into Tailwind v4
`@theme` variables during implementation.

---

## 1. Color Palettes (3 options for comparison)

All three palettes derive from the **existing MoodScale theme DNA** — brand blue
`hsl(221 83% 53%)`, navy `#1e3a5f`, and the therapist portal's green `rgba(55,120,90)` —
so whichever is chosen, the brand stays recognizable.

### Palette A — "Modern Cool" (applied to all Design A variants)

| Token | Value | Role |
|---|---|---|
| `--brand` | `#3b6fe0` | Primary actions, links. Refined (slightly desaturated) current brand blue |
| `--brand-strong` | `#2854b8` | Hover / pressed |
| `--brand-soft` | `#e8effc` | Selected states, soft badges |
| `--accent` | `#0ea5a4` | Teal secondary highlight |
| `--bg` / `--surface` | `#f7f8fa` / `#ffffff` | Page / card |
| `--ink` → `--ink-tertiary` | `#101828` → `#98a2b3` | 3-step text hierarchy |

Contrast check: brand on white 4.6:1 (AA), ink on bg 15.9:1.

### Palette B — "Warm Wellness" (applied to all Design B variants)

| Token | Value | Role |
|---|---|---|
| `--brand` | `#37785a` | Sage green — from existing therapist accent |
| `--brand-strong` | `#285c44` | Hover / pressed |
| `--accent` | `#e8a87c` | Warm peach — encouragement moments only (streaks, progress) |
| `--bg` | `#faf9f7` | Warm stone, not pure gray |
| `--ink` | `#1f2a24` | Green-tinted near-black |

Contrast check: brand on white 4.9:1 (AA), ink on bg 14.8:1.

### Palette C — "Professional Depth" (applied to all Design C variants)

| Token | Value | Role |
|---|---|---|
| `--brand` | `#1e3a5f` | Existing `--ms-navy`, unchanged |
| `--brand-strong` | `#152a45` | Existing `--ms-navy-dark` |
| `--accent` | `#7c6ee6` | Violet — analytics/chart highlights |
| `--bg` | `#f4f6f8` | Cool light gray |

Contrast check: brand on white 10.4:1 (AAA).

### Semantic status colors (identical in all palettes)

Success `#16a34a` · Warning `#d97706` · Danger `#dc2626` · Info `#2563eb`,
each with a matching `-bg` tint. Status is always shown as **dot + label pill**, never color alone.

---

## 2. Typography

| Role | Font | Rationale |
|---|---|---|
| Display / hero headings | **Fraunces** (serif) | Warm, editorial serif — delivers the "Playfair intent" of the current client portal, with better screen rendering and variable weight |
| UI, body, labels | **Inter** | Already loaded in all three portals; zero migration cost |

Scale (px): 12 · 14 · 16 (body min) · 18 · 22 · 28 · 36 · 48 · 64.
Line heights: 1.15 headings · 1.5 UI · 1.65 prose.

> Implementation note: fix the current bug where `font-heading`/`font-sub` are referenced
> in `md-latest/tailwind.config.ts` but Playfair/Raleway are never loaded in `layout.tsx`.

---

## 3. Spacing

4px base grid: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96.
Card padding standard: 24px. Section vertical rhythm on landing: 96px desktop / 64px mobile.

## 4. Radius

8 (inputs) · 12 (small cards) · 16 (cards) · 20 (hero cards) · pill (buttons, badges, avatars).
Softer than current shadcn 10px default — deliberate wellness choice.

## 5. Elevation

| Token | Use |
|---|---|
| `--shadow-rest` | `0 1px 2px rgba(16,24,40,.04)` — cards at rest (hairline border does the work) |
| `--shadow-hover` | `0 8px 24px rgba(16,24,40,.10)` — interactive hover only |
| `--shadow-modal` | `0 20px 48px rgba(16,24,40,.18)` — overlays |

Rule: elevation signals interactivity, never decoration.

## 6. Motion

Easing `cubic-bezier(0.25, 0.6, 0.3, 1)` ("gentle"). Durations: 150ms micro / 300ms standard /
450ms page-level. No bounce, no flash. `prefers-reduced-motion` fully honored.

## 7. Component states (all interactive elements)

| State | Treatment |
|---|---|
| Hover | `-1px` translateY + `--shadow-hover` (buttons/cards); `--brand-soft` bg (list rows) |
| Focus | 2px `--brand` ring, 2px offset |
| Active | `--brand-strong` bg, translateY reset |
| Disabled | 45% opacity, no pointer events |
| Loading | Skeleton shimmer in `--border` tone, 1.5s loop |

---

## 8. Tailwind v4 migration mapping

```css
@theme {
  --color-brand: #3b6fe0;        /* chosen palette's --brand */
  --color-brand-soft: #e8effc;
  --color-ink: #101828;
  --font-display: "Fraunces", serif;
  --radius-lg: 16px;
  /* ... 1:1 from tokens.css */
}
```

The same token names work in all three portals, ending the current OKLCH-vs-HSL split.
