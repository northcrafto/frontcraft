# The compact filter landing — a short, simple site that doesn't scroll forever

Some briefs don't want the long editorial scroll (hero → band → band → band →
footer). They want what most local-business and "one company, a few things"
sites actually are: **one commanding screen, then a small set of choices, then a
way to get in touch.** Fast to build, fast to use. When the user says "make it
shorter", "I don't want to scroll so much", "like *that* site", or the content is
a handful of services/places/categories rather than a story — reach for this
shape instead of stacking more full-bleed sections.

The whole site is ~3 screens:

```
┌─────────────────────────────┐
│  Full-screen HERO            │  one image, headline, one promise, one CTA
│  (image + scrim + text)      │
├─────────────────────────────┤
│  Filter tiles  [All][A][B]…  │  the "rutor" — click to filter
│  ┌────┐ ┌────┐ ┌────┐        │
│  │card│ │card│ │card│  …     │  grid filters IN PLACE, no new page
│  └────┘ └────┘ └────┘        │
├─────────────────────────────┤
│  Contact: info + form        │  name / email / topic / message
├─────────────────────────────┤
│  small footer                │
└─────────────────────────────┘
```

Why it works: the hero does the emotional job, the **filter tiles replace five
scrolling sections** with one interactive one (the visitor picks what they care
about and the rest gets out of the way), and the contact block closes the loop.
No long-form reading required, and there's nothing to build beyond one page.

## When to use it (and when not)

- **Use it** for: local businesses with a few service categories, destination/
  place guides, "what we offer" sites, anything where the content is a *set of
  comparable items* the visitor browses rather than a narrative they read.
- **Don't** force it when the content genuinely is a story or a long-form pitch
  (a single product launch, a manifesto, an editorial piece) — there the long
  scroll is right. This pattern is for *breadth* (many items, pick one), not
  *depth* (one thing, explained at length).

It still obeys everything else in this skill: pick a direction and palette with
the user, one accent, tinted neutrals, real images (verify them), no em-dashes in
copy, ration eyebrows (this layout naturally wants **one** — on the hero), design
every state, and run the review panel after.

## The three parts

### 1. Full-screen hero (the one screen that sells it)

`min-height: 100svh`, image full-bleed behind, content bottom-left (not centered —
that's the AI default). **The scrim must paint _above_ the image**, or light text
vanishes into a bright photo. The trap, spelled out in `SKILL.md` and
`review-agents.md`: a scrim with a *lower* `z-index` than the `<img>` renders
*behind* it and does nothing. Keep the media wrapper itself behind the content,
but the scrim above the image inside it:

```css
.hero { position:relative; min-height:100svh; display:flex; align-items:flex-end;
        padding:0 var(--gut) clamp(64px,12vh,120px); overflow:hidden; }
.hero__media { position:absolute; inset:0; z-index:0; }
.hero__img   { width:100%; height:100%; object-fit:cover; }
.hero__scrim { position:absolute; inset:0; z-index:1;   /* ABOVE the img */
  background:
    linear-gradient(to top, rgba(14,20,26,.92) 4%, rgba(14,20,26,.4) 42%, rgba(14,20,26,.5) 100%),
    linear-gradient(to right, rgba(14,20,26,.55), rgba(14,20,26,.12) 60%); }
.hero__content { position:relative; z-index:2; max-width:760px; }  /* above scrim */
```

Confirm legibility on the **rendered page**, not by reading the CSS. Add a
`text-shadow` on the title/lead as cheap insurance for bright photos.

### 2. Filter tiles + in-place grid (the part that kills the long scroll)

A row of category buttons ("rutorna") above a card grid. Clicking a tile shows
only the matching cards — **no navigation, no new page**. This is the move that
collapses what would be five sections into one.

Accessibility that's easy to get wrong here:
- The tiles are **filter toggles, not tabs.** Use `<button type="button">` with
  `aria-pressed`, inside a `role="group"` with an `aria-label`. Do *not* use
  `role="tab"`/`aria-selected` (that implies arrow-key navigation and linked
  tabpanels you don't have).
- Filtering is **silent to screen readers** unless you announce it. Add a
  visually-hidden `role="status" aria-live="polite"` region and write the result
  count into it on every filter ("3 platser").
- Show a real **empty state** if a category can ever be empty.
- Keep the per-tile **counts honest** — derive or double-check them against the
  actual number of cards in each category (a review agent should literally count).

```html
<div class="filters" role="group" aria-label="Filtrera">
  <button class="filter is-active" type="button" aria-pressed="true"  data-filter="alla">Allt <span>8</span></button>
  <button class="filter"           type="button" aria-pressed="false" data-filter="natur">Natur <span>3</span></button>
  <!-- … -->
</div>
<p class="sr-only" role="status" aria-live="polite" id="gridStatus"></p>
<div class="grid" id="grid">
  <a class="card" data-cat="natur" href="/real-link"> … image, tag, title, text … </a>
  <!-- … -->
  <p class="grid__empty" hidden>Inga träffar i den kategorin.</p>
</div>
```

```js
function applyFilter(value){
  var shown = 0;
  cards.forEach(function(card){
    var match = value === 'alla' || card.dataset.cat === value;
    card.classList.toggle('is-hidden', !match);          // .is-hidden { display:none }
    if (match) shown++;
  });
  empty.hidden = shown !== 0;
  status.textContent = shown + (shown === 1 ? ' träff' : ' träffar');
}
filters.forEach(function(btn){
  btn.addEventListener('click', function(){
    filters.forEach(function(b){ b.classList.remove('is-active'); b.setAttribute('aria-pressed','false'); });
    btn.classList.add('is-active'); btn.setAttribute('aria-pressed','true');
    applyFilter(btn.dataset.filter);
  });
});
```

Cards are real links to real destinations (pages, official sources, detail views)
— never `href="#"`. A subtle hover lift + image zoom and a fade-in on filter is
enough motion; honor `prefers-reduced-motion`.

### 3. Contact block (close the loop, à la a real small-business site)

A two-column section: practical info / "find us" on the left, a short form on the
right (name, email, a "what's it about?" select, message). Collapses to one column
on mobile.

Make the form **actually do something** — no dead submit button:
- With a backend or form service (Formspree, Basin, a serverless endpoint), POST
  to it and show a real success/error state.
- Static with no backend: compose a `mailto:` from the field values and open the
  mail client. If you do this, be honest in the status copy ("we'll try to open
  your mail app; if nothing happens, email …") and **don't wipe the fields** on
  submit, so the message survives a failed handoff. Show the address as a real
  fallback.

Form craft: every input has a `<label for>`, `required` + `novalidate` with JS
`checkValidity()`, focus moves to the first invalid field, set `aria-invalid` on
bad fields and clear it on input, visible focus rings, an `:user-invalid` style.

## Page plumbing this layout always needs

- **`scroll-padding-top`** on `html` (≈ nav height) so in-page anchors don't tuck
  the target heading under the fixed nav.
- **Skip link** to `<main tabindex="-1">` (a non-focusable section won't receive
  focus).
- **Mobile drawer must not stay focusable when closed** — an off-screen
  `translateX(100%)` menu is still in the tab order; add `visibility:hidden` (or
  `inert`) when closed, restore on open. Toggle `aria-expanded`, close on Escape,
  return focus to the burger, and morph the burger to an X.
- **`:focus-visible`** on *every* interactive element (buttons, links, the hero
  CTAs), not just the ones you remembered.

## Pre-flight (in addition to SKILL.md's)

- Tile **counts match** the real number of cards per category.
- Every card links somewhere real; the form submits or composes mail for real.
- Filter announces results to AT; empty state exists.
- Hero text legible **on the render**; scrim above the image.
- One eyebrow (hero), not one per section. Zero em-dashes in copy.
- The whole thing is genuinely short — if you've added a fourth and fifth full
  section, you've drifted back into the long-scroll shape; pull it back.
