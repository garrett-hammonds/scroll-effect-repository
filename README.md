# Scroll Effect Reference Sites

Exported HTML from three production sites whose scroll effects HMM studied to
build the `scroll-effects` skill in `hmm-base-repository`
(`.claude/skills/scroll-effects/`). The exports hold markup, CSS, and glue
scripts. The ScrollTrigger call sites live in external files that are not in
the exports, so the skill carries its own reference implementations; these
files are the evidence behind its pattern catalog.

| File | Site | Platform | Libraries observed |
|---|---|---|---|
| `21-oak-source-code.html` | 21 Oaks student apartments | Webflow | GSAP 3.15 + ScrollTrigger, Lenis 1.3 (desktop only), Splide, Finsweet |
| `breakthrough-energy-source-code.html` | Breakthrough Energy | Vue / Nuxt SSR | Lenis with a custom scrollbar, Rive canvas, container queries |
| `heron-ai-app-source-code.html` | Heron AI | Webflow + Vite | Lenis 1.1, Swiper, Barba, GSAP SplitText, CSS keyframes |

## What each site contributed

**21 Oaks**

- Lenis mount / unmount by media query, with scroll position preserved
- Section-aware header theme (`data-section="hero|light|dark"`)
- ScrollTrigger refresh after `document.fonts.ready` and after `load`
- Pausing a keyframe loop offscreen with an IntersectionObserver
- Reduced-motion override on the scribble underline
- Not copied: `st-pending` page hide until ScrollTrigger is ready, `will-change` on every card, hot-linked libraries, autoplaying hero mask

**Breakthrough Energy**

- The pure-CSS sticky pin: an `N × 100lvh` wrapper with a `position: sticky` stage
- `contain: content` and `overflow: clip` on every animated stage
- Chapter, side-title, and dot layers all present in the served DOM
- Not copied: no `prefers-reduced-motion` anywhere, 26 screens of pinned travel, canvas with no static fallback, custom scrollbar

**Heron AI**

- Complete reduced-motion blocks with final-state overrides
- SVG stroke draw via `stroke-dashoffset` (simplified in the skill with `pathLength="1"`)
- Sticky step section where the active item fades in as the reader scrolls
- CSS marquees on a duplicated track
- Not copied: infinite loops running offscreen, Barba transitions, a leftover `localhost` Vite client script

## How the skill maps them

| Pattern | 21 Oaks | Breakthrough | Heron |
|---|---|---|---|
| 1, 2 Reveal / stagger | external JS | external JS | yes |
| 3 Progress indicator | | custom scrollbar | |
| 5 Section-aware header | yes | inversion nav | |
| 6 SVG draw | scribble | | yes |
| 7 Marquee | | | yes |
| 8 Pinned steps | gallery pin | 26-screen story | why-us steps |
| 9 Parallax / scrub | yes | Rive scrub | |
| 10 Horizontal track | apartments row | | |
| 11 Masked media | hero switcher | masked titles | |
| Smooth scroll | Lenis, desktop | Lenis | Lenis |
| Reduced motion | partial | none | complete |

The full read of each site, including what not to copy and why, is in the
skill's `references/reference-sites.md`.

## Adding a site

Save the rendered HTML (View Source, not DevTools Elements) as
`<site>-source-code.html`, add a row to the first table, and note which
patterns it demonstrates. If the site's scroll scripts are external, save them
alongside the HTML so the call sites can be read.
