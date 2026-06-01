# sketch.html · Polish notes

Working file: `web/sketch.html`. Single-file vanilla HTML/CSS/JS one-pager. Previous neon-green direction (Next.js app + SITEMAP / UX-SPEC / STYLEGUIDE / POLISH-NOTES / WORKFLOW) lives under `_legacy/` — out of scope.

## Built

Hero (typographic, no photo) · About · Music (existing) · Live · Shows · Bookings · Contact. Glass-morph + ice-cyan + Anton/Inter/JetBrains-Mono. Reveal-on-scroll via IntersectionObserver. Scroll-snap is `proximity` (not mandatory) so tall sections allow intra-scroll.

## Outstanding polish — from audit

### P1
- [ ] **About section layout rework.** Current portrait + bio + meta + stats grid feels cramped now that everything is forced into 100vh. Need a new layout pattern entirely — see layout options proposed in chat.
- [ ] **Contact form rework.** Current Bookings form is dense and visually heavy. Rethink fields, density, and visual treatment.
- [ ] **Shows / credentials rework.** Current chips + 4 marker cells + CTAs reads as a fact sheet, not as credentials. Reconsider how venues, peak crowd, cadence, markets are presented.
- [ ] **Em dashes in copy.** 5 spots: bio (`released and unreleased`), About meta (`Tallinn / EE — Eastern European Time`), Shows markers (`90 min — open to longer`), Bookings intro (`Open to —`), Bookings textarea hint (`vibe — sell it to me`). Replace with commas, colons, or `·`.
- [ ] **`.shows__chip` touch target.** Padding `10px 16px` → ~38px height; bump to `12px 18px` for 44px AA.

### P2
- [ ] **Decorative `--signal` cyan.** Strip from: About `.about__caption` year ("2025"), Live secondary card years (`live__cell .live__caption`), Contact `.contact__say` ("Say hello →"), `.section__sub` lines in Live and Shows. Keep on the marquee Live caption (matches the existing music player live-pulse). Use `--fg-soft` for the rest.
- [ ] **Music title hierarchy slip.** `.music__title` clamps `56px–144px` while every new `.section__title` clamps `72px–200px`. Align music to the section pattern.

### P3
- [ ] **Hero scroll cue.** `.header__scroll` overlaps CTAs at viewport heights ≤700px. Hide below `min-height: 720px`.
- [ ] **`.contact__outro` element.** Currently `<h2 aria-hidden="true">NURK</h2>`. It's decorative — change to `<span>` so it's out of the heading hierarchy.

## Already applied

- **P0 contrast fix.** Body gradient endpoint capped from `oklch(0.96)` to `oklch(0.62)` so white text retains AA contrast at the bottom of the viewport. Revert if you want the original light-cyan washout.

## Deferred (not worked on yet)

- **Background canvas.** None of the 7 `bg-experiments/*` are landing yet. Hook in place: `<canvas id="bg" hidden>` at the top of `<body>`. Future swap-in is `removeAttribute('hidden')` + drawing logic.
- **Performance video.** `IMG_3880.mov` (572 MB raw) not trimmed. Marquee live frame swap point is the `<img src="live-wide.jpg">` inside `.live__marquee` — replace with `<video autoplay muted loop playsinline poster="live-wide.jpg">`.
- **Audio previews.** Only `here-i-am.mp3` plays. Other 6 tracks in `tracks.json` show "preview pending" — hook up mp3s or remove tracks.
- **Bookings form endpoint.** Ships with `mailto:musicbynurk@gmail.com` fallback. TODO comment at the form marks the swap point. Decide between Typeform / Tally / Formspree — visual stays identical, only `<form action>` changes.
- **Press kit ZIP.** Footer + Shows CTA currently fall back to `mailto`.
- **Custom OG image.** Currently uses `live-wide.jpg`. Could design a dedicated 1200×630.

## Decisions on file (don't relitigate without reason)

- **No prices.** Inquiry-led posture. "Every booking quoted individually."
- **No phone, no TikTok, no `CAT №.NURK / SS26` line in the footer.** (Nav keeps the CAT label.)
- **Hero is type-only** — no photo, no parallax. Wordmark + tagline + 2 CTAs + scroll cue.
- **Shows isn't a calendar.** Reconceived as venues + markets + cadence (NURK plays nearly every weekend; per-date listing is too high-churn).
- **Live photos use frame, not filter.** APRESKI + D3 shots are already on-palette; only a light `saturate(0.92) brightness(1.02) contrast(1.04)` is applied. Heavy duotone would look post-processed.

## Photo asset map

- `web/portrait.jpg` — About portrait (NURK at decks, white shirt, blue lighting).
- `web/live-wide.jpg` — Live marquee (D3, cyan vertical neon bars). Resampled from `2026.16.01_D3_*.jpeg`.
- `web/live-deck.jpg` — Live secondary, landscape (APRESKI two-DJ Pioneer deck). Resampled from `APRESKI-rk-24.jpeg`.
- `web/live-crowd.jpg` — Live secondary, portrait (NURK + crowd reaching in). Resampled from `APRESKI-rk-119.jpeg`.
- `IMG_4915.JPG` (red/pink lasers) — off-palette, skipped.
- `hero.jpg` previously existed for the Next.js direction — deleted during cleanup; sketch.html is type-only on the hero.

## Local serve

```sh
node -e "/* tiny static server, see .claude/launch.json */"
```

Or via Claude Code's preview: `preview_start sketch` (the `.claude/launch.json` config runs a Node static server on `:8765` rooted at `web/`).
