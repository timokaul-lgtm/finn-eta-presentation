# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-file browser-based presentation (`index.html`) about ETAs at FINN. No build step, no dependencies, no package manager — just HTML, CSS, and vanilla JS served statically via GitHub Pages.

**Live URL:** https://timokaul-lgtm.github.io/finn-eta-presentation/
**Password:** `FINN ETA CLM`

## Developing

Open `index.html` directly in a browser, or serve locally:

```bash
npx serve .
# or
python3 -m http.server 8080
```

## Deploying

Changes go live automatically ~30 seconds after pushing to `main`:

```bash
git add index.html
git commit -m "your message"
git push
```

## Architecture

Everything lives in `index.html` — styles, markup, and scripts are all inline.

**Slide engine:** Pure CSS + vanilla JS, no libraries. All 13 slides are `position: absolute` on a shared `#deck` container. Navigation sets `transform: translateX(-100% / 0 / 100%)` on each slide via JS. The `.animated` class is toggled on/off around each transition to enable/disable CSS transitions (prevents snap-back on page load).

**Password gate:** A `#gate` overlay is rendered on top of everything. On correct password it fades out and removes itself from the DOM. `sessionStorage` is used to skip the gate on refresh within the same browser session.

**Images:** The 4 dashboard screenshots are referenced with URL-encoded filenames (spaces → `%20`) as relative paths alongside `index.html`. They are committed to the repo and served as static assets.

**Key CSS classes:**
- `.slide` — base slide; default `transform: translateX(100%)` (off-screen right)
- `.slide.animated` — enables the CSS transition during navigation
- `.slide.center` — centres content (used for title and Q&A slides)
- `.eyebrow` — blue section label above each heading
- `.points` / `.point` / `.pt` — bullet list pattern used across content slides
- `.dev-grid` / `.dev-card` — deviation concept visualization (slide 3)
- `.badge.auto` / `.badge.manu` — brand pill badges (blue = automated feed, grey = manual)
- `#gate` — full-screen password overlay

**Slide inventory (13 slides):**
1. Title
2. What is an ETA? (concept + stats)
3. Mission / deviation concept visual
4. Limitations
5. Q4 2025 model rebuild (timeline)
6. Results (accuracy screenshot)
7. Brand overview (screenshot)
8. Setting ETAs — automated brands (BMW, Seat, Cupra, Stellantis)
9. BMW technical example (screenshot)
10. Setting ETAs — manual brands (MG, BYD, Hyundai, Kia)
11. Steering via ETA Accuracy
12. Accuracy dashboard (screenshot)
13. Q&A
