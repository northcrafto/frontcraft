# Redesigning an existing site — evolve it, don't detonate it

Greenfield is permission to invent. A redesign is not — there's a live site with
URLs, rankings, analytics, muscle-memory, and brand equity you can destroy in one
careless pass. Most "redesigns" that go wrong don't go wrong on taste; they go
wrong by silently breaking something that was working. This is the protocol.

## 1. Detect the mode first

- **Greenfield** — nothing exists. Use the main `SKILL.md` workflow.
- **Redesign · preserve** — keep the brand and IA, lift the execution. The common
  case. Most value, least risk.
- **Redesign · overhaul** — the brand itself is changing; closer to greenfield but
  with content and SEO to carry over.

If it's ambiguous which the user wants, **ask once**: *"Should this preserve the
existing brand and structure, or start visually from scratch?"* Don't guess — the
answer changes almost everything below.

## 2. Audit before you touch anything

Write down what exists, so you change things on purpose instead of by accident:

- **Brand tokens** — pull the *actual* colors, fonts, radius, and spacing off the
  live site (computed styles / stylesheet) before you recolor anything.
- **IA / page tree** — every page, its slug, and how nav maps to it.
- **Content blocks** — what each page actually says; the copy's voice.
- **Keep vs retire** — list which patterns are working (keep) and which are dated
  (retire). Not everything old is bad.
- **Dial reading** — read the existing site on the three spectrums (composure /
  motion / density). Your redesign should move deliberately *from* that reading,
  not land on an unrelated planet.
- **SEO baseline** — titles, meta, headings, and especially **URLs**. *SEO
  regression is the #1 way a redesign quietly costs the client money.* Note it
  before you move anything.
- **Analytics surface** — what events/buttons/forms are tracked, and by what name.

## 3. What never changes silently

Touch these only with the user's explicit say-so, and call it out loud when you do:

- **URL structure / route slugs** — moving a ranking page to a new path without a
  301 drops its traffic. Redirect or don't move it.
- **Primary nav labels** — they're how returning visitors navigate by habit.
- **Anchor IDs** used by inbound links or the nav's smooth-scroll.
- **Form field names and order** — renaming/reordering breaks analytics funnels
  *and* browser autofill.
- **Brand logo / wordmark**, unless the brand is the thing being changed.
- **Legal / consent / cookie copy.**

Renaming a tracked button from "Get started" to "Start now" silently zeroes a
funnel the client may watch weekly. Preserve the names; restyle the pixels.

## 4. Modernisation levers — in priority order

Pull them in this order; each later one costs more risk per unit of visual gain.
You can stop at any point once the site reads current.

1. **Typography refresh.** The biggest visual lift per unit of risk — a better
   display face, a real scale, tuned line-height/tracking. Often 70% of the
   "wow, it looks modern now" comes from here alone.
2. **Spacing & rhythm.** Open the whitespace, fix the spacing scale, give sections
   room to breathe.
3. **Color recalibration.** Re-tint neutrals, mute or sharpen the accent, fix
   contrast — *building from the extracted brand colors*, not a new palette out of
   nowhere (unless overhaul).
4. **Motion layer.** Add tasteful entrance reveals and hover states. Cheap once the
   bones are right; honor reduced motion.
5. **Hero recomposition.** Rebuild the opening for impact.
6. **Full block replacement.** Only when a section is genuinely unsalvageable.

## 5. The decision tree

- **IA, content, and SEO are sound, it just looks dated** → *targeted evolution*
  (levers 1–4). This is roughly **70% of the value at 40% of the risk** — the right
  call far more often than a teardown.
- **Structural / layout debt, but the brand and content are fine** → full visual
  redesign with **content and URLs preserved**.
- **The brand itself is changing** → treat as greenfield, but still carry over the
  content and protect the SEO/analytics surface from §3.

## 6. Then build, then review

Once you've chosen the mode and levers, you're back on the normal `SKILL.md`
workflow: settle direction + color *with the user* (a redesign still gets the
direction/color question unless they're fixed by the kept brand), build, run the
pre-flight, and dispatch the review panel. Add one redesign-specific reviewer
question: *"Did anything in §3 change without being asked for?"*
