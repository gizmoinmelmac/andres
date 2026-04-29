# Infrastructure

## Domain & Subdomains

| Property | Value |
|---|---|
| Root domain | `andresfajardo.co` |
| Registrar | Namecheap |
| DNS / Proxy | Cloudflare (Free plan) — **already active** |
| Cloudflare account | Admin@curubaventures... |
| Cloudflare Account ID | `a5fd6efa3db898967654686a7b78ff4d` |

### Subdomains in use

| Subdomain | Purpose | Hosting |
|---|---|---|
| `andresfajardo.co` | Personal portfolio (this repo) | GitHub Pages → migrating to CF Pages |
| `os.andresfajardo.co` | Personal mission control / agentic OS | Cloudflare |

## Current Hosting: GitHub Pages

The site is currently deployed via GitHub Pages. The `CNAME` file in the repo root points GitHub Pages to `andresfajardo.co`.

**Limitations of GitHub Pages:**
- No CDN edge caching (Cloudflare proxy compensates partially)
- No analytics beyond Google Analytics script
- Deploys can take 1–3 minutes to propagate
- No redirect rules, headers, or custom routing

## Target Hosting: Cloudflare Pages

`andresfajardo.co` DNS is already managed by Cloudflare (same account as `triolosislenos.com`, which is live on CF Pages). Migration is low-risk.

**Benefits of Cloudflare Pages over GitHub Pages:**
- Instant global CDN — static assets served from 300+ edge locations
- Automatic HTTPS with auto-renewing cert (same as now via Cloudflare proxy)
- Preview deployments on every PR/branch
- Custom redirect and header rules via `_redirects` / `_headers` files
- Built-in Web Analytics (privacy-friendly, no JS required)
- Faster deploys (typically < 30 seconds)

### Migration Steps

1. Go to Cloudflare Dashboard → Workers & Pages → Create application → Pages
2. Connect GitHub repo `gizmoinmelmac/andresfajardo.co` (or equivalent)
3. Set build config:
   - **Framework preset:** None
   - **Build command:** *(leave blank — static site)*
   - **Build output directory:** `/` (root)
4. Deploy — Cloudflare assigns a `*.pages.dev` preview URL
5. Add custom domain `andresfajardo.co` in CF Pages settings
6. Cloudflare will update its own DNS records automatically (CNAME → CF Pages)
7. Remove the `CNAME` file from the repo (no longer needed for CF Pages)
8. Disable GitHub Pages in repo Settings → Pages

### Reference: triolosislenos pattern
The `triolosislenos` CF Pages project in the same Cloudflare account is the established pattern to follow. Check its config for any `_redirects` or build settings worth replicating.
