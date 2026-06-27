# Review-agent loop — catching design bugs after every build

After you build (or change) a frontend, you run a panel of review subagents that
try to find what's wrong with it. They report; you judge; you fix; you re-review.
This file is the recipe and the agents' "training" — the briefs that make their
critique sharp instead of generic.

The mindset: the build is a draft until reviewers have attacked it. Most bad
shipped UI is not bad because the builder lacked taste; it's because nobody looked
again with fresh, adversarial eyes. These agents are those eyes.

## How to run it

1. **Give the reviewers something concrete to look at.** Point them at the built
   files (the HTML/CSS/JS you just wrote) and, if it's deployed or runnable, the
   live URL. If you have a screenshot/preview tool, capture the page and pass the
   image — reviewers catch far more from a render than from code alone. Text-over-
   image legibility especially cannot be trusted from code: a scrim can look correct
   in CSS yet render *behind* its image. Look at those sections (or screenshot them)
   before trusting them.
2. **Launch the panel in parallel.** One message, multiple Agent tool calls, so
   they run concurrently. Use the briefs below verbatim as each agent's prompt,
   filling in the file paths / URL.
3. **Collect structured findings**, adjudicate, fix, re-review (see below).

Scale the panel to the job: a quick component → 2 reviewers; a full page or
client site → all five; "audit this thoroughly" → run two rounds and add a
completeness critic that asks "what did we miss?".

## The panel (each agent's training brief)

Give every agent this shared instruction first:

> You are a senior design reviewer. Be specific and adversarial: your job is to
> find what's wrong, not to praise. For every issue report exactly: **location**
> (file + selector/section, or where on the page), **what's wrong**, **why it
> matters** (the user impact), **a concrete fix**, **severity** (blocker / high /
> medium / nit), and **confidence** (high / medium / low). Do not invent problems
> to fill a quota — if a category is clean, say so. No vague advice ("make it pop").

Then each gets its specialized lens:

### 1. Visual & layout bug hunter
> Hunt rendering and layout bugs: headline/line collisions (tight line-height +
> negative margins), text overflow and clipping, inconsistent spacing, broken
> alignment, elements overlapping, things that break at common widths (360, 768,
> 1280) and very tall/short viewports, z-index/sticky glitches (including an overlay/scrim that renders
> *behind* its own image from a stacking-context z-index bug, leaving overlaid text
> unreadable), scrollbars, color
> contrast below WCAG AA. Report the worst offenders first.

### 2. Image & asset auditor
> Audit every image and media asset. Flag: broken/404 sources, placeholder or
> obviously-wrong-subject images (a tropical beach on a Nordic site), a *stale or
> old image left in from a previous version* that no longer matches the copy,
> mismatched grading/aspect ratios, missing alt text, missing lazy-loading, and
> oversized files. **Scrutinize every text-over-image section hard — this is where
> text silently goes invisible:** (a) is the scrim/overlay actually painting *above*
> the image, or is it defeated by a stacking bug? The classic failure: a scrim
> nested inside a `z-index`-negative media wrapper with a *lower* z-index than the
> `<img>` renders *behind* the image and does nothing, so the photo shows through at
> full brightness. (b) Is the scrim dark/opaque enough for *that specific photo*
> where the text actually sits? A pale or bright image needs a far stronger scrim
> (or a solid color panel) than a dark one. Light text over a bright photo is a
> blocker. Do NOT pass legibility on token contrast alone — the image is part of the
> background, so judge the real render. For each, say whether to replace, regrade,
> strengthen the scrim, or fix the layering.

### 3. Content & information-architecture critic
> Ignore pixels. Judge whether the page emphasizes the *right* things. Ask: is the
> single most important or most distinctive thing the most prominent? Is anything
> genuinely notable buried while something minor leads? Example of the call to
> make: if a town is famous for one standout thing and the page lists it as a small
> side item while a generic item is the hero, that's an IA bug — promote the
> standout, demote the filler. Flag mis-weighted hierarchy, missing obvious
> sections, burying the lede, and copy that undersells the real story. Propose the
> corrected priority order.

### 4. Interaction & accessibility checker
> Check behavior and a11y: dead links (`href="#"`, links to nowhere), buttons that
> do nothing, missing or weak hover/focus-visible/active/empty/error/loading
> states, CTA labels that wrap at desktop, duplicate-intent CTAs, keyboard
> operability, semantic structure (landmarks, heading order), labelled controls,
> reduced-motion handling. Report anything a real user or screen reader would trip
> on.

### 5. Taste & AI-tells critic
> Judge whether this looks designed or templated. Flag generic AI tells: the
> centered-hero + three-equal-text-cards default, accidental purple-blue gradients,
> glass-everything, emoji-as-icon, lorem ipsum, system-default fonts, every section
> wearing the same small uppercase eyebrow, em-dashes used as a style crutch, and
> any place where the design retreats to a safe default instead of a choice. Say
> what's generic and what to do instead.

## Findings format (what comes back)

Ask each agent to return a short list like:

```
[high]  hero, index.html .hero h1 — headline "Pyttebron och Rönne å" wraps to 3
        lines at 390px and the descender on 'p' clips. Fix: reduce clamp min to
        2.2rem and set line-height 1.05 with pb. confidence: high
[medium] services — the UFO memorial is the town's most distinctive draw but sits
        as card IV; a generic park leads. Fix: make UFO the feature/first panel.
        confidence: medium
```

## Adjudicate — *is the agent right?*

This is the part that matters. A finding is a **claim**, not an instruction.

- **Verify each against the real code/render.** Reviewers hallucinate or
  misread. If you can't reproduce the problem, reject it (one-line reason).
- **Accept the true ones**, especially blocker/high severity and anything an
  agent gave high confidence with a concrete location.
- **Weigh the IA/content calls carefully.** "Promote the famous thing, demote the
  side project" is exactly the kind of judgment that lifts a page from fine to
  right — but it's a judgment, and you own it. If the reviewer is right, restructure;
  if their premise is wrong (the thing isn't actually the draw), say so and move on.
- **Resolve conflicts** between agents by deciding what serves the brief, not by
  averaging. Note trade-offs out loud.

Keep a quick accept/reject tally so the user can see what changed and why.

## Iterate, then stop

1. Apply accepted fixes, rebuild.
2. Run a lighter second pass (the same panel, or just the lenses that had findings).
3. **Stop** when no blocker/high findings remain, or after ~3 rounds. If you stop
   with findings still open, list them and explain the call (out of scope, disputed,
   needs the user's input).

Then, and only then, run the `SKILL.md` pre-flight check and report done.

## Why "train" them at all

A reviewer told only "find problems" returns vague mush ("improve spacing,
enhance hierarchy"). The briefs above force **specific, located, justified,
fixable** findings with a severity and a confidence — which is exactly what lets
you judge whether each one is right and act on it fast. The training is the
difference between a review you can use and one you ignore.
