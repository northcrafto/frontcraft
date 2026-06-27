# Premium playbook — building sites that look expensive

Read this when the user wants high-end, agency-grade, award-site quality ("make it
look expensive / fancy / premium"). The core taste rules in `SKILL.md` still apply
— this adds the finish that separates a costly site from a competent one.

The mindset: **expensive = restraint + precision, not more stuff.** Every premium
move below is about doing fewer things more exactly.

## Where to steal from (study these, name your reference)

Don't invent premium from scratch — channel sites that already nailed it:

- **Stripe** (stripe.com) — gradient meshes, immaculate type, layered depth, the
  gold standard for "polished SaaS."
- **Linear** (linear.app) — dark premium, precise spacing, subtle glow and grain,
  restrained color, crisp motion.
- **Vercel** (vercel.com) — high-contrast minimalism, geometric, confident black/
  white with sharp detail.
- **Apple** (apple.com) — scroll-driven product storytelling, huge type, pinned
  sections, full-bleed art direction.
- **Family / Cosmos / Igloo Inc** — experimental, 3D/WebGL heroes, tactile motion,
  the Awwwards "Site of the Day" end of the spectrum.
- **Agencies — Locomotive, Active Theory, Cuberto, Unseen Studio** — smooth scroll,
  custom cursors, image masks, magnetic interactions.
- **Editorial luxury — fashion/hospitality houses** — enormous whitespace, tiny
  tracked-out labels, one serif, near-monochrome, one hero image.

Pick ONE reference whose vibe fits the content and execute at that level. "Linear-
style dark premium" is a far better brief to yourself than "make it nice."

## Typography (the biggest expensive signal)

- A characterful display face at large sizes: Fraunces, GT Sectra, PP Editorial
  New, Canela, Reckless (serif); Neue Montreal, Söhne, PP Neue Montreal, Aeonik,
  Geist (grotesque). Pair with a clean, neutral text face.
- Hand-tune it: tight tracking on big headings (`letter-spacing: -0.02em` to
  `-0.04em`), generous line-height on body, `font-optical-sizing: auto`, `text-
  wrap: balance` on headlines, tabular numerals for stats.
- Fluid sizing with `clamp()` so type scales smoothly across viewports.

## Color, depth & texture

- Near-monochrome or dark-premium base + ONE precise accent. Rich tinted neutrals,
  never flat `#000`/`#fff`.
- **Layered soft shadows** instead of one hard drop:
  ```css
  box-shadow: 0 1px 2px rgba(0,0,0,.04), 0 8px 24px -8px rgba(0,0,0,.12),
              0 24px 64px -24px rgba(0,0,0,.18);
  ```
- **Subtle grain** lifts flat color out of "default": a faint SVG/PNG noise overlay
  at 3–6% opacity, or a CSS `radial-gradient` mesh.
- Hairline borders: `1px solid rgba(255,255,255,.08)` (dark) — definition without
  weight.

## Motion (engineered, not decorative)

- Tools: **GSAP + ScrollTrigger** for scroll work (pin, scrub, stagger, parallax);
  Framer Motion (React) or the Web Animations API for component motion; Lenis for
  smooth scroll. Lottie for vector micro-animations.
- Signature moves, used sparingly: scroll-linked reveals with stagger, a pinned
  section that scrubs through states, parallax depth on hero layers, magnetic
  buttons, a tasteful custom cursor, image masks that wipe/clip on enter, number
  counters that tick up.
- Always eased (`cubic-bezier(.16,1,.3,1)` is a lovely premium ease), fast
  (200–500ms), and gated behind `prefers-reduced-motion`. One or two moments per
  page — relentless motion reads cheap, not expensive.

## Imagery

- Large, high-quality, consistently graded. Full-bleed heroes; intentional crops;
  one coherent visual world. Consider a rendered/3D or abstract gradient hero for
  product/tech brands — for working WebGL/3D hero code (Three.js + react-three-
  fiber, with fallbacks), see `references/3d-hero.md`.
- Never mix mismatched stock. A unified grade (same warmth, contrast, mood) makes
  even stock feel art-directed.

## Layout & finish

- Big, confident sections with lots of air. A strong grid with the occasional
  intentional break. Generous, consistent spacing scale.
- Obsess over micro-detail: every hover state considered, brand-matched focus
  rings, fine dividers, a rich multi-column footer, polished empty/loading states.
- Performance is part of luxury: optimized images (sized, lazy, modern formats),
  no layout shift, fast paint. A janky "premium" site isn't premium.

## Glass, done honestly (when the brief actually wants it)

`SKILL.md` bans glassmorphism as an *unprompted default*. But some briefs genuinely
want it (an Apple-adjacent product, a dark dashboard overlay). When they do, do it
properly instead of slapping on `backdrop-filter: blur()`:

- The blur alone looks cheap. Add edge refraction: a faint inner border
  (`border: 1px solid rgba(255,255,255,0.10)`) and an inner highlight
  (`box-shadow: inset 0 1px 0 rgba(255,255,255,0.12)`), over a low-opacity fill.
- It only reads as glass over *something* — a photo, a gradient, content scrolling
  behind. Glass over a flat color is just a translucent box.
- **Always ship a fallback.** Under `@media (prefers-reduced-transparency: reduce)`
  (and where `backdrop-filter` is unsupported), replace it with a solid tinted
  surface — never leave unreadable text floating on a blur.

```css
.glass {
  background: rgba(255,255,255,0.08);
  backdrop-filter: blur(16px) saturate(140%);
  border: 1px solid rgba(255,255,255,0.10);
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.12), 0 8px 40px rgba(0,0,0,0.20);
}
@media (prefers-reduced-transparency: reduce) {
  .glass { background: rgba(20,20,24,0.92); backdrop-filter: none; }
}
```

Honesty note: Apple's "Liquid Glass" is an Apple-platform material; there is no
official web `liquid-glass.css`. A web version is a `backdrop-filter` approximation
— comment it as such, don't pretend it's the real material.

## Reality check

Premium is a finish level, not a sticker. If the budget/stack is a static page,
you can still hit it with great type, space, one grain texture, layered shadows,
and one GSAP reveal. If it's a full build, go further with WebGL/3D and smooth
scroll. Match ambition to the project — but whatever the scope, execute it exactly.
Then run the `SKILL.md` pre-flight, including the **Finish** check.
