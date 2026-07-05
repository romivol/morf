Animate the hero logo mark on the home page — the row of 4 gradient shapes above the "one
agent, every tool" headline. Right now they're static (a square, two intermediate rounded
squares, and a circle, side by side). Make them actually morph.

## What to build

Replace the static row with a **looping shape-morph animation**: a single shape that
continuously cycles from a sharp square to a full circle and back, in place — literally
demonstrating the product's core idea (one shape becoming another).

Two acceptable implementations, pick whichever fits the current codebase better:

**Option A — CSS-only (simplest, preferred if it looks smooth):**
Keep the 4 shapes as separate elements but animate each one's `border-radius` on a staggered
loop, so they appear to "breathe" between square and circle continuously, like a wave passing
through them left to right. Roughly:
```css
@keyframes morf-breathe {
  0%, 100% { border-radius: 3px; }
  50%      { border-radius: 50%; }
}
.morf-shape { animation: morf-breathe 3.2s ease-in-out infinite; }
.morf-shape:nth-child(1) { animation-delay: 0s; }
.morf-shape:nth-child(2) { animation-delay: 0.25s; }
.morf-shape:nth-child(3) { animation-delay: 0.5s; }
.morf-shape:nth-child(4) { animation-delay: 0.75s; }
```
Keep the existing gradient fill and opacity ramp across the 4 shapes exactly as they are now —
only `border-radius` should animate.

**Option B — single morphing shape (more literal "one becomes another"):**
Replace the 4 static shapes with ONE shape element that loops through the same square →
rounded → circle progression on a timer (via CSS animation or a tiny JS interval), so it reads
as "the one shape from the logo, alive." If you go this route, keep it visually similar in
size/footprint to the current 4-shape row so the hero layout doesn't shift.

Use your judgment on which reads better — Option A (wave of 4) is closer to the existing visual
and lower risk; Option B is more literal to the brand story. Either is fine, but pick one and
make it clean, not both half-implemented.

## Requirements

- Smooth, no jank — use CSS `animation`/`transition`, not JS-driven reflow, if possible.
- Timing should feel calm and premium, not frantic — 3-4 second loop is the right ballpark, not
  under 1s.
- Respect `prefers-reduced-motion: reduce` — freeze on the current static square→circle frame
  (exactly what's shown today) for users with that preference. Do not disable the whole hero,
  just stop this one animation.
- Keep the exact same colors/gradient (`--grad-a` → `--grad-b`) and opacity progression already
  used for the 4 shapes — don't change the color story, only add motion.
- This should only affect the hero logo mark row on the home page — do not touch the small nav
  logo, the favicon, or the terminal's morph sequence.
- Verify it doesn't cause layout shift or increase page weight noticeably (pure CSS keyframes
  are basically free — avoid adding a JS animation library for this).

## What NOT to do

- Don't change the logo's SVG markup structure if a pure-CSS `border-radius` animation on the
  existing `<rect>`/`<circle>` elements achieves the effect (note: SVG `<rect>` supports
  animatable `rx`/`ry`, so this can likely be done by animating `rx` via CSS or SMIL instead of
  `border-radius` if the shapes are SVG elements, not HTML divs — check the current
  implementation and use the correct property for whichever it is).
- Don't add sound, bounce/elastic easing, or anything playful/bouncy — keep it calm and premium,
  consistent with the rest of the site's restrained motion language.
- Don't make this an infinite CPU-heavy animation — a simple 3-4 keyframe loop is enough.
