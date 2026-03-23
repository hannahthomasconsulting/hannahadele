# Stays Page Redesign Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild `stays/index.html` around a full-width video hero and three distinct deliverable sections (marketing video, professional photography, short-form social content).

**Architecture:** Single-file HTML edit — all changes are contained in `stays/index.html`. The `<style>` block is rebuilt in place: old CSS removed, new classes added. The `<body>` sections are replaced one by one. No shared CSS or other pages are touched.

**Tech Stack:** Static HTML + CSS. No build step, no framework. Browser verification via `open stays/index.html`.

---

## Chunk 1: CSS — Remove old, add new

### Task 1: Strip removed CSS classes from `<style>` block

**Files:**
- Modify: `stays/index.html` — `<style>` block only

- [ ] **Step 1: Remove all CSS rules for sections being deleted**

In `stays/index.html`, delete the following CSS rule blocks from the `<style>` tag. Each block is labelled with a comment in the existing file:

- `/* HERO */` block — all rules: `.hero`, `.hero-eyebrow`, `.hero-headline`, `.hero-headline em`, `.hero-sub`, `.hero-cta`, `.hero-photo-stack`, `.hero-img`, `.hero-img img`, `.hero-img.tall`
- `/* BEFORE/AFTER BANNER */` block — all rules: `.before-after`, `.ba-side`, `.ba-before`, `.ba-after`, `.ba-label`, `.ba-text`, `.ba-arrow`
- `/* PHOTO GRID */` block — all rules: `.photo-grid-3`, `.photo-grid-4`, `.photo-cell`, `.photo-cell.tall`, `.photo-cell img`, `.photo-caption`
- `/* VIDEO SECTION */` block — all rules: `.video-section`, `.tiktok-row`, `.tiktok-row blockquote.tiktok-embed`
- `/* DELIVERABLES */` block — all rules: `.delivers`, `.delivers-grid`, `.deliver-card`, `.deliver-icon`, `.deliver-title`, `.deliver-desc`
- `/* PHOTO NOTE */` block — all rules: `.photo-note`, `.photo-note strong`

Keep untouched: `/* SECTION LABELS */`, `/* CTA */`, `/* MOBILE */` (mobile will be rewritten in Task 2).

- [ ] **Step 2: Open file in browser and verify no crash**

```bash
open "/Users/blakethomas/Desktop/hannah adeles home/stays/index.html"
```

Expected: page loads without JS errors. Most sections will be missing or unstyled — that's fine at this stage.

- [ ] **Step 3: Commit**

```bash
cd "/Users/blakethomas/Desktop/hannah adeles home"
git add stays/index.html
git commit -m "refactor: remove old CSS blocks from stays page"
```

---

### Task 2: Add new CSS classes to `<style>` block

**Files:**
- Modify: `stays/index.html` — `<style>` block only

- [ ] **Step 1: Add hero video CSS**

Insert after the existing `/* SECTION LABELS */` comment block (before `/* CTA */`):

```css
/* HERO VIDEO */
.hero-video {
  position: relative;
  background: #0d0d1a;
  height: 55vh;
  min-height: 320px;
  overflow: hidden;
}
.hero-video-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to top, rgba(0,0,0,0.72) 0%, rgba(0,0,0,0.15) 60%, transparent 100%);
  pointer-events: none;
}
.hero-video-content {
  position: absolute;
  bottom: 0; left: 0; right: 0;
  padding: 0 36px 28px;
}
.hero-video-eyebrow {
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  color: rgba(255,255,255,0.6);
  font-weight: 700;
  margin-bottom: 14px;
}
.hero-video-headline {
  font-size: 44px;
  font-weight: 900;
  color: white;
  line-height: 0.97;
  margin-bottom: 14px;
}
.hero-video-headline em { color: var(--yellow); font-style: normal; }
.hero-video-sub {
  font-size: 13px;
  color: rgba(255,255,255,0.78);
  line-height: 1.6;
  margin-bottom: 22px;
}
.hero-video-cta {
  display: inline-block;
  text-decoration: none;
  background: white;
  color: var(--navy);
  font-size: 12px;
  font-weight: 800;
  padding: 12px 24px;
  border-radius: 4px;
  text-transform: uppercase;
  letter-spacing: 0.07em;
}

/* INTRO STRIP */
.intro-strip {
  background: white;
  padding: 44px 36px;
  text-align: center;
}

/* DELIVERABLE SECTIONS */
.deliver-video {
  background: var(--navy);
  padding: 44px 36px;
}
.deliver-video .section-label { color: rgba(255,255,255,0.4); }
.deliver-video .section-headline { color: white; }
.deliver-video .section-sub { color: rgba(255,255,255,0.65); margin-bottom: 20px; }

.deliver-video-player {
  border-radius: 10px;
  overflow: hidden;
  border: 2px solid rgba(255,255,255,0.12);
  background: #000;
  aspect-ratio: 16/9;
}
.deliver-video-note {
  font-size: 11px;
  color: rgba(255,255,255,0.35);
  text-align: center;
  margin-top: 8px;
}

.deliver-photos {
  background: white;
  padding: 44px 36px;
}
.deliver-photos-row1 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 8px;
  margin-bottom: 8px;
}
.deliver-photos-row1 .photo-cell {
  aspect-ratio: 4/3;
  border-radius: 8px;
  overflow: hidden;
  background: #eee;
}
.deliver-photos-row2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 8px;
}
.deliver-photos-row2 .photo-cell {
  aspect-ratio: 16/9;
  border-radius: 8px;
  overflow: hidden;
  background: #eee;
}
.deliver-photos-row1 .photo-cell img,
.deliver-photos-row2 .photo-cell img {
  width: 100%; height: 100%; object-fit: cover; display: block;
}
.photo-callout {
  background: #fff0f6;
  border-left: 4px solid var(--pink);
  border-radius: 0 8px 8px 0;
  padding: 12px 16px;
  font-size: 12px;
  color: #444;
  line-height: 1.5;
  margin-top: 20px;
}
.photo-callout strong { color: var(--black); }

.deliver-social {
  background: var(--off);
  padding: 44px 36px;
  border-top: 2px solid #f0f0f0;
}
.tiktok-row {
  display: flex;
  gap: 16px;
  margin-top: 28px;
  overflow-x: auto;
  padding-bottom: 8px;
  -webkit-overflow-scrolling: touch;
}
.tiktok-row blockquote.tiktok-embed {
  flex: 0 0 auto;
  max-width: 300px !important;
  min-width: 300px !important;
  margin: 0 !important;
}
```

- [ ] **Step 2: Replace the mobile block entirely**

Find the existing `@media (max-width: 600px)` block and replace it with:

```css
@media (max-width: 600px) {
  .hero-video { height: auto; min-height: 260px; }
  .hero-video-content { padding: 0 20px 20px; }
  .hero-video-headline { font-size: 36px; }
  .intro-strip { padding: 36px 20px; }
  .deliver-video,
  .deliver-photos,
  .deliver-social { padding: 36px 20px; }
  .deliver-photos-row1,
  .deliver-photos-row2 { grid-template-columns: 1fr; }
  .tiktok-row { gap: 10px; }
}
```

- [ ] **Step 3: Open file in browser — no crash expected**

```bash
open "/Users/blakethomas/Desktop/hannah adeles home/stays/index.html"
```

Expected: page loads. CSS classes now exist but aren't used yet in markup.

- [ ] **Step 4: Commit**

```bash
cd "/Users/blakethomas/Desktop/hannah adeles home"
git add stays/index.html
git commit -m "feat: add new CSS classes for stays page redesign"
```

---

## Chunk 2: Markup — Replace sections

### Task 3: Replace hero section

**Files:**
- Modify: `stays/index.html` — hero markup only

- [ ] **Step 1: Remove old hero markup**

Find and delete the entire `<!-- HERO -->` block:

```html
<!-- HERO -->
<div class="hero">
  ...all content...
</div>
```

- [ ] **Step 2: Insert new hero-video markup in its place**

```html
<!-- HERO VIDEO -->
<div class="hero-video">
  <video autoplay muted loop playsinline
    style="position:absolute;inset:0;width:100%;height:100%;object-fit:cover;object-position:center;display:block">
    <source src="/stays/stay%20promo%20video.mov">
  </video>
  <div class="hero-video-overlay"></div>
  <div class="hero-video-content">
    <div class="hero-video-eyebrow">hospitality content · on-location</div>
    <div class="hero-video-headline">I'll make people want to <em>stay</em> there.</div>
    <div class="hero-video-sub">Hotels, Airbnbs, rentals &amp; resorts — I come to you, tell the story, and hand you a full content package.</div>
    <a href="mailto:hannahadeleshome@gmail.com" class="hero-video-cta">let's connect →</a>
  </div>
</div>
```

- [ ] **Step 3: Remove the before/after banner**

Find and delete the entire `<!-- BEFORE/AFTER BANNER -->` block:

```html
<!-- BEFORE/AFTER BANNER -->
<div class="before-after">
  ...all content...
</div>
```

- [ ] **Step 4: Open in browser and verify hero**

```bash
open "/Users/blakethomas/Desktop/hannah adeles home/stays/index.html"
```

Expected:
- Full-width dark area at top where video would play (video may not autoplay from `file://` — that's OK, dark fallback background should show)
- White text headline visible at bottom of the dark area: "I'll make people want to stay there."
- "let's connect →" white button visible
- Before/after banner gone

- [ ] **Step 5: Commit**

```bash
cd "/Users/blakethomas/Desktop/hannah adeles home"
git add stays/index.html
git commit -m "feat: replace hero with full-width video on stays page"
```

---

### Task 4: Add intro strip

**Files:**
- Modify: `stays/index.html` — after hero, before existing photo gallery section

- [ ] **Step 1: Insert intro strip after the hero-video block**

Add immediately after the closing `</div>` of `.hero-video`:

```html
<!-- INTRO STRIP -->
<div class="intro-strip">
  <div class="section-label">what you walk away with</div>
  <div class="section-headline">Three ways to make your property <em>unforgettable.</em></div>
  <p class="section-sub" style="max-width:460px;margin:0 auto">Pick one or bundle them all — marketing video, professional photography, and short-form social content.</p>
</div>
```

- [ ] **Step 2: Open in browser and verify**

```bash
open "/Users/blakethomas/Desktop/hannah adeles home/stays/index.html"
```

Expected: Centered white section below hero with the label, headline (pink "unforgettable."), and sub copy.

- [ ] **Step 3: Commit**

```bash
cd "/Users/blakethomas/Desktop/hannah adeles home"
git add stays/index.html
git commit -m "feat: add intro strip to stays page"
```

---

### Task 5: Replace photo gallery with Section 01 + Section 02

**Files:**
- Modify: `stays/index.html` — replace existing photo gallery and deliverables sections

- [ ] **Step 1: Remove the old photo gallery section**

Find and delete the entire `<!-- PHOTO GALLERY -->` block:

```html
<!-- PHOTO GALLERY -->
<div class="section-pad">
  ...all content including the three photo grids...
</div>
```

- [ ] **Step 2: Remove the old deliverables section**

Find and delete the entire `<!-- DELIVERABLES -->` block:

```html
<!-- DELIVERABLES -->
<div class="delivers">
  ...all content...
</div>
```

- [ ] **Step 3: Insert Section 01 (Marketing Video) in place of the removed blocks**

```html
<!-- SECTION 01: MARKETING VIDEO -->
<div class="deliver-video">
  <div class="section-label">01 · Marketing Video</div>
  <div class="section-headline">A cinematic promo, ready to post.</div>
  <p class="section-sub">Professional full-length property video — edited, color-graded, and ready for your listing page, website, or social ads. This is what sets a property apart.</p>
  <div class="deliver-video-player">
    <video controls style="width:100%;height:100%;display:block">
      <source src="/stays/stay%20promo%20video.mov">
    </video>
  </div>
  <p class="deliver-video-note">Commercial quality · Edited &amp; color-graded · Delivered as .mp4</p>
</div>
```

- [ ] **Step 4: Insert Section 02 (Professional Photography) immediately after Section 01**

```html
<!-- SECTION 02: PROFESSIONAL PHOTOGRAPHY -->
<div class="deliver-photos">
  <div class="section-label">02 · Professional Photography</div>
  <div class="section-headline">Gallery-quality. Every room. Every amenity.</div>
  <p class="section-sub">Shot by a commercial photographer — not iPhone shots. With or without lifestyle/UGC styling depending on the vibe you want.</p>
  <div class="deliver-photos-row1">
    <div class="photo-cell">
      <img src="/stays/professional space photos/9V2A4752-VSCO.jpeg" alt="Coastal Airbnb living space">
    </div>
    <div class="photo-cell">
      <img src="/stays/professional space photos/9V2A4735-VSCO.jpeg" alt="Coastal Airbnb bedroom">
    </div>
  </div>
  <div class="deliver-photos-row2">
    <div class="photo-cell">
      <img src="/stays/professional space photos/9V2A4695-VSCO.jpeg" alt="Coastal Airbnb amenities">
    </div>
    <div class="photo-cell">
      <img src="/stays/professional space photos/9V2A4699-VSCO.jpeg" alt="Coastal Airbnb exterior">
    </div>
  </div>
  <div class="photo-callout">
    <strong>📷 Commercial photography is included in every package.</strong> My husband is a professional commercial photographer — he's on every job. You don't hire us separately.
  </div>
</div>
```

- [ ] **Step 5: Open in browser and verify**

```bash
open "/Users/blakethomas/Desktop/hannah adeles home/stays/index.html"
```

Expected:
- Old photo grid and deliverables cards gone
- Dark navy Section 01 block with white headline and a video player (controls visible)
- White Section 02 block below it with 4 photos in two rows (4/3 ratio on top, 16/9 on bottom)
- Pink callout box at bottom of Section 02
- All 4 photos load correctly (not broken img icons)

- [ ] **Step 6: Commit**

```bash
cd "/Users/blakethomas/Desktop/hannah adeles home"
git add stays/index.html
git commit -m "feat: add marketing video and photography sections to stays page"
```

---

### Task 6: Replace video section with Section 03

**Files:**
- Modify: `stays/index.html` — replace `.video-section` with `.deliver-social`

- [ ] **Step 1: Remove the old video section markup**

Find and delete the entire `<!-- VIDEO SECTION -->` block including its `<script>` tag:

```html
<!-- VIDEO SECTION -->
<div class="video-section">
  ...all content including tiktok-row and the script tag...
</div>
<script async src="https://www.tiktok.com/embed.js"></script>
```

- [ ] **Step 2: Insert Section 03 in its place**

```html
<!-- SECTION 03: SHORT-FORM SOCIAL CONTENT -->
<div class="deliver-social">
  <div class="section-label">03 · Short-Form Social Content</div>
  <div class="section-headline">Share it on your feed — or I'll promote on mine.</div>
  <p class="section-sub" style="margin-bottom:0">Vertical UGC-style videos of the space, amenities, and experience. Social-ready for TikTok, Reels &amp; Shorts. Use them yourself, or let me post them to my audience.</p>
  <div class="tiktok-row">
    <blockquote class="tiktok-embed" cite="https://www.tiktok.com/@hannahadeleshome/video/7603965363243601165" data-video-id="7603965363243601165" style="max-width:300px;min-width:300px;"><section></section></blockquote>
    <blockquote class="tiktok-embed" cite="https://www.tiktok.com/@hannahadeleshome/video/7604225064669596942" data-video-id="7604225064669596942" style="max-width:300px;min-width:300px;"><section></section></blockquote>
    <blockquote class="tiktok-embed" cite="https://www.tiktok.com/@hannahadeleshome/video/7604323638451490062" data-video-id="7604323638451490062" style="max-width:300px;min-width:300px;"><section></section></blockquote>
    <blockquote class="tiktok-embed" cite="https://www.tiktok.com/@hannahadeleshome/video/7604881828167634189" data-video-id="7604881828167634189" style="max-width:300px;min-width:300px;"><section></section></blockquote>
    <blockquote class="tiktok-embed" cite="https://www.tiktok.com/@hannahadeleshome/video/7606002926846299405" data-video-id="7606002926846299405" style="max-width:300px;min-width:300px;"><section></section></blockquote>
    <blockquote class="tiktok-embed" cite="https://www.tiktok.com/@hannahadeleshome/video/7604993759675239694" data-video-id="7604993759675239694" style="max-width:300px;min-width:300px;"><section></section></blockquote>
  </div>
  <script async src="https://www.tiktok.com/embed.js"></script>
</div>
```

- [ ] **Step 3: Open in browser and verify**

```bash
open "/Users/blakethomas/Desktop/hannah adeles home/stays/index.html"
```

Expected:
- Off-white section below the photography section
- Headline: "Share it on your feed — or I'll promote on mine."
- TikTok embeds row visible and horizontally scrollable (embeds may need a moment to load)
- Old `.video-section` dark background and old headline gone

- [ ] **Step 4: Commit**

```bash
cd "/Users/blakethomas/Desktop/hannah adeles home"
git add stays/index.html
git commit -m "feat: add short-form social section to stays page"
```

---

### Task 7: Update CTA copy

**Files:**
- Modify: `stays/index.html` — CTA section copy only, no style changes

- [ ] **Step 1: Update CTA text**

Find the `<!-- CTA -->` block and update the following text nodes only (do not change any classes or structure):

| Element | Find | Replace with |
|---|---|---|
| `.cta-label` | `book a shoot` | `work together` |
| `.cta-headline` | `Ready to make your<br>property <em>irresistible?</em>` | `Have a property that<br>deserves to be <em>seen?</em>` |
| `.cta-sub` | `Tell me about your property. I'll tell you what we can do with it.` | `Whether you want to hire us for a full content shoot or explore a collab — I'm open to both. Let's talk.` |
| `.cta-btn` | `let's work together →` | `reach out →` |

The `.cta-email` line (`hannahadeleshome@gmail.com`) and all `href` attributes remain unchanged.

- [ ] **Step 2: Open in browser and verify**

```bash
open "/Users/blakethomas/Desktop/hannah adeles home/stays/index.html"
```

Expected: CTA section at bottom reads "Have a property that deserves to be seen?" with yellow "seen?", sub copy mentions collab, button says "reach out →".

- [ ] **Step 3: Commit**

```bash
cd "/Users/blakethomas/Desktop/hannah adeles home"
git add stays/index.html
git commit -m "feat: update CTA copy on stays page to welcome collabs"
```

---

## Chunk 3: Final verification

### Task 8: Full page review

**Files:**
- Read: `stays/index.html` — final state check

- [ ] **Step 1: Scan for any orphaned old class names**

```bash
cd "/Users/blakethomas/Desktop/hannah adeles home"
grep -n "class=\"hero\"\\|before-after\\|photo-grid\\|delivers-grid\\|deliver-card\\|photo-note\\|video-section" stays/index.html
```

Expected: no output. If any matches appear, remove them.

- [ ] **Step 2: Confirm all 4 photo src paths are correct**

```bash
grep -n "9V2A47" stays/index.html
```

Expected: 4 matches, all pointing to `/stays/professional space photos/` — none pointing to `/stays/photos/`.

- [ ] **Step 3: Confirm TikTok script appears exactly once**

```bash
grep -c "tiktok.com/embed.js" stays/index.html
```

Expected: `1`

- [ ] **Step 4: Open page in browser for full visual walkthrough**

```bash
open "/Users/blakethomas/Desktop/hannah adeles home/stays/index.html"
```

Verify in order:
1. Nav loads with "stays" active
2. Dark hero area with headline text and "let's connect →" button
3. Centered white intro strip: "Three ways to make your property unforgettable."
4. Navy Section 01 with video player
5. White Section 02 with 4 photos (2 rows) and pink callout box
6. Off-white Section 03 with TikTok row and new headline
7. Pink CTA: "Have a property that deserves to be seen?"
8. Footer with social icons

- [ ] **Step 5: Check mobile layout**

Open browser dev tools, set viewport to 375px wide. Verify:
- Hero text readable at 36px
- Photo rows stack to single column
- TikTok row scrolls horizontally

- [ ] **Step 6: Final commit**

```bash
cd "/Users/blakethomas/Desktop/hannah adeles home"
git add stays/index.html
git commit -m "feat: complete stays page redesign — video hero + 3 deliverable sections"
```
