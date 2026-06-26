# Business-site playbook — the image-led local/service site

The most common real-world request is a marketing site for a local business:
a restaurant, florist, event company, tradesperson, clinic, studio. Visitors
expect a familiar shape. Your job is to deliver that shape with taste — strong
photography, confident type, real links — not to reinvent the layout.

This is the recipe. Read it alongside the core `SKILL.md` rules (type, color,
spacing, the pre-flight check all still apply).

## The structure

```
Header        logo · nav links · phone / "Boka" CTA
Hero          full-bleed image · headline (one word italic) · subline · 1 CTA
About         short "vilka vi är" + one supporting image
Services      image-led card grid — the centerpiece
Proof         hours / gallery / testimonials / FAQ  (as content warrants)
Contact       form or clear details + repeated CTA
Footer        contact · nav · hours
```

Single page with anchor nav is fine for small sites; multi-page (a page per
service) is fine and often expected. Either way the header, type, palette, and
spacing must be identical across every page so it reads as one site.

## The hero (the part that sells)

A full-bleed photo with the headline over it. Keep text legible:

```html
<section class="hero">
  <img class="hero-img" src="https://images.unsplash.com/photo-XXXX?w=1920&q=70&auto=format&fit=crop" alt="..." />
  <div class="hero-overlay"></div>
  <div class="hero-content">
    <p class="eyebrow">Kävlinge sedan 1986</p>
    <h1>Allt nöje. Under <em>ett tak</em>.</h1>
    <p class="lede">Ljud, ljus, scen och artister för ditt nästa event.</p>
    <a class="btn" href="#kontakt">Få en offert</a>
  </div>
</section>
```

```css
.hero { position: relative; min-height: 78vh; display: grid; }
.hero-img { position: absolute; inset: 0; width: 100%; height: 100%; object-fit: cover; }
/* scrim so any photo keeps the text readable */
.hero-overlay { position: absolute; inset: 0;
  background: linear-gradient(180deg, rgba(0,0,0,.25), rgba(0,0,0,.55)); }
.hero-content { position: relative; align-self: end; color: #fff;
  padding: clamp(2rem, 6vw, 5rem); max-width: 40rem; }
.hero h1 em { font-style: italic; color: var(--accent); }
```

The italic-one-word headline ("Allt nöje. Under *ett tak*") is a reliable,
tasteful move. One CTA, not three.

## The services card grid (the centerpiece)

Image per card, a label overlaid, optional roman/index numeral, real link. This
is the pattern clients picture when they say "put our services in boxes."

```html
<section class="services" id="tjanster">
  <header class="section-head">
    <p class="eyebrow">Vad vi gör</p>
    <h2>Tjänster</h2>
  </header>
  <div class="card-grid">
    <a class="card" href="/ljud-ljus">
      <img src="...?w=800&q=70&auto=format&fit=crop" alt="Scen med ljusrigg" loading="lazy" />
      <div class="card-label"><span class="idx">I</span><h3>Ljud &amp; ljus</h3></div>
    </a>
    <!-- repeat for each service -->
  </div>
</section>
```

```css
.card-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1rem; }
.card { position: relative; aspect-ratio: 1 / 1; overflow: hidden; border-radius: var(--r);
  text-decoration: none; color: #fff; display: block; }
.card img { width: 100%; height: 100%; object-fit: cover;
  transition: transform .4s ease; }
.card:hover img, .card:focus-visible img { transform: scale(1.05); }
.card::after { content: ""; position: absolute; inset: 0;
  background: linear-gradient(180deg, transparent 45%, rgba(0,0,0,.65)); }
.card-label { position: absolute; left: 1rem; bottom: 1rem; z-index: 1; }
.card-label .idx { font-size: .75rem; letter-spacing: .15em; opacity: .85; }
.card-label h3 { margin: .1rem 0 0; font-size: 1.4rem; }
```

Notes:
- `auto-fit` + `minmax` gives a responsive grid for free — 4 across on desktop,
  2 on tablet, 1 on phone, no media queries needed.
- `aspect-ratio: 1/1` (the RP Nöje 600×600 look) keeps cards tidy; `4/3` or `3/2`
  also work — pick one and stay consistent.
- Every card is a real `<a>` to a real destination. No `href="#"`.
- Two grids ("Event & möten", "Ljud & scen") is a good way to group many services.

## About + contact

- **About:** two columns — a paragraph of real copy and one supporting image. Keep
  the measure to ~62ch; don't let text run edge to edge.
- **Contact:** a simple labelled form (name, email, message) and/or phone + address
  + a map link. For a static site with no backend, a `mailto:` form or a service
  like Formspree is fine — just don't ship a form whose button does nothing.

## Sourcing images safely

1. Prefer the project's own `images/` / `public/` assets or CMS.
2. If a `PEXELS_API_KEY` is set, search the Pexels API for fitting images (recipe in
   `SKILL.md` → Images). Searching by subject beats guessing photo IDs, so you get
   on-topic photos reliably.
3. Otherwise keyless Unsplash direct URLs:
   `https://images.unsplash.com/photo-<id>?w=<width>&q=70&auto=format&fit=crop`
4. **Verify before trusting:** `curl -s -o /dev/null -w "%{http_code}" "<url>"`
   should be 200, and actually look at a thumbnail to confirm the subject fits
   (a Swedish beach is not a Caribbean one). Wrong-subject stock is worse than none.
5. Pick a coherent set — similar light, similar grade — so mixed photos feel like
   one brand.

## Still applies (don't drop the taste)

Familiar structure is not an excuse for generic execution. Keep: one expressive
type choice, a committed palette with tinted neutrals, a consistent spacing scale,
designed hover/focus/empty states, real copy (no lorem), accessibility, and a
deliberate mobile layout. Run the pre-flight check from `SKILL.md` before shipping.
