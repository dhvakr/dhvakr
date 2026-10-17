# dhvakr.me — iteration 3

Personal site for **Divakaran T**, backend & cloud engineer, plus the **Ikat**
pitch page mounted underneath it.

Two static pages, no build step. Deployed on Cloudflare Pages.

```
/                     index.html          portfolio
/ikat/                ikat/index.html     Ikat — MCP control plane
/404.html                                 served for unmatched paths
/assets/css/style.css                     portfolio styles (Ikat is self-contained)
/_headers                                 security headers + caching
```

## Deploying

Cloudflare Pages, **production branch `iteration-3`**, no build command, output
directory `/` (the repository root).

The `main` branch is the GitHub profile README, not the site — don't point
Pages at it.

## Notes for future edits

- **Dark is the default.** An unstamped `:root` renders dark on purpose; the
  light tokens live in `[data-theme="light"]` and a `prefers-color-scheme`
  block. Both must be edited together.
- **Both pages share one theme key** (`dhvakr-theme` in `localStorage`), so a
  visitor's choice carries between `/` and `/ikat/`. Changing the key in one
  page without the other silently breaks that.
- **Colour means something.** On the portfolio, amber is "within objective"
  and red is "over it" — that contract is what lets the hero latency panel
  work without a legend. On `/ikat/`, indigo is allow and vermilion is deny.
- **Scroll-revealed sections start at `opacity: 0`.** The head script arms a
  2.5 s failsafe that shows everything if the main script never reports in, so
  a JS error can't leave the page blank. Keep that failsafe.
- **Every number on the portfolio is from the résumé in `/assets`.** If a
  figure changes there, change it here too.
- `assets/` is not content-hashed, so `_headers` caps its cache at one day.

## Local preview

```bash
python3 -m http.server 4330
```

Then open <http://localhost:4330/>. Opening `index.html` over `file://` will
not work properly — the canvas and the scroll observers need a real origin.
