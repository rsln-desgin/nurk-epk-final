# NURK EPK · session orient

## What you're working on

A single-file vanilla HTML/CSS/JS one-pager EPK for a Tallinn-based DJ named NURK.

**The working file is `web/sketch.html`.** That's the entire product. No build step. No framework.

## Layout

```
NURK EPK FINAL/
├── web/                  ← THE working files
│   ├── sketch.html       ← the EPK, edit this
│   ├── portrait.jpg, live-*.jpg
│   ├── audio/here-i-am.mp3
│   ├── tracks.json
│   └── bg-experiments/   ← 7 background tests, on hold (none working)
├── EPK Photo Content/    ← source photos (raw)
├── NURK SONGS/           ← source audio (raw)
├── INSPO/                ← user's design references
├── NURK INFO.md          ← copy / facts source of truth
├── SKETCH-TODO.md        ← outstanding polish (P1/P2/P3 from audit)
├── DESIGN.md             ← design rules (auto-loaded by impeccable)
└── _legacy/              ← previous neon-green direction; out of scope
```

**Do not touch `_legacy/`.** It contains a previous Next.js direction the user scrapped. Files there look real but aren't current. If you find yourself reading them, stop — read `SKETCH-TODO.md` and `web/sketch.html` instead.

## Rules of engagement

- **Polish in sessions.** The user iterates on this project. Don't chain audit fixes without invitation. Flag findings; let them choose what to apply.
- **Skills active:** `ui-ux-pro-max` and `impeccable`. Use them for any UI work.
- **Project-specific design rules live in `DESIGN.md`** — read it before designing.
- **Outstanding polish list lives in `SKETCH-TODO.md`** — read it before suggesting work.
- **Strategy decisions on file** (don't relitigate): no prices, no phone, no TikTok, no CAT line in footer, hero is type-only, Shows isn't a calendar. Reasoning in `SKETCH-TODO.md`.

## Local serve

`preview_start sketch` — runs a Node static server on `:8765` rooted at `web/`. Config: `.claude/launch.json`.

**The server supports HTTP range requests** (required for audio seeking). If `audio.duration` is ever `Infinity` in the console, the server is not running or was restarted without range support — kill `:8765` and restart via `preview_start sketch`. The server also serves `.wav` and `.m4a` with correct MIME types.

## Source-of-truth precedence (when docs disagree)

1. The current state of `web/sketch.html`
2. `SKETCH-TODO.md` (active decisions)
3. `DESIGN.md` (design rules)
4. `NURK INFO.md` (artist facts/copy)
5. Memory files in `~/.claude/projects/-Users-ruslan-Desktop-NURK-EPK-FINAL/memory/`

If anything in `_legacy/` contradicts these, `_legacy/` is wrong by definition.
