# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a static personal portfolio/vCard website for Andrés Fajardo at `andresfajardo.co`. No build system, package manager, or server-side code — everything is plain HTML, CSS, and jQuery.

**Hosting:** Currently GitHub Pages. Migration to Cloudflare Pages is in progress — see `docs/infrastructure.md`.  
**DNS:** Managed by Cloudflare (Free plan) — domain registered on Namecheap.  
**Docs:** `docs/infrastructure.md` (hosting/DNS setup) · `docs/progress.md` (task tracker)

## Design & Frontend Standards

Before any HTML/CSS/visual work, always invoke:
- **`/impeccable`** — primary design reference; use on every design task to avoid generic output
- **`/design-taste-frontend`** — layer in when making frontend implementation decisions or evaluating visual output

For any library, framework, or tool-specific syntax, use the **context7 MCP** rather than relying on training data.

## Development

Open `index.html` directly in a browser, or serve locally to avoid AJAX issues with portfolio detail loading:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

There are no build steps, no linting tools, and no test suite.

## Architecture

### Template: BookCard v1.2 (pixelwars)

The site uses a "book" metaphor with a 3D CSS flip layout:

- **`#rm-container`** — root container; toggled between `rm-closed` / `rm-open` / `rm-in` CSS classes to drive the 3D page-turn animation
- **`.rm-cover`** — the front "cover" of the book (home page)
- **`.rm-middle`** — hidden middle layer used during the flip
- **`.rm-right`** — the back "right" side (portfolio, resume, contact pages)

### Safe Mode

On mobile, IE, or older browsers, `safe-mod` class is added to `<html>`, disabling 3D transforms and falling back to simple show/hide + CSS animations. The layout breakpoint is 960px.

### Routing

Hash-based routing via `jquery.address`. Each page section has an `id` matching the hash (e.g. `#/home`, `#/resume`). Portfolio detail pages load via AJAX into `.p-overlay` elements using `.load()`.

### CSS Skins

The theme is composed of four independently swappable skin layers, each loaded via a `<link>` with a specific class:

| Link class | Directory | Controls |
|---|---|---|
| `.cover-skin` | `css/skins/cover/` | Cover page style (retro, neon, fire, etc.) |
| `.base-skin` | `css/skins/base/` | Base UI (modern, retro, clean, retro3d) |
| `.paper-bg-skin` | `css/skins/paper-bg/` | Paper texture on the right panel |
| `.body-bg-skin` | `css/skins/body-bg/` | Body background pattern |

To change the site's look, swap the `href` on the corresponding `<link>` in `index.html`.

### Key JS Files

- **`js/main.js`** — all application logic: layout, routing, masonry, scrollbars, lightbox, skill bars, 3D menu
- **`js/send-mail.js`** — contact form AJAX POST handler
- **`cgi-bin/`** — server-side mail handler (unused under GitHub Pages static hosting)

### Content Sections

All content lives in `index.html`. The four nav pages are: `#home` (cover), `#resume`, `#portfolio`, `#contact`. Portfolio detail pages are separate HTML files (`portfolio-*.html`) loaded dynamically.

### HTML Attributes on `<html>`

Behavior is configured via `data-*` attributes on the root `<html>` element in `index.html`:

- `data-safeMod` — force safe mode on/off
- `data-inAnimation` / `data-outAnimation` — CSS animation class names for page transitions
- `data-cover-h1-tune` through `data-cover-h3-span-tune` — FitText multipliers for cover typography
- `data-twitter-name` — Twitter handle for the Twitter widget
