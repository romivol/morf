The morf site currently reads as generically "AI-designed." Fix that with real, specific
design decisions — not just a color swap. Keep the dark terminal/hacker theme and the JetBrains
Mono + Inter pairing (those are genuinely right for this brand), but eliminate the templated
patterns below and replace them with choices actually derived from what morf is.

## The tells to remove

1. **The violet→cyan gradient is now a cliché of AI-generated design.** Replace it with a
   palette derived from the actual subject: a terminal. Pick ONE accent color, not a gradient,
   grounded in something real — e.g. the phosphor green of old terminals (`#39FF6A`-ish, but
   pick a refined, not neon, value), or an amber/CRT-amber tone, or a single saturated blue like
   a real terminal cursor. Use tints/shades of that ONE hue for emphasis, hover, and the
   "converted" state — not a two-color gradient. If you want to keep any gradient at all, justify
   it structurally (e.g. only inside the terminal's `morfed` word, nowhere else) rather than
   spreading it across icons, buttons, table rows, and headings like now.
2. **Kill the icon-in-rounded-gradient-square pattern** on the 6 feature cards. That exact
   shape (soft-cornered chip, centered glyph, gradient tint) is the single most common AI
   feature-card template. Replace it with something specific to a terminal/CLI tool: e.g. render
   each feature as a small inline command or status-line snippet (using the same status symbols
   ✓/±/— already established in the terminal), or drop icons entirely and let a distinctive
   type treatment (e.g. a large monospace index character, or the primitive name itself styled
   boldly) carry the card instead.
3. **Vary the "eyebrow" label pattern.** Not every section needs a small-caps label above its
   heading. Keep it only where it earns its place (e.g. sections that are genuinely reference
   material, like the CLI commands or FAQ) and drop it elsewhere in favor of the heading doing
   the work alone. Don't repeat the identical visual formula section after section.
4. **Break the perfect symmetry.** Right now every grid is perfectly even (3-col, 3-col, 2-col),
   every card is the same size, everything is centered. Introduce at least one real asymmetric
   layout choice — e.g. the before/after conversion section could be unbalanced (source card
   smaller/quieter, output card larger/brighter, since the *output* is the point), or the
   comparison table could break out of the container width while everything else stays
   contained, or feature cards could be different sizes based on actual importance (make "real
   format conversion" and "every primitive" visually bigger/first since those are the moat —
   don't give equal visual weight to zero-config and open-source, which are minor).
5. **Take one real typographic risk.** Right now the type is competent but safe — one weight of
   bold headlines, one body size, one mono treatment. Do something specific to a terminal's own
   vernacular: e.g. render the hero headline using an actual monospace grid-aligned baseline
   with visible character-cell spacing (like a real terminal renders text), or use a subtly
   different tracking/size for text that represents "before" vs "after" states, or give the
   product name `morf` a treatment that's used ONLY for the name (never for other emphasis) so
   it reads as a wordmark, not just bolded text.

## What to keep

- Dark background, JetBrains Mono + Inter pairing, the terminal signature animation, the
  overall information architecture (home + /docs split), the status symbols (✓ ± — ↝), the
  copy/content as written.
- The numbered 01→02→03→04 flow in "how it works" — that one is legitimate since clone → parse
  → convert → route is a real sequence, not decorative numbering. Keep it, but restyle it to
  match whatever new accent/type system you land on.

## Process

Before writing code: state your new 4-6 hex color token system (with the ONE accent color and
its tints/shades) and a one-paragraph description of what makes this treatment specific to
"morf as a terminal-native tool," not a generic dark dev-tool site. Then implement it
consistently across both the home page and /docs page so they still feel like one product.

## Quality bar (unchanged)

Keep everything from the original build spec's quality bar: responsive, accessible (focus
states, contrast, reduced-motion), no console errors, same deployment setup. This is a visual
refinement pass, not a rebuild — don't touch the JS logic (terminal animation, tabs, FAQ
accordions, copy buttons) except where the visual changes require it.
