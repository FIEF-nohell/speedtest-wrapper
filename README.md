# Netpulse

Browser-based internet speed test powered by [`@cloudflare/speedtest`](https://github.com/cloudflare/speedtest).

Live: **[speedtest.nohelll.com](https://speedtest.nohelll.com)**

![Netpulse OG preview](og-image.png)

## What it measures

- **Download / Upload** bandwidth against the Cloudflare edge (Mbps)
- **Idle ping** and **jitter**
- **Loaded ping** (down / up) with **bufferbloat grade** (A–D, Waveform thresholds)
- **Overall verdict** (Excellent / Good / Fair / Poor)

Past runs are stored in the browser under `localStorage` key `netpulse.history.v1` (up to 100 entries). No backend, no tracking.

## Stack

- Single-file static HTML
- `@cloudflare/speedtest` v1.3.0 loaded via `esm.sh` CDN
- Vanilla JS + Canvas 2D for charts (Catmull-Rom smoothing, eased y-axis)
- Fonts: Barlow Condensed + Inter (Google Fonts)

## Deploy to Vercel

1. Push this repo to GitHub.
2. In Vercel, **Add New Project** and import the repo. Zero-config — no build step needed, Vercel serves the static files.
3. Under **Settings → Domains**, add `speedtest.nohelll.com`.
4. At your DNS provider, add a CNAME record:
   - Name: `speedtest`
   - Value: `cname.vercel-dns.com`
5. Wait for DNS propagation + cert issuance.

That's it. Any push to the default branch triggers a redeploy.

## Local dev

No build step. Serve the folder:

```bash
python -m http.server 8000
# or
npx serve .
```

Open `http://localhost:8000`.

Opening `index.html` over `file://` also works, but the `speed.cloudflare.com/meta` CORS fetch may fail, falling back to `cdn-cgi/trace`.

## File layout

```
├── index.html        # Everything — markup, styles, test logic
├── favicon.svg       # Brand mark
├── og-image.png      # 1200x630 social preview
├── vercel.json       # Headers, clean URLs
├── .gitignore
└── README.md
```

## Credit

Made by [nohell](https://nohelll.com).
