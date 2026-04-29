# Progress Tracker

## Status Legend
`[ ]` todo · `[~]` in progress · `[x]` done

---

## Milestone 1 — Housekeeping & Hosting Migration

### Repo hygiene
- [x] Create CLAUDE.md with codebase guidance
- [x] Update `.gitignore` to current best practices
- [x] Create `docs/` folder with infrastructure and progress docs

### Hosting migration: GitHub Pages → Cloudflare Pages
- [ ] Create CF Pages application connected to GitHub repo
- [ ] Verify preview deploy on `*.pages.dev` URL
- [ ] Add custom domain `andresfajardo.co` in CF Pages settings
- [ ] Confirm DNS cutover — site resolves and HTTPS works
- [ ] Remove `CNAME` file from repo root
- [ ] Disable GitHub Pages in repo Settings

---

## Milestone 2 — Content Refresh

> To be defined. Add tasks here when scope is agreed.

---

## Milestone 3 — v2 Design Overhaul

### v2.html — New immersive page
- [x] Full-page Spline 3D scene with DHARMA / classified-station aesthetic
- [x] Directional veil, vignette, scanline texture
- [x] Spotlight effect following cursor
- [x] Content visibility tuned (dim tokens, sig contrast)
- [x] Pointer-events fix so Spline robot responds across full viewport
- [x] Sesh link removed
- [x] Email obfuscated via split data-attributes (af.uplifting638@passmail.com alias)
- [x] Mobile gyroscope parallax (tilt device to look around scene)
- [x] CSS `::selection` styled amber with dark text
- [x] DHARMA sequence easter egg (click `Seq —` line or press `4` to enter sequence; reveals personnel file + scene transform)
- [x] `docs/v2.md` reference document written

### Remaining
- [ ] Swap `index.html` → `v2.html` as primary entry point when ready to go live
- [ ] Populate easter egg personnel file with final copy
- [ ] Test on real mobile devices (gyroscope, touch targets)
- [ ] Verify Spline watermark purge script still works after CF Pages deployment

---

## Notes & Decisions

| Date | Decision | Reason |
|---|---|---|
| 2026-04-29 | Migrate hosting to Cloudflare Pages | DNS already on CF, CF Pages gives CDN, preview deploys, and header rules for free |
| 2026-04-29 | Keep static HTML/CSS/JS (no build step) | No framework dependency, zero build complexity, CF Pages handles it natively |
| 2026-04-29 | Build v2.html as separate file before swapping index.html | Allows side-by-side comparison; no risk to live site during development |
| 2026-04-29 | Use passmail alias (af.uplifting638@passmail.com) for contact email | Protects primary inbox from scraper-harvested spam; alias can be rotated |
| 2026-04-29 | Easter egg: no audio, no localStorage persistence | Audio is intrusive in shared spaces; fresh-every-visit feels more sacred/ritual |
