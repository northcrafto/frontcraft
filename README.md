# Frontcraft

A frontend design skill for [Claude Code](https://claude.com/claude-code) that
makes Claude build interfaces with actual taste, instead of the symmetric, gray,
centered, forgettable output you get by default.

Frontcraft pushes Claude to **commit to a design direction before writing markup**,
then execute it with real typographic discipline, restrained color, intentional
layout, and an anti-generic pre-flight check before anything ships. Stack-agnostic:
works with Next.js + Tailwind, plain HTML/CSS, React, Svelte, or Vue.

## What it does

- Settles the design **direction** with you up front. When you're working
  interactively it offers a few named directions and palettes and lets *you*
  choose, instead of guessing (so a law firm and a music app don't come out
  looking like the same template)
- Real typographic system: one expressive choice, a true type scale, headline
  collision checks
- Color restraint: one committed palette, tinted neutrals, a single earned accent
- Layout that breaks the "centered hero + three equal cards" default
- Real photography treated as a first-class part of the design: verified-loading
  stock, full-bleed heroes with readable overlays, image-led service card grids
- Builds the familiar small-business marketing shape (hero, about, services,
  contact) with taste instead of fighting it (see `references/business-site.md`)
- Goes premium on demand. When you want an agency-grade, "expensive" site it pulls
  from the moves that make sites like Stripe, Linear, Vercel and Apple feel costly:
  precise large type, luxurious space, layered depth and grain, engineered
  GSAP-style motion, art-directed imagery (see `references/premium.md`)
- Real, working 3D/WebGL hero code when the visual is the pitch: Three.js and
  react-three-fiber starters with fallbacks (see `references/3d-hero.md`)
- Kills the "this looks AI-generated" tells: no default-serif reach, no AI
  purple-blue gradient, one locked accent, rationed eyebrows, zero em-dashes in
  shipped copy, real copy and real images (see `references/anti-slop.md`)
- Purposeful motion, designed empty/error/hover/focus states, zero dead `#` links
- After every build, dispatches a panel of review subagents that hunt design bugs
  (stale images, headline collisions, dead links) and weak decisions (the wrong
  thing leading the page), then judges each finding and iterates (see
  `references/review-agents.md`)
- A pre-flight checklist that catches the common AI tells before you call it done

## Install

Copy the `frontcraft/` folder into your skills directory:

```bash
# user-level (available in every project)
cp -r frontcraft ~/.claude/skills/frontcraft

# or project-level (committed with a repo)
cp -r frontcraft .claude/skills/frontcraft
```

That's it. The skill activates automatically when you ask Claude to design, build,
redesign, or polish a frontend. You can also nudge it explicitly:

> "Use the frontcraft skill and build me a landing page for a coffee roaster."

## Better image search (optional)

Frontcraft always works with no setup — when a page needs photos it pulls
thematically chosen, verified stock automatically. But you'll get sharper,
better-matched images if you give it a **free Pexels API key** so it can *search*
for the right shot instead of relying on the keyless fallback.

1. Get a free key at **[pexels.com/api](https://www.pexels.com/api/)** (takes a
   minute, no cost).
2. Add it as an environment variable named `PEXELS_API_KEY`. The easiest way is
   your Claude Code user settings, `~/.claude/settings.json`:

   ```json
   {
     "env": {
       "PEXELS_API_KEY": "your-key-here"
     }
   }
   ```

   (Or export it in your shell: `export PEXELS_API_KEY=your-key-here`.)
3. Restart Claude Code so the new session picks up the variable.

That's it. With the key set, frontcraft searches Pexels and verifies each image;
without it, it falls back to keyless stock and still ships a good page. The key
lives only in your settings — it is never part of this skill, so nothing secret is
published or shared.

## Files

```
frontcraft/
├── SKILL.md              # the core design rules (always read when triggered)
└── references/
    ├── playbook.md       # deeper recipes, archetypes, worked examples (on demand)
    ├── business-site.md  # the image-led local/business-site recipe (on demand)
    ├── premium.md        # the high-end / "make it expensive" playbook (on demand)
    ├── 3d-hero.md        # working Three.js + react-three-fiber 3D hero code (on demand)
    ├── anti-slop.md      # the anti-AI-slop tell list + mechanical count (on demand)
    └── review-agents.md  # post-build review-agent loop + their training briefs (on demand)
```

## License

MIT, see [LICENSE](LICENSE). Use it, fork it, make it yours.
