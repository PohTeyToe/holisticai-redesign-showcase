# HolisticAI Redesign Showcase

Three landing page and app redesign variants for the [HolisticAI Health Portal](https://github.com/PohTeyToe/VJDS), built for stakeholder review. Each variant takes a different approach to visual design, animation, and interaction — from conservative refinement to bold experimentation.

**Live demo:** https://holisticai-redesign-showcase.onrender.com

---

## The 3 Variants

### v1 — Sasha Feedback

Faithful to the original landing-cinematic design with targeted enhancements based on stakeholder feedback. Pure CSS animations, light/dark mode toggle, and IntersectionObserver scroll-reveal effects. This is the closest to the current production design and carries the least implementation risk.

### v2 — Enhanced Motion

Same layout structure as v1 but with significantly richer interactions. Canvas-based particle hero background, framer-motion spring animations, animated counting stats, and scroll-linked progress indicators. Delivers a premium, polished feel without structural changes.

### v3 — Experimental

Structurally different from the other two. Full-viewport scroll-snap sections, split-screen layouts, sacred geometry SVG orb art, and side-rail dot navigation. Built on Tailwind CSS v4 instead of pure CSS. A bold, immersive experience aimed at a complete visual rebrand.

## Pages

Each variant includes 5 pages:

| Page | Description |
|-|-|
| Landing | Full marketing landing page with hero, features, journey, dosha preview, stats, CTA |
| Dashboard | Post-login home with health scores, recent activity, quick actions |
| Results | Dosha analysis results with visualizations and recommendations |
| Wellness Scanner | Multi-step wellness questionnaire with progress tracking |
| Meal Plan | Personalized daily meal plans with nutritional breakdowns |

A floating **variant switcher** pill (bottom-center) lets you jump between v1/v2/v3 at any time. Each variant's hero CTA ("Begin Your Journey") links directly to its dashboard for a realistic app flow. Inside app pages, each variant's own navbar links to the other pages within that variant.

## Shared Design DNA

All three variants share a common design foundation:

- **Fonts:** Crimson Pro (headings), DM Sans (body)
- **Color palette:** Brand green `#22c55e`, healing teal `#14b8a6`, terracotta `#ed7523`, sage `#6b8156`
- **Dark theme** as the default aesthetic
- **Aqua halo** background effects (radial gradient glows)

## Tech Stack

| | v1 | v2 | v3 |
|-|-|-|-|
| Framework | React 18 + TypeScript | React 18 + TypeScript | React 18 + TypeScript |
| Bundler | Vite 5 | Vite 5 | Vite 5 |
| Animations | Pure CSS + IntersectionObserver | framer-motion | framer-motion |
| Styling | CSS custom properties | CSS custom properties | Tailwind CSS v4 |
| Routing | React Router 6 | React Router 6 | React Router 6 |

## Run Locally

```bash
# Clone the repo
git clone https://github.com/PohTeyToe/holisticai-redesign-showcase.git
cd holisticai-redesign-showcase

# Serve the pre-built site (any static server works)
npx serve public
```

### Rebuilding a variant from source

Each variant in `build-tmp/` is an independent Vite project. To rebuild:

```bash
cd build-tmp/v2
npm install
MSYS_NO_PATHCONV=1 npx vite build --base=/v2/
# Copy dist/ into public/v2/
```

> **Note (Git Bash / MINGW):** The `MSYS_NO_PATHCONV=1` prefix is required to prevent MINGW from mangling the `--base=/v2/` path. Not needed on macOS/Linux.

After building, re-inject the variant switcher HTML into `public/vX/index.html` (the `<div id="variant-nav">` block outside the React root) and copy `index.html` to `404.html` for SPA routing.

## Project Structure

```
showcase/
  public/              # Deployed static site
    index.html         # Selector page (choose a variant)
    404.html           # SPA fallback redirect
    _redirects         # Render static site rewrite rules
    v1/                # Built output for variant 1
    v2/                # Built output for variant 2
    v3/                # Built output for variant 3
  build-tmp/           # Source code for each variant
    v1/                # Vite project — pure CSS approach
    v2/                # Vite project — framer-motion approach
    v3/                # Vite project — Tailwind v4 approach
  docs/                # Documentation
    VARIANTS.md        # Detailed variant comparison
  package.json
  vercel.json          # Vercel deployment config
```

## Deployment

Hosted as a **Render static site** on the `main` branch (single branch, no feature branches).

- **Render service:** `srv-d6msr46a2pns73ddogc0`
- **Auto-deploy:** enabled on push to `main`
- **SPA routing:** handled by `public/_redirects` (`/vX/* → /vX/index.html 200`)
- **Cache:** Render CDN caches aggressively; trigger a manual deploy with `clearCache` if stale content appears after push

## Known Fixes

- **Blank internal pages (V2/V3):** Caused by `AnimatePresence mode="wait"` wrapping `<Outlet />` in AppLayout. If the exit animation race-conditioned, the entering page stayed at `opacity: 0` permanently. Fixed by removing the AnimatePresence wrapper entirely — pages now render without transition animations.
- **V2 dashboard animations:** `useInView`-based conditional animations didn't fire for above-fold content. Fixed by using direct `animate` props instead.
- **V3 GeometricOrb:** `whileInView` on SVG elements failed for above-fold hero content. Fixed by switching to `animate`.

## Documentation

- [Variant Comparison](docs/VARIANTS.md) — detailed side-by-side breakdown of all three variants, page-by-page features, and recommendations for which to choose
- [Parent Project Tracker](../OVERVIEW.md) — phase overview and variant status
