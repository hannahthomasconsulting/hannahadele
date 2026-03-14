# hannahadele.com Production Site Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Convert the 5 approved `.brainstorm/` HTML mockups into a live production site at `hannahadele.com` with clean URLs, a shared stylesheet, real nav links, committed image assets, and mobile responsiveness.

**Architecture:** Pure HTML5/CSS3 static site on GitHub Pages. Each page lives in its own directory (`work-with-me/index.html`, etc.) so the URL is clean (`/work-with-me/`). One shared stylesheet at `css/shared.css` holds CSS variables, the reset, nav, stats-bar, and footer. All page-specific CSS stays in a `<style>` block within each page file. TikTok embeds remain as async `<blockquote>` + `embed.js`. Only the ~20 images referenced by pages are committed to the repo (source folders total 374 MB; we cherry-pick only what's needed).

**Tech Stack:** HTML5, CSS3 (system font stack, zero dependencies). GitHub Pages + custom domain `hannahadele.com`. Python 3 local preview. `git` for deploys.

---

## File Map

```
hannahadele.com repo root
├── index.html                         ← homepage (from homepage-flow3.html)
├── css/
│   └── shared.css                     ← NEW: CSS vars, reset, nav, stats-bar, footer, mobile
├── work-with-me/
│   └── index.html                     ← from page-work-with-me.html
├── stays/
│   ├── index.html                     ← from page-stays.html
│   └── photos/                        ← NEW: 10 cherry-picked JPEGs
│       └── 9V2A4XXX-VSCO.jpeg (×10)
├── flip-it/
│   └── index.html                     ← from page-flip-it.html
├── shop/
│   └── index.html                     ← from page-shop.html
├── photos/
│   └── hero.jpeg                      ← NEW: one portrait photo for homepage hero
├── dressers/                          ← already exists; stage 9 specific images
│   ├── 1/ (after 2.JPG, after 3.JPG)
│   ├── 3/ (after.PNG, before.PNG)
│   ├── 5/ (after.jpg)
│   ├── 6/ (after 2.JPG)
│   ├── 7/ (after.jpg, after 1.jpg)
│   └── 8/ (after.png)
├── CNAME                              ← already committed
├── docs/
│   └── design-spec.md                 ← already committed
└── .brainstorm/                       ← mockups stay here untouched
    ├── homepage-flow3.html
    ├── page-work-with-me.html
    ├── page-stays.html
    ├── page-flip-it.html
    └── page-shop.html
```

**URL → file mapping:**
| URL | File |
|-----|------|
| `hannahadele.com/` | `index.html` |
| `hannahadele.com/work-with-me/` | `work-with-me/index.html` |
| `hannahadele.com/stays/` | `stays/index.html` |
| `hannahadele.com/flip-it/` | `flip-it/index.html` |
| `hannahadele.com/shop/` | `shop/index.html` |

---

## Global Transformation Rules

Every mockup page needs these same changes applied — internalize these before touching any file:

| Mockup element | Production replacement |
|---|---|
| `<div class="frame-label">...</div>` | Delete entirely |
| `body { padding: 32px 16px 60px; background: #e8e8e8; }` | Delete (body is white, no padding) |
| `.site { border-radius: 20px; box-shadow: ...; }` | Delete (just `overflow: hidden` remains) |
| `<style>` block: nav, stats-bar, footer rules | Delete — handled by `shared.css` |
| `</style></head>` | Replace with `<link rel="stylesheet" href="/css/shared.css">` (root pages) or `<link rel="stylesheet" href="../css/shared.css">` (subdirectory pages) then `<style>` for page-only rules |
| `<span>shop</span>` in nav/footer | `<a href="/shop/">shop</a>` |
| `<a href="page-xxx.html">` in nav | Real production URL |
| Placeholder text at bottom of `<body>` | Delete |
| `<div class="cta-btn">get in touch →</div>` | `<a href="mailto:hannahadeleshome@gmail.com" class="cta-btn">get in touch →</a>` |
| `<title>hannahadeleshome — Full Homepage</title>` | Page-specific title (see each task) |

**Nav HTML template (same on every page — change `class="active"` to the current page):**
```html
<nav class="nav">
  <a href="/" class="logo">hannah adele's home</a>
  <div class="nav-links">
    <a href="/shop/">shop</a>
    <a href="/flip-it/">flip it</a>
    <a href="/stays/">stays</a>
    <a href="/work-with-me/">work with me</a>
    <a href="https://hannahthomasconsulting.com/" target="_blank" class="external">consulting ↗</a>
  </div>
</nav>
```
*(On the homepage, no link gets `class="active"` — the logo IS the home link.)*

**Footer HTML template (same on every page):**
```html
<footer class="footer">
  <a href="/" class="footer-logo">hannah adele's home</a>
  <div class="footer-links">
    <a href="/shop/">shop</a>
    <a href="/flip-it/">flip it</a>
    <a href="/stays/">stays</a>
    <a href="/work-with-me/">work with me</a>
    <a href="https://hannahthomasconsulting.com/" target="_blank" class="external">consulting ↗</a>
  </div>
</footer>
```

---

## Chunk 1: Foundation + Homepage

### Task 1: Start preview server + create shared CSS

**Files:**
- Create: `css/shared.css`

- [ ] **Step 1: Start the preview server**

From the project root directory (`/Users/blakethomas/Desktop/hannah adeles home/`), run this in a dedicated terminal tab and leave it running throughout all tasks:

```bash
python3 -m http.server 7788
```

Verify it works: open `http://localhost:7788/` in a browser. You'll see a directory listing — that's correct at this stage.

- [ ] **Step 2: Create the css directory and shared.css**

```bash
mkdir -p css
```

Create `css/shared.css` with this exact content:

```css
/* ═══════════════════════════════════════════════════════════
   hannahadele.com — Shared Stylesheet
   Referenced by all pages: /css/shared.css
   (subdirectory pages use: ../css/shared.css)
═══════════════════════════════════════════════════════════ */

*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

:root {
  --red:    #FF3A3A;
  --pink:   #FF7EB3;
  --yellow: #F5CB00;
  --blue:   #1557E8;
  --navy:   #0d2461;
  --black:  #1a1a1a;
  --white:  #ffffff;
  --off:    #fafafa;
}

body {
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  color: var(--black);
  background: white;
}

/* ── SITE WRAPPER ── */
.site {
  max-width: 760px;
  margin: 0 auto;
  background: white;
  overflow: hidden;
}

/* ── STICKY NAV ── */
nav.nav {
  background: white;
  padding: 14px 28px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 2px solid #ebebeb;
  position: sticky;
  top: 0;
  z-index: 100;
}
a.logo {
  font-size: 15px;
  font-weight: 900;
  letter-spacing: -0.02em;
  color: var(--black);
  text-decoration: none;
}
.nav-links {
  display: flex;
  gap: 22px;
  font-size: 11px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.09em;
}
.nav-links a {
  color: #666;
  text-decoration: none;
}
.nav-links a:hover { color: var(--black); }
.nav-links a.active { color: var(--black); font-weight: 900; }
.nav-links a.external { color: var(--blue); font-weight: 800; }

/* ── STATS BAR ── */
.stats-bar {
  background: var(--navy);
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}
.stat {
  padding: 20px 16px;
  text-align: center;
  border-right: 1px solid rgba(255,255,255,0.1);
}
.stat:last-child { border-right: none; }
.stat-num {
  font-size: 26px;
  font-weight: 900;
  color: var(--yellow);
  line-height: 1;
  margin-bottom: 4px;
}
.stat-label {
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: rgba(255,255,255,0.5);
  font-weight: 600;
}

/* ── FOOTER ── */
footer.footer {
  background: var(--blue);
  padding: 24px 36px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
a.footer-logo {
  font-size: 14px;
  font-weight: 900;
  color: white;
  letter-spacing: -0.02em;
  text-decoration: none;
}
.footer-links {
  display: flex;
  gap: 20px;
  font-size: 11px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}
.footer-links a {
  color: rgba(255,255,255,0.55);
  text-decoration: none;
}
.footer-links a:hover { color: white; }
.footer-links a.external { color: var(--yellow); font-weight: 800; }

/* ══════════════════════════════════════════
   MOBILE BREAKPOINTS (≤ 600px)
   Applied globally — page-specific mobile
   overrides live in each page's <style> block
══════════════════════════════════════════ */
@media (max-width: 600px) {
  nav.nav { padding: 12px 16px; }
  .nav-links { gap: 12px; font-size: 9px; }
  a.logo { font-size: 13px; }

  .stats-bar { grid-template-columns: repeat(2, 1fr); }
  .stat:nth-child(2) { border-right: none; }
  .stat { padding: 16px 12px; }
  .stat-num { font-size: 20px; }

  footer.footer { flex-direction: column; gap: 16px; text-align: center; }
  .footer-links { flex-wrap: wrap; justify-content: center; gap: 14px; }
}
```

- [ ] **Step 3: Verify file was created**

```bash
wc -l css/shared.css
```
Expected: 130+ lines

- [ ] **Step 4: Commit**

```bash
git add css/shared.css
git commit -m "feat: add shared stylesheet with CSS vars, nav, stats-bar, footer, mobile base"
```

---

### Task 2: Homepage (`index.html`)

**Files:**
- Create: `index.html`
- Create: `photos/hero.jpeg` (one portrait image)

**Source mockup:** `.brainstorm/homepage-flow3.html`

**Homepage-specific changes beyond the Global Rules:**

1. Nav has no `active` link (no homepage link in nav — the logo IS the home link)

2. Hero section — the mockup has `<div class="hero-photo">your<br>photo<br>here</div>` placeholder. Replace with a real `<img>`:
   ```html
   <img src="/photos/hero.jpeg" alt="Hannah Adele Thomas" class="hero-photo">
   ```
   And update the `.hero-photo` CSS to remove the placeholder styles, keep sizing:
   ```css
   .hero-photo {
     width: 140px;
     height: 140px;
     border-radius: 50%;
     border: 4px solid white;
     object-fit: cover;
     flex-shrink: 0;
   }
   ```

3. Hero CTA button — make it a link:
   ```html
   <a href="/work-with-me/" class="hero-cta">work with me →</a>
   ```
   *(The mockup says "see what I've made →" — update the copy to "work with me →" since that's the primary conversion goal)*

4. Bottom CTA button:
   ```html
   <a href="mailto:hannahadeleshome@gmail.com" class="cta-btn">get in touch →</a>
   ```

5. The 3 "work cards" (Brand Partnerships / Hospitality / Brand Storytelling) — wrap each in an anchor:
   ```html
   <a href="/work-with-me/" style="text-decoration:none">
     <div class="work-card" style="border-color:var(--red)">...</div>
   </a>
   ```

6. Add mobile breakpoints to the page-specific `<style>` block:
   ```css
   @media (max-width: 600px) {
     .hero { grid-template-columns: 1fr; padding: 36px 20px 28px; }
     .hero-photo { display: none; }
     .hero-headline { font-size: 38px; }
     .hero-sub { max-width: 100%; }
     .who { grid-template-columns: 1fr; gap: 24px; padding: 36px 20px; }
     .who-headline { font-size: 22px; }
     .pillars { padding: 36px 20px; }
     .pillars-grid { grid-template-columns: repeat(2, 1fr); }
     .proof { padding: 36px 20px; }
     .videos-grid { grid-template-columns: 1fr; }
     .audience { padding: 36px 20px; }
     .audience-grid { grid-template-columns: 1fr; }
     .work { padding: 36px 20px; }
     .work-grid { grid-template-columns: 1fr; }
     .cta-section { padding: 44px 20px; }
     .cta-headline { font-size: 28px; }
   }
   ```

7. `<head>` template:
   ```html
   <meta name="description" content="Nashville-based content creator, furniture flipper & STR host. Former teacher, former $40M tech sales rep. Let's build something people actually watch.">
   <title>Hannah Adele's Home | Nashville Creator & Brand Partner</title>
   <link rel="stylesheet" href="/css/shared.css">
   ```

- [ ] **Step 1: Choose the hero portrait photo**

Open this folder in Finder:
```
/Users/blakethomas/Desktop/hannah adeles home/high quality photos of me in different settings /
```
Browse the portraits. Pick one that:
- Shows Hannah's face clearly
- Works cropped to a circle (centered subject, not too zoomed out)
- Good lighting

Create the photos directory and copy the chosen file:
```bash
mkdir -p photos
# Replace CHOSEN_FILE.jpeg with the actual filename:
cp "/Users/blakethomas/Desktop/hannah adeles home/high quality photos of me in different settings /CHOSEN_FILE.jpeg" photos/hero.jpeg
```

- [ ] **Step 2: Create index.html**

Build `index.html` from `.brainstorm/homepage-flow3.html` applying the Global Rules and homepage-specific changes above.

Structural checklist for the finished file:
- `<head>` has title, description meta, viewport, charset, `<link>` to `/css/shared.css`, `<style>` for page-specific rules only
- No `<div class="frame-label">` anywhere
- `body` has no padding or gray background
- `.site` has no border-radius or box-shadow in the page `<style>`
- `<nav class="nav">` uses real `<a>` tags (not `<span>`) for all internal links
- `<footer class="footer">` uses real `<a>` tags
- Hero has `<img src="/photos/hero.jpeg">` not a placeholder div
- CTA buttons are real `<a>` tags
- No placeholder text at bottom of `<body>`

- [ ] **Step 3: Verify in browser**

Open `http://localhost:7788/` — check:
- No gray outer frame, no rounded card corners
- Hero photo (circle crop) appears in top-right of hero
- "work with me →" button links to `/work-with-me/`
- Each work card is clickable and links to correct inner page
- Nav links all work (click each — shop, flip it, stays, work with me)
- Stats bar shows: 1.4M / 533K / $40M / 523
- Footer links navigate correctly

- [ ] **Step 4: Check mobile (375px)**

In browser DevTools → toggle device toolbar → set to 375px wide. Verify:
- Nav text doesn't overflow or overlap logo
- Hero is single column
- Pillars show 2 columns (not 4)
- Nothing clips horizontally

- [ ] **Step 5: Commit**

```bash
git add index.html photos/hero.jpeg
git commit -m "feat: add production homepage — clean URLs, real nav, portrait photo"
```

---

## Chunk 2: Inner Pages

### Task 3: Work With Me (`work-with-me/index.html`)

**Files:**
- Create: `work-with-me/index.html`

**Source mockup:** `.brainstorm/page-work-with-me.html`

**Key details:**
- `<link rel="stylesheet" href="../css/shared.css">` ← note `../`
- Nav: `<a href="/work-with-me/" class="active">work with me</a>`
- Service 02 CTA: `<a href="/stays/" ...>see the stays portfolio →</a>`
- Service 03 CTA: already links to `https://hannahthomasconsulting.com/` — keep as-is
- Bottom CTA: `<a href="mailto:hannahadeleshome@gmail.com" class="cta-btn">get in touch →</a>`
- No `<img>` tags on this page — only TikTok embeds
- Title: `Hannah Adele's Home | Work With Me`
- Description: `Brand partnerships, hospitality content, and brand storytelling. Former $40M tech sales rep turned creator. Let's make something people actually watch.`

**Mobile CSS (add to page `<style>` block):**
```css
@media (max-width: 600px) {
  .hero { padding: 36px 20px 28px; }
  .hero-headline { font-size: 36px; }
  .service { padding: 36px 20px; }
  .deliverables-grid { grid-template-columns: 1fr; }
  .examples-section { padding: 36px 20px; }
  .tiktok-row { gap: 10px; }
  .tiktok-row .tiktok-embed { min-width: 260px !important; max-width: 260px !important; }
  .ideal-tags { gap: 6px; }
  .cta-section { padding: 44px 20px; }
}
```

- [ ] **Step 1: Create directory and index.html**

```bash
mkdir -p work-with-me
```

Build `work-with-me/index.html` from `.brainstorm/page-work-with-me.html` applying Global Rules and the specifics above.

- [ ] **Step 2: Verify in browser**

Open `http://localhost:7788/work-with-me/` — check:
- Red hero: "Let's make something people actually watch."
- Stat bar: 1.4M / 533K / $40M in software sold / 523 posts
- TikTok horizontal scroll row loads (12 embeds — may take a few seconds for TikTok's embed.js)
- "see the stays portfolio →" button links to `/stays/`
- "visit hannahthomasconsulting.com ↗" opens external site in new tab
- Bottom CTA: `hannahadeleshome@gmail.com` is visible
- Nav "work with me" link appears bolder/active

- [ ] **Step 3: Commit**

```bash
git add work-with-me/index.html
git commit -m "feat: add /work-with-me production page"
```

---

### Task 4: Stays (`stays/index.html` + photos)

**Files:**
- Create: `stays/index.html`
- Create: `stays/photos/` with 10 images

**Source mockup:** `.brainstorm/page-stays.html`

**Images to copy** — all from `stays/professional commercial photos/`:
```
9V2A4748-VSCO.jpeg
9V2A4682-VSCO.jpeg
9V2A4699-VSCO.jpeg
9V2A4739-VSCO.jpeg
9V2A4694-VSCO.jpeg
9V2A4706-VSCO.jpeg
9V2A4684-VSCO.jpeg
9V2A4691-VSCO.jpeg
9V2A4723-VSCO.jpeg
9V2A4731-VSCO.jpeg
```

**Image path change:** In the HTML, replace every instance of:
```
/stays/professional commercial photos/
```
with:
```
/stays/photos/
```

**Key details:**
- `<link rel="stylesheet" href="../css/shared.css">` ← note `../`
- Nav: `<a href="/stays/" class="active">stays</a>`
- "let's work together →" CTA: `<a href="mailto:hannahadeleshome@gmail.com" ...>`
- Title: `Hannah Adele's Home | Stays`
- Description: `Professional hospitality content for STR hosts and hotels. Photo + short-form video. Nashville-based with in-house commercial photography.`

**Mobile CSS:**
```css
@media (max-width: 600px) {
  .hero { padding: 36px 20px 28px; flex-direction: column; }
  .hero-headline { font-size: 36px; }
  .hero-photos { grid-template-columns: 1fr; }
  .hero-photos .hero-photo-main,
  .hero-photos .hero-photo-stack { border-radius: 10px; }
  .gallery-grid { grid-template-columns: repeat(2, 1fr); gap: 8px; }
  .tiktok-row { gap: 10px; }
  .pitch { padding: 36px 20px; }
}
```

- [ ] **Step 1: Copy the 10 photos into stays/photos/**

The folder `stays/photos/` doesn't exist yet — we need to create it and copy (not move) the images. The original `professional commercial photos/` folder stays untouched so the mockup preview still works.

```bash
mkdir -p "stays/photos"

cp "stays/professional commercial photos/9V2A4748-VSCO.jpeg" "stays/photos/"
cp "stays/professional commercial photos/9V2A4682-VSCO.jpeg" "stays/photos/"
cp "stays/professional commercial photos/9V2A4699-VSCO.jpeg" "stays/photos/"
cp "stays/professional commercial photos/9V2A4739-VSCO.jpeg" "stays/photos/"
cp "stays/professional commercial photos/9V2A4694-VSCO.jpeg" "stays/photos/"
cp "stays/professional commercial photos/9V2A4706-VSCO.jpeg" "stays/photos/"
cp "stays/professional commercial photos/9V2A4684-VSCO.jpeg" "stays/photos/"
cp "stays/professional commercial photos/9V2A4691-VSCO.jpeg" "stays/photos/"
cp "stays/professional commercial photos/9V2A4723-VSCO.jpeg" "stays/photos/"
cp "stays/professional commercial photos/9V2A4731-VSCO.jpeg" "stays/photos/"
```

Verify all 10 are there:
```bash
ls stays/photos/ | wc -l
```
Expected: `10`

- [ ] **Step 2: Create stays/index.html**

Build from `.brainstorm/page-stays.html`. The most critical change is all 10 image paths — do a find-and-replace on `/stays/professional commercial photos/` → `/stays/photos/`.

Structural checklist:
- No `frame-label` div
- No gray body background
- `<link>` to `../css/shared.css`
- All 10 image tags reference `/stays/photos/...`
- No broken image tags (verify each filename matches what you copied)
- Nav and footer use real `<a>` tags with production URLs
- "stays" nav link has `class="active"`

- [ ] **Step 3: Verify in browser**

Open `http://localhost:7788/stays/` — check:
- Pink hero: "Content that makes people want to stay."
- All 3 hero photos render (no broken icons)
- Stat bar: 1 property / 2 nights / 30+ photos / 6 videos
- 6 TikTok embeds load in horizontal scroll row
- 6-photo gallery grid renders fully
- "let's work together →" button is a clickable mailto link

- [ ] **Step 4: Commit**

```bash
git add stays/index.html stays/photos/
git commit -m "feat: add /stays production page with 10 cherry-picked photos"
```

---

### Task 5: Flip It (`flip-it/index.html` + dresser images)

**Files:**
- Create: `flip-it/index.html`
- Stage 9 specific dresser images from existing `dressers/` folder

**Source mockup:** `.brainstorm/page-flip-it.html`

**Dresser images to stage** (these files already exist on disk — just need to be `git add`ed):
```
dressers/7/after.jpg
dressers/7/after 1.jpg
dressers/1/after 2.JPG
dressers/1/after 3.JPG
dressers/6/after 2.JPG
dressers/5/after.jpg
dressers/3/after.PNG
dressers/3/before.PNG
dressers/8/after.png
```

**Image path notes:** The mockup already uses absolute paths (`/dressers/7/after.jpg`) — these are correct for production as-is. No path changes needed for dresser images.

**Key details:**
- `<link rel="stylesheet" href="../css/shared.css">` ← note `../`
- Nav: `<a href="/flip-it/" class="active">flip it</a>`
- Commission inquiry CTA: `<a href="mailto:hannahadeleshome@gmail.com" ...>`
- Title: `Hannah Adele's Home | Flip It`
- Description: `Bold painted furniture commissions by Hannah Adele Thomas. Nashville-based. Stripes, plaids, checks. Drop off your piece or I'll source one. Custom quotes available.`

**Mobile CSS:**
```css
@media (max-width: 600px) {
  .hero { padding: 36px 20px 28px; }
  .hero-headline { font-size: 36px; }
  .hero-split { grid-template-columns: 1fr; }
  .hero-split .hero-right { display: none; }
  .tagline-band { padding: 18px 20px; font-size: 15px; }
  .portfolio-grid { padding: 36px 20px; }
  .grid-3 { grid-template-columns: repeat(2, 1fr); gap: 8px; }
  .grid-2 { grid-template-columns: 1fr; gap: 8px; }
  .ba-section { padding: 36px 20px; }
  .ba-grid { grid-template-columns: 1fr; gap: 16px; }
  .how-section { padding: 36px 20px; }
  .how-grid { grid-template-columns: 1fr; gap: 16px; }
  .commission-section { padding: 36px 20px; }
  .commission-grid { grid-template-columns: repeat(2, 1fr); }
  .cta-section { padding: 44px 20px; }
}
```

- [ ] **Step 1: Create directory and index.html**

```bash
mkdir -p flip-it
```

Build `flip-it/index.html` from `.brainstorm/page-flip-it.html` applying Global Rules and specifics above. Image paths stay as `/dressers/...` — do not change them.

- [ ] **Step 2: Stage the 9 dresser images**

```bash
git add "dressers/7/after.jpg"
git add "dressers/7/after 1.jpg"
git add "dressers/1/after 2.JPG"
git add "dressers/1/after 3.JPG"
git add "dressers/6/after 2.JPG"
git add "dressers/5/after.jpg"
git add "dressers/3/after.PNG"
git add "dressers/3/before.PNG"
git add "dressers/8/after.png"
```

Verify they're staged:
```bash
git diff --cached --name-only | grep dressers
```
Expected: 9 files listed

- [ ] **Step 3: Verify in browser**

Open `http://localhost:7788/flip-it/` — check:
- Yellow hero: "Bold furniture. Zero regrets."
- All 3 hero dresser photos display
- Red tagline band renders
- 5-photo portfolio grid shows all images
- Before/After pair shows plain dresser → teal stripes
- No broken image icons anywhere

- [ ] **Step 4: Commit**

```bash
git add flip-it/index.html
git commit -m "feat: add /flip-it production page with dresser portfolio images"
```

---

### Task 6: Shop (`shop/index.html`)

**Files:**
- Create: `shop/index.html`

**Source mockup:** `.brainstorm/page-shop.html`

**Key details:**
- No `<img>` tags — uses emoji icons only
- `<link rel="stylesheet" href="../css/shared.css">` ← note `../`
- Nav: `<a href="/shop/" class="active">shop</a>`
- Amazon link already correct: `https://www.amazon.com/shop/hannahadeleshome`
- Title: `Hannah Adele's Home | Shop`
- Description: `Shop Hannah Adele's favorite things. Amazon storefront with DIY, home decor, kitchen, organization, fashion & outdoors picks. ShopMy coming soon.`

**Mobile CSS:**
```css
@media (max-width: 600px) {
  .hero { padding: 36px 20px 28px; }
  .hero-headline { font-size: 36px; }
  .shop-section { padding: 36px 20px; }
  .cat-grid { grid-template-columns: repeat(2, 1fr); }
  .shopmy-banner { margin: 0 20px 36px; }
}
```

- [ ] **Step 1: Create directory and index.html**

```bash
mkdir -p shop
```

Build `shop/index.html` from `.brainstorm/page-shop.html` applying Global Rules and specifics above.

- [ ] **Step 2: Verify in browser**

Open `http://localhost:7788/shop/` — check:
- Blue hero: "My favorite things."
- Yellow "shop my amazon storefront →" button links to Amazon (opens new tab)
- 6 category cards display in 3-column grid with emoji icons
- ShopMy "coming soon" banner shows with dashed border
- Nav "shop" link is active/bolder

- [ ] **Step 3: Commit**

```bash
git add shop/index.html
git commit -m "feat: add /shop production page"
```

---

## Chunk 3: Final Polish + Deploy

### Task 7: Cross-page link audit

**Files:** Read-only audit of all 5 production HTML files. No new files.

- [ ] **Step 1: Scan for leftover mockup references**

```bash
grep -rn "page-\|\.brainstorm\|homepage-flow3\|page-work-with-me\|page-stays\|page-flip-it\|page-shop" \
  index.html work-with-me/index.html stays/index.html flip-it/index.html shop/index.html
```

Expected output: **nothing** (zero lines). Any output = broken link that needs fixing.

- [ ] **Step 2: Fix any discovered broken links**

If Step 1 found leftover references, update them:

| Old (mockup) | New (production) |
|---|---|
| `page-shop.html` | `/shop/` |
| `page-flip-it.html` | `/flip-it/` |
| `page-stays.html` | `/stays/` |
| `page-work-with-me.html` | `/work-with-me/` |
| `homepage-flow3.html` or `../` for homepage | `/` |

- [ ] **Step 3: Verify active nav state on every page**

Each page should have exactly one nav link with `class="active"`. Check:

```bash
grep -l 'class="active"' index.html work-with-me/index.html stays/index.html flip-it/index.html shop/index.html
```
Expected: all 4 inner pages listed (NOT index.html — homepage has no active nav link)

```bash
grep 'class="active"' work-with-me/index.html stays/index.html flip-it/index.html shop/index.html
```
Expected: exactly one match per file, on the correct link

- [ ] **Step 4: Scan for any remaining placeholder text**

```bash
grep -rn "let me know what to adjust\|Scroll the full page\|your.photo.here\|frame-label\|frame-wrapper" \
  index.html work-with-me/index.html stays/index.html flip-it/index.html shop/index.html
```
Expected: **nothing**

- [ ] **Step 5: Commit any fixes**

```bash
git add index.html work-with-me/index.html stays/index.html flip-it/index.html shop/index.html
git commit -m "fix: resolve all mockup link remnants and nav active states"
```
*(Only run this commit if Step 1-4 found issues. Skip if everything was already clean.)*

---

### Task 8: Push to production + verify live

- [ ] **Step 1: Final pre-push status check**

```bash
git status
git log --oneline -10
```

Expected:
- `git status` → `nothing to commit, working tree clean`
- `git log` → 7–10 commits, each representing a logical step (shared CSS, homepage, 4 inner pages, any fixes)

- [ ] **Step 2: Push to GitHub**

```bash
git push origin main
```

Expected output ends with something like:
```
To git@github.com:hannahthomasconsulting/hannahadele.git
   30b1269..xxxxxxx  main -> main
```

- [ ] **Step 3: Monitor GitHub Pages deployment**

GitHub Pages rebuilds automatically on push. Check build status:
```bash
open "https://github.com/hannahthomasconsulting/hannahadele/actions"
```
Wait for the green checkmark (~30–90 seconds).

- [ ] **Step 4: Verify the live site**

Test all 5 pages on the live domain:

```bash
curl -s -o /dev/null -w "%{http_code}" https://hannahadele.com/
curl -s -o /dev/null -w "%{http_code}" https://hannahadele.com/work-with-me/
curl -s -o /dev/null -w "%{http_code}" https://hannahadele.com/stays/
curl -s -o /dev/null -w "%{http_code}" https://hannahadele.com/flip-it/
curl -s -o /dev/null -w "%{http_code}" https://hannahadele.com/shop/
```

Expected: `200` for each. (If DNS is still propagating, use `hannahthomasconsulting.github.io/hannahadele/` instead.)

Open in a real browser:
- Navigate through all 5 pages
- Check photos load on `/stays/` and `/flip-it/`
- Check TikToks load on `/work-with-me/` and `/stays/`
- Test on mobile (or DevTools 375px)

- [ ] **Step 5: Share the live URL with Hannah 🎉**

```
https://hannahadele.com
```

---

## Appendix: Quick Reference

### Preview server
```bash
# From project root:
python3 -m http.server 7788
# Then open: http://localhost:7788/
```

### Git workflow
```bash
git status                    # always check before committing
git add <specific files>      # never use git add -A (might catch large source folders)
git commit -m "feat: ..."
git push origin main
```

### Image folders (DO NOT git add these entire folders)
- `stays/professional commercial photos/` — ~69 MB, 30+ files. Only 10 are used. ✅ Already handled in Task 4.
- `dressers/` — large video/photo archive. Only 9 specific image files are used. ✅ Handled in Task 5.
- `high quality photos of me in different settings /` — ~148 MB. Only `photos/hero.jpeg` (one copy) is committed. ✅ Handled in Task 2.

### CSS variable values (from mockups — source of truth)
```css
--red:    #FF3A3A
--pink:   #FF7EB3
--yellow: #F5CB00
--blue:   #1557E8
--navy:   #0d2461
--black:  #1a1a1a
--white:  #ffffff
--off:    #fafafa
```
