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

## Next Steps (from brief §13)
- [ ] Commission Cina GEO webfont license (Public Type)
- [ ] Client: confirm 23 vs 25 years
- [ ] Client: consolidate "Marketing Expertise" / "Expertise" nav items
- [ ] Fix LOGO.svg — `fill="currentColor"`, add BestinBrands wordmark SVG
- [ ] Manually set Cina GEO Test as font family on all 13 text styles in Figma
- [ ] Build foundation components (nav, footer, button, input, card, hero, stats band, bento, logo grid)
- [ ] Wireframe 7 top-level routes at desktop/tablet/mobile
- [ ] Design Home → About Us → Brands in priority order
- [ ] Accessibility pass before handoff (`design:accessibility-review` skill)
- [ ] Developer handoff spec (`design:design-handoff` skill)
