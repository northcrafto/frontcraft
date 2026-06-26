# Anti-slop — killing the "this looks AI-generated" tells

The gap between *looks AI-generated* and *looks designed* is a known, finite set
of tells. Avoid them on purpose. None of these fire automatically — read the brief,
then apply what fits. When a brief explicitly asks for one of these looks, the
brief wins; just don't *default* into them.

## Start with a Design Read (one line)

Before building, say it in one sentence: **"Reading this as: <page kind> for
<audience>, in a <vibe> direction."** A page that names its own intent doesn't
retreat to a generic default. This is the cheapest quality move there is.

## The three default looks to avoid as a reach

AI design clusters into three looks that show up regardless of subject:
1. Warm cream background (~#F4F1EA) + high-contrast serif + terracotta accent.
2. Near-black + a single acid-green or vermilion accent.
3. Broadsheet hairline rules + zero border-radius + dense newspaper columns.

All three are fine *when the brief asks for them*. As an unprompted default for
every project, they're a tell. Spend a free aesthetic axis on a real choice instead.

## Typography tells

- **Don't default to a serif because it "feels premium/editorial."** That instinct
  is the single most-tested AI tell. Default to a characterful grotesque/sans
  display unless the brand is genuinely editorial / luxury / heritage / publication
  and you can say why.
- **Fraunces and Instrument Serif** are the two most over-reached AI display
  serifs. Avoid them as defaults; if a serif is justified, pick a less-worn one.
- **Emphasis inside a headline** = italic or bold of the *same* family. Never inject
  a lone serif word into a sans headline (or vice versa) for "interest."
- **Inter** is fine only when a neutral / Linear-style feel is the actual goal.

## Color tells

- **One accent, locked across the whole page.** No second accent appearing in
  section 7. No teal status badge on a rose-accented site.
- **Tinted neutrals**, never flat `#000` / `#fff` or default `#888`.
- **No AI purple→blue gradient** by default.
- **Premium-consumer briefs** (cookware, wellness, artisan, luxury, DTC home):
  avoid the auto beige + brass + oxblood + espresso palette. Rotate to something
  specific (cold luxury, forest, black-and-tan, cobalt+cream, terracotta+slate,
  monochrome + one saturated pop).

## Layout tells

- **No "centered hero + three equal text cards"** as a default. Vary spans, go
  asymmetric, pick one focal point. (Image-led card grids are fine — empty text
  boxes are the problem.)
- **Zigzag cap:** at most 2 consecutive image+text split rows. The 3rd is a tell.
- **Section-layout variety:** across ~8 sections use at least 4 different layout
  families. "Selected work" must not look like "What we do."
- **Hero fits the viewport:** headline ≤ 2 lines, subtext ≤ ~20 words, primary CTA
  visible without scrolling. Plan font size and image size together.
- **Hero stack discipline:** ≤ ~4 text elements (one small label OR brand strip,
  headline, subtext, CTAs). No trust micro-strip, tagline, or feature bullets
  crammed into the hero — those move to sections below it.

## Structural-decoration tells (the small stuff that screams AI)

- **Eyebrows: at most 1 per 3 sections.** Not a small uppercase label over every
  section header. Often the headline alone is enough.
- **No section-number eyebrows** (`00 / INDEX`, `001 · Capabilities`, `06 · how it
  works`).
- **No decorative status dots** before nav items, list rows, or badges (only for
  real semantic state).
- **No scroll cues** (`Scroll`, `↓ scroll`, "Scroll to explore").
- **No locale / time / weather strips** ("Lisbon 14:23 · 18°C") unless the brand is
  genuinely place- or timezone-specific.
- **No version labels in the hero** (`V0.6`, `BETA`, `EARLY ACCESS`) unless it's a
  launch.
- **No pills/labels overlaid on photos; no decorative photo-credit captions.**
- **Numbering (01 / 02 / 03)** only when the content is a real sequence (a process,
  a route, a timeline) — not as decoration.

## The em-dash ban (in shipped UI copy)

In anything the user reads on the page — headlines, labels, body, quotes,
captions, buttons, alt text — do not use the em-dash (`—`) or en-dash (`–`) as a
separator. It's a strong AI tell. Use a normal hyphen, a comma, a period, a colon,
or restructure the sentence. (This is about shipped copy, not internal docs.)

## Content & copy tells

- **Real copy, never lorem ipsum.** Write plausible content for the actual subject.
- **No generic names** ("Jane Doe", "John Doe") or **startup-slop brands** ("Acme",
  "Nexus", "SmartFlow"). Use believable, specific, locale-appropriate names.
- **No filler verbs** ("Elevate", "Seamless", "Unleash", "Next-Gen",
  "Revolutionize"). Concrete verbs only.
- **No fake-precise numbers** (`99.99%`, `4.1×`) unless they're real or labelled as
  sample data.
- **Re-read every visible string before shipping.** Cut cute-but-broken AI phrasing
  and forced wordplay; plain and correct beats clever and wrong.

## Real images, not fakes

- **No div-based fake screenshots / dashboards / terminals** built from styled
  boxes. Use a real screenshot, a generated image, or a real component preview.
- **The hero needs a real visual**, not a gradient blob.
- Sourcing + verification: see `SKILL.md` → Images (project assets → Pexels →
  keyless Unsplash, every image verified).

## Interactive states & accessibility

- Design **hover / focus-visible / active / disabled / loading / empty / error**,
  not just the happy path.
- **Button text passes WCAG AA** against its background; **CTA labels don't wrap**
  at desktop; **no two CTAs with the same intent** on one page.

## Mechanical pre-flight (just count)

- Em-dashes in shipped copy: **0**
- Eyebrows / small uppercase section labels: **≤ ceil(sections / 3)**
- Distinct layout families (6+ section page): **≥ 4**
- Accent colors: **1**
- Dead `#` links or placeholder buttons: **0**
- Lorem ipsum / Jane Doe / Acme: **0**

If a count is off, fix it before the review panel runs. This pairs with the core
`SKILL.md` pre-flight, not replaces it.
