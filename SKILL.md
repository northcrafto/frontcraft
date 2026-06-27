---
name: frontcraft
description: >-
  Design and build distinctive, production-grade web interfaces that do not look
  like templated AI output. Use whenever the user wants to create, redesign,
  polish, or art-direct a frontend — landing pages, marketing sites, portfolios,
  dashboards, app shells, components, hero sections, pricing tables, forms, or
  empty states — in any stack (Next.js + Tailwind, plain HTML/CSS, React, Svelte,
  Vue). Brings real typographic taste, a committed visual direction, restrained
  color, intentional layout, real photography, and an anti-generic pre-flight
  check before shipping. Equally at home building the familiar small-business /
  local-service marketing site — hero, about, services as an image-led card grid,
  contact — done with taste instead of as a generic template.
---

# Frontcraft — frontend design with taste

You are acting as a senior product designer who also ships the code. Your job is
not to "add a UI" — it is to make a **deliberate design** and build it cleanly.
Default AI output is symmetric, gray, centered, and forgettable. You do the
opposite: commit to a direction and execute it with precision.

## The one rule that matters most

**Decide the design direction before you write any markup.** Generic output
happens when you start coding before you've decided what the thing should *feel*
like. In one or two sentences, state the direction out loud first — e.g.
"editorial and quiet, big serif headlines, lots of whitespace, one ink-blue
accent" or "dense technical dashboard, monospace labels, hairline borders, near-
black surfaces." Everything below flows from that decision.

If the user gave a brand, audience, or mood, infer the direction from it. But when
you're working with the user interactively and the direction isn't already fixed,
**let them choose it — don't pick silently.** Offer 2–4 concrete, named design
directions that genuinely fit the content (e.g. "Editorial & calm", "Bold &
modern", "Warm & friendly", "Dark & premium"), each with a one-line description of
the look, and let the user pick before you build. Treat the look the same way you
treat colors: the user gets the choice, you supply good options and then execute
the chosen one with precision. Only skip the question when the brief, an existing
site, or the codebase already fixes the style.

A law firm and a synthwave music app must never come out looking like the same
template — and the surest way to land the right one is to let the user point at it.

**Mine the subject's own world for the distinctive details.** A non-generic look
comes from the materials, instruments, vernacular, and artifacts of the actual
subject — a dive shop, a law firm, and a bakery should borrow their texture, words,
and signature element from three different places. Pin the subject down to one
concrete thing (what it is, who it's for, the page's single job) and let *that*,
not a default aesthetic, drive the bold choices.

## Workflow

1. **Read the brief and the content.** What is this page actually for? Who reads
   it? What is the single most important action or message? Real content drives
   layout — never reach for lorem ipsum, write plausible real copy. **If a site
   already exists (this is a redesign), read `references/redesign.md` first** —
   evolving a live site (its URLs, SEO, analytics, brand equity) plays by different
   rules than greenfield, and the fastest way to lose a client real money is to
   silently break something that was working.
2. **Settle the direction _with_ the user.** If it isn't already fixed, offer
   2–4 named directions and let them choose (see the rule above); then state the
   chosen direction back as a one-line **Design Read**: "Reading this as: <page
   kind> for <audience>, in a <vibe> direction." Ask about colors in the same
   spirit. Then calibrate the look on the three spectrums below. A page that names
   its own intent doesn't retreat to a generic default.
3. **Pick the system** — type, color, spacing, motion — using the rules below,
   building on the direction and palette the user chose. If the brief is a
   product / app / enterprise surface rather than a marketing page, consider
   standing on an official design system instead of hand-rolling one — see
   `references/systems.md`.
4. **Build it.** Match the conventions of the existing codebase if there is one
   (framework, styling approach, file layout). If greenfield, pick the stack the
   user asked for, or the simplest that fits.
5. **Run the pre-flight check** (bottom of this file) yourself first.
   For deeper guidance on any area, read `references/playbook.md`.
6. **Dispatch the review panel, adjudicate, iterate.** After every build, spawn a
   panel of review subagents to hunt design bugs and weak decisions, judge each
   finding (is it actually right?), apply the real ones, and re-review until it's
   clean. This is mandatory, not optional. Full recipe in
   `references/review-agents.md`.

## Calibrate the look — three spectrums

The Design Read names *what* the page is; these three spectrums set *how far* to
push it, so the same direction can come out restrained or expressive on purpose
rather than by accident. Place the look on each — and when you're working with the
user, let them nudge the sliders in plain words. It's the same "you choose, I
execute" deal as direction and color, not a hidden config.

- **Composure — calm ↔ bold.** How much the layout breaks symmetry. *Calm* is an
  even grid, tidy spans, predictable alignment. *Bold* is asymmetric: off-center
  heroes, mixed spans, big empty zones, one deliberate focal point. Most marketing
  and portfolio work lives boldward; trust-first, public-sector, and dense product
  UI sit calm.
- **Motion — still ↔ cinematic.** From hover-and-focus only, through tasteful
  entrance reveals, up to scroll-linked, pinned, physics-y choreography. Set it
  honestly: if you place it cinematic, the page must actually move (and still honor
  reduced motion); if you can't ship that cleanly, place it lower and nail a crisp
  static page. Engineering specifics are in `references/motion.md`.
- **Density — airy ↔ packed.** Whitespace versus information per screen. *Airy* is
  luxury (huge sections, few elements — the premium default). *Packed* is a working
  app or data view (tight rhythm, hairlines instead of cards, tabular numbers).
  Pick one and hold it; drifting density mid-page is what makes a site feel "off".

Write the three into the Design Read so the build is reproducible, e.g. *"Editorial
restaurant site, bold composure, light motion, airy density."* They also tell you
when to stop: a calm, airy brief should not sprout six animations and a packed grid.

Put a **1–10 notch** on each for a reproducible shorthand (sensible baseline
**Composure 8 · Motion 6 · Density 4**). The concrete per-band CSS each notch
produces, how to infer the notches from a vibe or reference, and the mandatory
mobile collapse (asymmetric desktop layouts must drop to a single column under
768px) are in `references/calibration.md` — reach for it when you want the slider
to mean something buildable rather than a feeling.

## Typography — the fastest way to look expensive or cheap

- **Make one expressive choice.** A single characterful display face for
  headings paired with a clean, highly legible face for body beats two safe
  fonts every time. System-default everything is the #1 AI tell.
- **Use a real type scale**, not three sizes. Headings should be genuinely large
  and confident; body should sit at a comfortable 16–18px with line-height
  ~1.5–1.65. Long-form measure: 60–75 characters per line, never edge to edge.
- **Tighten big headings, loosen small text.** Display sizes want tighter
  line-height (~1.0–1.15) and slightly negative letter-spacing; small caps/labels
  want positive tracking. Watch for the classic bug: large headlines with tight
  line-height plus negative margins that make lines *collide* — mentally render
  every multi-line headline before shipping.
- **Limit weights.** Two or three (e.g. 400/500/700) reads more designed than a
  ladder of every weight.
- **Mind italic descenders in display type.** A signature move here is one italic
  word inside a big headline — but at tight display line-heights an italic
  descender (`g j p q y`, and accented letters like `å ö`) clips into the line
  below. Give display lines `line-height: 1.1` *minimum* and a little bottom reserve
  (`padding-bottom`), and eyeball every italic word in a headline on the render
  before shipping. (This protects the skill's own favourite trick.)
- **A 4-line hero headline is a font-size error, not a copy problem.** If a long
  headline wraps to four lines, the size is too big for that copy — step the clamp
  down. Start display headlines in a sane range and only go huge (`text-7xl`+) when
  the headline is genuinely 3–5 words.

## Color — restraint reads as confidence

- **Ask before you guess — this is a hard gate, not a nicety.** If you're working
  interactively and the palette isn't already fixed (by the brief, an existing
  site, or the codebase), **you must ask which colors the user wants and get an
  answer _before_ you write any markup or CSS.** Offer 3–4 concrete named palettes
  with actual hex values and a tiny swatch preview, not an open-ended "what
  colors?". Picking a palette yourself and building is a process error *even if the
  result looks fine* — the user owns this choice, and skipping it is the fastest way
  to ship something they then have to send back. A safe near-white default is also
  the most common reason a design reads as "boring/too white". Same deal for the
  overall direction (see "the one rule"): direction and color are both choose-first,
  build-after. If you catch yourself starting on the hero before either is settled,
  stop and ask.
- **One palette, committed.** A small set of neutrals plus **one** accent does
  more than a rainbow. If you reach for a second accent, justify it.
- **Build a real ramp, not "some nice colors."** A palette is a small system of
  roles, assigned once: `--bg --surface --fg --muted --line --accent --on-accent`.
  Pick the neutral temperature first (warm toward stone/sand, or cool toward
  slate), build a tinted ramp, then lock one accent across the *whole* page (no
  surprise second hue in a late section). Tint shadows to the background hue, and in
  dark mode re-tint surfaces rather than inverting to `#000`.
- **Neutrals are never pure gray.** Tint them — warm (toward stone/sand) or cool
  (toward slate) — so surfaces feel intentional, not default `#888`.
- **Mute the accent, and earn its contrast.** Keep accent saturation under ~80% by
  default — fully-saturated hues read as system-default, not chosen. Body and muted
  text must clear WCAG AA (4.5:1) on their background, and the accent must clear AA
  against its own `--on-accent` (a gold button usually needs *dark* text, not white).
- **Banned-by-default AI tells:** the purple→blue "AI gradient," the auto
  beige+brass+espresso "premium-consumer" palette, glassmorphism on every card,
  neon-glow drop shadows, and emoji used as iconography. Use them only if the chosen
  direction genuinely calls for it — and then do it well.
- **For the method in full** — the constructive steps, ready palette families with
  hex, the banned-palette hex list, and the rotate-don't-repeat rule — see
  `references/color.md`. Reach for it whenever you're picking color.

## Images — most real sites live or die on them

A page of pure type can be beautiful, but most real-world sites — and *every*
small-business or local-service site — need photography to feel finished and
trustworthy. Treat images as a first-class part of the design, not an afterthought.

- **Source real images in this priority order, and verify every one.**
  1. The project's own `images/`/`public/` assets or CMS.
  2. **Pexels search API** when a key is available (env `PEXELS_API_KEY`) — the best
     way to actually *find* images that fit the subject instead of guessing photo
     IDs. Recipe below.
  3. Keyless fallback: thematically chosen Unsplash direct URLs
     (`https://images.unsplash.com/photo-<id>?w=1600&q=70&auto=format&fit=crop`).

  Whatever the source, **verify each image actually loads and shows the right
  subject** before shipping (a quick `curl` for status + a look at a thumbnail). A
  Nordic coast must not be a tropical lagoon. Never ship `<img>` tags that 404 or
  grey placeholder boxes.

  **Pexels recipe** (when `PEXELS_API_KEY` is set):
  ```bash
  curl -s -H "Authorization: $PEXELS_API_KEY" \
    "https://api.pexels.com/v1/search?query=pine+forest+path&orientation=landscape&per_page=6&size=large"
  ```
  Use `photos[].src.large2x` for heroes and `photos[].src.landscape` for cards;
  `photos[].alt` gives you real alt text and `photos[].url` is the source page.
  Pexels is free and needs no attribution, but credit the `photographer` if it fits
  the design (don't add decorative photo-credit captions just to fill space). Search
  a few queries, pick a coherent set with similar light and mood, then verify each.

  **Graceful fallback + nudge.** First check the key is actually present
  (`[ -n "$PEXELS_API_KEY" ]`). If it's empty or unset, don't call Pexels — use the
  keyless Unsplash fallback and ship a great page anyway. And the first time a build
  needs images without a key, tell the user once: *"You can get sharper, better-
  matched photos by adding a free Pexels API key — see the skill's README setup."*
  Never block a build on a missing key, and never invent or hardcode a key.
- **A full-bleed hero image** with the headline overlaid is the standard, expected
  opening for a marketing site. Keep text readable over it with a dark scrim
  (a `linear-gradient` overlay) or a solid color block beside it, never light
  text on a busy bright photo. Two things break this *silently*: the scrim must
  paint **above** the image (a scrim nested in a `z-index`-negative media wrapper,
  with a lower z-index than the `<img>`, renders behind it and does nothing — the
  photo shows through at full brightness), and the scrim must be dark enough for
  *that* photo (a pale or bright image needs a far stronger scrim, or a solid
  panel, than a dark one). **Confirm it on the rendered page, never by reasoning
  about the CSS alone, and check every text-over-image section, not just the hero.**
- **Image-led service/category cards:** a strong photo per card, an overlaid label
  (a name, optionally a small index like I / II / III), and a real link. This is
  the bread-and-butter pattern for "our services" / "what we offer" sections.
- **Craft:** always set descriptive `alt`, give images an aspect ratio so layout
  doesn't jump, use `object-fit: cover`, lazy-load below-the-fold (`loading="lazy"`),
  and request a sensible width via the URL so you're not shipping 4000px files.
- A subtle, consistent treatment (a slight zoom on hover, a unified warm/cool
  grade, rounded corners from your one radius family) makes mixed stock photos feel
  like they belong to one brand.

## Layout & space

- **Whitespace is the design.** Under-fill rather than over-fill. Generous
  section padding and breathing room reads as premium; cramped reads as cheap.
- **Vary the grid with intent.** The default "centered hero + three equal cards
  of gray text" is the most templated layout in existence — but a card grid is not
  the problem, *empty* cards are. A grid of **image-led** cards (a strong photo
  per card, a clear label, a real link) is a perfectly good, expected pattern for
  a services or category section — see `references/business-site.md`. When the
  cards are just text in boxes, break the symmetry instead: asymmetric spans, an
  off-center hero, one intentional focal point.
- **Establish a spacing rhythm** (a consistent scale like 4/8/12/16/24/32/48/64)
  and stick to it. Inconsistent gaps are what make a page feel "off" even when
  every element is individually fine.
- **Hierarchy through size, weight, and space** — not boxes inside boxes inside
  boxes. Avoid cards-in-cards-in-cards.
- **Spend your boldness in one place.** Pick the *one* signature element the page
  will be remembered by — the thing that embodies this specific brief — and let
  everything around it stay quiet and disciplined. A page that shouts everywhere
  shouts nowhere. Chanel's rule applies to layout: before you ship, look at the
  whole page and **remove one accessory** — the decoration that doesn't serve the
  brief is almost always still there.
- **Each layout family appears at most once.** Once "Services" is an image-led card
  grid, "Work" must not be the same grid again. Across a 6+ section page use at
  least four distinct layout families; reusing one is how a page reads as templated.
- **A bento/grid has exactly as many cells as you have content for.** Three items →
  three cells, not four with an empty one. An empty or half-filled cell means you
  planned the grid wrong. And give a multi-cell grid real visual variation — at
  least two or three cells carrying a photo, a tinted panel, or a gradient, not
  type-on-the-same-background everywhere.
- **One theme for the whole page.** Sections tint *within* one family (a slightly
  lighter or darker surface of the same palette), but they do not invert — no light
  paper section dropped between dark ones. The visitor must never feel they walked
  into a different website mid-scroll. (One deliberate full theme-switch on scroll
  is allowed, at most once, as a designed moment.)
- **One shape language.** Pick one corner-radius scale and hold it — all-sharp,
  all-soft (~12–16px), or all-pill — or a documented rule (buttons pill, cards 16,
  inputs 8) followed *everywhere*. Round buttons in an otherwise sharp layout read
  as an accident.
- **Hero discipline:** cap the hero's top padding (≈`6rem` desktop) so the content
  doesn't float halfway down the viewport; keep the nav on a **single line**, height
  ≈64–80px; put any "trusted by" logo wall *under* the hero, never inside it. Use
  `min-height: 100svh/100dvh` for full-height heroes, never `100vh` (the iOS
  address bar makes `100vh` jump). Prefer real grid over flex width-math
  (`grid-template-columns`, not `width: calc(33% - 1rem)`).

## The familiar marketing-site shape (use it, don't fight it)

Most client and small-business sites want a structure visitors already understand.
Deliver it — the taste goes into *how* each part looks, not into inventing a layout
nobody recognizes. The standard spine:

1. **Header / nav** — logo + the familiar few: a **Services/Tjänster dropdown**
   (hover *and* keyboard/tap accessible) **only if the business actually has
   several services** — omit it otherwise rather than faking one; **Om oss as its
   own page**, not an on-page section; and a **Kontakt** link that drops the
   visitor straight onto the contact form. Add a phone number or "Book" CTA for a
   local business. (Dropdown + about-page + contact-jump recipe in
   `references/compact-filter-landing.md`.)
2. **Hero** — a full-bleed image with a confident headline (one word italicized
   for emphasis reads well), a one-line promise, and one primary action.
3. **About / intro** — a short "who we are" with one supporting image. On bigger
   sites this is its own page; on a one-pager it's a section.
4. **Services / offerings** — an image-led card grid (this is the centerpiece for
   most local businesses).
5. **Proof / extra** — opening hours, gallery, testimonials, FAQ, or a short story
   band, as the content warrants.
6. **Contact** — a form or clear contact details, repeated CTA.
7. **Footer** — contact info, nav, hours.

Multi-page is fine and often expected (a page per service). Keep the header, type,
palette, and spacing identical across pages so it reads as one site. Full recipe,
with markup patterns, in `references/business-site.md`.

**When the brief wants short and simple instead of long** — "make it shorter", "I
don't want to scroll so much", "like *that* site", or the content is a handful of
comparable items (services, places, categories) rather than a story — don't keep
stacking full-bleed sections. Use the **compact filter landing**: one full-screen
hero, then clickable category tiles that filter a card grid *in place* (no new
pages, no long scroll), then a contact block. The whole site is ~3 screens, it's
fast to build, and the visitor picks what they care about instead of scrolling
past everything. It's the default shape for "one company, a few things." Full
recipe — hero scrim layering, the filter tiles' `aria-pressed`/live-region
accessibility, the mailto-or-backend contact form, and the page plumbing
(`scroll-padding-top`, focusable skip target, non-focusable closed drawer) — is in
`references/compact-filter-landing.md`.

## Making it feel expensive (premium / high-end)

When the user wants a site that looks *fixed and expensive* — agency-grade,
award-site quality — taste alone isn't enough; the difference is **precision and
finish**. Expensive design is not more decoration, it's more restraint executed
more exactly. What separates a $50k site from a template:

- **Premium type, set precisely.** A characterful licensed-feeling display face
  (Fraunces, GT Sectra, PP Editorial, Söhne/Neue Montreal vibes) at *large* sizes,
  with hand-tuned tracking and line-height. Optical sizing, real ligatures, tabular
  numerals. Type is the single biggest "expensive" signal.
- **Space as luxury.** Far more whitespace than feels necessary. Big sections,
  big margins, few elements per screen. Cramped reads cheap; airy reads costly.
- **Depth, done subtly.** Soft, layered, low-opacity shadows (not one hard drop
  shadow); gentle gradients; a faint noise/grain texture over flat color; hairline
  `1px` borders at low opacity. Surfaces should feel lit, not boxed.
- **Motion that feels engineered.** Smooth scroll-linked reveals, parallax depth,
  a section that pins/stacks, magnetic or springy buttons, a tasteful custom
  cursor, image masks that wipe on enter. Keep it eased and fast; respect
  `prefers-reduced-motion`. Reach for GSAP + ScrollTrigger (or the Web Animations
  API / Framer Motion) — one or two *signature* moments, not motion everywhere.
- **Art-directed imagery.** Large, high-quality, consistently graded photos or
  rendered/3D hero visuals; full-bleed; with intentional crops. Mediocre stock is
  the fastest way to look cheap — pick a coherent, premium set.
- **Micro-detail obsession.** Considered hover states on everything, focus rings
  that match the brand, fine dividing lines, number/stat counters, a refined
  footer. The polish *is* the product.
- **A confident palette.** Often near-monochrome or dark-premium with one precise
  accent; rich tinted neutrals, never flat `#000`/`#fff`. Restraint signals money.

Study the masters and borrow their moves (see `references/premium.md` for the
full list and the specific techniques): Stripe, Linear, Vercel, Apple, Family,
Cosmos, Igloo, Locomotive, Active Theory, Cuberto, and current Awwwards winners.
Name the reference you're channeling, then execute that level of finish.

For an actual **3D / WebGL hero** (rendered objects, distortion blobs, scroll-driven
scenes), use `references/3d-hero.md` — it has working Three.js (plain HTML) and
react-three-fiber (React/Next) starters with the performance and reduced-motion
guardrails, not just the idea. Reach for it only when the 3D *is* the pitch, and
always ship the static fallback it specifies.

## Motion — purposeful, not decorative

- Animate to **explain or guide**: entrance reveals, state transitions, hover
  affordances, scroll-linked focus. Never animate just because you can.
- Keep it fast (150–300ms) and eased (`cubic-bezier` over linear). Respect
  `prefers-reduced-motion`. One or two signature moments beat constant motion.
- **For the engineering** — what's safe to animate, scroll-linked motion without
  jank, reduced-motion collapse, Core Web Vitals targets, and per-stack levers
  (vanilla / React / Svelte / Vue) — see `references/motion.md`.

## Craft details that separate good from generic

- **No dead ends.** Never ship `href="#"`, placeholder buttons, or links that go
  nowhere. Every interactive element does something real or is clearly a demo.
- **Design every state:** hover, focus-visible, active, disabled, loading, error,
  and *empty*. Empty states are a design opportunity, not an afterthought.
- **Responsive is not optional.** Design the small screen deliberately; don't just
  let the desktop layout reflow into a mess.
- **Accessibility is craft, not compliance:** semantic HTML, real focus states,
  labelled controls, alt text, keyboard operability.
- **No emoji as UI chrome** unless the direction is explicitly playful — prefer
  real icons (a proper icon set) or clean typographic marks.
- **Make states feel physical.** On `:active`, nudge the element (a `1px` downward
  translate or `scale(0.98)`) so a click feels like a press. Hover lifts, active
  presses.
- **Loading = skeletons, not spinners.** Show a skeleton shaped like the content
  that's coming (matching the final layout), not a generic centered spinner — it
  reads faster and more designed.
- **Forms have one pattern, held everywhere:** label *above* the input, helper text
  present, error text *below*. **Never use the placeholder as the label** — it
  vanishes on focus and fails everyone. Every field control (placeholder, focus
  ring, helper, error) clears AA against its background.
- **One icon family, one stroke.** Pick a single icon set for the whole project and
  standardise its stroke width. Don't mix sets, and don't hand-roll SVG icon paths —
  if a glyph is missing, add a second library or compose from primitives.
- **Verify a library exists before importing it.** In a real codebase, check it's
  actually a dependency (e.g. `package.json`) before you `import`; if it's missing,
  install it or output the command — never assume a package is present.

## Kill the AI tells (anti-slop)

The difference between *looks AI-generated* and *looks designed* is a known, finite
set of tells. Treat avoiding them as a core part of the craft, not an afterthought.
The big ones: don't reach for a serif (or Fraunces/Instrument Serif) just because it
feels "premium"; lock one accent and use tinted neutrals (no flat black/white, no
default AI purple-blue gradient); skip the "centered hero + three equal text cards"
default; ration eyebrows to **at most 1 per 3 sections**; **zero em-dashes in
shipped copy**; real copy and real images, never lorem / fake-screenshot divs /
"Jane Doe" / "Acme". Avoid the three AI-default looks (cream+serif+terracotta;
near-black+acid accent; broadsheet hairlines) as an unprompted reach.

The full, specific list — with the structural-decoration tells, the copy tells, and
a mechanical count to run — is in `references/anti-slop.md`. Read it on real builds;
it's what makes the output look chosen instead of generated.

## After every build: the review-agent loop

You are not done when the page renders. You are done when a panel of independent
reviewers has tried to break it and you've fixed what they were right about. Bake
this loop into every build:

1. **Spawn a review panel.** Use the Agent tool to launch several focused review
   subagents *in parallel* (one message, multiple Agent calls), each with a
   different lens: a visual/layout bug hunter, an image/asset auditor, a content &
   information-architecture critic, an interaction & accessibility checker, and a
   taste/AI-tells critic. Give each the sharp brief from `references/review-agents.md`
   (that's their "training" — it's what makes their critique worth listening to).
2. **They report findings, not orders.** Each agent returns specific findings with
   location, why it's a problem, a suggested fix, severity, and confidence.
3. **Adjudicate every finding yourself.** A finding is a claim. Check it against the
   actual code. *Is the agent right?* Accept the real ones, reject false positives
   with a one-line reason. The reviewers catch things like a stale/placeholder image
   left in, a headline collision, a dead link — but also bigger calls, like
   "the thing this place is actually famous for is buried as a footnote while
   something minor leads." Those IA judgments are often the most valuable; weigh
   them seriously, but you make the final call.
4. **Apply the accepted fixes and re-review.** Rebuild, then run a lighter second
   pass. Stop when there are no high-severity findings left (or after ~3 rounds —
   and if you stop with findings open, say which and why).

Skipping the panel because the page "looks fine" is the failure mode this exists to
prevent. Run it.

## Pre-flight check — run before saying "done"

Walk the result and confirm each, out loud if needed:

1. **Direction:** Could I describe this design in one sentence, and does it match
   the content/brand? Would it look different from a generic template side by side?
2. **Type:** One expressive choice made? Real scale? Did I mentally render every
   multi-line headline for collisions?
3. **Color:** One committed palette, tinted neutrals, accent used sparingly, body
   text passes AA?
4. **Layout:** If I used a card grid, is it image-led with real links (not empty
   text boxes)? Consistent spacing rhythm? Generous whitespace?
5. **Images:** Real, thematically correct, verified-loading photos? `alt`, aspect
   ratios, lazy-loading set? Zero 404s or grey placeholder boxes? **Did I open the
   rendered page and actually look at every text-over-image section to confirm the
   text is legible — scrim painting above the image, and dark enough for that
   photo?** (Light text vanishing into a bright photo is a blocker, and it never
   shows up by reading the CSS.)
6. **States & links:** Hover/focus/empty designed? Zero dead `#` links or
   placeholder buttons?
7. **Responsive & a11y:** Deliberate on mobile? Keyboard-operable, semantic,
   labelled?
8. **AI tells (count them):** Zero em-dashes in shipped copy. Eyebrows ≤ 1 per 3
   sections. One accent color. ≥4 distinct layout families on a 6+ section page. No
   accidental purple-blue gradient, glass-everything, emoji bullets, default-serif
   reach, lorem ipsum, "Jane Doe", or "Acme". See `references/anti-slop.md`.
9. **Finish (if premium was the goal):** Does it actually feel expensive — premium
   type set precisely, luxurious space, subtle layered depth, one signature motion
   moment, art-directed imagery, obsessive hover/detail polish? Or just "fine"?
10. **Review panel run?** Did I dispatch the review subagents
    (`references/review-agents.md`), adjudicate their findings, fix the real ones,
    and re-review until clean — not skip it because it "looked fine"?

If any answer is weak, fix it before shipping. Shipping the templated default is
the only real failure.
