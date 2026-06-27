# Motion & performance — engineered, not bolted on

Read this when a build has real motion, or when "premium" is the goal. The core
SKILL.md says *why* to animate (explain, guide, give feedback); this file is *how*
to make it smooth, cheap, and accessible, in whatever stack you're in.

The rule that gates everything: **every animation earns its place.** Before adding
one, say in a sentence what it communicates — hierarchy, sequence, feedback, or a
state change. "It looked cool" is not an answer. Motion you can't justify is the
thing that makes a page feel busy and amateur, not expensive.

## Performance non-negotiables (every stack)

- **Animate only `transform` and `opacity`.** Never animate `top`, `left`,
  `width`, `height`, `margin`, or `box-shadow` in a loop — they trigger layout and
  paint on every frame and stutter on mobile. Move with `translate`, size with
  `scale`, fade with `opacity`.
- **`will-change` is a scalpel, not seasoning.** Put it only on the element that is
  actually about to move, and take it off after. Blanket `will-change` wastes GPU
  memory.
- **Never drive animation from a raw scroll handler that writes framework state.**
  A `scroll` listener (or `requestAnimationFrame` loop) that updates React/Vue/
  Svelte state runs every frame, re-renders the tree, and collapses on mobile. Use
  the right tool instead (next section).
- **Grain, noise, and blur backdrops go on one fixed, `pointer-events: none`
  layer.** Putting a noise filter on a scrolling container repaints it continuously
  and kills frame rate.
- **Z-index is a system, not confetti.** Reserve it for real stacking contexts
  (sticky nav, modal, overlay, grain). Don't sprinkle `z-50` to fix a paint order
  you could fix structurally.

## Scroll-linked motion without the jank

Pick the lightest tool that does the job:

1. **Just "appear on enter"?** Use `IntersectionObserver` (vanilla) or the
   framework's in-view hook. No scroll math, no per-frame work. This covers most
   reveals.
2. **Progress tied to scroll (parallax, a value that tracks position)?** Use a
   platform/library mechanism that runs off the main render path: CSS
   scroll-driven animations (`animation-timeline: view()` / `scroll()`) where
   supported, or the library's scroll-value primitive (see per-stack notes).
3. **Pin / stack / horizontal-pan (the section sticks while you scroll through
   it)?** This is the one case to reach for GSAP + ScrollTrigger. Pin at the
   viewport top, scrub against real scroll distance, and clean up on unmount.

## Reduced motion is mandatory

Any non-trivial motion must honor `prefers-reduced-motion`. Parallax, pinning,
infinite loops, and pointer physics **collapse to static or instant** — not "a bit
slower." In CSS, gate the motion or override it under
`@media (prefers-reduced-motion: reduce)`. In JS, read the preference once and skip
the animation path entirely, setting the final state directly.

## Core Web Vitals (check before you call it done)

- **LCP < 2.5s** — the hero image is the usual LCP element. Mark it high-priority
  (preload / `fetchpriority="high"` / `priority`), serve a sensible width, and
  don't lazy-load it.
- **CLS < 0.1** — reserve space for every image (aspect-ratio or width/height),
  for fonts (`font-display: swap` + a matched fallback), and for embeds. Nothing
  should jump as the page settles.
- **INP < 200ms** — keep heavy work off the main thread; don't block input with
  animation setup. Lazy-load anything below the fold and any heavy library.

## Per-stack notes (same principles, different levers)

- **Plain HTML/CSS/JS:** CSS transitions + `@keyframes` for hover and load-ins;
  `IntersectionObserver` for reveals; CSS scroll-driven animations for cheap
  parallax; the Web Animations API (`element.animate`) when you need JS control;
  GSAP only for pin/scrub. This is Frontcraft's default for static and small-business
  sites and it's plenty.
- **React / Next:** use a motion library's primitives for continuous values
  (scroll progress, pointer physics) so they live *outside* the render cycle —
  never `useState` for a value that changes every frame. Isolate any motion in a
  client leaf component; render the rest as static/server markup. GSAP lives in an
  effect with an explicit cleanup that reverts its context on unmount.
- **Svelte / Vue:** built-in transition/animation directives for enter/leave;
  `IntersectionObserver` (or an in-view action/directive) for reveals; same GSAP
  isolation + cleanup rule for pin/scrub.
- **One animation engine per component tree.** Don't run GSAP/Three.js and a
  React motion lib over the same elements — they fight for the same frames.

## Signature-moment discipline

One or two engineered moments beat motion everywhere: a hero reveal, a section
that pins, a magnetic CTA. Pick the moments that carry meaning and leave the rest
still. A horizontal-scroll / kinetic marquee is a once-per-page move at most; a
second one reads as filler. If you claim a motion-heavy direction, the page must
actually move on entrance, scroll, and hover — a static page that promised
cinematic motion is broken. If you can't ship the motion cleanly in scope, dial it
down and ship a crisp static page instead of half-built animation that cuts off or
jumps.
