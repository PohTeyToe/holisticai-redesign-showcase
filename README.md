# HolisticAI Redesign Showcase

Three landing page and app redesign variants for the [HolisticAI Health Portal](https://github.com/PohTeyToe/VJDS), built for stakeholder review. Each variant takes a different approach to visual design, animation, and interaction — from conservative refinement to bold experimentation.

**Live demo:** https://pohteytoe.github.io/holisticai-redesign-showcase/

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

A floating **variant switcher** (bottom-right) lets you jump between v1/v2/v3 without leaving the current page type. Inside app pages, a **nav pill** (top-left) links to the other app pages within the same variant.

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

# Or build a variant from source
cd build-tmp/v1
npm install
npm run build
# Output lands in build-tmp/v1/dist/
```

Each variant in `build-tmp/` is an independent Vite project with its own `package.json`, `vite.config.ts`, and `src/` directory.

## Project Structure

```
showcase/
  public/              # Deployed static site
    index.html         # Selector page (choose a variant)
    404.html           # SPA fallback for GitHub Pages
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

## Documentation

- [Variant Comparison](docs/VARIANTS.md) — detailed side-by-side breakdown of all three variants, page-by-page features, and recommendations for which to choose.
