# morocco.warfield.me — rules for Claude

Guest info site for Lucy's 30th birthday trip to Marrakech, Nov 19–23, 2026.
Owner: Lucas Warfield. Guests open this on their phones, often on mobile data abroad.

## Hosting
- Static HTML/CSS/JS, no build step, no framework. Served by GitHub Pages from this repo.
- Custom domain via the `CNAME` file (`morocco.warfield.me`). Never delete or edit `CNAME`.
- Pushing to the default branch deploys. Keep `main` deployable at all times.

## Non-negotiables
- Every page keeps `<meta name="robots" content="noindex, nofollow">`; keep `robots.txt` disallowing all.
- No per-person pricing on the site. Costs live in the linked Google Doc.
- Mobile-first, iOS Safari is the primary target; desktop (13" laptop) secondary. Check 390px width first.
- No horizontal scroll at any width. Respect `env(safe-area-inset-*)`.
- Living content (packing list, logistics) stays in the linked Google Doc; photos stay a link to the Google Photos album (no iframes — they break on mobile Safari).
- Don't change finalized links (Partiful, riad map pin, trip calendar, Google Doc, Photos) unless asked.

## Structure
- `/` — main site: three tabs (Home / Schedule / Links & Info). Tab bar at the bottom on phones, top on desktop.
- `/themes/maximalist/` — Moroccan Maximalist Night scroll collage.
- `/themes/black-gold/` — Black & Gold Night (placeholder until assets arrive).
- Theme pages are separate pages so their images never slow down the main site.

## Design system
- The event poster is the design anchor: deep indigo, lantern gold, blush coral.
- All colors, fonts and the type scale live as CSS custom properties in one `:root` block.
  Restyle by editing tokens, not by hard-coding values in rules.
- Current fonts: Syncopate (display, uppercase, wide tracking) + Instrument Sans (body), from Google Fonts.
  (Subject to change — update this line when fonts change.)
- Images: WebP, compressed, `width`/`height` set, `loading="lazy"` below the fold.
- Animations: scroll-driven via rAF/IntersectionObserver, transform/opacity only,
  and honor `prefers-reduced-motion`.

## Working style
- Show a short summary of what changed after each task; commit with a clear message.
- Before pushing visual changes, check the page at phone width and laptop width.
