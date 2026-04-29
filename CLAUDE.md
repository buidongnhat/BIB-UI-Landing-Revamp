# BIB Landing — Project Memory

## Project
- **Client:** BestinBrands (BIB) — B2B beauty distributor, Bangladesh
- **Site:** `bestinbrands.com` revamp — corporate/B2B landing, not e-commerce
- **Scope:** Mirror current IA, English only, scroll-reveal motion, no charts
- **Source of truth:** `design-direction-brief.md` (all 8 open questions resolved)

---

## Figma File
- **URL:** `https://www.figma.com/design/34lhOdI1DdGIwceCQ6AVL8/BIB-Landing-Revamp`
- **Auth:** `designs@aegona.com` — Aegona Design team (Pro plan)
- **Pages:**
  - `Logo` — BIB crossed-arc mark SVG (white fill, needs `currentColor` fix)
  - `UI Style guide` — tokens showcase (Color, Typography, Spacing, Radius, Motion)
  - `UI Visual direction` — brand principles, photo tiers, color context, type rules, layout archetypes, guardrails

---

## Figma Variables (5 collections)

- **Color** — 19 vars: `Neutral/*`, `Brand/*`, `Photo/*`, `Semantic/*`
- **Spacing** — 11 vars: `4xs`–`4xl` (4px–128px, 8pt grid), scoped to width/height/gap
- **Typography** — 29 vars: `Size/*` (px), `Weight/*` (numeric), `Line Height/*`, `Letter Spacing/*`, `Font Family`
  - Letter spacing stored as **percent** values (18, 4, −0.5, −1) not em
- **Radius** — 3 vars: `None` 0px, `SM` 2px, `MD` 4px — scoped to corner radius
- **Motion** — 5 vars: `Duration/Fast` 200ms, `Duration/Default` 400ms, `Duration/Slow` 600ms, `Reveal Offset` 16px, `Stagger` 80ms

---

## Text Styles (13 styles)

All styles have `fontSize` and `lineHeight` bound to Typography variables. `letterSpacing` bound where non-zero.

| Style | Size var | Weight | Notes |
|---|---|---|---|
| `Display/Hero` | Size/Display Hero (80px) | Light 300 | LH Display, LS −1% |
| `Display/Section` | Size/Display Section (56px) | Medium 500 | LH Display, LS −1% |
| `Heading/H1` | Size/H1 (40px) | Semi Bold 600 | LH Heading, LS −0.5% |
| `Heading/H2` | Size/H2 (32px) | Semi Bold 600 | LH Heading |
| `Heading/H3` | Size/H3 (24px) | Medium 500 | LH Snug |
| `Heading/H4` | Size/Body LG (18px) | Medium 500 | LH Snug, LS 18%, UPPER |
| `Body/LG` | Size/Body LG (18px) | Regular 400 | LH Body |
| `Body/MD` | Size/Body MD (16px) | Regular 400 | LH Body |
| `Body/SM` | Size/Body SM (14px) | Regular 400 | LH Body |
| `Label/Section` | Size/Body SM (14px) | Regular 400 | LH Snug, LS 18%, UPPER |
| `Label/Caption` | Size/Caption (12px) | Regular 400 | LH Snug, LS 4% |
| `UI/Button` | Size/Body MD (16px) | Medium 500 | LH Snug, LS 4% |
| `UI/Stat Number` | Size/Stat Number (80px) | Extra Light 200 | LH Tight, LS −1% |

---

## Style Guide Frames

### UI Style guide — `BIB Style Guide` (frame id `27:2`)
- Color swatches (4 groups, color variables applied as fills)
- Typography scale (all 13 styles with sample text, textStyleId applied)
- Spacing bars (proportional, 11 tokens)
- Border radius examples (3 values)
- Motion token table (5 tokens)

### UI Visual direction — `BIB Style Guide` (frame id `35:2`)
- **Brand Principles** — 3 cards: Reserved not sterile · Evidence-led · B2B not B2C
- **Photography Register** — 4 tiers with usage rules (T1 Bangladesh-scale, T2 Business/People, T3 Retail, T4 Editorial Product)
- **Color in Context** — 3 context frames (cream canvas, dark hero, photo tier)
- **Typography Rules** — 5 Do/Don't pairs specific to Cina GEO
- **Layout Archetypes** — 6 wireframe previews (Hero, Stats Band, Bento, Section Divider, Logo Grid, Contact Hero)
- **Critical Guardrails** — 8 rules (no stock, scrim required, no illustration, Sundora boundary, etc.)

### Text style application
- 250 text nodes across both frames have `textStyleId` applied
- Applied via size + textCase + letterSpacing heuristic: `size ≥ 64` → Display/Hero, `size ≥ 22` → Heading/H3, `size ≥ 15` → Body/MD, `size ≥ 13` → Body/SM, uppercase + ls ≥ 8% → Label/Section, else → Label/Caption

---

## ⚠️ Known Issues / Manual Steps

### Font: Cina GEO Test
- **Cannot be loaded via Figma Plugin API** (`loadFontAsync` fails — it's a locally-installed font, not a cloud font)
- All 13 text styles currently show **Inter** with correct weights as a stand-in
- **Action:** In Figma → Assets → Text styles → manually change each style's family from Inter to **Cina GEO Test**, keeping the weight. All 250 bound nodes update automatically
- Correct weight per style: Display/Hero → Light, Display/Section → Medium, H1/H2 → Semi Bold, H3/H4/Button → Medium, Body/Label → Regular, Stat Number → Extra Light
- License: commercial webfont license required from Public Type (`contact@publictype.us`) before launch

### Variable collection names
- Figma stripped emoji prefixes on save — collections are named `Color`, `Spacing`, `Typography`, `Radius`, `Motion` (not `🎨 Color` etc.)
- Plugin scripts must use plain names when looking up collections

### Line height variable binding
- `setBoundVariable('lineHeight', var)` succeeded at time of creation but inspection later showed some bindings as null — may need re-verification after font is corrected

### "23 vs 25 years"
- Current site: 23 years · New deck (p. 10): 25 years — **client must confirm** before launch; cascades to hero, stats band, About, and all comms

---

## Design Tokens — File Locations
- `tokens.css` — CSS custom properties (`--bib-*`), source for non-WordPress contexts
- `theme.json` — WordPress 6.6+ block theme token registry (`--wp--preset--*`)
- `design-direction-brief.md` — design source of truth (all decisions + rationale)
- `src/images/LOGO.svg` — crossed-arc mark only, white fill hardcoded — needs `fill="currentColor"` + wordmark SVG

---

## Local Dev Environment

- **Server:** `python3 -m http.server 8765` from `extract/` — serves all three pages
  - `http://localhost:8765/about-us/` — About Us (primary working page)
  - `http://localhost:8765/home/` — Home
  - `http://localhost:8765/market/` — Market
- **Restart:** `lsof -ti:8765 | xargs kill -9 2>/dev/null; cd extract && python3 -m http.server 8765`
- **Font serving:** `extract/about-us/font/Cina/` — all 9 weights, woff2/woff/ttf/eot. `home/` and `market/` use symlink `font → ../about-us/font`

---

## Extracted Site Structure

```
extract/
  about-us/
    index.html          ← primary working file (all new sections inline)
    css/                ← 9 CSS files from WordPress theme (master, header, footer, about-us-page, owl, aos…)
    font/Cina/          ← Cina GEO webfont files (9 weights)
    img/                ← section images downloaded from Figma
      section-our-company.png   (Figma asset 3bf78395, 2574×1930)
      section-our-vision.png    (Figma asset 0261e6bf, 2870×1081)
      section-our-mission.png   (Figma asset 7941d86b, 2870×942)
    our-company-block.html      ← standalone block (style + HTML)
    our-vision-mission-block.html ← standalone block (style + HTML)
  home/
    index.html          ← original extract, new bib-nav injected, active state: Home
    font → symlink to ../about-us/font
  market/
    index.html          ← original extract, new bib-nav injected, active state: Market
    font → symlink to ../about-us/font
```

---

## Implemented Components

### `.bib-nav` (Figma node 66:2)
- `position: fixed; top:0; left:0; right:0; z-index:1000` on `#masthead.site-header`
- `#about-us-page { padding-top: 72px }` compensates for fixed nav height
- Black bg `#000`, height 72px, max-width 1440px content-wrapper, 48px side gutters
- Nav links: Cina GEO Regular 16px, `rgba(255,255,255,0.6)` default, `#fff` hover
- Active state: `rgba(255,255,255,0.14)` background pill
- Contact CTA: `#FAF6F5` cream button with black text
- Routing: `/home/`, `/about-us/`, `/market/`, external links for Brands/Expertise/Retail/Contact
- Mobile ≤768px: links hidden, burger icon shown

### `.bib-our-company` (Figma node 103:502)
- Full-viewport section (`height: calc(100vh - 72px)`)
- Background: `#051436` midnight + `section-our-company.png` at 72% opacity
- Diagonal scrim: `189.66deg`, transparent 11.42% → `rgba(0,0,0,0.35)` 54.78% → `rgba(0,0,0,0.88)` 90.81%
- Title: Cina GEO Light 80px/96px, letter-spacing -1%
- Eyebrow label: `#C97A3A` sunset-amber, uppercase 14px, 18% letter-spacing
- Stats: SemiBold 40px/48px numbers, dividers `rgba(255,255,255,0.24)` 64px tall
- Content-wrapper: max-width 1440px, 48px gutters, bottom gap 72px

### `.bib-vm` (Figma node 103:560)
- Two equal rows stacked (Vision top, Mission bottom), each 50% of section height
- Each row: full-bleed `object-fit: cover` background image + directional gradient scrim
- Vision row: scrim `#000 → rgba(5,20,54,0)` left-to-right; text in left column
- Mission row: scrim `rgba(5,20,54,0) → #000` at 88.94%; text in right column
- Title: Cina GEO SemiBold 40px/48px, letter-spacing -0.5px
- Body: Regular 18px/24px, `#FAF6F5` canvas color

### `.bib-value` (Figma node 106:604) — Our Value Section
- White bg, 1440px wrapper, 2-column bento grid (4px gap, 48px side gutters)
- Header: 200px height, 2-col grid, title Cina GEO SemiBold 40px/48px
- 6 tiles: Authenticity, Diversity, Empowerment, Team Spirit, Ethicality, Respect
- Each tile has full-bleed photo bg, 40% darken scrim, centered uppercase label (Medium 24px, 10% letter-spacing)
- **Hover interaction:** description subtext reveals via `max-height: 0→120px` + `opacity: 0→1` (500ms easing), image scales 1.05×, label shifts up 8px, scrim darkens
- **Descriptions mapped from old site:** Authenticity, Ethicality, Respect, Empowerment, Diversity texts preserved; Team Spirit added new
- **Mobile (≤640px):** descriptions always visible (no hover on touch devices)
- **Scroll-reveal animations:** IntersectionObserver fires at 15% threshold, each tile has directional entrance:
  - Authenticity: slide from left (100ms delay)
  - Diversity: slide from right (250ms)
  - Empowerment: slide from bottom (400ms)
  - Ethicality: slide from right (550ms)
  - Respect: slide from top (700ms)
  - Team Spirit: slide from left (800ms)
  - Each: 80px offset, 700ms duration, `cubic-bezier(0.22, 0.61, 0.36, 1)`
  - Respects `prefers-reduced-motion: reduce`

### JS Full-Page Scroll Engine
- Every `#about-us-page > section` uses `height: calc(100dvh - 72px)` (with `100vh` fallback) + `overflow-y: auto; overscroll-behavior: contain`
- First section is always visible on load via CSS `:first-child` rule (no animation delay)
- `history.scrollRestoration = 'manual'` + `scrollTo(0,0)` on load prevents stale scroll position on reload
- Slide-in animation: `opacity: 0; transform: translateY(32px)` → `opacity: 1; transform: none` on `.is-in`
- Easing: `cubic-bezier(0.16, 1, 0.3, 1)` (expo-out — fast start, long gentle settle), 900ms duration
- Wheel/touch/keyboard events intercepted; 1100ms movement lock between section jumps
- **Two-phase boundary gate** (replaces old arm/disarm system):
  - Phase 1: scroll hits section top/bottom → all further scroll events are absorbed for 800ms (COOLDOWN)
  - Phase 2: after cooldown expires, the next scroll in the same direction commits the section jump
  - If user stops scrolling for 2000ms (EXPIRE), gate resets
  - Prevents accidental section transitions when reading content at section boundaries
  ```js
  const COOLDOWN = 800, EXPIRE = 2000;
  let gateDir = 0, gateReady = false;
  function hitBoundary(dir) {
      if (gateDir !== dir) { resetGate(); gateDir = dir; gateCooldownId = setTimeout(() => gateReady = true, COOLDOWN); return false; }
      if (gateReady) { resetGate(); return true; } // commit jump
      return false; // still in cooldown
  }
  ```

---

## Sections Status (About Us)

| Section | Figma Node | Status |
|---|---|---|
| Navbar | 66:2 | ✅ Implemented |
| Our Company | 103:502 | ✅ Implemented |
| Our Vision & Mission | 103:560 | ✅ Implemented |
| Our Value | 106:604 | ✅ Implemented (bento grid + hover reveal + scroll-reveal animations) |
| Best in Brands | TBD | ⏳ Original markup (needs redesign) |
| Initiatives | TBD | ⏳ Original markup (needs redesign) |
| Talents at BestinBrands | TBD | ⏳ Original markup (needs redesign) |

---

## Known CSS Gotchas

- WordPress `master.css` conflicts with CSS scroll-snap — use JS scroll engine instead
- Non-breaking spaces (`\xc2\xa0`) in extracted HTML cause Edit tool "string not found" — use Python `re.sub` for those replacements
- Font 404s: CSS path `../../../font/Cina/` in extracted theme resolves to `assets/font/Cina/` — correct URL is `../font/Cina/` relative to `css/` folder
- `position: sticky` on `.bib-nav` inside 72px `<header>` has no scroll range — use `position: fixed` on `#masthead.site-header` instead
- **Section shrinking on reload:** `100vh` is unreliable across reloads (browser chrome state). Fixed by using `100dvh` via `@supports`, CSS `:first-child` always-visible rule, and `history.scrollRestoration = 'manual'`
- **Section transitions:** old arm/disarm scroll system was too sensitive on trackpads. Replaced with two-phase gate (800ms cooldown → then commit). Easing upgraded to expo-out `cubic-bezier(0.16, 1, 0.3, 1)` at 900ms
- **White gap at section bottom:** Applying `transform: translateY(32px)` on full-viewport section containers pushes them down, leaving a 32px gap where the `body` background shows through. Fix: Only apply entrance transforms to internal elements, not the `100vh` section container itself.
- **Vercel Routing:** Deployed site returns 404 because files are inside `extract/`. Fixed by adding `vercel.json` with rewrites `/(.*) -> /extract/$1` and redirects `/ -> /home/`.

---

## Next Steps (from brief §13)
- [ ] Commission Cina GEO webfont license (Public Type)
- [ ] Client: confirm 23 vs 25 years
- [ ] Client: consolidate "Marketing Expertise" / "Expertise" nav items
- [ ] Fix LOGO.svg — `fill="currentColor"`, add BestinBrands wordmark SVG
- [ ] Manually set Cina GEO Test as font family on all 13 text styles in Figma
- [ ] Redesign remaining About Us sections from Figma: Best in Brands, Initiatives, Talents
- [ ] Build remaining page routes (Brands, Expertise, Retail, Contact)
- [ ] Accessibility pass before handoff
- [ ] Developer handoff spec

---

## Session Summary (Latest Updates)
- **Home Hero Banner:** Modernized structure, removed `max-height` restriction to enable full `100vh` display, and added staggered `IntersectionObserver` reveal animations (matching the About Us page).
- **Navigation:** Converted header to `position: fixed` for persistent top placement across all pages.
- **About Us Animations:** Implemented scroll-triggered slide-in animations for "Our Vision & Mission" backgrounds.
- **Animation Replay:** Updated `IntersectionObserver` logic on Home Hero, Our Company, Vision/Mission, and Our Value to dynamically remove active classes when scrolling out of view, allowing animations to cleanly replay upon re-entry.
- **Layout Bug Fix:** Removed redundant container-level `translateY` entrance animations on About Us sections that were causing a 32px white layout gap at the bottom of the screen.
- **Deployment:** Created `vercel.json` at project root to handle URL rewrites (`/extract/*`) and root redirects (`/` -> `/home/`) for seamless Vercel hosting.
