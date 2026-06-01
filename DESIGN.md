# DESIGN.md

Design rules for the NURK EPK. Auto-loaded by `impeccable`. Read before designing.

## Identity

Glass-morphism + ice-cyan + editorial-typographic. Quiet, cold, precise. Not a club poster, not a SaaS landing page.

The system is **committed**, not restrained — glass and ice-cyan carry the surface. Don't compress it back to a generic minimalism.

## Color (OKLCH only)

All tokens defined in `web/sketch.html` `:root`. Use these — never hard-code.

| Token | Value | Use |
|---|---|---|
| `--canvas` | `oklch(0.87 0.075 220)` | rare; primarily set via gradient |
| `--canvas-soft` | `oklch(0.93 0.04 222)` | rare |
| `--canvas-deep` | `oklch(0.38 0.085 220)` | dark accents |
| `--paper` | `oklch(0.74 0.04 230)` | mid surface |
| `--fg` | `oklch(0.97 0.005 250)` | primary text |
| `--fg-soft` | `oklch(0.90 0.012 245)` | secondary text |
| `--ink` | `oklch(0.18 0.04 245)` | text on signal-cyan surfaces |
| `--muted` | `oklch(0.78 0.018 245)` | tertiary / mono caps eyebrows |
| `--signal` | `oklch(0.93 0.085 220)` | **functional only** — see below |
| `--border` | `oklch(1 0.01 245 / 0.16)` | glass-card borders |
| `--border-strong` | `oklch(1 0.01 245 / 0.28)` | hover states |

**Body gradient endpoint is capped at `oklch(0.62)`** so white text retains AA contrast at the bottom of the viewport. Don't push it lighter.

## `--signal` cyan is functional only

Use `--signal` only for:
- Primary CTAs (`.glass-cta--signal`, form submit)
- Active states (current track row, focused input)
- Real-time / "live" indicators (the pulse dot pattern from the music player)
- Focus rings (`:focus-visible`)
- Interaction destinations (link hover color)

Do **not** use `--signal` for:
- Decorative year captions
- Section sub-eyebrows
- "Say hello →" type flourishes
- Anything just to "add a pop"

Default for accents/eyebrows is `--fg-soft` or `--muted`.

## Typography

| Family | Variable | Use |
|---|---|---|
| Anton | `--display` | section titles, big numerics, hero wordmark |
| Inter | `--sans` | body text, form inputs |
| JetBrains Mono | `--mono` | eyebrows, labels, meta cells, mono caps |

Rules:
- **Anton: never below `-0.02em` letter-spacing** (terminals collide)
- **Mono caps: 0.22–0.30em letter-spacing**, uppercase
- **Section titles**: `clamp(72px, 12vw, 200px)` (`.section__title`). Apply consistently to every section title — don't drift smaller.
- **Body line length**: 56ch in `.about__bio`. Don't blow past 65ch.
- **Hierarchy**: ≥1.25 ratio between scale steps.

## Spacing / rhythm

- Section padding: `120px 32px 80px` desktop, `96px 18px 64px` mobile.
- Glass card radius: `14px` (matches player, nav, CTAs). Mini chips: `999px`.
- Touch targets ≥ 44×44.

## Motion

- Easing: `--ease` = `cubic-bezier(0.16, 1, 0.3, 1)` (ease-out quint-ish). No bounce, no elastic.
- Reveal-on-scroll rhythm: 80ms stagger between siblings, 600ms duration. Apply via `.reveal` + IntersectionObserver.
- Animate `transform` and `opacity` only — never layout properties.
- Respect `prefers-reduced-motion` (already wired globally).

## Glass card stack (reusable)

Every glass surface uses this exact stack (matches `.nav`, `.player`, `.glass-cta`, `.card`):

```css
background: oklch(1 0.01 245 / 0.06);
border: 1px solid oklch(1 0.01 245 / 0.14);
backdrop-filter: blur(28px) saturate(140%);
box-shadow:
  inset 0  1px 0 oklch(1 0.01 245 / 0.18),
  inset 0 -1px 0 oklch(0.18 0.04 245 / 0.10),
  0 24px 60px oklch(0.18 0.04 245 / 0.30);
```

Plus the SVG-noise `::after` overlay (`mix-blend-mode: overlay`, opacity 0.45) for texture continuity. **Apply this to every new glass surface** — texture continuity is what binds the system together.

## Photos

**Frame, not filter.** The chosen source photos (APRESKI, D3, portrait) are already cyan/blue from their stage lighting — they don't need duotone or heavy color grading.

CSS filter ceiling: `saturate(0.92) brightness(1.02) contrast(1.04)`. Anything heavier reads post-processed and amateur.

Wrap photos in glass cards (`.card`) so they inherit the same surface treatment as other elements. Add a soft inner cyan vignette via `::before` for cohesion.

## Project-specific anti-patterns

In addition to the impeccable shared bans (em dashes, gradient text, hero-metric template, modals-as-first-thought), this project also forbids:

- **Prices on the page.** Inquiry-led. "Every booking quoted individually."
- **Calendar / date listings.** Shows is venues + markets + cadence, not a schedule.
- **Photos on the hero.** Hero is type-only.
- **`href="#"`.** Breaks scroll-snap. Use real anchors or `mailto:`.
- **Decorative `--signal`** (see above).

## Impeccable shared rules that DO NOT apply here

The shared `impeccable` design laws say "glassmorphism as default" is an absolute ban. **It does not apply to this project.** Glass + ice-cyan is the chosen identity, not a reflex. Use it deliberately and consistently.

(Every other shared ban — em dashes, gradient text, hero-metric, identical card grids, modals — still applies.)
