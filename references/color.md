# Color — building a palette with taste, not reaching for a default

Read this when you're choosing color for a build. Color is where most "looks
AI-generated" judgments are won or lost, and it's the cheapest place to look
expensive or cheap. The core SKILL.md gives you the rules; this file gives you the
*method* (how to actually construct a palette) plus ready-made families and the
specific defaults to avoid.

The one idea: **a palette is a small system of roles, committed once.** Not "some
nice colors" — a tinted neutral ramp plus exactly one accent, each assigned a job,
locked across the whole page.

---

## The constructive method (do this every time)

**1. Pick the neutral temperature first.** Decide warm (toward stone/sand/bone) or
cool (toward slate/zinc). This single choice carries most of the mood. Then build a
5–6 step ramp that is *tinted*, never flat `#888` and never pure `#000`/`#fff`:

```
bg        the page background (the largest area)
surface   raised panels/cards, a step off bg
fg        primary text/headlines (high contrast on bg)
muted     secondary text, captions (still AA: ≥ 4.5:1 on bg)
line      hairline borders/dividers (a low-opacity fg)
```

Every neutral in the ramp shares the same hue bias. A warm page never drops a cool
grey divider into section 7, and vice versa.

**2. Choose ONE accent, with intent.** The accent is for the single thing you want
clicked or noticed — not for decoration. Guidance:
- **Saturation < ~80%** by default. Fully-saturated hues read as "system default,"
  not "chosen." A slightly muted accent almost always looks more expensive.
- It must clear **WCAG AA against its own on-color** (`--on-accent`). A gold button
  with white text usually fails; use dark text on gold, or darken the gold.
- One accent. If you genuinely need a second color, it's a *semantic state*
  (success/error), not a second brand accent.

**3. Assign roles as tokens.** Whatever the stack, name the jobs. This *is* the
design system:

```css
:root {
  --bg:        ...;
  --surface:   ...;
  --fg:        ...;
  --muted:     ...;
  --line:      ...;
  --accent:    ...;
  --on-accent: ...;   /* text/icon color that sits ON the accent */
}
```

**4. Lock it and finish it.**
- **One accent across the whole page.** Audit every section before shipping.
- **Tint shadows to the background hue** — no pure-black drop shadow on a warm
  page. `box-shadow` uses an rgba of the darkest neutral, not `#000`.
- **Dark mode is re-tinted, not inverted.** Don't flip `#fff`→`#000`. Pick dark
  surfaces that keep the hue bias (`#131e29`, not `#000`), and *raise* the accent's
  luminance a little so it still pops and still passes AA on dark.

---

## Ready palette families (rotate; never ship the same one twice running)

Each is a committed system: tinted neutrals + one accent, with an on-accent color
that passes AA. Copy a block, then tune to the brand. They are starting points with
taste built in, not the only options.

```css
/* Cold Luxury — cool greys + steel-blue pop. Tech, finance, premium hardware. */
--bg:#ECEEF1; --surface:#F8F9FB; --fg:#14171C; --muted:#565D66;
--line:rgba(20,23,28,.12); --accent:#2E5AAC; --on-accent:#FFFFFF;

/* Forest (dark) — deep green + bone + amber. Outdoors, craft, heritage. */
--bg:#0F1B14; --surface:#17271D; --fg:#EDEBE0; --muted:#9FB0A4;
--line:rgba(237,235,224,.14); --accent:#D69A2D; --on-accent:#14211A;

/* Black & Tan — true off-black + warm tan, sharp contrast, zero beige. */
--bg:#0B0B0C; --surface:#161615; --fg:#F2EEE7; --muted:#A7A199;
--line:rgba(242,238,231,.13); --accent:#C8965A; --on-accent:#16120E;

/* Cobalt + Cream — one saturated blue against a single warm neutral. */
--bg:#F4F1E9; --surface:#FBF9F3; --fg:#14213A; --muted:#5C6378;
--line:rgba(20,33,58,.12); --accent:#1D3FCF; --on-accent:#FFFFFF;

/* Terracotta + Slate — warm rust against cool grey, no brass. */
--bg:#ECEDEF; --surface:#F7F8F9; --fg:#1B2127; --muted:#5A626B;
--line:rgba(27,33,39,.12); --accent:#B14A30; --on-accent:#FFFFFF;

/* Olive + Brick + Paper — muted olive neutral + brick-red accent. */
--bg:#F1EFE6; --surface:#F8F6EF; --fg:#23261C; --muted:#5E6150;
--line:rgba(35,38,28,.12); --accent:#9E3B2E; --on-accent:#FFFFFF;

/* Monochrome + one pop — off-white/off-black + a single bright.
   Pick ONE pop: electric #1466FF, emerald #0F9D6A, rose #E5484D, hot #E8590C. */
--bg:#F6F6F4; --surface:#FFFFFF; --fg:#121212; --muted:#5A5A58;
--line:rgba(18,18,18,.12); --accent:#1466FF; --on-accent:#FFFFFF;
```

**Rotation rule:** if the last build used a family (or the beige+brass look below),
this one uses a different family. Don't ship the same palette twice in a row.

---

## The defaults to avoid as an unprompted reach

These are fine *when the brief asks for them*. As the automatic reach for every
project they're the tell. (See also `anti-slop.md` → the three default looks.)

- **Beige + brass + espresso** (the premium-consumer / "warm craft" auto-palette).
  Concretely, avoid defaulting to:
  - Backgrounds `#f5f1ea` `#f7f5f1` `#fbf8f1` `#efeae0` `#faf7f1` (cream/chalk/bone)
  - Accents `#b08947` `#b6553a` `#9a2436` `#bc7c3a` `#9c6e2a` (brass/clay/oxblood/ochre)
  - Text `#1a1714` `#1b1814` (espresso near-black)
  Reach for one of the families above instead, unless the brand genuinely *is*
  vintage/artisan and you can say why this exact palette fits.
- **AI purple → blue gradient** (`#7c3aed`→`#2563eb` and relatives) as a hero
  background or button glow. Banned as default.
- **Near-black + one acid-green/vermilion** as an unthinking "dark tech" reach.
  Fine if executed with intent; a tell if it's just the default dark look.

---

## Quick checks before you ship color

- One accent, used on the whole page? (No surprise second hue in a late section.)
- Neutrals tinted, no flat `#000`/`#fff`/`#888`?
- Body and muted text both clear AA (4.5:1) on their background?
- Accent text (`--on-accent`) clears AA on the accent?
- Shadows tinted to the background hue, not pure black?
- If dark mode: surfaces re-tinted (not inverted), accent luminance nudged up?
- Is this a different palette family from the last build?

---

## Worked example — a coastal-town site, "cinematic"

Brief reads as a premium, cinematic place-brand. The lazy reach is beige + brass
(warm-craft default) — skip it. Two good paths:

- **Rotate to a family:** Cold Luxury or Forest both fit "cinematic + place."
- **Justify a warm system deliberately:** if the place's light genuinely calls for
  warmth, build it as a *committed* system rather than the default — e.g. deep
  marine ink as the dark surface, a warm off-white, and **one** muted gold accent
  with dark text on it (so the CTA passes AA). State the choice in the Design Read
  ("warm, because the coastal light is warm — not because it's a default"), lock the
  gold across the page, and tint shadows to the marine hue.

Either way the move is the same: name the intent, build the ramp, pick one accent,
lock it, finish the details. That discipline is what reads as designed.
