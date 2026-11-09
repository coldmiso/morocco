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
- `/themes/maximalist/` — Moroccan Maximalist Night scroll collage.
- `/themes/black-gold/` — Black & Gold Night (placeholder until assets arrive).
- Theme pages are separate pages so their images never slow down the main site.

## Design system
- The event poster is the design anchor: deep indigo, lantern gold, blush coral.
  Main site is light: tan paper background with indigo ink text (owner moved away from the dark purple).
  Gold text on paper uses `--accent-text` (ochre) for contrast; bright `--accent` gold is for fills only.
- All colors, fonts and the type scale live as CSS custom properties in one `:root` block.
  Restyle by editing tokens, not by hard-coding values in rules.
- Current fonts — main site: Gloock (display: hero, headings, cards; one weight, no italic, so
  `font-synthesis:none`) from Google Fonts + the system UI stack (body).
  Theme pages use the same fonts and paper palette; each keeps its own small `:root` (marked
  "keep in sync" with `/index.html`). The Black & Gold card stays black with gold type.
  (Subject to change — update this line when fonts change.)
- Images: WebP, compressed, `width`/`height` set, `loading="lazy"` below the fold.
- Main-site background texture: `assets/paper-800.webp` (phones) / `paper-1213.webp` (≥768px), set via
  `--bg-image` on a fixed `body::before` layer (not `background-attachment:fixed`, which breaks on iOS),
  lightened by `--bg-wash`. Text that sits directly on it must pass 4.5:1 against the texture.
- Animations: scroll-driven via rAF/IntersectionObserver, transform/opacity only,
  and honor `prefers-reduced-motion`.

## Working style
- Show a short summary of what changed after each task; commit with a clear message.
- Before pushing visual changes, check the page at phone width and laptop width.
