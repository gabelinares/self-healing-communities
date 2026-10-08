# Design System

Everything below is taken from the live code (`:root` in `hero-versions/index.html`).

## Colour

| Token | Hex | Use |
|---|---|---|
| `--emerald` | `#009169` | Primary brand green; headline emphasis, links, spiral dots |
| `--emerald-bright` | `#00DBB6` | Highlights on dark green, the spiral's travelling "swell" |
| `--emerald-deep` | `#06513C` | Dark green: footer, closing section, active states, "Risk Stewardship" |
| `--emerald-soft` | `#A4D6C6` | Soft green on dark backgrounds (footer text) |
| `--paper` | `#F4ECDC` | Page background |
| `--paper-warm` | `#EFE2CB` | Warmer paper |
| `--cream` | `#FBF6EA` | Cards, ovals, text on green |
| `--terracotta` | `#C9442F` | The "Old Way" / friction side |
| `--terracotta-soft` | `#E8A88E` | Soft friction tint |
| `--terracotta-bright` | `#C36938` | The client's original site orange: single-use accent (stats, the active spiral step) |
| `--ink` | `#0F2A22` | Body text and headlines |
| `--ink-soft` | `#4A5F58` | Secondary text |
| `--rule` | `rgba(15,42,34,.16)` | Hairlines |
| Nav button | `#007A58` | Darker than `--emerald` so cream text passes contrast (5:1) |

The spiral section sits on a warm radial gradient: `#FBF6EA → #F2E7CF → #E8D6B8`.

## Typography

- **Archivo** (variable, Google Fonts) carries everything. Headlines use the display settings:
  `--disp-wdth: 90` (slightly condensed) and `--disp-wght: 700`. Retune the whole voice from those
  two tokens.
- **Fraunces italic** is used only for quoted voices (the book's testimonial pages and the founder
  quote).
- **Headline emphasis is a colour break, not italics.** `<em>` inside a headline turns emerald and
  starts a new line (`em::before{content:"\A"}`). This was the client's preference (Sept 18,
  "Version B").
- Eyebrow labels: 11px, 600, uppercase, letter-spacing .2em, `--ink-soft`.

## Shape and motion

- **Large soft corners** (about 28–56px) on major blocks: the opening photo, the closing section,
  the book. Warm, never boxy.
- **Spiral step ovals:** 14px radius (9px on phones), even 10/16px padding, sized to their text.
- **Motion is ambient and slow:** drifting dots, a slow breathing pulse, scroll-driven reveals.
  Everything respects `prefers-reduced-motion`.
- **Dots are the visual language.** The river (scatter → flow), the spiral (a current of dots), the
  circle of leadership (a stipple of dots) and the closing "gather around" orbit all use the same
  vocabulary.

## Logos

In `Self Healing Communities Fund logos/`: full, stacked and symbol versions, each in deep emerald, bright emerald,
white and black, as SVG and PNG. The site uses deep emerald on light backgrounds and white on dark.

## Rules the client has set

- Warm, human and local, **not futuristic**. Primary audience is around 60, not fast tech adopters.
- Real contextual photography over stock wherever possible.
- **No heart-hands imagery** (a reviewer read it as blood).
- No text width caps that leave a narrow column inside a wide box. Cap the control, never the prose.
