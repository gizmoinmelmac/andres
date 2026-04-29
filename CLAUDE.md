# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static personal site for Andrés Fajardo at `andresfajardo.co`. No build system, package manager, or server-side code — everything is self-contained HTML + CSS + vanilla JS.

**Hosting:** Currently GitHub Pages. Migration to Cloudflare Pages in progress — see `docs/infrastructure.md`.  
**DNS:** Cloudflare (Free plan) — domain on Namecheap.  
**Docs:** `docs/infrastructure.md` (hosting/DNS) · `docs/progress.md` (task tracker)

## Design & Frontend Standards

Before any HTML/CSS/visual work, always invoke:
- **`/impeccable`** — primary design reference; use on every design task
- **`/design-taste-frontend`** — layer in for frontend implementation decisions

For library/framework syntax, use the **context7 MCP** rather than training data.

## Development

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

No build steps, no linting, no test suite.

## Architecture

The site is two self-contained single-page files. No shared CSS, JS, or assets between them.

### `index.html` — homepage (DHARMA Station 04)

Dark atmospheric page built around a full-page Spline 3D scene (robot figure). DHARMA Initiative aesthetic: classified document meets interactive art installation.

**Key elements:**
- **Spline scene** — `<spline-viewer>` web component, full-page background. A shadow-DOM purge IIFE removes the Spline watermark at runtime.
- **Veil + vignette + scanlines** — layered fixed overlays that create depth and texture over the 3D scene.
- **Spotlight** — `#spotlight` radial glow follows the cursor (desktop only).
- **Content** — `.content` (fixed, left-aligned): station label, hex seal SVG, name H1, descriptor, LinkedIn + contact links.
- **Signature** — `.sig` (fixed, bottom-left): coordinates + the `Seq — 04 · 08 · 15 · 16 · 23 · 42` trigger.
- **π trigger** — `.pi-trigger` (fixed, bottom-right): a tiny `π` glyph linking to `black-file.html` in a new tab.
- **DHARMA sequence easter egg** — clicking the `Seq —` line opens a terminal panel; entering the six numbers (`4 8 15 16 23 42`) and pressing INITIATE reveals a typewriter-animated personnel file, then dismisses.

**Palette:** All colors use OKLCH — `--bg` (9% dark amber), `--text` (87% warm), `--dim` (56% muted), `--accent` (74% amber), `--rule` (26% dark rule).

**Fonts:** Chakra Petch (display/H1) + Azeret Mono (all other text).

**Mobile:** Gradient flips bottom-up; content moves to bottom of viewport; hex seal hidden; gyroscope parallax activated on first touch (iOS 13+ requires permission gesture).

### `black-file.html` — The Black File / Archive 314 (π)

Scrollable flashlight room — a faithful port of the original `old_site/dark-room.htm` (Zachary Johnson technique), reskinned in the DHARMA amber palette.

**Three coupled mechanics (all in vanilla JS, no deps):**
- **Flashlight (`#spot`)** — `position: fixed`, 200%×200% element with `radial-gradient(transparent 0, black 450px)`, `pointer-events: none`, `z-index: 100`. JS shifts `background-position` 1:1 with cursor delta from center, punching a circular hole in the otherwise black overlay.
- **Title shadow** — `#archive-title` has a visible amber color (`#9a8a74`) plus a cursor-following `text-shadow: black`. The word is seen AND casts a shadow; shadow direction is the inverse of cursor position (light source = cursor), blur grows with distance from the stage center-third reference point.
- **Wall cast-shadow** — `#wall` (`position: relative`) uses `box-shadow` (Y-axis only, inverse to cursor Y) to cast a black bloom upward into the dark stage, simulating the wall's top edge throwing a shadow. `position: relative` on `#wall` is load-bearing: it places `#wall` in a higher paint layer than the static `#stage`, so the box-shadow bleeds into the stage area correctly.

**Layout:** `#stage` (top 40vh, `#3a3228` — amber-tinted `#444`) + `#wall` (bottom 60vh, `#a89070` — amber-tinted `#999`). Body `overflow: hidden`; `#wall` scrolls its content internally via `overflow-y: auto`.

**Palette (hex, not OKLCH — intentionally different from `index.html`):**
- Stage bg `#3a3228` · Wall bg `#a89070` · Title `#9a8a74` · Wall text `#1c1610` · Accent `#7a5828`

**Four archive cards** — Coffee · Movies & Scripts · Music · Stuff, in a 2-col CSS Grid (`auto-fit, minmax(300px, 1fr)`). Single column on mobile.

**Footer** — EOF line + "Return to Station 04" link back to `/`.

**Mobile / reduced-motion:** `#spot` hidden, body scrolls normally, title shows static shadow, single-column grid.

### `old_site/` (gitignored)

The legacy BookCard v1.2 (pixelwars) site is preserved on disk in `old_site/` but is gitignored and not served. It included jQuery-based routing, CSS skin layers, AJAX portfolio detail loading, and a 3D CSS flip layout. Not referenced by any live page.
