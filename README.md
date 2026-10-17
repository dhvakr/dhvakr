# dhvakr.me — iteration 3

Personal site for **Divakaran T**, backend & cloud engineer, plus the **Ikat**
pitch page mounted underneath it.

Two static pages, no build step. Deployed on Cloudflare Pages.

```
/                     index.html          portfolio
/ikat/                ikat/index.html     Ikat — MCP control plane
/404.html                                 served for unmatched paths
/assets/css/style.css                     portfolio styles (Ikat is self-contained)
résumé                Google Doc, linked live as export?format=pdf
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
- **Colour means something.** Black and white carry the page. On the
  portfolio, green is "within objective", rust is "over it", and brown marks
  the earlier state — that contract is what lets the hero latency panel work
  without a legend. On `/ikat/`, indigo is allow and vermilion is deny.
- **The light tokens are duplicated** in `[data-theme="light"]` and the
  `prefers-color-scheme` block, and the two are kept byte-identical on
  purpose so one find/replace reaches both. Keep them that way.
- **Scroll-revealed sections start at `opacity: 0`.** The head script arms a
  2.5 s failsafe that shows everything if the main script never reports in, so
  a JS error can't leave the page blank. Keep that failsafe.
- **Every number on the portfolio comes from the Google Doc résumé**, which
  the résumé links hit live via `export?format=pdf`. There is no PDF in the
  repo any more. If a figure changes in that doc, change it on the page too.
- `assets/` is not content-hashed, so `_headers` caps its cache at one day.

## Local preview

```bash
python3 -m http.server 4330
```

Then open <http://localhost:4330/>. Opening `index.html` over `file://` will
not work properly — the canvas and the scroll observers need a real origin.
