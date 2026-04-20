# BIB Landing — Design Direction & Style Alignment

> A translation of the *Beauty Company Profile* deck (`BIB_COMPANYPROFILE_BEAUTY_026.pdf`, v026, 52 pp.) into a web design system for `bestinbrands.com`. Every claim below is tied to specific deck pages. Anything I inferred rather than observed is flagged `(inferred)`.
>
> **Updated 2026-04-20 (round 2)** — all 8 Open Questions resolved. Font confirmed as **Cina GEO** (not Gill Sans — updated below). Scroll-reveal motion, English-only scope, mirror current `bestinbrands.com` IA, no data-viz. Remaining work is execution (Figma foundation).
>
> **One content fact to verify with client:** the current site at `bestinbrands.com` states **"23 years"** of experience; the new deck states **"25 years"** (p. 10). Same company, two different numbers. Likely the deck is more current, but this needs a single source of truth before the new site goes live.

---

## 1. Purpose & scope

**Goal.** The new website should feel like a continuation of the company-profile deck — same register, same palette, same photography register, same editorial restraint.

**In scope:** BIB corporate/B2B landing site. Audience per voice guidelines: prospective brand partners, existing partners, retail/channel partners, trade press.

**Out of scope:**
- **Sundora is a customer of BIB** *(confirmed)* — not the same brand. Sundora photography and consumer-facing register (e.g., p. 17 "Beauty Market" divider) stay off this site. Sundora is treated as a named channel partner only, alongside Unimart, Artisan, Daraz.
- E-commerce / D2C consumer flows.
- Visual brand book beyond web (packaging, retail signage, out-of-home).

---

## 2. Visual DNA observed in the deck

These are the recurring visual decisions I extracted from the source, with page references.

| Pattern | Where it appears | Note |
|---|---|---|
| Warm cream page background (not white) | pp. 2, 4, 5, 10–16, 18, 20–22, 25, 30, 40, 45–46 | Almost every content page. Consistent. |
| Full-bleed dark photography, white caps title overlay | pp. 1 (cover), 9 (section divider), 17 (beauty), 24, 52 (closing) | Used for section openers. Signature "hero" pattern. |
| Letter-spaced ALL-CAPS section label, top-left | p. 4, 5, 10, 11, 14, 15, 18, 20, 22, 25, 30, 40, 45, 46 | Single line, no supporting subhead. Thin, restrained. |
| Editorial photographic mosaic / bento | pp. 13 (Values), 14 (Portfolio), 22 (Retail Landscape), 40 (Retail) | Photography is the content; text labels are overlaid white caps. |
| Brand logo grid on neutral panel | p. 15 (Beauty Portfolio), p. 16 (other brand grids) | Clusters under holding-company (PUIG, COTY, LVMH…), white/off-white logos on taupe. |
| Numbered agenda with thin rules | p. 2 | `01 \|` prefix + thin 1px rule under each item. |
| Stats overlay on warm landscape photo | p. 10 (25 yrs / 400+ / 120+) | Proof-point pattern for credentials block. |
| Headshot grid with NAME/ROLE labels | p. 12 | Rows of professional portraits on light panel. |
| Map with muted landmass + teal highlight | p. 5 | Data-geo graphic. Teal-on-sand palette. |
| Pie / bar charts on product photography | pp. 18, 20 | Dusty-rose blocks on muted mauve background. Decorative, hard to read. |
| Logo: "X" crossed-arcs mark + "BestinBrands" wordmark | p. 1, 52 | Only seen in **white/inverted** form in the deck. Mark SVG confirmed at `src/images/LOGO.svg`. |

---

## 3. Color tokens

**Sampled directly from the PDF pages** (pixel-level, from ~seven content pages). Names are descriptive, not branded — rename if there's a house convention.

### Neutrals (the backbone)

| Token | Hex | Role | Source |
|---|---|---|---|
| `surface/canvas` | **#FAF6F5** | Default page background (warm cream) | Dominant bg on pp. 5, 10, 12, 14, 15, 20 |
| `surface/panel` | **#DADADA** | Light card/panel (team, brand-logo grid) | p. 12 headshot panel |
| `ink/primary` | **#2D2B2A** | Headings, titles, body (warm near-black) | Title text on pp. 10, 12, 14 |
| `ink/secondary` | **#413F3E** | Long-form body copy, metadata | Body on pp. 10, 12 |
| `ink/muted` | `#6B6966` *(inferred)* | Captions, micro-copy | Not directly sampled — proposed |
| `rule/hairline` | `#E6E0DC` *(inferred)* | Agenda dividers, section separators | Proposed to match p. 2 rule feel |

### Brand color *(confirmed — Q2)*

Client decision: **BIB's brand color is pure black `#000000`**. This is the UI primitive for CTAs, links, focused states, inverted surfaces, and brand-fill accents. It is distinct from the deck's photographic midnight navy — midnight navy is a photo-tier descriptor, not a UI fill.

| Token | Hex | Role | Note |
|---|---|---|---|
| `brand/ink` | **#000000** | Primary brand color — CTAs, links, primary icons, inverted surface fill | Confirmed |
| `brand/ink-90` | `#1A1A1A` *(inferred)* | CTA hover | Softens a hard click-back against cream |
| `brand/ink-60` | `#666666` *(inferred)* | Disabled / muted interactive | Consistent neutral stop |
| `photo/midnight` | `#051436` | **Photo-tier descriptor, not a UI fill.** Used when specifying hero photography (Padma Bridge family, pp. 1, 9, 52) or the gradient scrim behind white text over navy photography. | Don't use as a brand or UI surface — would introduce ambiguity with `brand/ink`. |

**Skeptical note on pure `#000`.** Three things worth naming before locking:

1. **Pure `#000` on body copy** can read heavy against `#FAF6F5` cream over long reading. The deck's body text actually samples at `#2D2B2A` (warm near-black), which is what `ink/primary` captures. My recommendation: **use `brand/ink #000` for brand elements (logo fill, CTAs, focus rings, links) and `ink/primary #2D2B2A` for headings and body.** This is both faithful to the deck and easier on the eye.
2. **`brand/ink` on `surface/canvas`** → contrast 20.8:1 (AAA). No accessibility concern.
3. **White text on `brand/ink`** → contrast 21:1. No concern.

### Photo-derived accents (use sparingly, not as UI)

| Token | Hex | Where | Use |
|---|---|---|---|
| `photo/sunset-amber` | ~#C97A3A | Stats overlay on p. 10 | Illustrative only — don't weaponize into UI |
| `photo/teal-ocean` | ~#2E7A94 | Map on p. 5 | Illustrative only — data-viz accent allowed |
| `photo/dusty-rose` | ~#C99A9C | Chart blocks on pp. 18, 20 | Avoid in UI — too fashion-cosmetic, pulls toward Sundora/consumer register |
| `photo/taupe` | ~#58534D | Brand-logo panel bg on p. 15 | Tier divider / press quote panel |

### Semantic (inferred — the deck has none)

The deck contains no UI states. Proposing a conservative web palette grounded in neutrals:

| Token | Hex | Role |
|---|---|---|
| `semantic/success` | `#3A7A3A` | Confirmations |
| `semantic/warning` | `#B88128` | Warnings |
| `semantic/error` | `#B0352E` | Errors |
| `semantic/info` | `#2D4878` | Informational |

**Flag:** there is no established BIB semantic palette. These are starting points only, to be reviewed against the website's actual error/empty-state needs.

### Contrast & accessibility

- `ink/primary #2D2B2A` on `surface/canvas #FAF6F5` → **contrast ratio ≈ 14.5:1** (AAA).
- `brand/ink #000000` on `surface/canvas #FAF6F5` → **contrast ratio ≈ 20.8:1** (AAA).
- `#FFFFFF` on `brand/ink #000000` → **contrast ratio 21:1** (AAA).
- `#FFFFFF` on `photo/midnight #051436` → **contrast ratio ≈ 17.5:1** (AAA).
- **White body text over photography** (pp. 4, 10, 11, 17, 45, 46) **fails WCAG AA at small sizes** on many source pages because there is no consistent overlay/scrim. On web, this pattern needs either a fixed-opacity scrim or a gradient under the text block. Do not replicate the deck's text-on-photo treatment verbatim.

---

## 4. Typography *(confirmed — Q1: Cina GEO)*

Client confirmed the deck's source typeface is **Cina GEO** — a geometric sans designed by **Michael Cina** and published by **Public Type** in 2022. This changes the direction from the humanist-sans assumption in round 1; Cina GEO is squarely **geometric**, drawn in the lineage of Futura / Geosans with a few idiosyncratic softenings.

### Cina GEO — what it is and how to license it

| Property | Detail |
|---|---|
| Designer | Michael Cina |
| Foundry | Public Type (publictype.us) |
| Released | 2022 |
| Classification | Geometric sans-serif (not humanist) |
| Weights | **9 weights:** Thin, ExtraLight, Light, Regular, Medium, SemiBold, Bold, ExtraBold, Black (each with matching italic) |
| Italics | Yes, true italics across all 9 weights |
| OpenType | Standard ligatures, small caps, tabular figures, stylistic alternates |
| Licensing | **Free for personal use.** Commercial use requires a paid license from Public Type. Webfont licenses are tier-priced (pageview and/or domain count) — foundry quote needed. |
| Bengali coverage | **None** — Latin-only. (Not an issue: Q8 confirmed English-only scope.) |

**Licensing action item.** Commercial webfont license required before launch. Contact Public Type directly (contact@publictype.us) for a quote. Unlike Monotype's subscription model, small-foundry licenses are usually a one-time purchase tied to pageview bands — often cheaper over multi-year horizons than a Gill Sans Nova subscription would be.

**No free substitute shipped with the site.** Geometric-sans free alternatives (Geist, Work Sans, DM Sans, Neue Haas Grotesk clones) visually read too differently from Cina GEO's specific proportions to be viable here. Budget for the commercial license.

**Local-file fallback for Figma:** if the team already has a desktop license of Cina GEO via the designer's personal account, install it locally in Figma. Confirm with client who holds the license before that becomes a bottleneck.

### Type ramp (Cina GEO)

A modular scale on an 8pt grid. Weight tokens use Cina GEO's 9-weight family directly.

| Token | Weight | Size (desktop) | Line | Tracking | Notes |
|---|---|---|---|---|---|
| `display/hero` | **Medium (500)** | 64–80px | 1.05 | -0.01em | Full-caps hero titles (cover pattern). Geometric sans typically needs lighter weight at display sizes than humanist — Medium, not Bold. |
| `display/section` | **Medium (500)** | 40–56px | 1.1 | 0 | Section openers |
| `label/section` *(all-caps)* | **Regular (400)** | 14–16px | 1.3 | **+0.18em** | The signature letter-spaced label — top-left of most content pages |
| `heading/h1` | **SemiBold (600)** | 40px | 1.15 | -0.005em | Page title (non-hero) |
| `heading/h2` | **SemiBold (600)** | 32px | 1.2 | 0 | Section head |
| `heading/h3` | **Medium (500)** | 24px | 1.3 | 0 | Sub-section |
| `body/lg` | **Regular (400)** | 18px | 1.55 | 0 | Introductory body |
| `body/md` | **Regular (400)** | 16px | 1.6 | 0 | Default body |
| `body/sm` | **Regular (400)** | 14px | 1.55 | 0 | Secondary copy |
| `caption` | **Regular (400)** | 12px | 1.5 | +0.04em | Metadata, photo captions |
| `stat/number` | **Bold (700)** | 56–80px | 1 | -0.01em | Credentials block (25 / 400+ / 120+) |
| `stat/label` | **Regular (400)** | 14–16px | 1.3 | 0 | Stat descriptor |

### Rules specific to Cina GEO (not Gill Sans)

- **Weight calibration is different from Gill Sans.** Geometric sans types need lighter weights at large sizes — a Bold hero in Cina GEO reads heavier than in Gill Sans. Default hero and section display to **Medium (500)**, not SemiBold/Bold. Review at spec sign-off.
- **Geometric O, C, G → wide circular counters.** Don't set hero titles too tight (`tracking ≤ -0.02em` will collide the counters). Keep display tracking between `-0.01em` and `0`.
- **Small-caps feature** is present in Cina GEO OpenType. Prefer true small caps (`font-feature-settings: "smcp"`) over CSS `text-transform: uppercase` for non-display caps — better even-stroke density.
- **Use all-caps** for section labels and primary/hero display text only. Don't extend to body, lists, or UI labels — geometric caps are visually louder than humanist caps.
- Never stack more than two type sizes in the same text block.
- Keep paragraph measure between **50–75 characters**. The deck's full-bleed body-over-photo blocks (pp. 45, 46) run too wide; web should narrow them.
- **Italic treatment differs.** Cina GEO's italics are true italics with geometric construction — they read as a deliberate register shift, not a decoration. Reserve italic for press quotes and editorial pull quotes, not for emphasis inside body.
- **Bengali companion font no longer needed.** Q8 confirmed English-only scope — removes the previous round's requirement for a Bengali pair.

---

## 5. Imagery rules

### Photography register

The deck uses four distinct photo families. Treat them as tiers:

| Tier | Register | Examples in deck | Web usage |
|---|---|---|---|
| **T1 — Bangladesh-scale** | Night landscapes, Padma Bridge, Dhaka skyline, aerial roundabouts; deep navy/midnight, long exposures, starfields | pp. 1, 9, 10, 11, 51, 52 | **Signature.** Use for the homepage hero and major section openers. This is the BIB photo DNA. |
| **T2 — Business / people** | Studio portraits on neutral backgrounds, team grid | p. 12 | Leadership, careers, about. Keep on `surface/panel` (#DADADA) with generous whitespace. |
| **T3 — Retail environment** | Store interiors, mall exteriors, travel retail, fragrance displays | pp. 22, 25, 30, 40, 45, 46 | "How we distribute" content. Photograph BIB's own retail footprint, not stock. |
| **T4 — Editorial product / category** | Moody product stills, editorial hand shots, mosaic category grids | pp. 13, 14, 20 | Category explainers. Handle with care — can slide into consumer/Sundora register. |

### Rules

- **No stock photography without scrutiny.** The deck's images read as specific (real Bangladesh, real stores). Stock kills that register.
- **Always include a scrim when overlaying text.** Minimum 40% black linear gradient from the text side, or a solid 65–85% black panel behind body copy. Non-negotiable for accessibility.
- **No illustration, no 3D render, no gradient backgrounds outside photography.** The deck has zero illustration; the web should follow.
- **No cartoon/icon bento tiles.** The category mosaic on p. 14 works because it's all photographic — swap any tile to an icon and the register collapses.

---

## 5a. Information architecture *(confirmed — Q5: mirror current bestinbrands.com)*

Client confirmed: mirror the existing `bestinbrands.com` information architecture. This is a revamp, not a re-scoping — so we keep the page set and navigation labels the user base already understands, and invest the visual-design work in surface quality, not rearchitecture.

### Top-level navigation (from current site)

| Label | Scope | Notes |
|---|---|---|
| **Home** | Hero + credentials band + portfolio preview + partner logos + contact CTA | The single longest scroll page on the site. Uses the most section-divider heroes. |
| **Brands** | Parent page + child pages per category | **Children:** Perfume · Skincare & Makeup · Toys · Food & Beverage · Sports. Each child = brand-logo grid + editorial category photography (T4 register). |
| **Retail Partners** | Who BIB distributes to | **Children:** Department Stores · Supermarkets · Hospitality · Restaurants · E-commerce · Corporate. Each child = partner-logo grid + short blurb + representative T3 photography. |
| **Marketing Expertise** | How BIB supports partners | Service description page. |
| **Expertise** | Overlapping with Marketing Expertise — **see flag below** | |
| **About Us** | Company story, leadership, values, timeline | Pulls team grid (p. 12) and mission/vision (p. 11) from the deck. |
| **Contact** | Offices, map, form | Uses closing page (p. 52) as the visual reference — Padma Bridge hero, three addresses, form below. |

### Flag for client — "Marketing Expertise" vs "Expertise"

The current site has **two separate nav items with overlapping names**. This is almost always a redundancy, not two different things. Before we wireframe nav, the client should confirm:

1. Are these truly two distinct pages (and if so, what's the content difference)?
2. Or should they consolidate into one — e.g., "Expertise" with sub-sections for Marketing, Distribution, Retail Execution?

Consolidating would tighten the nav from 7 items to 6 and remove user confusion about which page has what. Recommendation: consolidate unless there's a strong business reason not to.

### Pages explicitly *not* migrating

- **No Sundora-specific sub-section** on BIB's site (Q6 resolved — Sundora is a customer, not a brand under BIB).
- **No data/market-research pages** beyond what's on Home (Q7 resolved — no charts).
- **No language switcher** (Q8 resolved — English only).

---

## 6. Layout patterns

### Grid

- **12-column** desktop, 24px gutters, 80px horizontal margin ≥ 1440px viewport.
- **8-column** tablet, 16px gutters, 32px margin.
- **4-column** mobile, 16px gutters, 20px margin.
- Vertical rhythm on **8pt** scale.

### Reusable page blocks (derived from deck slide archetypes)

| Deck pattern → | Web block | Notes |
|---|---|---|
| Cover (p. 1) | **Hero full-bleed** | Navy-tinted photo (T1), left-aligned caps title, logo top-left, scroll cue bottom. 72–100vh. |
| Agenda (p. 2) | **Split 50/50** | Photo left, numbered list right. 500+ viewport width; stacks on mobile. |
| Credentials (p. 10) | **Stats row** | 4–5 stats on photo hero band, scrim behind stats. |
| Vision/Mission (p. 11) | **Two-column on dark hero** | Paired statement block. Don't exceed 2 columns. |
| Team (p. 12) | **Headshot grid** | 4 cols desktop / 2 cols tablet / 2 cols mobile. Square crops. |
| Values mosaic (p. 13) | **Photo bento** | 6 cells, mixed aspect ratios. Each cell = photo + caps label. Caption only on hover/focus on desktop; always-visible on touch. |
| Portfolio mosaic (p. 14) | **Category bento** | 7 cells, photo-led, same rules as values. |
| Brand logos (p. 15) | **Holding-company grid** | Taupe panel, clusters under holding-company headers. Logos monochrome/inverted. |
| Retail evolution (pp. 22, 30, 40) | **Photo + caption row** | 3-up photo strip with caption below each. |
| Skin/Makeup routine (pp. 45, 46) | **Steps row** | Numbered product/step row on photo background (add scrim). |
| Closing (p. 52) | **Contact hero** | Full-bleed signature Padma Bridge photo, logo center, addresses bottom. |

### Section divider behavior

A section divider in the deck is a full-bleed dark hero with a single caps label. On web, this pattern is useful for **major navigation sections** (e.g., between "Who we are" and "How we distribute") but shouldn't be over-used — every hero page on scroll quickly becomes fatiguing. **Budget: 2–3 section dividers per landing page max.**

---

## 7. Components for the landing page

Minimum component set to ship a BIB landing site:

- **Navigation:** top-bar (logo left, menu center/right, CTA right); transparent-over-photo variant for heroes, solid `surface/canvas` variant on scroll. Logo uses white fill on dark heroes, `brand/ink` on cream.
- **Footer:** three-column, dark (`brand/ink` or `photo/midnight` per client preference), with office addresses (from p. 52), contact, social, legal.
- **Hero (3 variants):** full-bleed photo hero, split hero, quiet cream hero.
- **Stats band:** 4–5 stat cards on dark hero.
- **Section label:** `label/section` caps + thin hairline rule.
- **Card:** photo-led, caps label overlay, optional body on hover.
- **Brand-logo grid:** holding-company cluster, monochrome logos on taupe.
- **Quote / press pull:** italic or Gill Sans Italic on `surface/panel`.
- **CTA button:** `brand/ink` fill, white text; outline variant; ghost variant; hover → `brand/ink-90`.
- **Form elements:** input, textarea, select, checkbox — neutral-first, `brand/ink` for focus rings.
- **Page divider:** full-bleed dark section.
- **Contact block:** addresses + map embed (or static map image).

**Responsive.** Build mobile-first. All photo-led bento blocks need a collapse-to-stack mobile spec — don't shrink slides, restructure them.

**Interaction states.** The deck has zero interaction states. Propose for each component: default / hover / focus / active / disabled. Lock these in Figma Variables before building.

**Motion — scroll-reveal (confirmed Q4).** The landing page uses scroll-triggered reveals as its primary motion pattern. Specifics:

- **Fade + rise (8–16px translateY), 400–600ms, `cubic-bezier(0.22, 0.61, 0.36, 1)`** for text blocks and cards entering viewport.
- **Trigger threshold:** element at **15%** past viewport top (not 0% — avoids pop-in on fast scrolls).
- **Stagger** grid cells by **60–80ms** in reading order. Never more than 6 cells per stagger before snapping to simultaneous.
- **No parallax on hero photography.** It fights the scrim and causes layout shift on mobile Safari. If we want a hero sense of depth, use a slow `scale(1.02 → 1)` over the full hero visible range instead.
- **`prefers-reduced-motion: reduce`** disables all reveals — elements appear statically at full opacity. Required, not optional.
- **No auto-playing carousels, no parallax, no confetti.** Keep the tone editorial — this is a distributor's corporate site, not a product launch.

**Accessibility target.** WCAG 2.1 AA. Specifically: all text-on-photo at ≥ 4.5:1, focus rings visible against any background, touch targets ≥ 44×44px.

---

## 8. Deck → Web: what breaks, and how we fix it

This is where "make the website look like the deck" gets complicated. The deck optimizes for presentation (16:9, sequential reading, speaker present). The website optimizes for self-service, responsiveness, search, and accessibility.

| Deck assumption | Why it breaks on web | Proposed fix |
|---|---|---|
| 16:9 canvas | Viewports range from 320px to 3440px wide | Restructure every slide into a component that reflows at 4 breakpoints |
| Sequential reading | Users scan / skim / enter mid-page | Add section navigation, in-page TOC on long pages, scroll-cue anchors |
| Text-over-photo without scrim | Fails contrast AA at small sizes | Mandatory scrim or solid panel behind all body copy on photography |
| All-caps body chunks (e.g., stats labels) | Tanks readability; breaks screen-reader pronunciation | Use CSS `text-transform: uppercase` only on short labels, not body |
| Fine letter-spacing at small sizes | Crushes legibility below 12px | Only apply tracking at ≥ 14px; remove below that |
| No interaction states | No hover, focus, or loading behavior defined | Specify all 5 states per component in Figma |
| Heavy full-page photography | Slow page weight, poor LCP | Use `next/image`-style responsive images, AVIF/WebP, lazy-load below-the-fold, cap hero images at ~200KB served |
| Decorative all-caps section labels | Fail as `<h1>/<h2>` if styled incorrectly | Keep semantic heading tags; the caps styling is presentational only |
| Beauty Market divider (p. 17) | Consumer register — doesn't match BIB B2B voice | Excluded from this site *(Q6 confirmed)*. |
| Cina GEO needs a commercial webfont license | Small-foundry paid license | See Section 4 — contact Public Type for pageview-tier quote. No free substitute. |
| Pie/bar charts on pp. 18, 20 | Consumer/decorative register, not needed | **Removed entirely** — Q7 confirmed no charts on the new site. |

---

## 9. Sundora & the consumer/B2B boundary *(confirmed — Q6)*

Sundora is a customer of BIB, **not the same brand** (client-confirmed). This matters for visual design because the deck lets Sundora's consumer register leak in (p. 17 in particular).

**Rules for this site:**
- The site's primary register is BIB B2B — reserved, evidence-led, cream-and-black.
- Sundora is referenced as a named channel partner alongside Unimart, Artisan, Daraz. Same treatment as any other channel.
- Do not port Sundora photography (sequin party shots, Gen-Z beauty energy) into the BIB site. That photography belongs on Sundora's own site.
- The `photo/dusty-rose` and `photo/mauve` accents (pp. 18, 20) pull toward Sundora/consumer register — avoid them in UI.

---

## 10. Logo assets *(Q3 answered)*

**File:** `src/images/LOGO.svg`.

**What's in the file:**
- The "crossed arcs / X" mark only (no "BestinBrands" wordmark).
- Viewbox `0 0 83 99`; aspect is taller than wide.
- **Hard-coded `fill="white"`** — the mark is white-only as delivered.

**What needs to happen before production:**

1. **Replace `fill="white"` with `fill="currentColor"`** in the SVG `<path>`. This lets CSS control the color per context (white on dark hero, `brand/ink #000` on cream nav, etc.) without shipping two files.
2. **Add the "BestinBrands" wordmark as a separate SVG** if you want the combined logo (as on the cover, p. 1). The current file is mark-only.
3. **Provide a monochrome dark version** if the wordmark isn't already single-color — the deck's wordmark reads white-on-dark; a black-on-light version for light hero nav is needed.

Per client: "it's gonna be heavy-image, so it'll be dark" — interpreting this as: heroes and nav will predominantly sit on dark photography, so the white mark is the default. The `currentColor` change above just gives you the flexibility for the exceptions (footer on cream, press kit, etc.) without a separate file.

---

## 11. Verification — what I observed vs. inferred

| Claim | Status |
|---|---|
| Page background #FAF6F5 | **Observed** (pixel sampled, pp. 5, 10, 12, 14, 15, 20) |
| Ink color #2D2B2A → #413F3E | **Observed** (sampled from titles/body) |
| Brand color #000000 | **Confirmed by client (Q2)** |
| Photo-tier midnight #051436 | **Observed** (cover p. 1 sampled #041335, closing p. 52 sampled #051436) |
| Warm taupe #58534D for brand-logo panel | **Observed** (p. 15, sampled) |
| Light-gray panel #DADADA | **Observed** (p. 12) |
| Semantic color palette | **Inferred** — deck has none |
| Typeface: **Cina GEO** (Michael Cina / Public Type, 2022) | **Confirmed by client (Q1, revised)** |
| `ink/muted` #6B6966, `rule/hairline` #E6E0DC, `brand/ink-90/60` | **Inferred** — proposed for UI needs |
| Photography tiers | **Observed** — four distinct families |
| 12/8/4-column responsive grid | **Proposed** — deck has no grid system |
| Logo asset at `src/images/LOGO.svg`, white fill | **Confirmed by file inspection** |
| Scroll-reveal motion (fade + rise, staggered) | **Confirmed by client (Q4)** |
| Content scope mirrors current `bestinbrands.com` | **Confirmed by client (Q5)** |
| No data visualization / charts | **Confirmed by client (Q7)** |
| English-only scope; no Bengali companion font | **Confirmed by client (Q8)** |
| **"23 years" (current site) vs "25 years" (new deck, p. 10)** | **Client to verify** — pick one and cascade across site and materials |

---

## 12. Open questions — all resolved

### Resolved

1. ~~**Deck source fonts.**~~ → **Cina GEO** (Michael Cina / Public Type, 2022). Geometric sans — 9 weights. Commercial webfont license required from Public Type. Full specs in Section 4.
2. ~~**Brand accent.**~~ → **`#000000`.** Reconciled with the deck's photographic midnight in Section 3.
3. ~~**Logo.**~~ → **Provided** at `src/images/LOGO.svg`. Fixes noted in Section 10.
4. ~~**Motion & interaction.**~~ → **Scroll-triggered reveals** (fade + rise, 400–600ms, staggered 60–80ms, honors `prefers-reduced-motion`). No parallax. No auto-carousels. Full spec in Section 7.
5. ~~**Content scope.**~~ → **Mirror current `bestinbrands.com` IA.** Architecture and sections in Section 5a below.
6. ~~**Sundora boundary.**~~ → **Confirmed:** Sundora stays out of the site's visual language.
7. ~~**Data visualization.**~~ → **No charts.** The new site carries no data viz — only credential stats (25/400+/120+ band).
8. ~~**Languages.**~~ → **English only.** No Bengali companion font needed. Cina GEO's Latin-only coverage is sufficient.

### One fact to verify with client (not a design decision)

**"23 years" vs "25 years."** Current site says 23; new deck says 25. Same company. Before launch, confirm the correct number and cascade it across `display/hero`, credentials band, and the copy in About/Contact. Likely the deck is more current, but we should not assume.

---

## 12a. WordPress token translation

Tokens from Sections 3 (color), 4 (typography), 6 (layout), and 7 (motion) are translated into WordPress-native files. These sit at the repo root and are the **operational source of truth** for the theme — the markdown brief remains the design source of truth, but the JSON/CSS files are what WordPress actually reads.

### Files

| File | Role | Consumed by |
|---|---|---|
| `theme.json` | Canonical token registry — colors, font families + faces, font sizes, spacing scale, shadow presets, block-level defaults, element styles (h1–h4, buttons, links, paragraphs, quotes, separators) | WordPress block theme (v6.6+). Auto-generates `--wp--preset--*` CSS vars and Global Styles UI controls. |
| `tokens.css` | CSS custom properties mirror — identical values, `--bib-*` naming | Classic PHP templates, external embeds, dev tooling, any context where WordPress's auto-generated vars aren't available. |

### Slug mapping (WordPress convention)

WordPress generates CSS variables from `theme.json` slugs using the pattern `--wp--preset--{category}--{slug}`. The mapping from the brief's token names to WordPress slugs:

| Brief token | theme.json slug | Generated CSS var |
|---|---|---|
| `surface/canvas` | `canvas` | `--wp--preset--color--canvas` |
| `surface/panel` | `panel` | `--wp--preset--color--panel` |
| `ink/primary` | `ink-primary` | `--wp--preset--color--ink-primary` |
| `ink/secondary` | `ink-secondary` | `--wp--preset--color--ink-secondary` |
| `ink/muted` | `ink-muted` | `--wp--preset--color--ink-muted` |
| `rule/hairline` | `rule-hairline` | `--wp--preset--color--rule-hairline` |
| `brand/ink` | `brand-ink` | `--wp--preset--color--brand-ink` |
| `brand/ink-90` | `brand-ink-90` | `--wp--preset--color--brand-ink-90` |
| `brand/ink-60` | `brand-ink-60` | `--wp--preset--color--brand-ink-60` |
| `photo/midnight` | `photo-midnight` | `--wp--preset--color--photo-midnight` |
| `photo/taupe` | `photo-taupe` | `--wp--preset--color--photo-taupe` |
| `semantic/*` | `semantic-success`, `semantic-warning`, `semantic-error`, `semantic-info` | `--wp--preset--color--semantic-*` |
| `display/hero` | `display-hero` (font-size) | `--wp--preset--font-size--display-hero` |
| `display/section` | `display-section` | `--wp--preset--font-size--display-section` |
| `heading/h1–h3` | `heading-h1`, `heading-h2`, `heading-h3` | `--wp--preset--font-size--heading-*` |
| `body/lg`, `body/md`, `body/sm` | `body-lg`, `body-md`, `body-sm` | `--wp--preset--font-size--body-*` |
| `caption` | `caption` | `--wp--preset--font-size--caption` |
| `stat/number` | `stat-number` | `--wp--preset--font-size--stat-number` |
| Cina GEO | `cina-geo` (font-family) | `--wp--preset--font-family--cina-geo` |
| 8pt spacing scale | `4xs`..`4xl` | `--wp--preset--spacing--{4xs..4xl}` |

### Font-file deployment

`theme.json` references font files under `file:./assets/fonts/CinaGEO-*.woff2`. Before any WP build:

1. **Acquire the commercial webfont license** from Public Type (see Section 4).
2. **Convert the delivered files to WOFF2** if the foundry provides OTF/TTF only. `fonttools` or `glyphhanger` handle this.
3. **Place files** at `{theme-root}/assets/fonts/` matching the filenames in `theme.json`.
4. **Verify** via WP admin → Appearance → Editor → Styles → Typography: Cina GEO should appear in the font dropdown, with all 9 weights available.

The font-family list in `theme.json` includes all 9 weights × 2 styles (upright + italic) = 18 faces. If the foundry ships only a subset, delete the unused `fontFace` entries to prevent 404s.

### What's not in theme.json and why

- **Motion tokens** (scroll-reveal duration, easing, stagger, reveal offset). WordPress's theme.json has no motion primitives. These live only in `tokens.css` as `--bib-motion-*` and should be consumed by custom blocks or a small motion JS module — not by Gutenberg core.
- **Photo-tier descriptors (`photo/*`)** are included in the palette because the block editor's color picker will offer them for authors — with descriptive names like "Photo Dusty Rose (avoid in UI)" so editors understand not to use them as UI fills. Remove from the palette if you want to hide them from authors entirely.
- **Semantic palette** ships as starting values. Until a real error/warning/info state is specified, these are inferred — see Section 3.
- **Z-index scale and touch-target minimum** live in `tokens.css` only — WordPress has no concept for these at the token level.

### Compatibility target

- **WordPress 6.6+ block theme** (schema version 3). Font faces via `fontFace` are supported without third-party plugins.
- **WordPress 6.1–6.5** works with schema version 2 — downgrade the `version` field if required.
- **Classic themes (PHP templates, non-block)** — use `tokens.css` directly and ignore `theme.json`. All `--bib-*` variables are available globally once the stylesheet is enqueued.
- **Gutenberg blocks on a classic theme** — you can still ship `theme.json` alongside classic PHP templates; Gutenberg reads it for block-editor styles while PHP continues rendering page shells.

### Verification checklist before first commit

- [ ] `theme.json` validates against `https://schemas.wp.org/trunk/theme.json` (use VS Code with the JSON schema registered, or `wp theme.json validate` via WP-CLI).
- [ ] All font files exist at the referenced paths. No 404s in the Network tab on the homepage.
- [ ] Color swatches render in the Global Styles UI under Appearance → Editor → Styles → Colors.
- [ ] Font sizes render in the block toolbar size picker. Fluid sizes clamp correctly at viewport <768px and >1440px.
- [ ] `--wp--preset--color--canvas` is readable from CSS inside a block editor iframe (spot-check via DevTools).
- [ ] `prefers-reduced-motion: reduce` at the OS level disables the `.bib-reveal` animation — test on both macOS (System Settings → Accessibility → Display) and iOS.
- [ ] Link hover state shows `--brand-ink-90` (not default WP blue) — verify on a fresh install with no plugin overrides.

---

## 13. Next steps

Order these in the Figma file itself — not as separate tickets.

1. **Commission Cina GEO webfont license from Public Type** — contact contact@publictype.us for a pageview-tier quote. Block #3 (Figma Variables) on this — we can't lock type styles without the licensed files.
2. **Client to verify the "23 vs 25 years" fact** — quick check, one source of truth cascades to deck, site, and all comms.
3. **Client to confirm or consolidate "Marketing Expertise" / "Expertise"** — see Section 5a flag. Affects nav wireframes.
4. **Fix the logo SVG** — replace `fill="white"` with `fill="currentColor"`, commission "BestinBrands" wordmark SVG.
5. **Drop `theme.json` and `tokens.css` into the WordPress theme** at its root (`/wp-content/themes/{theme}/`). Run the verification checklist in Section 12a. Confirm the block editor picks up the palette and font sizes before any layout work.
6. **Set up Figma Variables** mirroring the same slugs as `theme.json` (so Figma → WordPress translation is a rename, not a re-derivation). Use modes for light (cream canvas) and dark (photo-hero context). Motion tokens per Section 7.
7. **Build moodboard page in Figma** — pull 8–12 reference frames from the deck (full-size pages), plus 4–6 web references for the distribution/holding-company register (LVMH corporate, Kering, Interparfums, DFS, Inter IKEA) annotated with *what specifically* is being referenced.
8. **Build foundation components** (Section 7): nav, footer, button, input, card, hero variants, stats band, section label, photo bento, brand-logo grid. Include all 5 interaction states per component. Include scroll-reveal specs (Section 7) as a dedicated "Motion" page.
9. **Wireframe the 7 top-level routes** (Section 5a) at desktop/tablet/mobile. Don't design yet — just IA + content-block choreography using the block vocabulary in Section 6.
10. **Design the three highest-value pages in priority order:** Home → About Us → Brands (category landing). Applied examples convert a token system into a working design language — and these three exercise every component in Section 7.
11. **Accessibility pass** with the `design:accessibility-review` skill before handoff. Don't skip — the deck's text-on-photo habit is the #1 thing that will fail.
12. **Developer handoff spec** with the `design:design-handoff` skill once the system is approved.

---

*This brief is a starting position, not a lock. I've marked every place I inferred rather than observed. Push back on anything that doesn't match what you see in the deck.*
