# Design System: BestinBrands (BIB) Landing Site
### Corporate B2B Web Revamp — bestinbrands.com

> Source of truth: `design-direction-brief.md` (all 8 open questions resolved), `tokens.css`, `theme.json`.
> This document translates those sources into a component-level implementation reference.
> Brand voice reference: `.claude/brand-voice-guidelines.md`

---

## Visual DNA

### Palette

All colors sampled pixel-level from `BIB_COMPANYPROFILE_BEAUTY_026.pdf`.

| Token | CSS var | Hex | Role |
|---|---|---|---|
| Canvas (warm cream) | `--bib-canvas` | `#FAF6F5` | Default page background — almost every content page in the deck |
| Ink Primary (warm near-black) | `--bib-ink-primary` | `#2D2B2A` | Headings, titles, body copy — warmer than pure black |
| Ink Secondary | `--bib-ink-secondary` | `#413F3E` | Long-form body, metadata |
| Ink Muted | `--bib-ink-muted` | `#6B6966` | Captions, micro-copy *(inferred)* |
| Panel (light neutral) | `--bib-panel` | `#DADADA` | Card/panel backgrounds — headshot grid (p. 12), brand-logo grid |
| Rule / Hairline | `--bib-rule-hairline` | `#E6E0DC` | Section separators, agenda dividers *(inferred from p. 2)* |
| Brand Ink (primary black) | `--bib-brand-ink` | `#000000` | CTAs, links, focus rings, inverted surfaces — **confirmed by client** |
| Brand Ink 90 (hover) | `--bib-brand-ink-90` | `#1A1A1A` | CTA hover — softens hard click-back against cream |
| Brand Ink 60 (disabled) | `--bib-brand-ink-60` | `#666666` | Disabled / muted interactive |
| Photo Midnight | `--bib-photo-midnight` | `#051436` | **Photo-tier descriptor only.** Hero photography (Padma Bridge, pp. 1, 9, 52). Never a UI fill. |
| Photo Taupe | `--bib-photo-taupe` | `#58534D` | Brand-logo panel background (p. 15) |
| White | `--bib-white` | `#FFFFFF` | Text on dark heroes, inverted elements |

**Photo-only colors — do not use as UI fills:**

| Token | Hex | Source | Risk |
|---|---|---|---|
| Photo Sunset Amber | `#C97A3A` | Stats overlay p. 10 | Illustrative only |
| Photo Teal Ocean | `#2E7A94` | Map p. 5 | Data-viz accent only |
| Photo Dusty Rose | `#C99A9C` | Chart blocks pp. 18, 20 | Avoid — pulls toward Sundora consumer register |

**Contrast verification (WCAG 2.1 AA):**
- `#2D2B2A` on `#FAF6F5` → **14.5:1 AAA** ✓
- `#000000` on `#FAF6F5` → **20.8:1 AAA** ✓
- `#FFFFFF` on `#000000` → **21:1 AAA** ✓
- `#FFFFFF` on `#051436` → **17.5:1 AAA** ✓
- White body text over photography without scrim → **fails AA at small sizes** — scrim is mandatory

**Atmosphere rules:**
- No decorative shadows. No gradients except photo scrims.
- No illustration, no 3D render, no gradient backgrounds outside photography.
- Borders use `--bib-rule-hairline` (#E6E0DC), 1px or `0.5px`.
- Border radius: `--bib-radius-none` 0px · `--bib-radius-sm` 2px · `--bib-radius-md` 4px — use sparingly; CTA buttons are `0px` (sharp).

---

### Typography

**Typeface: Cina GEO** — geometric sans by Michael Cina, Public Type (2022).
9 weights × 2 styles (upright + italic) = 18 font faces.
**Commercial webfont license required before launch.** Contact: `contact@publictype.us`.

```css
--bib-font-primary: "Cina GEO", "Helvetica Neue", Arial, sans-serif;
```

Fallback for local Figma work: Inter or DM Sans at matching weights. Not for production.

**Type ramp (8pt grid):**

| Style token | CSS var | Weight | Size (desktop) | Line height | Tracking | Notes |
|---|---|---|---|---|---|---|
| `display/hero` | `--bib-fs-display-hero` | Medium 500 | clamp(48px→80px) | 1.05 | −0.01em | Full-caps hero titles. Geometric: Medium, not Bold at display. |
| `display/section` | `--bib-fs-display-section` | Medium 500 | clamp(40px→56px) | 1.1 | 0 | Section openers |
| `heading/h1` | `--bib-fs-h1` | SemiBold 600 | 40px | 1.15 | −0.005em | Page title (non-hero) |
| `heading/h2` | `--bib-fs-h2` | SemiBold 600 | 32px | 1.2 | 0 | Section head |
| `heading/h3` | `--bib-fs-h3` | Medium 500 | 24px | 1.3 | 0 | Sub-section |
| `label/section` | `--bib-fs-body-sm` | Regular 400 | 14–16px | 1.3 | **+0.18em** | Signature letter-spaced ALL-CAPS label, top-left — the deck's most recurring pattern |
| `body/lg` | `--bib-fs-body-lg` | Regular 400 | 18px | 1.6 | 0 | Introductory body |
| `body/md` | `--bib-fs-body-md` | Regular 400 | 16px | 1.6 | 0 | Default body |
| `body/sm` | `--bib-fs-body-sm` | Regular 400 | 14px | 1.55 | 0 | Secondary copy |
| `caption` | `--bib-fs-caption` | Regular 400 | 12px | 1.5 | +0.04em | Photo captions, metadata |
| `stat/number` | `--bib-fs-stat-number` | Bold 700 | clamp(56px→80px) | 1 | −0.01em | Credentials band: 25 / 400+ / 120+ |

**Cina GEO rules (geometric-specific):**
- Hero/section display defaults to **Medium 500**, not SemiBold — geometric sans reads heavier than humanist at display sizes.
- Display tracking: keep between `−0.01em` and `0`. Wider circular counters will collide tighter than that.
- Use CSS `font-feature-settings: "smcp"` (true small caps) for the `label/section` style rather than `text-transform: uppercase` only — better stroke density.
- Reserve italic for press quotes and editorial pull-text, not inline emphasis.
- Paragraph measure: **50–75 characters** (≈ `65ch` max). Non-negotiable for reading comfort.
- Tracking: only apply letter-spacing at ≥ 14px. Remove below that — crushes legibility.

---

### Grid

| Breakpoint | Columns | Gutter | Margin |
|---|---|---|---|
| Desktop ≥ 1440px | 12 | 24px | 80px |
| Tablet 768–1439px | 8 | 16px | 32px |
| Mobile 320–767px | 4 | 16px | 20px |

- **Base unit:** 8pt vertical rhythm
- **Content width:** 720px (body text, narrow layouts)
- **Wide width:** 1280px (full-bleed bento, photo rows, brand-logo grids)
- Build **mobile-first**. All bento/photo blocks collapse to stack — don't shrink, restructure.

---

## Component Specifications

### Navigation — Transparent / Sticky

```
[ BIB Mark + BestinBrands wordmark ]   [ Home · Brands · Retail Partners · Expertise · About · Contact ]   [ → Get in Touch ]
```

**Two states:**

| State | Background | Text | Logo fill |
|---|---|---|---|
| Over photo hero | `transparent` | `#FFFFFF` | white (current LOGO.svg default) |
| Scrolled / on cream | `rgba(250,246,245,0.95)` + `backdrop-filter: blur(12px)` | `--bib-ink-primary` | `fill="currentColor"` → black |

- **Height:** 64px, `position: sticky; top: 0; z-index: var(--bib-z-nav)`
- **Border-bottom (scrolled state):** `1px solid var(--bib-rule-hairline)`
- **Nav labels:** `label/section` style — 14px, `letter-spacing: +0.18em`, `text-transform: uppercase`
- **Active item:** `border-bottom: 1px solid currentColor` on the label — no color swap
- **CTA button:** `brand/ink` fill, white text, sharp corners, `padding: 0.875rem 1.5rem`
- **Logo fix required:** `src/images/LOGO.svg` → replace `fill="white"` with `fill="currentColor"`. Wordmark SVG also needed.

**Flag for client before wireframing:** "Marketing Expertise" and "Expertise" appear as two separate nav items on the current site. Recommend consolidation → 6-item nav. Confirm before building.

---

### Hero — Three Variants

#### Variant A: Full-Bleed Photo Hero (primary, from deck pp. 1, 9, 52)

```
┌──────────────────────────────────────────────────────────────────────────┐
│  [T1 Photography — Bangladesh-scale: Padma Bridge, Dhaka skyline,         │
│   deep navy #051436, long exposures]                                      │
│                                                                           │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  ← mandatory scrim      │
│                                                                           │
│  INTRODUCING OUR COMPANY                         ← label/section, white  │
│                                                                           │
│  Bangladesh's Authorized                         ← display/hero, white,  │
│  Distributor for International                      left-aligned          │
│  Brands.                                                                  │
│                                                                           │
│  ↓                                               ← scroll cue anchor     │
└──────────────────────────────────────────────────────────────────────────┘
```

- **Viewport:** `min-height: 90vh`, `aspect-ratio: 16/9` fallback
- **Image:** `object-fit: cover`, T1 photography register only (see Photography below)
- **Scrim:** mandatory — `linear-gradient(180deg, rgba(0,0,0,0) 0%, rgba(0,0,0,0.55) 100%)` over full image
- **Title position:** absolute, `bottom: 10%`, `left: var(--bib-layout-margin-desktop)`
- **No parallax.** Use slow `scale(1.02 → 1.0)` over the full visible scroll range if depth is desired. No scroll-driven transforms — causes layout shift on mobile Safari.
- **Logo:** white fill, top-left corner of nav (not in hero body)

#### Variant B: Split Hero (from deck p. 2 — Agenda pattern)

50/50 split: T1 photo left | numbered content list right on `--bib-canvas` background. Stacks vertically at mobile.

#### Variant C: Quiet Cream Hero

No photography. Headline centered or left on `--bib-canvas`. Used for secondary pages (Contact, Retail Partners children). Section-label eyebrow above H1.

---

### Stats Band (from deck p. 10)

Sits inside a full-bleed dark photo section. Mandatory scrim behind.

```
┌─────────────────────────────────────────────────────────────────────────┐
│  [T1 photography — wide/aerial, dark]                                    │
│                                                                          │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  ← scrim               │
│                                                                          │
│  [ 25 YRS ]    [ 400+ ]    [ 120+ ]    [ 3 ]                            │
│  of expertise  Employees   Brands      Offices                           │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

- **Stat number:** `stat/number` style — Bold 700, `clamp(56px→80px)`, white, `letter-spacing: −0.01em`
- **Stat label:** 14–16px, Regular 400, white, `letter-spacing: 0`
- **Layout:** 4-column desktop; 2×2 tablet; single-column stacked mobile
- **Content fact unresolved:** Current site states "23 years"; deck states "25 years." Client must confirm before launch.

---

### Section Label (signature recurring pattern)

The deck's most consistent typographic motif — a single letter-spaced caps line, usually top-left of a content section.

```css
.bib-label-section {
  font-family: var(--bib-font-primary);
  font-size: var(--bib-fs-body-sm);    /* 14px */
  font-weight: var(--bib-fw-regular);  /* 400 */
  line-height: var(--bib-lh-snug);     /* 1.3 */
  letter-spacing: var(--bib-tr-label-caps); /* 0.18em */
  text-transform: uppercase;
  color: var(--bib-ink-primary);
}
```

White variant: same properties, `color: var(--bib-white)` — used on dark heroes.

---

### Photo Bento Grid (from deck pp. 13, 14 — Values, Portfolio mosaics)

6 or 7 cells, mixed aspect ratios, all photographic. Each cell = photo + caps label overlay.

```
┌─────────────────┬──────────┬──────────────────┐
│                 │          │                  │
│  [Photo cell]   │ [Photo]  │   [Photo cell]   │
│  LABEL CAPS     │  LABEL   │   LABEL CAPS     │
│  2-col span     │  1-col   │   2-col span     │
├─────────────────┴──────────┼──────────────────┤
│                            │                  │
│   [Photo cell]             │   [Photo cell]   │
│   LABEL CAPS               │   LABEL CAPS     │
│   3-col span               │   2-col span     │
└────────────────────────────┴──────────────────┘
```

- **No icon tiles.** Every cell must be photographic — a single icon swap collapses the register.
- **Label on hover (desktop):** caption always-visible on touch/mobile.
- **Image hover:** `scale(1.03)` at `transition: transform 600ms cubic-bezier(0.22, 0.61, 0.36, 1)` — unhurried.
- **Scrim on each cell:** `linear-gradient(to top, rgba(0,0,0,0.65) 0%, transparent 60%)` behind label text.

---

### Brand-Logo Grid (from deck pp. 15–16)

Holding-company clusters on taupe panel (`--bib-photo-taupe` #58534D).

```
┌──────────────────────────────────────────────────────────────────────────┐
│  [--bib-photo-taupe background]                                          │
│                                                                          │
│  PUIG              COTY              LVMH              INTERPARFUMS      │
│  ┌─────┬─────┐    ┌─────┬─────┐    ┌─────┬─────┐    ┌─────┬─────┐     │
│  │Logo │Logo │    │Logo │Logo │    │Logo │Logo │    │Logo │Logo │     │
│  │     │     │    │     │     │    │     │     │    │     │     │     │
│  └─────┴─────┘    └─────┴─────┘    └─────┴─────┘    └─────┴─────┘     │
└──────────────────────────────────────────────────────────────────────────┘
```

- Logos: monochrome/inverted (white or single-color) — no color logos on taupe
- Holding-company header: `label/section` style in white
- Grid: 4-up desktop / 3-up tablet / 2-up mobile

---

### CTA Button (all variants)

```
[ Primary ]   Background: #000000 / Text: #FFFFFF / Hover: #1A1A1A
[ Outline  ]   Border: 1px #000000 / Text: #000000 / Hover bg: #000000 text: #FFFFFF
[ Ghost    ]   Border: 1px #FFFFFF / Text: #FFFFFF (on dark) / Hover bg: rgba(255,255,255,0.1)
```

- **Border radius:** `0px` — sharp corners, no softening
- **Padding:** `0.875rem 1.5rem`
- **Typography:** Medium 500, `letter-spacing: 0.04em`
- **Touch target:** minimum `44px` height (WCAG 2.5.5)
- **Focus ring:** `box-shadow: 0 0 0 2px var(--bib-canvas), 0 0 0 4px var(--bib-brand-ink)`

---

### Headshot Grid (from deck p. 12 — Team)

4 columns desktop / 2 columns tablet / 2 columns mobile. Square crops on `--bib-panel` (#DADADA) background.

- **Generous whitespace** between card and panel edge
- **Name/role labels:** `heading/h4` style (Medium 500, 18px) for name; `caption` for role title
- **No stylistic effects** — portrait photography should read unaffected, professional

---

### Photo + Caption Row (from deck pp. 22, 30, 40 — Retail evolution)

3-up photo strip with caption below each.

```
┌────────────────┐  ┌────────────────┐  ┌────────────────┐
│                │  │                │  │                │
│  [T3 photo]    │  │  [T3 photo]    │  │  [T3 photo]    │
│                │  │                │  │                │
└────────────────┘  └────────────────┘  └────────────────┘
Caption text here.  Caption text here.  Caption text here.
```

- Caption: `--bib-fs-caption` 12px, `letter-spacing: 0.04em`, `--bib-ink-muted`
- Optional: `border-left: 2px solid var(--bib-ink-muted); padding-left: 12px`

---

### Section Divider (full-bleed dark section)

T1 photography, single caps label. Budget max 2–3 per landing page — over-use fatigues the pattern.

- **Label:** `label/section` style, white, vertically and horizontally centered
- **Min-height:** `50vh`
- **Scrim:** mandatory

---

### Contact Hero (from deck p. 52 — closing)

Full-bleed Padma Bridge photo (T1), logo centered, three office addresses at bottom.

- **Offices:** Bangladesh · Singapore · Dubai
- **Layout:** `display: grid; grid-template-rows: 1fr auto` — addresses pinned to bottom

---

## Photography Tiers

Four distinct registers — treat as a strict editorial framework.

| Tier | Register | Examples in deck | Web usage |
|---|---|---|---|
| **T1 — Bangladesh-scale** | Night landscapes, Padma Bridge, Dhaka skyline, aerial roundabouts; deep navy/midnight `#051436`, long exposures, starfields | pp. 1, 9, 10, 11, 51, 52 | **Signature BIB photography.** Homepage hero, major section openers, section dividers, contact hero. This is the brand DNA. |
| **T2 — Business / People** | Studio portraits on neutral `#DADADA` backgrounds, professional team grid | p. 12 | Leadership, careers, About Us. Keep generous whitespace, neutral panel. |
| **T3 — Retail environment** | Store interiors, mall exteriors, travel retail, fragrance displays | pp. 22, 25, 30, 40, 45, 46 | "How we distribute" content (Retail Partners pages, steps rows). BIB's own retail footprint only — no stock. |
| **T4 — Editorial product/category** | Moody product stills, editorial hand shots, category mosaic grids | pp. 13, 14, 20 | Category explainers on Brands pages. Handle carefully — can slide into Sundora consumer register. |

**Mandatory rules:**
- **No stock photography** without specific scrutiny. The deck reads as specific (real Bangladesh, real stores). Stock kills that register.
- **Always scrim text-over-photo.** Minimum: `linear-gradient` 40% black from text side, or solid 65–85% black panel. Non-negotiable for WCAG compliance.
- **No illustration, no 3D render, no gradient backgrounds outside photography.**
- **No cartoon/icon bento tiles** — every mosaic cell must be photographic.
- **No Sundora consumer photography** (sequin shots, Gen-Z beauty energy) — belongs on Sundora's site, not BIB's.

---

## Motion & Transitions

**Confirmed by client (Q4): scroll-triggered reveals only.** No parallax. No auto-playing carousels.

| Event | Properties | Duration | Easing | CSS var |
|---|---|---|---|---|
| Scroll reveal — text/card enter | `opacity: 0→1` + `translateY(16px→0)` | 400–600ms | `cubic-bezier(0.22, 0.61, 0.36, 1)` | `--bib-motion-duration-default` / `--bib-motion-easing-default` |
| Grid stagger | `staggerChildren: 80ms` | per-element | same | `--bib-motion-stagger` |
| Image hover (bento, card) | `scale(1→1.03)` | 600ms | `cubic-bezier(0.22, 0.61, 0.36, 1)` | `--bib-motion-duration-slow` |
| Nav link hover | `opacity: 1→0.6` | 200ms | `ease` | `--bib-motion-duration-fast` |
| CTA hover | `background: #000→#1A1A1A` | 200ms | `ease` | `--bib-motion-duration-fast` |

**Scroll-reveal specifics:**
- **Trigger:** element 15% past viewport top (not 0% — avoids pop-in on fast scrolls)
- **Stagger cap:** no more than 6 cells per stagger group; beyond 6, all reveal simultaneously
- **Hero depth:** `scale(1.02→1.0)` over full hero scroll range if desired — not `translateY` parallax

**`prefers-reduced-motion: reduce` — required, not optional:**

```css
@media (prefers-reduced-motion: reduce) {
  :root {
    --bib-motion-duration-fast:    0ms;
    --bib-motion-duration-default: 0ms;
    --bib-motion-duration-slow:    0ms;
    --bib-motion-reveal-offset:    0px;
    --bib-motion-stagger:          0ms;
  }
}
```

All `.bib-reveal` elements must appear at full opacity statically when this preference is set. Test on macOS System Settings → Accessibility → Display and iOS.

---

## Scroll-Reveal Implementation

```css
/* Primitive — pair with IntersectionObserver */
.bib-reveal {
  opacity: 0;
  transform: translateY(var(--bib-motion-reveal-offset)); /* 16px */
  transition:
    opacity var(--bib-motion-duration-default) var(--bib-motion-easing-default),
    transform var(--bib-motion-duration-default) var(--bib-motion-easing-default);
}
.bib-reveal.is-visible {
  opacity: 1;
  transform: translateY(0);
}
```

```js
const observer = new IntersectionObserver(
  (entries) => entries.forEach(e => {
    if (e.isIntersecting) { e.target.classList.add('is-visible'); observer.unobserve(e.target); }
  }),
  { threshold: 0.15 }
);
document.querySelectorAll('.bib-reveal').forEach(el => observer.observe(el));
```

For staggered grid cells, apply `transition-delay: calc(var(--bib-motion-stagger) * var(--index))` in CSS, setting `--index` per item inline.

---

## Component File Structure

```
src/
├── components/
│   ├── layout/
│   │   ├── Nav.jsx                 # Transparent/sticky, two fill states, currentColor logo
│   │   ├── Footer.jsx              # Dark bg (#000), 3-col: addresses + nav + legal
│   │   └── ScrollReveal.jsx        # IntersectionObserver wrapper with stagger support
│   ├── home/
│   │   ├── HeroFullBleed.jsx       # Variant A: T1 photo + scrim + display/hero title
│   │   ├── HeroSplit.jsx           # Variant B: 50/50 photo + agenda list
│   │   ├── HeroQuiet.jsx           # Variant C: cream, no photo
│   │   ├── StatsBand.jsx           # 4-stat row on dark photo + scrim
│   │   ├── PhotoBento.jsx          # 6–7 cell mosaic, photographic only
│   │   ├── BrandLogoGrid.jsx       # Holding-company clusters on taupe
│   │   └── SectionDivider.jsx      # Full-bleed dark photo + label (use max 2–3×/page)
│   ├── about/
│   │   ├── HeadshotGrid.jsx        # Team portrait grid on #DADADA panel
│   │   ├── MissionVision.jsx       # Two-column on dark hero
│   │   └── ValuesRow.jsx           # Named values: Diversity, Respect, Authenticity…
│   ├── brands/
│   │   ├── CategoryBento.jsx       # T4 editorial product mosaic
│   │   └── BrandChild.jsx          # Brand-logo grid + editorial copy per category
│   ├── retail/
│   │   └── PhotoCaptionRow.jsx     # 3-up T3 photo strip with captions
│   ├── contact/
│   │   └── ContactHero.jsx         # Full-bleed T1 Padma Bridge, logo centered, 3 offices
│   └── ui/
│       ├── SectionLabel.jsx        # 14px letter-spaced ALL-CAPS label
│       ├── Button.jsx              # Primary / outline / ghost variants
│       ├── Scrim.jsx               # Mandatory text-over-photo overlay
│       ├── HairlineRule.jsx        # 1px #E6E0DC section separator
│       └── FocusRing.jsx           # Brand-consistent focus styles
├── styles/
│   └── tokens.css                  # --bib-* custom properties (source of truth for non-WP)
├── theme.json                      # WordPress 6.6+ block theme token registry
└── pages/ (or app/)
    ├── index.jsx                   # Home
    ├── brands/
    │   ├── index.jsx               # Brands parent
    │   ├── perfume.jsx             # Child: Perfume
    │   ├── skincare-makeup.jsx
    │   ├── toys.jsx
    │   ├── food-beverage.jsx
    │   └── sports.jsx
    ├── retail-partners/
    │   ├── index.jsx               # Retail Partners parent
    │   └── [channel].jsx           # Department Stores / Supermarkets / Hospitality / etc.
    ├── expertise.jsx               # (pending client consolidation of "Expertise" + "Marketing Expertise")
    ├── about.jsx
    └── contact.jsx
```

---

## CSS Custom Properties (from `tokens.css`)

```css
:root {
  /* Color: Neutrals */
  --bib-canvas:        #FAF6F5;
  --bib-panel:         #DADADA;
  --bib-ink-primary:   #2D2B2A;
  --bib-ink-secondary: #413F3E;
  --bib-ink-muted:     #6B6966;
  --bib-rule-hairline: #E6E0DC;
  --bib-white:         #FFFFFF;

  /* Color: Brand */
  --bib-brand-ink:     #000000;
  --bib-brand-ink-90:  #1A1A1A;
  --bib-brand-ink-60:  #666666;

  /* Color: Photo-tier (not UI fills) */
  --bib-photo-midnight:     #051436;
  --bib-photo-sunset-amber: #C97A3A;
  --bib-photo-teal-ocean:   #2E7A94;
  --bib-photo-dusty-rose:   #C99A9C;
  --bib-photo-taupe:        #58534D;

  /* Semantic (inferred — no precedent in deck; starting values only) */
  --bib-semantic-success: #3A7A3A;
  --bib-semantic-warning: #B88128;
  --bib-semantic-error:   #B0352E;
  --bib-semantic-info:    #2D4878;

  /* Typography: Family */
  --bib-font-primary: "Cina GEO", "Helvetica Neue", Arial, sans-serif;
  --bib-font-system:  -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;

  /* Typography: Size */
  --bib-fs-caption:         0.75rem;   /* 12px */
  --bib-fs-body-sm:         0.875rem;  /* 14px */
  --bib-fs-body-md:         1rem;      /* 16px */
  --bib-fs-body-lg:         1.125rem;  /* 18px */
  --bib-fs-h3:              1.5rem;    /* 24px */
  --bib-fs-h2:              2rem;      /* 32px */
  --bib-fs-h1:              2.5rem;    /* 40px */
  --bib-fs-display-section: clamp(2.5rem, 4vw + 1rem, 3.5rem);   /* 40–56px */
  --bib-fs-display-hero:    clamp(3rem, 5vw + 1rem, 5rem);       /* 48–80px */
  --bib-fs-stat-number:     clamp(3.5rem, 5vw + 1rem, 5rem);     /* 56–80px */

  /* Typography: Weight (all 9 Cina GEO weights) */
  --bib-fw-thin:       100;
  --bib-fw-extralight: 200;
  --bib-fw-light:      300;
  --bib-fw-regular:    400;
  --bib-fw-medium:     500;
  --bib-fw-semibold:   600;
  --bib-fw-bold:       700;
  --bib-fw-extrabold:  800;
  --bib-fw-black:      900;

  /* Typography: Line-height */
  --bib-lh-tight:   1;
  --bib-lh-display: 1.05;
  --bib-lh-heading: 1.15;
  --bib-lh-snug:    1.3;
  --bib-lh-body:    1.6;

  /* Typography: Tracking */
  --bib-tr-label-caps: 0.18em;
  --bib-tr-caption:    0.04em;
  --bib-tr-heading:   -0.005em;
  --bib-tr-display:   -0.01em;

  /* Spacing (8pt grid) */
  --bib-sp-4xs: 0.25rem;   /* 4px  */
  --bib-sp-3xs: 0.5rem;    /* 8px  */
  --bib-sp-2xs: 0.75rem;   /* 12px */
  --bib-sp-xs:  1rem;      /* 16px */
  --bib-sp-sm:  1.5rem;    /* 24px */
  --bib-sp-md:  2rem;      /* 32px */
  --bib-sp-lg:  3rem;      /* 48px */
  --bib-sp-xl:  4rem;      /* 64px */
  --bib-sp-2xl: 5rem;      /* 80px */
  --bib-sp-3xl: 6rem;      /* 96px */
  --bib-sp-4xl: 8rem;      /* 128px */

  /* Layout */
  --bib-layout-content-size:     720px;
  --bib-layout-wide-size:        1280px;
  --bib-layout-gutter-desktop:   1.5rem;  /* 24px */
  --bib-layout-gutter-tablet:    1rem;    /* 16px */
  --bib-layout-margin-desktop:   5rem;    /* 80px */
  --bib-layout-margin-tablet:    2rem;    /* 32px */
  --bib-layout-margin-mobile:    1.25rem; /* 20px */

  /* Motion */
  --bib-motion-duration-fast:    200ms;
  --bib-motion-duration-default: 400ms;
  --bib-motion-duration-slow:    600ms;
  --bib-motion-easing-default:   cubic-bezier(0.22, 0.61, 0.36, 1);
  --bib-motion-reveal-offset:    16px;
  --bib-motion-stagger:          80ms;

  /* Scrims (text-over-photo — mandatory) */
  --bib-scrim-full:    linear-gradient(180deg, rgba(0,0,0,0) 0%, rgba(0,0,0,0.55) 100%);
  --bib-scrim-bottom:  linear-gradient(to top, rgba(0,0,0,0.65) 0%, transparent 60%);

  /* Focus ring */
  --bib-shadow-focus-ring: 0 0 0 2px var(--bib-canvas), 0 0 0 4px var(--bib-brand-ink);

  /* Border radii */
  --bib-radius-none: 0;
  --bib-radius-sm:   2px;
  --bib-radius-md:   4px;

  /* Touch target (WCAG 2.5.5) */
  --bib-touch-target-min: 44px;

  /* Z-index scale */
  --bib-z-base:    1;
  --bib-z-nav:     100;
  --bib-z-overlay: 200;
  --bib-z-modal:   300;
  --bib-z-toast:   400;
}
```

---

## WordPress Token Mapping (from `theme.json`)

WordPress generates `--wp--preset--{category}--{slug}` from `theme.json` slugs. The BIB slug convention:

| Brief token | `theme.json` slug | WP CSS var |
|---|---|---|
| `surface/canvas` | `canvas` | `--wp--preset--color--canvas` |
| `ink/primary` | `ink-primary` | `--wp--preset--color--ink-primary` |
| `brand/ink` | `brand-ink` | `--wp--preset--color--brand-ink` |
| `photo/midnight` | `photo-midnight` | `--wp--preset--color--photo-midnight` |
| `display/hero` | `display-hero` | `--wp--preset--font-size--display-hero` |
| `stat/number` | `stat-number` | `--wp--preset--font-size--stat-number` |
| Cina GEO | `cina-geo` | `--wp--preset--font-family--cina-geo` |
| 8pt scale | `4xs`…`4xl` | `--wp--preset--spacing--{slug}` |

**Font file deployment path:** `{theme-root}/assets/fonts/CinaGEO-*.woff2`
Font files from `extract/about-us/font/Cina/` already include `.woff2` and `.woff` for all 9 weights (Thin → Black). Move these into the theme's `assets/fonts/` directory once the commercial webfont license is acquired.

**Motion tokens are not in `theme.json`.** WordPress has no motion primitives. `--bib-motion-*` live in `tokens.css` only and are consumed by custom block JS or a dedicated motion module.

---

## Deck → Web: What Breaks and How to Fix It

| Deck assumption | Why it breaks on web | Fix |
|---|---|---|
| 16:9 canvas, fixed layout | Viewports range 320px–3440px | Restructure each slide into responsive components at 4 breakpoints |
| Sequential reading (presenter in room) | Users scan, skim, enter mid-page | Section anchors, in-page nav on long pages, visible scroll cues |
| Text-over-photo without scrim | Fails WCAG AA at small sizes | Mandatory `--bib-scrim-*` on every photo hero |
| All-caps body chunks | Tanks legibility; breaks screen-reader pronunciation | CSS `text-transform: uppercase` on labels only (short, ≤ 3 words), never body |
| Fine tracking at small sizes | Crushes legibility below 12px | Letter-spacing only at ≥ 14px |
| No interaction states defined | No hover/focus/loading behavior | Specify all 5 states per component in Figma before building |
| Heavy full-page photography | Poor LCP, slow page weight | `next/image` or responsive `<picture>` + AVIF/WebP; hero images ≤ 200KB served; lazy-load below fold |
| Pie/bar charts (pp. 18, 20) | Consumer/decorative register | **Removed entirely** — Q7 confirmed no data-viz on this site |
| Beauty Market divider (p. 17) | Sundora consumer register | **Excluded** — Q6 confirmed |
| Cina GEO needs commercial license | No free substitute | Contact Public Type — commercial webfont license required before launch |

---

## Accessibility Target — WCAG 2.1 AA

- All text-on-photo at **≥ 4.5:1** contrast (scrim is the mechanism)
- Focus rings visible against every background (`--bib-shadow-focus-ring`)
- Touch targets ≥ **44×44px** (`--bib-touch-target-min`)
- `text-transform: uppercase` only on short labels — never applied to body or paragraphs (screen-reader pronunciation)
- `prefers-reduced-motion: reduce` disables all `.bib-reveal` animations
- Heading tags (`<h1>–<h4>`) maintain semantic meaning — caps styling is CSS only
- Run `design:accessibility-review` skill before handoff

---

## Pre-Launch Checklist

**Content — client to confirm:**
- [ ] "23 years" (current site) vs "25 years" (new deck, p. 10) — confirm one source of truth
- [ ] "Marketing Expertise" + "Expertise" — consolidate or keep as two nav items?

**Logo:**
- [ ] `src/images/LOGO.svg` — replace `fill="white"` with `fill="currentColor"`
- [ ] Commission "BestinBrands" wordmark as separate SVG
- [ ] Verify white mark on dark heroes; `currentColor` black on cream nav

**Font:**
- [ ] Acquire Cina GEO commercial webfont license from Public Type (`contact@publictype.us`)
- [ ] Convert/place WOFF2 files at `{theme-root}/assets/fonts/CinaGEO-*.woff2`
- [ ] Verify font loads in WP Editor → Appearance → Editor → Styles → Typography

**WordPress tokens:**
- [ ] `theme.json` validates against `https://schemas.wp.org/trunk/theme.json`
- [ ] Color swatches appear in WP Global Styles color picker
- [ ] Font sizes appear in block toolbar; fluid sizes clamp correctly at <768px and >1440px
- [ ] `--wp--preset--color--canvas` readable from CSS inside block editor iframe
- [ ] Link hover shows `brand-ink-90` (not default WP blue)

**Motion:**
- [ ] `prefers-reduced-motion: reduce` disables reveals — test macOS and iOS
- [ ] Scroll-reveal threshold at 15% (not 0%)
- [ ] No more than 6 stagger cells before snap-to-simultaneous
- [ ] Zero parallax, zero auto-carousels

**Accessibility:**
- [ ] All text-on-photo ≥ 4.5:1 contrast
- [ ] Focus rings visible on all interactive elements, all backgrounds
- [ ] Touch targets ≥ 44×44px
- [ ] Run `design:accessibility-review` skill before handoff

**Performance:**
- [ ] Hero images ≤ 200KB served (AVIF/WebP)
- [ ] Below-fold images lazy-loaded
- [ ] LCP measured on Home, Brands, About at mobile + desktop

**Handoff:**
- [ ] Run `design:design-handoff` skill for developer spec once system is approved
