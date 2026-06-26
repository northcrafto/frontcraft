# Frontcraft playbook — deeper guidance

Read this when you need more than the core SKILL.md rules: concrete recipes,
direction archetypes, and worked examples. This file is loaded on demand.

## Choosing a direction (archetypes to steal from)

You don't have to invent a style from nothing. Pick an archetype that fits the
content, then make it specific. Never blend more than two.

- **Editorial / publication** — large serif or high-contrast display headlines,
  generous margins, a strong baseline grid, restrained color, photography or
  rules as the only ornament. Good for: agencies, writers, premium brands.
- **Technical / terminal** — monospace or grotesque type, hairline borders,
  dense data, near-black or paper-white surfaces, one signal color. Good for:
  dev tools, dashboards, infra, security.
- **Soft / humanist** — warm tinted neutrals, rounded geometry, friendly sans,
  gentle shadows, roomy spacing. Good for: consumer apps, health, education.
- **Brutalist / raw** — exposed structure, oversized type, high contrast, blunt
  borders, deliberate "unstyled" honesty. Good for: portfolios, culture, music.
- **Luxury / minimal** — near-monochrome, enormous whitespace, tiny tracked-out
  labels, one hero image, almost no color. Good for: fashion, hospitality.

Specificity is everything: "editorial with a warm paper background, one oxblood
accent, and a condensed display serif" beats "modern and clean."

## Type pairing recipes that work

- **Serif display + clean sans body:** e.g. a high-contrast serif (Fraunces,
  Playfair, GT Super vibe) over a neutral sans (Inter, Geist, Söhne vibe).
- **Grotesque display + same-family text:** one well-made grotesque across the
  board (e.g. Neue Haas / Helvetica Now vibe) — safe, Swiss, timeless.
- **Mono accent:** body in a clean sans, but labels/eyebrows/code in a mono
  (JetBrains Mono, IBM Plex Mono) for a technical signal.

When using web fonts, load only the weights you use, and set a sensible fallback
stack so layout doesn't shift.

## A reliable spacing & sizing system

```
space: 4 8 12 16 24 32 48 64 96 128   (px or 0.25rem steps)
radius: 0 / 4 / 8 / 16 / full — pick ONE family and stay in it
type:  12 14 16 18 21 28 36 48 64 80  (a ~1.25–1.33 ratio scale)
```

Pick values from one scale and reuse them. The "almost right" gap (a stray 13px,
a 17px) is what makes pages feel amateur.

## Tailwind notes (when the stack is Tailwind)

- Extend the theme rather than littering arbitrary values: define your palette,
  font families, and a couple of custom sizes in config so the design is a system.
- Use `tracking-tight` on big headings, `leading-relaxed` on body. Reach for
  `max-w-prose` / `max-w-2xl` on text columns to control measure.
- Compose with `@layer components` (or a tiny set of class groups) instead of
  copy-pasting 20-utility strings everywhere — keeps the design editable.

## Plain HTML/CSS notes (when there's no framework)

- Start from a small set of CSS custom properties: `--bg --fg --muted --accent`,
  a spacing scale, and a type scale. This *is* your design system.
- Use a modern reset, `clamp()` for fluid type (`clamp(2rem, 5vw, 4rem)`), and
  CSS grid for layout. No framework needed to look expensive.
- Logical properties (`margin-inline`, `padding-block`) and `:focus-visible` get
  you responsive + accessible cheaply.

## Worked example — a hero that isn't generic

Generic (avoid): centered h1, centered subhead, centered button, three equal
feature cards below, purple-blue gradient background.

Better: an off-center composition — oversized headline pinned left spanning two
grid columns, a single supporting line beneath it, one primary action and one
quiet text link; the right column holds a single strong image or a live product
detail, not a stack of cards. Background is a tinted near-white. One accent on the
primary action only. The eye has a clear path: headline → action → proof.

## Redesign mode (when improving existing UI)

1. **Audit first.** Name the specific generic tells in the current design before
   changing anything (default fonts, equal-card rows, gray neutrals, dead links,
   inconsistent spacing).
2. **Preserve behavior.** Keep working functionality, routes, and content intact;
   you're restyling and re-structuring, not rebuilding logic.
3. **Change the system, not just surface.** Fix the type scale, palette, and
   spacing rhythm at the root — don't just tweak one component.
4. Re-run the pre-flight check from SKILL.md.

## Quick anti-slop checklist

- [ ] Direction stated in one sentence, fits the content
- [ ] One expressive type choice + real scale
- [ ] Multi-line headlines mentally rendered (no collisions)
- [ ] One committed palette, tinted neutrals, sparse accent
- [ ] Not the centered-hero + 3-equal-cards default
- [ ] Consistent spacing scale, generous whitespace
- [ ] Hover / focus-visible / empty / error states designed
- [ ] Zero `href="#"` or placeholder buttons
- [ ] Deliberate mobile layout
- [ ] Semantic, keyboard-operable, labelled, alt text
- [ ] No accidental AI gradient / glass-everything / emoji chrome / lorem
