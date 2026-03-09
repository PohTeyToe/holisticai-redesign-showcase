# Variant Comparison

Detailed comparison of the three HolisticAI redesign variants. For a quick overview, see the [README](../README.md).

---

## Overview

| | v1 — Sasha Feedback | v2 — Enhanced Motion | v3 — Experimental |
|-|-|-|-|
| Animation approach | Pure CSS transitions + IntersectionObserver | framer-motion springs + canvas particles | framer-motion + Tailwind v4 transitions |
| Layout style | Traditional scroll, section-based | Traditional scroll, section-based | Full-viewport scroll-snap sections |
| Styling system | CSS custom properties | CSS custom properties | Tailwind CSS v4 with custom tokens |
| Theme support | Light + dark mode toggle | Dark only | Dark only |
| Icon system | Inline SVG | Inline SVG | Lucide React |
| Navigation | Top navbar + hamburger mobile | Top navbar + scroll progress bar | Top navbar + side-rail dot navigation |
| Complexity | Low | Medium | High |
| Risk level | Minimal — conservative refinement | Low — additive enhancements only | Higher — structural departure from current design |
| Bundle impact | Smallest (no animation library) | Medium (framer-motion) | Largest (framer-motion + Tailwind runtime) |

---

## Design Decisions and Tradeoffs

### v1 — Sasha Feedback

Built directly from stakeholder feedback on the original landing-cinematic design. The philosophy is "refine, don't reinvent." Every animation uses CSS transitions or keyframes — no JavaScript animation libraries. The light/dark mode toggle gives users control over their viewing experience, and the scroll-reveal effects (powered by a custom `useScrollReveal` hook with IntersectionObserver) add polish without complexity.

**Tradeoff:** Less visually distinctive. The animations feel clean but won't make anyone say "wow." This is intentional — the goal is reliability and fast iteration.

### v2 — Enhanced Motion

Takes the exact same layout and information architecture as v1, then layers on premium motion design. The canvas particle system in the hero creates an ambient, living background. Spring-physics animations (via framer-motion) make interactions feel organic. The `useCountUp` hook animates stats into view, and the `useScrollProgress` hook drives a thin progress bar across the top of the viewport.

**Tradeoff:** The framer-motion dependency adds bundle weight and introduces a runtime animation layer. Canvas particles consume GPU resources on low-end devices. The payoff is a noticeably more premium feel that differentiates the product.

### v3 — Experimental

A structural departure. Instead of traditional scrolling, the landing page uses full-viewport scroll-snap sections — each section occupies the entire screen and snaps into place. The sacred geometry SVG orb (`GeometricOrb` component) is a custom animated illustration that serves as a visual anchor. Tailwind v4 replaces handwritten CSS, trading fine-grained control for rapid iteration speed.

**Tradeoff:** Scroll-snap can feel disorienting to users who expect free scrolling. The structural differences make this harder to merge back into the main codebase. Tailwind v4 is a different styling paradigm from the rest of the project. This variant is best suited for a full rebrand scenario.

---

## Cross-Variant Navigation

A floating **variant switcher pill** is injected as pure HTML (outside React's root div) at the bottom-center of every page. It provides instant switching between v1/v2/v3 and a link back to the selector page. Each variant's hero CTA ("Begin Your Journey") links to `/dashboard` for a realistic app flow.

> **Animation reliability note:** Page transition animations (`AnimatePresence mode="wait"` wrapping `<Outlet />`) were removed from V2 and V3 due to an intermittent blank-page bug. The exit animation race condition could leave entering pages stuck at `opacity: 0`. Pages now render immediately without enter/exit transitions. V1 was unaffected (uses CSS-only animations).

---

## Page-by-Page Comparison

### Landing Page

| Feature | v1 | v2 | v3 |
|-|-|-|-|
| Hero | Gradient text + CSS fade-in | Canvas particle background + spring entrance | Full-viewport snap section + geometric orb |
| Features | Icon grid with scroll-reveal | Staggered motion entrance | Scroll-snap section with split layout |
| Journey | Timeline with step reveals | Animated timeline with parallax | Full-screen journey steps |
| Stats | Static number display | Animated count-up on scroll | Integrated into sections |
| CTA | Standard button with hover | Animated button with spring | Full-viewport CTA section |
| Nav | Sticky top + hamburger mobile | Sticky top + scroll progress bar | Sticky top + side dot rail (desktop) |

### Dashboard

| Feature | v1 | v2 | v3 |
|-|-|-|-|
| Layout | Glass-morphism cards in grid | 3D tilt cards with hover depth | Sacred geometry orbital diagram |
| Health scores | Colored progress bars | Animated ring gauges | Radial score display |
| Activity feed | Simple list | Motion-animated list items | Timeline with geometric markers |
| Quick actions | Button grid | Hover-animated action cards | Orbital action nodes |

### Results (Dosha Analysis)

| Feature | v1 | v2 | v3 |
|-|-|-|-|
| Primary viz | Horizontal bar charts | Animated dosha ring (SVG) | Pentagon radar chart |
| Score display | Percentage text + bars | Animated percentage + ring fill | Geometric score nodes |
| Recommendations | Card list | Staggered reveal cards | Scroll-snap recommendation sections |
| Detail level | Tabbed content panels | Expandable accordion | Full-page sections per dosha |

### Wellness Scanner

| Feature | v1 | v2 | v3 |
|-|-|-|-|
| Flow | Step wizard with progress bar | Step wizard + canvas particle background | Sacred geometry scan point selector |
| Progress | Linear progress bar | Animated segmented progress | Geometric completion ring |
| Input style | Standard form inputs | Motion-enhanced inputs | Tailwind-styled inputs |
| Transitions | CSS slide transitions | Spring page transitions | Snap-scroll between steps |

### Meal Plan

| Feature | v1 | v2 | v3 |
|-|-|-|-|
| Day selection | Tab bar (Mon-Sun) | 3D flip tab cards | Scroll-snap day sections |
| Meal cards | Flat cards with nutritional info | 3D tilt meal cards with hover | Geometric meal cards |
| Nutrition data | Inline text stats | Animated bar charts | Circular macro gauges |
| Layout | Vertical scroll list | Grid with stagger animation | Horizontal snap scroll |

---

## Recommendations

### Choose v1 when:
- Stakeholders want minimal disruption from the current design
- Timeline is tight and predictability matters
- The team wants to ship fast with low QA overhead
- Light mode support is a requirement
- Performance on low-end devices is a priority

### Choose v2 when:
- The goal is a premium, polished feel without changing the site's structure
- The team is comfortable with framer-motion as a dependency
- Stakeholders responded well to the current layout but want it to feel "more alive"
- You want the best balance of visual impact vs. implementation risk

### Choose v3 when:
- The project is pursuing a full visual rebrand
- Stakeholders are open to a fundamentally different browsing experience
- The team is ready to adopt Tailwind v4 as the styling system
- Differentiation from competitors matters more than familiarity
- There is time for thorough usability testing of the scroll-snap paradigm
