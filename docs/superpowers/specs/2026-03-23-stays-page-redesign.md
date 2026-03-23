# Stays Page Redesign — Spec
**Date:** 2026-03-23
**Status:** Approved

## Overview

Redesign `stays/index.html` to lead with the new promotional video and restructure the page around three distinct deliverables: marketing video, professional photography, and short-form social content. The goal is to differentiate Hannah Adele's offering from generic UGC creators and attract both paying clients and properties interested in a content-for-stay collab/trade.

---

## Page Structure (top to bottom)

### 1. Nav
No change. Existing sticky nav with "stays" active.

---

### 2. Hero — Promo Video
**CSS class: `.hero-video`**

Container:
```css
.hero-video {
  position: relative;
  background: #0d0d1a; /* near-black fallback if video fails */
  height: 55vh;
  min-height: 320px;
  overflow: hidden;
}
```

Video element — uses `position: absolute` to correctly fill a `min-height`-constrained container:
```html
<video autoplay muted loop playsinline
  style="position:absolute;inset:0;width:100%;height:100%;object-fit:cover;object-position:center;display:block">
  <source src="/stays/stay%20promo%20video.mov">
</video>
```
Note: omit `type` attribute — browsers sniff `.mov`/H.264 without it.

Gradient overlay (renders above video, below text):
```css
position: absolute; inset: 0;
background: linear-gradient(to top, rgba(0,0,0,0.72) 0%, rgba(0,0,0,0.15) 60%, transparent 100%);
pointer-events: none;
```

Text overlay `.hero-video-content`:
```css
position: absolute; bottom: 0; left: 0; right: 0;
padding: 0 36px 28px;
```

Content inside `.hero-video-content`:
- **Eyebrow:** `font-size: 11px; text-transform: uppercase; letter-spacing: 0.18em; color: rgba(255,255,255,0.6); font-weight: 700; margin-bottom: 14px`
  - Copy: `hospitality content · on-location`
- **Headline:** CSS class `.hero-video-headline` (must be a class, not inline, so the mobile media query can override `font-size`)
  - `font-size: 44px; font-weight: 900; color: white; line-height: 0.97; margin-bottom: 14px`
  - Copy: `I'll make people want to <em>stay</em> there.`
  - `em { color: var(--yellow); font-style: normal }`
- **Sub:** `font-size: 13px; color: rgba(255,255,255,0.78); line-height: 1.6; margin-bottom: 22px`
  - Copy: `Hotels, Airbnbs, rentals & resorts — I come to you, tell the story, and hand you a full content package.`
- **CTA `.hero-video-cta`:**
  ```css
  display: inline-block; text-decoration: none;
  background: white; color: var(--navy);
  font-size: 12px; font-weight: 800;
  padding: 12px 24px; border-radius: 4px;
  text-transform: uppercase; letter-spacing: 0.07em;
  ```
  - `href="mailto:hannahadeleshome@gmail.com"` — Copy: `let's connect →`

---

### 3. Intro Strip
**CSS class: `.intro-strip`**

```css
.intro-strip { background: white; padding: 44px 36px; text-align: center; }
```

- **Label:** use `.section-label` class — Copy: `what you walk away with`
- **Headline:** use `.section-headline` class — Copy: `Three ways to make your property <em>unforgettable.</em>` — `em { color: var(--pink); font-style: normal }`
- **Sub:** use `.section-sub` class with an additional inline style `style="max-width:460px;margin:0 auto"` to center it. The class default `margin-bottom: 28px` is acceptable here.
  - Copy: `Pick one or bundle them all — marketing video, professional photography, and short-form social content.`

---

### 4. Section 01 — Marketing Video
**CSS class: `.deliver-video`**

```css
.deliver-video { background: var(--navy); padding: 44px 36px; }
```

- **Label:** use `.section-label` class with descendant override `color: rgba(255,255,255,0.4)` — implemented as `.deliver-video .section-label { color: rgba(255,255,255,0.4); }` in the `<style>` block.
  - Copy: `01 · Marketing Video`
- **Headline:** use `.section-headline` class with descendant override `color: white` — `.deliver-video .section-headline { color: white; }`
  - Copy: `A cinematic promo, ready to post.`
- **Sub:** use `.section-sub` class with descendant override `color: rgba(255,255,255,0.65); margin-bottom: 20px` — `.deliver-video .section-sub { color: rgba(255,255,255,0.65); margin-bottom: 20px; }`
  - Copy: `Professional full-length property video — edited, color-graded, and ready for your listing page, website, or social ads. This is what sets a property apart.`
- **Video player `.deliver-video-player`:**
  ```css
  .deliver-video-player {
    border-radius: 10px; overflow: hidden;
    border: 2px solid rgba(255,255,255,0.12);
    background: #000; aspect-ratio: 16/9;
  }
  ```
  ```html
  <div class="deliver-video-player">
    <video controls style="width:100%;height:100%;display:block">
      <source src="/stays/stay%20promo%20video.mov">
    </video>
  </div>
  ```
  No autoplay. No poster image.
  - `aspect-ratio: 16/9` on a block element requires Chrome 88+, Safari 15+, Firefox 89+. This project targets modern browsers — no legacy fallback needed.
- **Spec note** below player: `font-size: 11px; color: rgba(255,255,255,0.35); text-align: center; margin-top: 8px`
  - Copy: `Commercial quality · Edited & color-graded · Delivered as .mp4`

---

### 5. Section 02 — Professional Photography
**CSS class: `.deliver-photos`**

```css
.deliver-photos { background: white; padding: 44px 36px; }
```

- **Label:** use `.section-label` — Copy: `02 · Professional Photography`
- **Headline:** use `.section-headline` — Copy: `Gallery-quality. Every room. Every amenity.`
- **Sub:** use `.section-sub` — Copy: `Shot by a commercial photographer — not iPhone shots. With or without lifestyle/UGC styling depending on the vibe you want.`

Photo grid:
```css
.deliver-photos-row1 {
  display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-bottom: 8px;
}
.deliver-photos-row1 .photo-cell { aspect-ratio: 4/3; border-radius: 8px; overflow: hidden; background: #eee; }

.deliver-photos-row2 {
  display: grid; grid-template-columns: 1fr 1fr; gap: 8px;
}
.deliver-photos-row2 .photo-cell { aspect-ratio: 16/9; border-radius: 8px; overflow: hidden; background: #eee; }

.deliver-photos-row1 .photo-cell img,
.deliver-photos-row2 .photo-cell img { width: 100%; height: 100%; object-fit: cover; display: block; }
```

Images — all from `/stays/professional space photos/` (**not** `/stays/photos/`, which is removed from git):
```html
<!-- Row 1 -->
<img src="/stays/professional space photos/9V2A4752-VSCO.jpeg" alt="Coastal Airbnb living space">
<img src="/stays/professional space photos/9V2A4735-VSCO.jpeg" alt="Coastal Airbnb bedroom">
<!-- Row 2 -->
<img src="/stays/professional space photos/9V2A4695-VSCO.jpeg" alt="Coastal Airbnb amenities">
<img src="/stays/professional space photos/9V2A4699-VSCO.jpeg" alt="Coastal Airbnb exterior">
```

Callout `.photo-callout` (replaces old `.photo-note` — remove `.photo-note` CSS rule):
```css
.photo-callout {
  background: #fff0f6; border-left: 4px solid var(--pink);
  border-radius: 0 8px 8px 0; padding: 12px 16px;
  font-size: 12px; color: #444; line-height: 1.5; margin-top: 20px;
}
.photo-callout strong { color: var(--black); }
```
Note: this rule must be defined in the page `<style>` block — there is no global `strong` rule in `shared.css`. The old `.photo-note strong` rule is being renamed here.

Copy: `📷 <strong>Commercial photography is included in every package.</strong> My husband is a professional commercial photographer — he's on every job. You don't hire us separately.`

---

### 6. Section 03 — Short-Form Social Content
**CSS class: `.deliver-social`** (replaces `.video-section`)

```css
.deliver-social { background: var(--off); padding: 44px 36px; border-top: 2px solid #f0f0f0; }
```

- **Label:** use `.section-label` — Copy: `03 · Short-Form Social Content`
- **Headline:** use `.section-headline` — Copy: `Share it on your feed — or I'll promote on mine.`
- **Sub:** use `.section-sub` with `style="margin-bottom:0"` inline override to suppress the default `28px` bottom margin (since the TikTok row follows directly).
  - Copy: `Vertical UGC-style videos of the space, amenities, and experience. Social-ready for TikTok, Reels & Shorts. Use them yourself, or let me post them to my audience.`
- **TikTok row:** identical `.tiktok-row` markup — all 6 existing `<blockquote class="tiktok-embed">` elements, unchanged video IDs
- **Move** (do not duplicate) `<script async src="https://www.tiktok.com/embed.js"></script>` from the old `.video-section` — place it after the closing `</div>` of `.tiktok-row`, before the closing `</div>` of `.deliver-social`. Must appear after the blockquotes or embeds will not initialise.

---

### 7. CTA Section
**CSS class: `.cta-section`** — reuse all existing styles unchanged. Update copy only:

| Element | New copy |
|---|---|
| `.cta-label` | `work together` |
| `.cta-headline` | `Have a property that deserves to be <em>seen?</em>` — em = `var(--yellow)` |
| `.cta-sub` | `Whether you want to hire us for a full content shoot or explore a collab — I'm open to both. Let's talk.` |
| `.cta-btn` | `reach out →` → `mailto:hannahadeleshome@gmail.com` |
| `.cta-email` | `hannahadeleshome@gmail.com` (unchanged) |

---

### 8. Footer
No change.

---

## What's Removed

Remove all markup AND CSS definitions for the following:

| Class(es) | Section |
|---|---|
| `.hero`, `.hero-eyebrow`, `.hero-headline`, `.hero-sub`, `.hero-cta`, `.hero-photo-stack`, `.hero-img` | Old photo-stack hero |
| `.before-after`, `.ba-side`, `.ba-before`, `.ba-after`, `.ba-label`, `.ba-text`, `.ba-arrow` | Before/after banner |
| `.photo-grid-3`, `.photo-grid-4`, `.photo-cell`, `.photo-caption` | Old gallery grid |
| `.delivers`, `.delivers-grid`, `.deliver-card`, `.deliver-icon`, `.deliver-title`, `.deliver-desc` | Old 4-card deliverables section |
| `.photo-note` | Replaced by `.photo-callout` |
| `.video-section` | Replaced by `.deliver-social` |

---

## Assets

| Asset | Path | Used in |
|---|---|---|
| Promo video | `/stays/stay%20promo%20video.mov` | Hero (autoplay) + Section 01 (controls) |
| Photo 1 | `/stays/professional space photos/9V2A4752-VSCO.jpeg` | Section 02 row 1 left |
| Photo 2 | `/stays/professional space photos/9V2A4735-VSCO.jpeg` | Section 02 row 1 right |
| Photo 3 | `/stays/professional space photos/9V2A4695-VSCO.jpeg` | Section 02 row 2 left |
| Photo 4 | `/stays/professional space photos/9V2A4699-VSCO.jpeg` | Section 02 row 2 right |
| TikTok embeds | 6 existing video IDs (unchanged) | Section 03 |

---

## CSS Class Summary

**New classes:** `.hero-video`, `.hero-video-content`, `.hero-video-headline`, `.hero-video-cta`, `.intro-strip`, `.deliver-video`, `.deliver-video-player`, `.deliver-photos`, `.deliver-photos-row1`, `.deliver-photos-row2`, `.photo-callout`, `.deliver-social`

**Retained classes:** `.section-label`, `.section-headline`, `.section-sub`, `.cta-section`, `.cta-label`, `.cta-headline`, `.cta-sub`, `.cta-btn`, `.cta-email`, `.tiktok-row`, `.tiktok-embed`, `.footer`

**Descendant overrides needed in `<style>` block:**
- `.deliver-video .section-label { color: rgba(255,255,255,0.4); }`
- `.deliver-video .section-headline { color: white; }`
- `.deliver-video .section-sub { color: rgba(255,255,255,0.65); margin-bottom: 20px; }`

---

## Design System

Variables from `shared.css` — reference only, do not redefine:
- `--pink: #FF7EB3` / `--yellow: #F5CB00` / `--navy: #0d2461` / `--off: #fafafa` / `--black: #1a1a1a`

Hero fallback `background: #0d0d1a` on `.hero-video` — hardcoded, intentionally near-black (not `--navy`).

---

## Mobile (`@media (max-width: 600px)`)

```css
.hero-video { height: auto; min-height: 260px; }
.hero-video-content { padding: 0 20px 20px; }
.hero-video-headline { font-size: 36px; } /* overrides the 44px class default */
.intro-strip { padding: 36px 20px; }
.deliver-video,
.deliver-photos,
.deliver-social { padding: 36px 20px; }
.deliver-photos-row1,
.deliver-photos-row2 { grid-template-columns: 1fr; }
.tiktok-row { gap: 10px; } /* carry forward from existing mobile rule */
```

---

## Scope

- **In scope:** `stays/index.html` only
- **Out of scope:** `shared.css`, other pages, video format conversion
