# Calibration — turning the three spectrums into buildable numbers

`SKILL.md` names the three spectrums (Composure / Motion / Density) in words so the
user can nudge them in plain language. This file converts each into concrete,
buildable defaults — a 1–10 notch and the CSS that notch actually produces — so a
calibration is reproducible instead of vibes. Write the three numbers into the
Design Read (e.g. *"Composure 8 / Motion 6 / Density 3"*); a sensible all-round
baseline is **Composure 8 · Motion 6 · Density 4**.

## Infer the notches from the vibe

When the user gives a reference or a mood instead of numbers, map it:

| Vibe / reference | Composure | Motion | Density |
|---|---|---|---|
| Minimal, Linear-like, calm SaaS | 5–6 | 3–4 | 2–3 |
| Editorial / magazine | 7–8 | 4–6 | 3–5 |
| Agency / Awwwards / "wow" | 9–10 | 8–10 | 3–4 |
| Trust-first, public-sector, healthcare | 3–4 | 2–3 | 4–5 |
| Working app / dashboard / data | 4–6 | 3–5 | 8–10 |
| Small-business / local-service marketing | 6–8 | 4–6 | 4–6 |

## Composure (calm ↔ bold) — how far symmetry breaks

- **1–3 (calm):** symmetrical grid, equal columns, centered headers, predictable
  alignment. `grid-template-columns: repeat(12, 1fr)` with even spans.
- **4–7 (mid):** intentional asymmetry — left-aligned section headers over centered
  content, mixed aspect ratios side by side (a 4:3 next to a 16:9), a deliberate
  ~`-2rem` overlap between two blocks, one clear focal point per section.
- **8–10 (bold):** off-center heroes, uneven spans (`grid-template-columns: 2fr 1fr
  1fr`), masonry, and **big empty zones used on purpose** (`padding-left: 20vw`, a
  headline occupying one third with the rest blank). The emptiness is the move.

## Motion (still ↔ cinematic) — how much it moves

- **1–3 (still):** hover and focus transitions only. `transition: … .2s` on color,
  background, transform. Nothing on scroll.
- **4–7 (mid):** entrance reveals on scroll, staggered with small `animation-delay`
  cascades, eased `cubic-bezier(0.16, 1, 0.3, 1)`. One signature moment.
- **8–10 (cinematic):** scroll-linked / pinned / parallax choreography (ScrollTrigger
  or equivalent), orchestrated page-load sequence. If you place it here the page
  **must** actually move — and still collapse under `prefers-reduced-motion`.
  Engineering in `motion.md`.

## Density (airy ↔ packed) — information per screen

- **1–3 (airy):** huge sections, few elements. Section padding `py-32`…`py-48`
  (≈8–12rem). Luxury default.
- **4–7 (mid):** normal marketing rhythm, `py-16`…`py-24`. Cards with comfortable
  padding.
- **8–10 (packed):** tight vertical rhythm, **hairline `1px` rules instead of card
  boxes**, `font-mono` (tabular) for all numbers, dense tables. A working app/data
  view — *not* a marketing page. At Density > 7, generic card containers are banned:
  let data breathe in plain layout, separated by lines, not boxes.

## The rule that ties them together

**Hold the calibration.** A calm/airy brief must not sprout six animations and a
packed grid; a packed dashboard must not float in luxury whitespace. Drifting
density or composure mid-page is exactly what makes a site feel "off" even when
every individual section is fine.

## Mobile is not a notch — it's a hard override

Asymmetric, overlapping, multi-column layouts (anything Composure 4+) **must
collapse to a strict single column on small screens** (`< 768px`): full-width
blocks, simple vertical stack, modest padding (`px-4 py-8`-ish). Don't assume the
desktop grid "just reflows" — design the collapse deliberately, per section. The
boldest desktop composition and the calmest mobile stack are the *same* design done
right, not two different calibrations.
