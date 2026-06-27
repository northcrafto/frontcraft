# Reaching for an existing design system

Read this when the brief is a *product* surface, not a marketing page. Most of what
Frontcraft builds (landing pages, portfolios, local-business and marketing sites)
is best as a bespoke design with taste — no heavy framework. But when the brief is
an app, an admin tool, or an enterprise product, the right move is often to stand
on an official design system instead of hand-rolling one badly.

## When the brief names a world, use that world's system

| The brief reads as… | Reach for | Why |
|---|---|---|
| Microsoft / enterprise app surface | Fluent UI | Official Microsoft tokens, accessibility handled |
| Google-flavored product UI | Material 3 | Official, theme-able |
| Data-dense analytics / IBM-style B2B | Carbon | Mature data-density patterns |
| Shopify app surface | Polaris | Required for Shopify admin |
| Atlassian / Jira-style product | Atlaskit | Official Atlassian tokens |
| GitHub-style devtool or community page | Primer | Official; Brand variant for marketing |
| UK public-sector service | GOV.UK Frontend | Expected by regulation |
| US public-sector / trust-first | USWDS | Same |
| Accessible React foundation you'll theme | Radix Themes | Polished primitives |
| Modern SaaS where you own the components | shadcn/ui | You own the code; easy to restyle |
| Quick local-business / agency MVP | Tailwind + vanilla, or Bootstrap | Boring, fast, fine |

## Honesty rules

- **Install and use the official package.** Don't recreate a system's CSS by hand,
  and don't import its tokens only to override most of them. If you're going to
  fight the system, you didn't want the system.
- **One system per project.** Don't mix Fluent with Carbon, or drop shadcn/ui
  components into a Material app. Pick one and commit.
- **Never ship a system in its default state.** shadcn/ui especially: restyle radii,
  color, shadow, and type to the chosen direction, or it looks like every other
  shadcn site.
- **An aesthetic is not a system.** "Glassmorphism", "bento", "brutalist",
  "editorial" have no official package — build those with native CSS + your tokens,
  and say in a comment what's borrowed inspiration vs. real material.

## Frontcraft's actual sweet spot

For marketing, portfolio, and small-business work, **don't reach for any of these.**
A small set of CSS custom properties (`--bg --surface --fg --muted --line --accent`),
a real type scale, and a spacing rhythm *is* your design system, and it will look
more distinctive than any off-the-shelf kit. Reach for an official system only when
the surface is genuinely product/app/enterprise and consistency with that ecosystem
matters more than a unique look.
