# SECTIONS — Beachfront Property Landing Page

Detailed section-by-section spec for the staging landing page at
https://vinobrandhorse.github.io/beachfront-property/. Use this when rebuilding
the page inside `brandhorse/roatan-real-estate`.

For overall migration goals, brand tokens, and process see `HANDOFF.md`.

---

## 0. Page-level (head, document chrome)

**`<title>`**: `Roatan Real Estate — Find Your Perfect Beachfront Property`

**`<meta name="description">`**: "Browse beachfront homes, investment condos, jungle retreats, and luxury villas in Roatan, Honduras."

**Favicon / apple-touch-icon**: brand logo PNG.

**Open Graph + Twitter Card**:
- `og:type`: website
- `og:title`: same as `<title>`
- `og:description`: same as `meta description`
- `og:image`: production-hosted hero image (full https URL, 1200×630-ish)
- `og:url`: canonical URL of the new page
- `twitter:card`: `summary_large_image`
- `twitter:title` / `twitter:description` / `twitter:image`: same values

**Font loading**: Google Fonts `Montserrat` weights 400, 500, 600, 700 (and `Inter` 600 for one micro-CTA — see §5).

**Body font default**: Montserrat, 16px / 400 / line-height 24px, color near-black `#020817`, anti-aliased.

---

## 1. Navbar (sticky)

Reuses production `<Navbar />`. Just include the live site's existing component.

If for any reason a fresh build is needed, here's the spec used in staging
(matches the live site 1:1):

**Behavior**: sticky to top, z-index above content. Translucent white background
(`rgba(255,255,255,0.95)`) with subtle backdrop blur. 1px slate-200 bottom
border.

**Outer height**: 81px on all breakpoints.

**Inner container**: max-width 1440px, centered. Horizontal padding scales by
breakpoint: 16px (mobile) → 24px (≥640) → 64px (≥1024).

**Layout**: flex row, `space-between` + `align-center`.

**Left**: logo (dark variant, 82×32px, anchor to `/`).

**Center (≥768px only)**: 5 nav links, gap 28px between them. Each link:
Montserrat 14px / 500 / line-height 20px, color slate-700, transitions to
`#00224d` on hover. Order and URLs:
- Properties → `/properties`
- Agents → `/agents`
- Testimonials → `/testimonials`
- Blog → `/blog`
- Contact → `/contact`

**Right (≥768px only)**: "Sign In" button. Background `#00224d`, white text,
Montserrat 14/500, padding `8px 24px`, border-radius 6px. Anchor to `/login`.

**Right (≤767px only)**: hamburger button. Transparent background, 6px padding,
3-line SVG icon (24×24 viewBox, stroke `#001f4d`), `aria-label="Open menu"`,
`aria-expanded` reflects drawer state. Toggling opens §2.

---

## 2. Mobile menu drawer (only shown ≤767px)

Slide-in from the right. Should reuse whatever drawer pattern the production
site already has — staging spec just for reference:

**Trigger**: hamburger in §1, plus the close button inside the drawer, plus
`Escape` key, plus clicking any link inside.

**Container**: fixed inset, z-index above sticky navbar, white background.
`transform: translateX(100%)` by default; `translateX(0)` when open.
0.25s ease transition. `aria-hidden` flips with state. Body scroll locks when
open.

**Header bar** (81px tall, slate-200 bottom border, 20px horizontal padding):
- Logo (left, 82×32px)
- Close button (right, 22×22 X-icon SVG, `aria-label="Close menu"`)

**Nav list**: same 5 links as desktop nav, stacked vertically with full-width
hit areas. Each: 14px vertical padding, slate-50 hairline divider between items,
font 18px / 500, color deep-ocean-blue (#001f4d), hover sky-blue.

**Sign In button** (bottom of drawer): full width minus 24px margin, 48px tall,
`#00224d` background, white text, 15px / 500, rounded 6px.

---

## 3. Hero (`section.hero`)

Full-bleed dark blue section with photographic background.

**Background**: `#001f4d` base color, overlaid with the Roatan coastline hero
photo (cover-cropped, center-positioned), overlaid again with a left-to-right
gradient: `linear-gradient(90.02deg, rgba(0,31,77,1) 22.65%, rgba(0,52,128,0.5) 71.69%, rgba(0,72,179,0) 99.99%)`. This keeps the left third readable while
revealing the photo on the right.

**Outer padding**: 100px on desktop. Scales down at smaller widths (56px top,
72px bottom, 20px sides on mobile).

**Content column** (left-aligned, 620px wide on desktop, full width on mobile):

1. **Eyebrow text**: "ROATAN REAL ESTATE GUIDE"
   - Montserrat 14 / 400 / line-height 1.5
   - color `#2eb0c7` (cyan accent)
   - letter-spacing 0.7px
   - all-caps

2. **H1**: "Find Your Perfect Beachfront Property in Roatan"
   - Montserrat 60 / 600 / line-height 1 (tight) on desktop
   - 34px / lh 1.1 on mobile
   - color white
   - 18px gap below eyebrow

3. **Sub-paragraph**: "Browse by neighborhood or property type — beachfront homes, investment condos, jungle retreats, and more."
   - Montserrat 18 / 400 / line-height 28px
   - color `#e0ebf5`, opacity 0.85
   - 30px vertical padding (creates breathing room before CTAs)
   - 15px / lh 24 on mobile, no forced line break

4. **CTAs** (flex row, 12px gap, stacked vertically on mobile):
   - **Primary**: "Explore Roatan Areas" with right-arrow SVG.
     - 40px tall, min-width 200px, padding 0 56px, rounded 4px
     - background `#f4df1e` (daffodil yellow), border same color
     - text Montserrat 14 / 400, color `#001f4d`
     - anchors to `#areas` (the properties section)
   - **Alternate**: "Browse Property Types"
     - same dimensions, no icon
     - background `rgba(255,255,255,0.1)`, border `#f4df1e`
     - text 14 / 400, color white
     - anchors to `#types`

**Responsive notes**: at ≤720px the overlay shifts to a top-to-bottom gradient
(`rgba(0,31,77,0.65)` → `rgba(0,31,77,0.85)`) for better mobile contrast, and
CTAs become full-width stacked.

---

## 4. Featured Beachfront Properties (`section#areas`)

Surface-colored section (`#f1f5f9`) containing the 6 hand-picked listings.

**Outer padding**: 112px vertical / 100px horizontal on desktop. Scales down at
smaller widths.

**Section header** (centered):
- H2: "Featured Beachfront / Properties in Roatan" (two lines on desktop, wraps naturally on smaller)
  - Montserrat 36 / 700 / line-height 40px
  - color `#001f4d`
  - capitalize
- Sub: "Direct beach access, premium views, and proven rental upside. / Hand-picked listings from across the island's most desirable shores." (two lines)
  - Montserrat 18 / 400 / line-height 28px
  - color `#64748b` (slate-500)

**Grid**: 3 columns × 2 rows on desktop, 2 columns ≤1100px, 1 column ≤640px.
24px gap.

### Property card (anchor, clickable as a whole)

Each card wraps the whole content in an `<a>` (target=_blank) that points to
the listing's detail page on roatanrealestate.com. White background, 6px
border-radius, soft shadow `0 2px 8px rgba(0,31,77,0.06)`. On hover: lift
`translateY(-4px)`, deepen shadow.

**Image** (top): 240px tall, full width, `background-size: cover`. Status pill
overlays top-left at 16px inset: "For Sale", bg `#001f4d`, white text, 12 / 600,
padding `5px 14px`, pill radius.

**Body** (padding 24px, vertical gap 14px):

- **Header row** (flex space-between):
  - Price (left): Montserrat 24 / 700 / lh 1.2, color `#001f4d`
  - Tag pill (right): "Homes" / "Condos" / "Residential", border slate-300, padding `4px 12px`, font 12 / 600 / color slate-500
- **Title** (h3): Montserrat 18 / 600 / lh 1.4, color `#001f4d`
- **Description**: 14 / 400 / lh 1.55, color slate-500. Truncates naturally.
- **Meta row** (top-divider 1px gray-200, padding-top 16px, gap 18px): three icon-label pairs (beds / baths / sqft). Icon 16×16 SVG with stroke `currentColor` colored sky-blue, label 14 / 500 / slate-500.
- **CTA** (styled as span, not anchor — the whole card is the link): "I'm Interested", background `#f4df1e`, color `#001f4d`, font 14 / 600, full-width inside the body, 12 / 16 padding, rounded 4px. Hover lifts.

**The 6 cards** (data in `HANDOFF.md` §5; image URLs are CDN-hosted on Spark
Platform; detail URLs hit `/properties/<slug>`):

1. $1,190,000 — 2 BR / 4 BA Home — Lawson Rock
2. $499,000 — 3 BR / 3 BA Home (Casa de Pina) — Sandy Bay
3. $599,000 — 3 BR / 3.5 BA Home — Sandy Bay
4. $1,390,000 — 7 BR / 6 BA Home — Sandy Bay
5. $1,600,000 — 3 BR / 3.5 BA Condo (Infinity Bay) — West Bay
6. $1,995,000 — 9 BR / 9 BA / 6,000 sqft (The Sanctuary) — Sandy Bay

**Section CTA below the grid** (centered, 56px margin-top):
"View All Beachfront Properties" with right-arrow SVG.
- 44px tall, padding 0 32px, rounded 4px
- background `#4c9feb` (sky blue), white text, 14 / 500
- border same color, hover darker `#3a8cd6`
- anchors to `/properties?keyword=beachfront`

---

## 5. Browse by Property Type (`section#types`)

White-background section.

**Outer padding**: 100px on desktop, scales down.

**Section header** (centered):
- Eyebrow: "BROWSE BY PROPERTY TYPE", 14 / 400 / cyan→ here color is `#4c9feb` (sky blue), letter-spacing 0.7px, all-caps.
- H2: "What Kind of Property / Are You Looking For?" (two lines).

**Grid**: 6 cards in a 3-col × 2-row grid on desktop (40px gap).

- At ≤1100px, becomes 2 columns.
- At ≤720px, becomes a **horizontal scroll-snap carousel** (one card visible at a time, swipeable, no scrollbar). Cards take `100% - 8px` width each. Padding-bottom 16px to clear the snap area.

### Type card (clickable as a whole)

Anchor to `/properties?keyword=<type>` (opens new tab).

- Background `#001f4d`, 10px left-border `#4c9feb`, padding 40px (28 on mobile).
- min-height 266px on desktop.
- Vertical gap 19px between icon, body, CTA.
- Hover lifts `translateY(-4px)` with shadow.

**Icon** (top): 40×40px SVG, yellow (`#f4df1e`) stroke. 6 distinct icons (one per type) — files in `assets/icons/property/`.

**Body** (gap 7px):
- Title (h3): Montserrat 20 / 600 / lh 1.5, white, capitalize.
- Description: Montserrat 18 / 400 / lh 28px, color `#e0ebf5` at 0.75 opacity.

**CTA**: "Explore →" in Inter 12 / 600, color `#2eb0c7` (cyan). Underline on hover. Bottom of card.

**The 6 types** (title — description — slug):
1. **Beachfront Homes** — "Direct beach access, premium views, high rental upside." → `?keyword=beachfront`
2. **Investment Condos** — "Turnkey rental income, managed properties, proven ROI." → `?keyword=condo`
3. **Jungle Retreats** — "Privacy, nature, unique lifestyle — growing buyer segment." → `?keyword=jungle`
4. **Lots & Land** — "Build your vision from the ground up at entry-level prices." → `?keyword=land`
5. **Luxury Villas** — "World-class finishes, infinity pools, private estates." → `?keyword=luxury`
6. **Eco Properties** — "Sustainable builds, off-grid options, conservation areas." → `?keyword=eco`

---

## 6. Why Invest in Roatan (Investment Stats)

Surface-colored section (`#f1f5f9`).

**Outer padding**: 110px vertical / 100px horizontal on desktop. Fixed 517px
height on desktop (centered vertically). Auto-height on mobile.

**Section header** (centered, 40px gap below):
- Eyebrow: "WHY INVEST IN ROATAN", 14 / 400 / `#2eb0c7`, letter-spacing 0.7px, 400px width on desktop.
- H2: "The Caribbean's Best-Kept / Investment Secret" (two lines), Montserrat 48 / 700 / lh 1.25, capitalize, color `#001f4d`.

**Stats grid**: 4 columns × 1 row on desktop, max-width 1100px, 40px gap.
- At ≤760px: 2 columns × 2 rows (28 / 20 gap).
- At ≤720px (mobile): single column, 28px gap, centered.

### Each stat (centered text)

- **Value**: Montserrat 48 / 700 / lh 1.25, color `#4c9feb` (sky blue).
- **Label**: Montserrat 18 / 400 / lh 28px, color `#020817` at 0.8 opacity.

**The 4 stats** (value / label):
1. **+42%** — "Engagement growth / (last 6 months)"
2. **$180K** — "Average entry price / for condos"
3. **12%+** — "Avg. annual rental / yield potential"
4. **1 hr** — "Direct flight from / Miami / Houston"

---

## 7. CTA Banner

Single-row banner above the footer. Full-width band of sky blue.

**Outer padding**: 48px on desktop. 36px / 20px on mobile.

**Background**: `#4c9feb`.

**Inner container**: max-width 1200px, centered, flex row, 82px gap.
On mobile: stacked column, 24px gap, full-width button.

**Left column** (text):
- H2: "Ready to Find Your Property in Roatan?"
  - Montserrat 32 / 700 / lh 36px, white
  - 26px / lh 1.25 on mobile
- Sub: "Talk to a local expert. No pressure — just the right information for your decision."
  - Montserrat 18 / 400 / lh 28px, color `#e0ebf5`
- Trust row (flex, 8px gap, 4px margin-top):
  - 5 yellow star SVGs (`#f4df1e`), 16×16 each
  - Text "Trusted by 1,200+ buyers" — Montserrat 16 / 400, white

**Right column** (CTA):
- Button: "Download The Guide" with right-arrow SVG.
- 40px tall, min-width 200px, padding 0 56px, rounded 4px.
- Background `#f4df1e`, color `#001f4d`, 14 / 400.
- Anchor to `/guide` (opens new tab).

---

## 8. Footer (sticky to bottom, dark blue)

Reuses production `<Footer />`. Just include the live site's existing component.

If a fresh build is needed, the spec used in staging (mirrors live 1:1):

**Outer**: full-width, background `#001f4d`.

**Inner container**: max-width 1440px, centered. Padding scales:
- mobile (<640): `48px 16px`
- sm (≥640): `64px 24px`
- lg (≥1024): `80px 64px`

**Top section** (`.footer__top`, margin-bottom 48px / lg:80px):
- Layout: column by default, **row at ≥1024px** with 56px gap and `align-start`.
- Two children: brand block + columns block.

### 8a. Brand block

- Layout: flex column, 28px gap.
- max-width 400px **only at ≥1024px** (no constraint below — but content is narrow lines anyway).
- **Logo**: light-variant (`logo-light.png`), exactly `width: 102px; height: 40px; object-fit: contain; object-position: left center`. On mobile, capped at the same 102×40 max.
- **Description**: 3 separate `<p>` tags (NOT one wrapping paragraph) so the layout reads as 3 short lines regardless of viewport. Each `<p>` margin 0.
  - p1: "Your premier real estate partner"
  - p2: "for buying, selling, and renting"
  - p3: "properties in Roatan, Honduras."
  - Each: Montserrat 18 / 400 / lh 28px, color `rgb(203, 213, 225)` (slate-300).

### 8b. Columns block

- Layout: flex column by default → flex row at ≥640px (48px gap) → `justify-end` at ≥1024px (96px gap) → 128px gap at ≥1280px.
- 3 columns, each with `min-width: 160px` (sizes to content, doesn't compress).

Each column (`.footer__col`): flex column, 16px gap between items.

**Column heading** (`<h4>`): Montserrat 20 / 500 / lh 28px, color `rgb(241, 245, 249)` (slate-100).

**Column links** (`<a>`): Montserrat 18 / 400 / lh 28px, color `rgb(203, 213, 225)` (slate-300), hover white.

**The 3 columns + content**:

1. **Navigation**
   - Properties → `/properties`
   - Areas → `/areas`
   - Agents → `/agents`
   - Testimonials → `/testimonials`
   - Contact → `/contact`

2. **Guides & Resources**
   - Property Buying Guide → `/buying-guide`
   - Property Selling Guide → `/selling-guide`
   - Investor Information → `/investor-information`
   - Blog → `/blog`

3. **Legal**
   - Privacy Policy → `/privacy-policy`
   - Terms of Service → `/terms-of-service`
   - Cookies Policy → `/cookies-policy`
   - FAQ → `/faq`

### 8c. Bottom (copyright)

- Border-top: 1px solid `rgb(51, 65, 85)` (slate-700).
- Padding: 56px 0 0 (just top padding, separates from cols).
- Center-aligned text.
- Single `<p>` (Montserrat 16 / 400 / lh 24, color `rgb(148, 163, 184)` slate-400, margin-bottom 24px):
  > © 2026 Roatan Real Estate. All rights reserved. Crafted [@3daywebsite.co](https://3daywebsite.co).
- The `@3daywebsite.co` text is an anchor (color inherits, underlined, opens new tab).

**NO social icons on the live site footer**. Staging doesn't have them either.

---

## 9. Global responsive breakpoints

Match the production site's Tailwind defaults:

| Token | Min width | Common use |
|---|---|---|
| (default) | 0 | base mobile styles |
| `sm` | 640 | tablet portrait |
| `md` | 768 | tablet landscape / small laptop |
| `lg` | 1024 | desktop |
| `xl` | 1280 | large desktop |

**Key transitions in this page**:
- Hide nav links + Sign In, show hamburger: < `md`
- Property type grid → mobile carousel: < `sm` (or 720 in staging, close enough)
- Stats grid: 4-col on desktop → 2-col at < 760 → 1-col on mobile
- Footer top: column → row at `lg`
- Footer cols: column → row at `sm`, then gap scales `sm:48 → lg:96 → xl:128`
- Footer brand max-width 400: only at `lg`
- Section padding (hero, neighborhoods, types, footer): tightens at each breakpoint going down

---

## 10. Accessibility notes

- All interactive cards are real `<a>` tags wrapping the whole region — no JS-only click handlers, no missing focus rings.
- Hamburger button has `aria-label`, `aria-expanded`, `aria-controls`.
- Mobile menu has `aria-hidden` flipping with state. Body scroll lock when open.
- `Escape` closes the mobile menu.
- Decorative SVGs use `aria-hidden="true"`.
- Real images (logo, hero, property photos) have alt text. Pure-decoration imgs (icons) have empty `alt=""`.

---

## 11. What NOT to copy from staging

- `styles.css` — written ad-hoc for the static prototype. The production migration should use Tailwind utilities and the existing design system.
- The runtime `fetch()` partials loader (`<script>` in `index.html`). The whole reason for that pattern was to fake "components" in static HTML — in production, just import the real React components.
- The hardcoded property listings array. Pull from the same data source the listings page uses.

---

_End of section spec._
