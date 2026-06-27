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

**Run this check against the _finished_ build, not just the brief — name which of
the three your result is closest to.** The most-missed one is #2: a dark
navy/charcoal/near-black background with a single bright accent **reads as default
"dark-SaaS" slop**, and *cyan, teal, and electric blue count as the "acid" accent*
every bit as much as acid-green or vermilion. A dark theme with one glowing accent
is not automatically "premium/cinematic" — by default it's the tell. And escaping
a default look is **not** a slightly different dark shade or a new accent hue; it's
committing to an art-directed *identity*: a palette and type with real character,
and **photography carrying the page**. When a dark build reads generic, the
fastest, most reliable exit is usually the opposite move — a light, image-led
editorial layout (white/paper, a characterful display face, one warm accent, big
verified photos) where the pictures do the work. If you can't name a real reason
the build is dark-with-a-bright-accent, treat it as look #2 and redesign.

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
  a route, a timeline) — not as decoration. **Never on a filterable/sortable grid:**
  the moment a filter hides items the visible numbers go non-contiguous (`06`, `07`
  floating with gaps), which reads as a bug, not a flourish.

## More tells the review panel keeps catching

These show up once the obvious ones are gone. They're the second layer — the moves
the model reaches for when it's *trying to look designed*. Let the review-agent loop
surface them on each build and fold new ones in here over time. None fire
automatically; kill them only when they're an unprompted reach.

- **Middle-dot (`·`) overuse.** Ration it to ~1 per metadata line. It is not the
  universal separator for everything (`foo · bar · baz · qux`). Prefer line breaks,
  hairlines, or columns when you need to separate more than two things.
- **Decoration strip across the hero bottom** (`BRAND. MOTION. SPATIAL.`,
  `TYPE / FORM / MOTION`, `ESTD. 2018 · LISBON`). An agency-portfolio cliché. Allowed
  only when the strip is real navigation or real status, not atmosphere.
- **Floating corner paragraph in a section header.** Giant left headline with a tiny
  explainer paragraph floating top-right, aligned to nothing. Either stack headline
  over body (max ~65ch), or build a real two-column header where the right column
  carries a visual — not a stray paragraph.
- **Poetic-craftsman labels.** `From the field`, `Field notes`, `On our desks`,
  `Loose plates`, "Quietly trusted by". Use plain functional labels (`Testimonials`,
  `Latest writing`, `Trusted by`) or drop the label.
- **Micro-meta sentences under a heading.** A little sentence explaining the section
  to itself ("This is a feature we ship today, not a roadmap promise") is clutter.
  Eyebrow (if any) + headline + body is enough.
- **Generic step labels.** `Stage 1 / Stage 2`, `Phase 01 / 02 / 03`, `Step 1 / 2 / 3`.
  The step's actual content is the label — use the verb (`Install`, `Configure`,
  `Ship`), not "Step 1: Install".
- **`<br>`-broken, italicized headlines** as a default "design move". Headlines
  should read naturally first; get clever only when the brief asks for it.
- **Vertical rotated text** and **crosshair / hairline grid lines drawn just to
  "feel designed".** Use them only when they organize real content.
- **Filled-track scoring/progress bars** as comparison visuals on a marketing page,
  and **live-stock counters** (`Reservation 412 of 800`) or **version footers**
  (`v1.4.2`, `Build 0048`, `last sync 4s ago`) on marketing/portfolio pages. These
  are devtool/dashboard fixtures, not landing-page content.
- **Custom mouse cursors** are high-risk (accessibility, performance, touch). Treat
  as a deliberate, justified choice for an experimental brief — never a default
  flourish.
- **Headlines that only scream.** Don't reach straight for the biggest size; control
  hierarchy with weight, color, and space too. And no gradient-filled display text as
  a default.

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

- Closest of the 3 default looks to the finished build: **name it.** If it *is*
  one (especially dark + a single bright/cyan/teal/acid accent) and the brief
  didn't ask for it: **redesign**, don't ship.
- Em-dashes in shipped copy: **0**
- Eyebrows / small uppercase section labels: **≤ ceil(sections / 3)**
- Distinct layout families (6+ section page): **≥ 4**
- Accent colors: **1**
- Middle-dot (`·`) separators per metadata line: **≤ 1**
- Marquees / kinetic scroll strips: **≤ 1**
- Custom cursors, vertical rotated text, hero decoration strips (unbriefed): **0**
- Dead `#` links or placeholder buttons: **0**
- Lorem ipsum / Jane Doe / Acme: **0**

If a count is off, fix it before the review panel runs. This pairs with the core
`SKILL.md` pre-flight, not replaces it.
