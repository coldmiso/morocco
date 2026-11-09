# morocco.warfield.me — rules for Claude

Guest info site for Lucy's 30th birthday trip to Marrakech, Nov 19–23, 2026.
Owner: Lucas Warfield. Guests open this on their phones, often on mobile data abroad.

## Hosting
- Static HTML/CSS/JS, no build step, no framework. Served by GitHub Pages from this repo.
- Custom domain via the `CNAME` file (`morocco.warfield.me`). Never delete or edit `CNAME`.
- `_config.yml` keeps this file out of the published site; keep `CLAUDE.md` in its `exclude` list.
- Pushing to the default branch deploys. Keep `main` deployable at all times.

## Non-negotiables
- Every page keeps `<meta name="robots" content="noindex, nofollow">`; keep `robots.txt` disallowing all.
- No per-person pricing on the site. Costs live in the linked Google Doc.
  Exception (owner-approved): the "$125 to Lucy" deposit item on the Home tab stays.
- Mobile-first, iOS Safari is the primary target; desktop (13" laptop) secondary. Check 390px width first.
- No horizontal scroll at any width. Respect `env(safe-area-inset-*)`.
- Living content (packing list, logistics) stays in the linked Google Doc; photos stay a link to the Google Photos album (no iframes — they break on mobile Safari).
- Don't change finalized links (Partiful, riad map pin, trip calendar, Google Doc, Photos) unless asked.

## Structure
- `/` — main site: three tabs (Home / Schedule / Links & Info). Tab bar at the bottom on phones, top on desktop.
  Schedule is one scrolling page (no day tabs): sticky day headers, dress codes link to the theme pages,
  and during the trip it opens on today (Marrakech time). Itinerary lives in `DATA.schedule`.
- `/themes/maximalist/` — Moroccan Maximalist Night scroll collage (floating "Trip site" back button, top-left).
- `/themes/black-gold/` — Black & Gold Night (placeholder until assets arrive).
- Theme pages are separate pages so their images never slow down the main site.

## Design system
- The event poster is the design anchor: deep indigo, lantern gold, blush coral.
  Main site switches by time of day on the viewer's clock: DAY (7 AM–6 PM) = plain paper with indigo ink,
  NIGHT = the original deep indigo with cream text. A tiny script in `<head>` sets `<html data-time>`
  before first paint; night tokens live in the `:root[data-time="night"]` block right after `:root`.
  Preview with `?time=day` / `?time=night`. No background texture/image.
  Gold text on paper uses `--accent-text` (ochre) for contrast; bright `--accent` gold is for fills only.
- All colors, fonts and the type scale live as CSS custom properties in the `:root` block (plus its night override).
  Restyle by editing tokens, not by hard-coding values in rules.
- Current fonts — main site: the system UI stack for body AND headings (semibold), chosen for legibility.
  Gloock (Google Fonts, one weight, no italic → `font-synthesis:none`) is used only for the hero title
  via `--font-hero`.
  Theme pages use the same fonts and paper palette; each keeps its own small `:root` (marked
  "keep in sync" with `/index.html`). The Black & Gold card stays black with gold type.
  (Subject to change — update this line when fonts change.)
- Images: WebP, compressed, `width`/`height` set, `loading="lazy"` below the fold.
- Animations: scroll-driven via rAF/IntersectionObserver, transform/opacity only,
  and honor `prefers-reduced-motion`.

## Working style
- Show a short summary of what changed after each task; commit with a clear message.
- Before pushing visual changes, check the page at phone width and laptop width.
