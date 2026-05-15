# HANDOFF: Beachfront Property Landing Page → roatan-real-estate

This document hands off a static staging landing page for migration into the
production codebase at **`brandhorse/roatan-real-estate`** (the live React app
behind https://roatanrealestate.com).

---

## 1. Goal

Add a new SEO-targeted landing page for **Beachfront Properties** to the live
Roatan Real Estate site. The page will:

- Live at a keyword-aligned path (e.g. `/beachfront-property`)
- Reuse the production site's existing **Navbar** and **Footer** React components
- Match the brand's existing design system, tokens, and responsive behavior
- Be hooked into routing alongside the other top-level pages

This staging build was a visual reference / clickable prototype, not the final
implementation. The next session is the migration into the production repo.

---

## 2. Where the work lives now

| Asset | Location |
|---|---|
| Staging repo (source) | `vinobrandhorse/beachfront-property` |
| Staging URL (live) | https://vinobrandhorse.github.io/beachfront-property/ |
| Production repo (target) | `brandhorse/roatan-real-estate` |
| Production site | https://roatanrealestate.com |
| Original Figma design | `FKl7ML8X0GIn3gexvpSfgd` — node `11743:2024` (desktop), `11762:2100` (mobile) |
| Boss feedback thread | Slack (2 items, both addressed in staging — see §7) |

The staging repo is owned by `vinobrandhorse` (a personal account). The
production repo lives under the `brandhorse` org. Migration moves the page
content into the production repo's app structure (React + Tailwind from what
we observed).

---

## 3. What the page contains (in order, top to bottom)

1. **Navbar** — same as live site (logo · Properties · Agents · Testimonials · Blog · Contact · Sign In)
2. **Hero**
   - Eyebrow: `ROATAN REAL ESTATE GUIDE`
   - H1: `Find Your Perfect Beachfront Property in Roatan`
   - Sub: `Browse by neighborhood or property type — beachfront homes, investment condos, jungle retreats, and more.`
   - Two CTAs: `Explore Roatan Areas` (yellow primary) → anchors to property listings · `Browse Property Types` (alternate) → anchors to types section
   - Background: cropped Roatan coastline photo with deep-blue gradient overlay
3. **Featured Beachfront Properties** (6 cards in a 3-col grid; carousel-friendly on mobile)
   - Each card: photo, "For Sale" badge, price, property type tag, title, short description, beds/baths/sqft, "I'm Interested" CTA
   - Cards link out to the actual live property listings on roatanrealestate.com
   - "View All Beachfront Properties" button (sky blue) at the bottom → `/properties?keyword=beachfront`
4. **Browse by Property Type** (6 cards: Beachfront Homes, Investment Condos, Jungle Retreats, Lots & Land, Luxury Villas, Eco Properties)
   - Each links to `/properties?keyword=<type>`
   - Mobile: horizontal scroll-snap carousel
5. **Why Invest in Roatan** (4 stats)
   - +42% engagement growth (last 6 months)
   - $180K average entry price for condos
   - 12%+ avg. annual rental yield potential
   - 1 hr direct flight from Miami / Houston
6. **CTA banner**: `Ready to Find Your Property in Roatan?` with `Download The Guide` button → `/guide`
7. **Footer** — same as live site (Navigation · Guides & Resources · Legal columns)

---

## 4. Brand tokens to match

These are the values I extracted from the live site's computed styles. They
should already match what's in the production codebase, but listing them here
as a sanity check:

| Token | Value |
|---|---|
| Deep Ocean Blue | `#001f4d` (primary background) |
| Sky Blue | `#4c9feb` (CTAs, stat values) |
| Light Sky Blue | `#92f2ff` (badge backgrounds) |
| Daffodil Yellow | `#f4df1e` (primary CTA fill) |
| Cyan Accent | `#2eb0c7` (eyebrow text, card CTAs) |
| Sign-in dark | `#00224d` |
| Surface | `#f1f5f9` |
| Slate 100 | `rgb(241, 245, 249)` (footer headings) |
| Slate 300 | `rgb(203, 213, 225)` (footer body/links) |
| Slate 400 | `rgb(148, 163, 184)` (copyright) |
| Slate 700 | `rgb(51, 65, 85)` (nav links, footer border) |

**Font**: Montserrat (weights 400, 500, 600, 700) — same as live.

**Breakpoints** (Tailwind defaults — what the live site uses):
- `sm` 640px · `md` 768px · `lg` 1024px · `xl` 1280px

---

## 5. Featured property data (6 cards)

These were scraped from the live `/properties?keyword=beachfront` page. The
migration should ideally **pull these dynamically** from the same MLS feed the
production site uses, rather than hardcoding. If hardcoded for now:

| # | Price | Title | Beds/Baths/SqFt | Image | Detail URL |
|---|---|---|---|---|---|
| 1 | $1,190,000 | 2 Bed 4 Bath Homes in Lawson Rock | 2 / 4 / — | `cdn.photos.sparkplatform.com/rra/20260216032710579611000000-o.jpg` | `/properties/2-br-4.0-ba-homes-in-lawson-rock-26-104-roatan-honduras` |
| 2 | $499,000 | 3 Bed 3 Bath Homes in Sandy Bay (Casa de Pina) | 3 / 3 / — | `cdn.photos.sparkplatform.com/rra/20260217212355719274000000-o.jpg` | `/properties/3-br-3.0-ba-homes-in-seadancer-26-97-roatan-honduras` |
| 3 | $599,000 | 3 Bed 3.5 Bath Homes in Sandy Bay | 3 / 3.5 / — | `cdn.photos.sparkplatform.com/rra/20260224164629116280000000-o.jpg` | `/properties/3-br-3.5-ba-homes-in-sandy-bay-26-74-roatan-honduras` |
| 4 | $1,390,000 | 7 Bed 6 Bath Homes in Sandy Bay | 7 / 6 / — | `cdn.photos.sparkplatform.com/rra/20260207205044569117000000-o.jpg` | `/properties/7-br-6.0-ba-homes-in-sandy-bay-26-69-roatan-honduras` |
| 5 | $1,600,000 | 3 Bed 3.5 Bath Condos in West Bay (Infinity Bay) | 3 / 3.5 / — | `cdn.photos.sparkplatform.com/rra/20260127175429574874000000-o.jpg` | `/properties/3-br-3.5-ba-condos-in-infinity-bay-beach-resort-26-54-roatan-honduras` |
| 6 | $1,995,000 | 9 Bed 9 Bath in Sandy Bay (The Sanctuary) | 9 / 9 / 6,000 | `cdn.photos.sparkplatform.com/rra/20260123211720715178000000-o.jpg` | `/properties/9-br-9.00-ba-residential-in-sandy-bay-26-35-roatan-honduras` |

---

## 6. Asset inventory

All assets live in `/assets/` in the staging repo. Most should already exist
inside the production codebase, but worth checking:

- `assets/logo/logo.png` — dark logo for white navbar (164×64 native)
- `assets/logo/logo-light.png` — light logo for dark footer (400×156 native)
- `assets/hero/hero.png` — Roatan coastline photo, clean (no text baked in)
- `assets/icons/property/{beachfront,investment,jungle,lots,luxury,eco}.svg` — 6 property type icons (yellow on transparent)
- `assets/icons/social/{facebook,instagram,youtube,linkedin}.png` — only used if the production footer keeps social icons (live site currently does NOT have them)

The live site uses Supabase-hosted logos at:
`https://xgohuadqnxtebpsswmah.supabase.co/storage/v1/object/public/media/brand/roatan-logo-{dark,light}.png` — those are 1975×771 / 1501×586 native. Prefer those for retina quality.

---

## 7. Boss feedback (from Slack)

Two asks, both addressed in staging:

1. ✅ **"Please make sure the global headers and footers are being reused — those are components."**
   - In staging this is approximated by extracting to `partials/navbar.html` and `partials/footer.html` with a runtime loader.
   - **In production**: just import the existing `<Navbar />` and `<Footer />` React components. Do NOT recreate them from the staging HTML.
2. ✅ **"The path should align with the targeted keyword — e.g. `/beach-front-property` or whatever we're optimizing for here."**
   - Staging URL slug: `beachfront-property` (one word, matches the live site's `?keyword=beachfront` filter).
   - Production route should be the same: `/beachfront-property`.

Open / nice-to-have:

- ⏳ Property cards data should ideally come from the live MLS query, not be hardcoded.
- ⏳ Confirm Open Graph / Twitter Card meta is set on the new route for clean Slack/iMessage previews. Hero image URL on production CDN.
- ⏳ Sitemap entry for the new route so it's indexable.

---

## 8. Suggested migration steps

In the new cowork session targeting `brandhorse/roatan-real-estate`:

1. **Scaffold a new route/page** for `/beachfront-property` using the repo's existing routing pattern (probably React Router v6 routes, or Next.js `app/` directory — depends on the stack).
2. **Reuse the existing `<Navbar />` and `<Footer />` components** at the top/bottom of the page.
3. **Build sections as components**, ideally reusing primitives that already exist in the codebase (Hero, Card, Stat, CtaBanner). Look in `src/components/` (or equivalent) for existing patterns.
4. **Wire the 6 property cards** to whatever data source the rest of the site uses (Supabase, Spark MLS API, etc.). If the listings page already has a query for `?keyword=beachfront`, reuse it.
5. **Pull copy + assets** from the data tables in §3 and §5 of this doc.
6. **Match responsive breakpoints** to the rest of the site (Tailwind default sm/md/lg/xl).
7. **Add Open Graph meta + canonical link + sitemap entry** for the new route.
8. **Test against the staging visual** (https://vinobrandhorse.github.io/beachfront-property/) for parity, then ship.

---

## 9. Files in this staging repo

```
beachfront-property/
├── index.html              ← page content (sections inlined)
├── styles.css              ← all custom CSS (will not be ported — production uses Tailwind)
├── partials/
│   ├── navbar.html         ← reference structure for global nav (use production <Navbar/> instead)
│   └── footer.html         ← reference structure for global footer (use production <Footer/> instead)
└── assets/
    ├── hero/hero.png
    ├── logo/{logo.png, logo-light.png}
    └── icons/property/* + icons/social/*
```

The HTML structure in `index.html` and the partials is your reference for what
each section should *look like and contain*. The CSS in `styles.css` is NOT
intended to be ported — it was written ad-hoc for the static prototype. The
production migration should use the existing design system / Tailwind utilities.

---

## 10. Reference URLs

- Staging (clickable, current): https://vinobrandhorse.github.io/beachfront-property/
- Production target repo: https://github.com/brandhorse/roatan-real-estate
- Production live site: https://roatanrealestate.com
- Beachfront listings query: https://roatanrealestate.com/properties?keyword=beachfront
- Figma design: https://www.figma.com/design/FKl7ML8X0GIn3gexvpSfgd/Roatan-Real-Estate-Brand-Kit (node `11743:2024`)

---

_End of handoff._
