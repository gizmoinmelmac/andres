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

## Milestone 3 — Design / UX Update

> To be defined.

---

## Notes & Decisions

| Date | Decision | Reason |
|---|---|---|
| 2026-04-29 | Migrate hosting to Cloudflare Pages | DNS already on CF, CF Pages gives CDN, preview deploys, and header rules for free |
| 2026-04-29 | Keep static HTML/CSS/JS (no build step) | No framework dependency, zero build complexity, CF Pages handles it natively |
