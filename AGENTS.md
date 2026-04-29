# AGENTS.md

This file provides guidance to Codex (Codex.ai/code) when working with code in this repository.

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
- **π trigger** — `.pi-trigger` (fixed, bottom-right): a tiny `π` glyph linking to `dark-room.html` in a new tab.
- **DHARMA sequence easter egg** — clicking the `Seq —` line opens a terminal panel; entering the six numbers (`4 8 15 16 23 42`) and pressing INITIATE reveals a typewriter-animated personnel file, then dismisses.

**Palette:** All colors use OKLCH — `--bg` (9% dark amber), `--text` (87% warm), `--dim` (56% muted), `--accent` (74% amber), `--rule` (26% dark rule).

**Fonts:** Chakra Petch (display/H1) + Azeret Mono (all other text).

**Mobile:** Gradient flips bottom-up; content moves to bottom of viewport; hex seal hidden; gyroscope parallax activated on first touch (iOS 13+ requires permission gesture).

### `dark-room.html` — Archive 314 (π)

Scrollable "classified trivia archive" in the same DHARMA aesthetic. No Spline scene.

**Key elements:**
- **Torch mask** — `#torch-mask`: a fixed full-page dark overlay with a transparent radial hole at `--tx`/`--ty` (cursor position). Creates a flashlight effect on desktop. Hidden on `(hover: none)` and `(prefers-reduced-motion: reduce)`.
- **Hex watermark** — faint SVG hexagon centered in background, `opacity: 0.03`.
- **Four archive cards** — Coffee · Movies & Scripts · Music · Stuff, in a 2-col CSS Grid (`auto-fit, minmax(340px, 1fr)`). Single column on mobile.
- **Footer** — EOF line + "Return to Station 04" link back to `/`.

### `old_site/` (gitignored)

The legacy BookCard v1.2 (pixelwars) site is preserved on disk in `old_site/` but is gitignored and not served. It included jQuery-based routing, CSS skin layers, AJAX portfolio detail loading, and a 3D CSS flip layout. Not referenced by any live page.
