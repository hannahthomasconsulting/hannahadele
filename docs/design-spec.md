# hannahadeleshome.com — Design Specification

**Version:** 1.0
**Date:** March 2026
**Status:** Mockups complete → Ready for implementation

---

## 1. Project Overview

**hannahadeleshome.com** is Hannah Adele Thomas's personal brand website. Primary purpose: a pitch tool for brand partnerships and hospitality content deals, with secondary functions as a portfolio and link-in-bio destination.

**Hannah's credentials:**
- TikTok: @hannahadeleshome — 2,656 followers, 533.9K likes, 1.4M top video views
- Based in Nashville, TN
- Former teacher, former $40M tech sales rep
- DIY/home content creator, furniture flipper, STR host

**Site goals (in priority order):**
1. Convert brand managers and hospitality clients into leads
2. Showcase the furniture flip commission service
3. Surface the Amazon storefront (+ future ShopMy)
4. Establish credibility as a serious creator with real-world business chops

---

## 2. Visual Design System

### 2.1 Color Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `--red` | `#e8352a` | Primary accent, hero backgrounds, CTAs |
| `--pink` | `#f564a9` | Hospitality/stays accent |
| `--yellow` | `#f7c948` | Highlight text, badges, key accent |
| `--blue` | `#2563eb` | Navigation active, footers, links |
| `--navy` | `#0d2461` | Stats bars, dark sections |
| `--white` | `#ffffff` | Cards, backgrounds |
| `--off` | `#f8f6f2` | Off-white section backgrounds |
| `--black` | `#111111` | Body text |

### 2.2 Typography

- **Font stack:** `'Helvetica Neue', Helvetica, Arial, sans-serif`
- No custom web fonts — system stack only (fast loading)
- **Weights in use:** 400 (body), 600 (nav/labels), 700 (semibold), 800 (buttons/labels), 900 (headlines)
- **Headline style:** Heavy 900 weight, tight line-height (~1.0–1.1), large sizes (32–56px)
- **Eyebrow labels:** 10px, 700 weight, letter-spacing 0.12–0.18em, uppercase, muted color
- **Em emphasis:** Used for colorful keyword highlights within headlines (yellow or blue)

### 2.3 Spacing System

- **Page max-width:** 760px (centered, `margin: 0 auto`)
- **Section padding:** 44–56px vertical, 36px horizontal
- **Card padding:** 20–28px
- **Nav padding:** 16px vertical, 28px horizontal
- **Border separator:** `2px solid #ebebeb`

### 2.4 Interaction Patterns

- `overflow: hidden` on wrapper prevents horizontal scroll bleed
- Horizontal scroll rows: `display:flex; overflow-x:auto; -webkit-overflow-scrolling:touch`
- Card hover: `background: #eeeae3` (slight darkening on off-white cards)
- Buttons: No border-radius on primary CTAs (sharp corners = bold editorial feel)
- Images: `object-fit: cover` in fixed aspect-ratio containers

---

## 3. Site Architecture

```
/                   → Homepage (hannahadeleshome.com)
/work-with-me       → Brand partnerships + hospitality + consulting pitch page
/stays              → Short-term rental photography portfolio
/flip-it            → Furniture flip commission showcase
/shop               → Amazon storefront + future ShopMy
```

External link: `hannahthomasconsulting.com` (Hannah's B2B consulting site — links out, not a page on this domain)

---

## 4. Page-by-Page Specification

---

### 4.1 Homepage (`/`)

**Visual treatment:** White page with gray outer background
**Hero color:** Red (`--red`)

#### Sections (top to bottom):

1. **Nav** — Logo left, 5 links right (shop, flip it, stays, work with me, consulting ↗)
2. **Hero** — Red bg, large headline with yellow em, sub copy, two CTA buttons ("work with me →", "see my content ↗ → TikTok")
3. **Stats bar** — Navy bg, 4 stats: 1.4M views / 533K likes / $40M software sold / Nashville TN
4. **Featured video row** — "most watched" label, horizontal scroll of 3 embedded TikToks
5. **Three content pillars** — 3-col grid cards: Flip It (yellow), Stays (pink), Shop (blue) — each links to inner page
6. **About strip** — Photo left, bio right ("convincing you that you CAN do it, hard ≠ bad")
7. **Footer** — Blue bg, logo + nav links

---

### 4.2 Work With Me (`/work-with-me`)

**Hero color:** Red (`--red`)
**Purpose:** Primary brand pitch page

#### Sections:

1. **Nav**
2. **Hero** — Red bg, "Let's make something people actually watch." / single "get in touch →" CTA
3. **Stats bar** — Navy: 1.4M views / 533K likes / $40M in software sold / 523 posts
4. **Services intro** — Off-white bg, "Pick your fit. Let's build something."
5. **Service 01 — Brand Partnerships** — White bg, red accent
   - Deliverables grid: Dedicated sponsored video, Integrated product mentions, Instagram Reels + Stories, TikTok + YouTube Shorts, Brand usage rights, Performance recap
   - Ideal for: home, lifestyle, fashion, outdoors, fitness, maker goods, tools, food & beverage, CPG
6. **Brand Content Examples** — White bg, horizontal scroll of 12 embedded TikToks + "see all on TikTok ↗"
   - Video IDs: 7613174632006307103, 7611573582493256974, 7610151017199471886, 7604993759675239694, 7595247402315943181, 7595020853490896142, 7581148692615384334, 7580435043227553079, 7577167559129042189, 7576714406692687159, 7539305446650268942, 7528112821985365303
7. **Service 02 — Hospitality Content** — Off-white bg, pink accent
   - Note: "Professional commercial photography included" (husband is commercial photographer)
   - Deliverables: Professional listing photo gallery, 1–3 short-form highlight videos, Amenity + experience content, Social-ready vertical video, Before & after capability, Full usage rights
   - CTA links to `/stays`
8. **Service 03 — Brand Storytelling** — White bg, blue accent
   - Background: sold $40M in software, now helps tech+lifestyle brands communicate
   - CTA links to `hannahthomasconsulting.com`
9. **CTA section** — Red bg, "Let's make something people actually care about." / email: hannahadeleshome@gmail.com
10. **Footer**

---

### 4.3 Stays (`/stays`)

**Hero color:** Pink (`--pink`)
**Purpose:** Hospitality portfolio — convince STR owners/hotels to book Hannah

#### Sections:

1. **Nav**
2. **Hero** — Pink bg, "Content that makes people want to stay." / 3 hero photos in a grid (living room main, kitchen, outdoor porch)
   - Photos: `9V2A4700.jpeg` (main living), `9V2A4726.jpeg` (kitchen), `9V2A4699-VSCO.jpeg` (outdoor porch)
3. **Stats bar** — Navy: 1 property / 2 nights / 30+ photos / 6 videos
4. **TikTok content row** — "content I made there" label, 6 embedded TikToks (horizontal scroll)
   - Video IDs: 7603965363243601165, 7604225064669596942, 7604323638451490062, 7604881828167634189, 7606002926846299405, 7604993759675239694
5. **Gallery** — 6-photo grid (3+3), living-room focused
   - Photos: 9V2A4706, 9V2A4713, 9V2A4710, 9V2A4684, 9V2A4691, 9V2A4717
6. **Pitch section** — "Your space deserves content that converts." / deliverables list + "let's work together →" CTA
7. **Footer** (blue)

**Image path note:** All images must use absolute paths from server root (`/stays/professional commercial photos/...`) because HTML lives in `.brainstorm/` subdirectory.

---

### 4.4 Flip It (`/flip-it`)

**Hero color:** Yellow (`--yellow`)
**Purpose:** Showcase furniture flip portfolio + drive commission inquiries

#### Concept:
Hannah rescues old/discarded furniture (dressers, nightstands, cabinets) and transforms them with bold, vibrant painted patterns — stripes, plaids, checks. She takes commissions: client can drop a piece off or Hannah sources it; client can pick design or leave it to Hannah. Price range $300–600 but NOT advertised on site.

#### Sections:

1. **Nav**
2. **Hero** — Yellow bg, "Bold furniture. Zero regrets." / 3 real dresser photos in split layout
   - Tall slot: `dressers/7/after.jpg` (matched blue/white stripe set)
   - Top right: `dressers/1/after 3.JPG` (hot pink plaid)
   - Bottom right: `dressers/6/after 2.JPG` (teal mint stripes)
3. **Red tagline band** — "i take old furniture and make it something you'd actually brag about."
4. **Portfolio grid** — 5 dresser photos
   - 3-col row: `dressers/1/after 2.JPG`, `dressers/5/after.jpg`, `dressers/7/after 1.jpg`
   - 2-col row: `dressers/3/after.PNG`, `dressers/8/after.png`
5. **Before/After section** — Dresser 3 pair
   - Before: `dressers/3/before.PNG` (plain brown dresser)
   - After: `dressers/3/after.PNG` (teal vertical stripes)
6. **How It Works** — Navy bg, 3 steps: Pick Your Piece → Pick Your Vibe → I Make It Happen
7. **Commission Options** — 4-card grid: Drop It Off / I'll Source It / You Choose the Design / Trust My Eye
8. **Pricing note** — Yellow bg, "pricing varies by piece — reach out for a custom quote"
9. **CTA section** — Red bg, "Ready to commission your piece?"
10. **Footer** (blue)

---

### 4.5 Shop (`/shop`)

**Hero color:** Blue (`--blue`)
**Purpose:** Link to Amazon storefront; ShopMy coming soon

#### Sections:

1. **Nav**
2. **Hero** — Blue bg, "My favorite things." / "shop my amazon storefront →" yellow CTA button / affiliate disclosure note
3. **Categories** — 6-card grid linking to Amazon storefront
   - DIY + Craft 🎨, Home Decor 🏠, Kitchen 🍳, Organization 📦, Fashion + Style 👗, Outdoors + Garden 🌿
4. **ShopMy coming soon** — Dashed border banner, "coming soon" badge, "ShopMy storefront — launching soon"
5. **Footer** (blue)

---

## 5. Component Inventory

| Component | Used On | Notes |
|-----------|---------|-------|
| `.nav` | All pages | Sticky, white, 2px border-bottom |
| `.hero` | All pages | Different color per page |
| `.stats-bar` | Homepage, Work With Me | Navy bg, 4-col grid |
| `.tiktok-row` | Stays, Work With Me | Horizontal scroll, `overflow-x:auto` |
| `.service` | Work With Me | Alternating white/off-white bg |
| `.deliverables` / `.deliverables-grid` | Work With Me | 2-col checklist |
| `.cat-card` | Shop | 3-col grid, off-white bg |
| `.portfolio-grid` | Flip It | 3-col then 2-col |
| `.ba-cell` / before-after | Flip It | Side-by-side with overlay tags |
| `.footer` | All pages | Blue bg |

---

## 6. Content & Copy Reference

### Voice/Tone:
- Casual, direct, confident — not corporate
- Self-aware and funny (see: "I watched myself put on mod podge with my bare hands")
- Bold claims backed by real receipts ($40M in software sold)
- "Hard ≠ bad" — core brand philosophy

### Key Brand Lines:
- "convincing you that you CAN do it, hard ≠ bad" (bio)
- "Let's make something people actually watch." (Work With Me hero)
- "Bold furniture. Zero regrets." (Flip It hero)
- "Content that makes people want to stay." (Stays hero)
- "My favorite things." (Shop hero)

### Contact:
- Email: `hannahadeleshome@gmail.com`
- TikTok: `@hannahadeleshome`
- Amazon: `amazon.com/shop/hannahadeleshome`
- Consulting: `hannahthomasconsulting.com`

---

## 7. Implementation Notes

### Tech Stack (to be determined):
- Static site or lightweight CMS (Webflow, Framer, or custom HTML/CSS)
- No JavaScript framework required — mostly static content
- TikTok embed script: `https://www.tiktok.com/embed.js`

### Image Assets:
- **Stays photos:** `/stays/professional commercial photos/` — 30+ professional shots by Blake Thomas (commercial photographer / Hannah's husband)
- **Dresser photos:** `/dressers/1–8/` — 8 piece folders, each with before/after JPG/PNG
- **Portrait photos:** `/high quality photos of me in different settings/` — lifestyle shots for about sections and hero crops

### Responsive:
- Mockups built at 760px max-width
- Mobile breakpoints needed: nav collapses, grid cols reduce, font sizes scale down
- Horizontal scroll rows already mobile-ready (touch scroll)

### Performance:
- TikTok embeds load async — won't block render
- Images should be optimized/WebP for production
- No Google Fonts (system stack = fast)

### SEO:
- Title tags per page: `hannahadeleshome — [Page Name]`
- Meta descriptions needed for each page
- `hannahadeleshome.com` is the target domain

---

## 8. Files Reference

All mockup files live in `.brainstorm/`:

| File | Page | Status |
|------|------|--------|
| `homepage-flow3.html` | `/` | ✅ Complete |
| `page-work-with-me.html` | `/work-with-me` | ✅ Complete |
| `page-stays.html` | `/stays` | ✅ Complete |
| `page-flip-it.html` | `/flip-it` | ✅ Complete |
| `page-shop.html` | `/shop` | ✅ Complete |

Preview server: `python3 -m http.server 7788` from project root
Preview URL: `http://localhost:7788/.brainstorm/[filename].html`
