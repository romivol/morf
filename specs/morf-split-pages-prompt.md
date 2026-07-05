Split the morf site into two pages: a shorter home page and a new `/docs` page. Keep the
existing visual system (dark terminal theme, tokens, fonts, gradient rules) exactly as-is —
this is a content restructuring, not a redesign.

## Page 1 — Home (`/`)

Keep only the "sell it in 60 seconds" sections, in this order:
1. Nav (add a `docs` link, pointing to `/docs`, placed before `GitHub ★`)
2. Hero (logo, H1, sub, install bar, tool-name strip)
3. The morph terminal (signature animation)
4. The problem
5. Before/after conversion (the interactive tabs)
6. Features (6 cards)
7. Comparison table (morf vs APM vs Ruler vs copy-paste)
8. Quick start (3 steps)
9. CTA band ("Write once. morf it everywhere.")
10. Footer

At the end of the features section (or right before the comparison table), add a short
transition block linking to docs, e.g.:
> "Want the full conversion matrix, every command, and answers to common questions? **Read the docs →**"
Style this as a simple text link or a light bordered card — not a full section, just a bridge.

## Page 2 — Docs (`/docs`)

Move these sections here, unchanged in content, same order:
1. "How it works" (the 4-step flow: clone → parse → convert → route)
2. The full conversion matrix table (primitive × tool)
3. "The CLI" — all 6 command cards
4. Use cases (3 cards)
5. FAQ (accordions)
6. Roadmap

Docs page needs its own simple nav: logo (links back to `/`), and anchor links to its own
sections (`how it works`, `matrix`, `commands`, `faq`, `roadmap`), plus a `← back to home` link
and the `GitHub ★` button. Reuse the same sticky-nav component/styling as the home page — same
blur, same scroll-shadow behavior — just with different links.

Give the docs page its own `<title>` and meta description, e.g.:
`<title>morf docs — commands, conversion matrix & FAQ</title>`

## Shared requirements

- Both pages share the same CSS/tokens — extract shared styles into a common stylesheet/module
  if the current implementation is a single HTML file, so there's no duplicated design system
  to keep in sync.
- Both pages keep the same footer (GitHub/LinkedIn/npm placeholders, `Built by [ your name ]`,
  MIT line).
- Preserve all existing behavior: the terminal animation on home, the before/after tabs on
  home, the FAQ accordions and command-card copy buttons on docs (carry over the copy-button
  improvement from the last round if it's already implemented there).
- Keep responsive breakpoints and accessibility behavior (focus states, reduced-motion) intact
  on both pages.
- Update any internal anchor links (`#how`, `#compare`, `#faq`, etc.) that now point to
  sections which moved to `/docs` — home page's nav should no longer link to `#how`/`#faq`
  directly; it should link to `/docs#how` / `/docs#faq` instead (or just `/docs` if you'd rather
  not deep-link into anchors from the other page — your call, whichever is cleaner to implement
  correctly).
- If the project uses client-side routing (e.g. it's a Vite/React app), use the router's
  standard navigation; if it's static HTML, this is simply two `.html` files
  (`index.html` and `docs.html` or `docs/index.html`) with normal `<a href>` links — whichever
  matches how the project is currently built and deployed on Vercel.

## What NOT to do

- Don't change any copy, colors, spacing tokens, or the terminal animation itself.
- Don't add new sections beyond what's listed above — this is a reorganization, not new content.
- Don't break the existing Vercel deployment routing — confirm `/docs` resolves correctly after
  the change (check `vercel.json` or the project's routing config if one exists).
