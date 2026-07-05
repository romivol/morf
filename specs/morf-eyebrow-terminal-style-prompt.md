Restyle every section "eyebrow" label across the site (home page and /docs) so it reads as a
real terminal command instead of a generic small-caps label. This replaces the current pattern
(e.g. "QUESTIONS" in plain tracked-out caps above "Good to know.") with something that actually
looks like the user ran a command and got that section as output — leaning into the
terminal-native identity rather than a generic marketing eyebrow.

## The pattern

Replace each eyebrow with a styled command line: a `$` prompt (in the accent green) followed by
a `morf`/`man` command whose subcommand or flag matches the section's actual content. Style it
like a single line of real terminal output — monospace, small, dimmed relative to the heading
below it — NOT bold or the same size as the heading.

```html
<div class="eyebrow-cmd">
  <span class="prompt">$</span> man morf <span class="flag">--faq</span>
</div>
<h2>Good to know.</h2>
```

Suggested command per section — adjust wording if a section's actual name differs slightly in
the code, but keep this spirit (verb/flag matches what the section actually shows):

- Hero → no eyebrow (unchanged)
- The problem → `$ morf --why`
- Before/after conversion → `$ morf diff --target cursor` (or whichever target tab is active,
  if that's easy to wire up dynamically — otherwise a static example is fine)
- Features ("Built to move between tools") → `$ morf --features`
- How it works (clone/parse/convert/route) → `$ morf install --verbose`
- Conversion matrix → `$ morf --matrix`
- The CLI (command cards) → `$ morf --help`
- Use cases → `$ morf --why switch-tools` (or similar — invent something plausible)
- Comparison → `$ morf --compare`
- Quick start → `$ morf --quickstart`
- FAQ → `$ man morf --faq`
- Roadmap → `$ morf --roadmap`

Use your judgment to keep each one short, plausible-looking, and consistent with morf's actual
flag style already established elsewhere on the site (e.g. `--target`, `--all`, `--dry-run` use
double-dash long flags) — don't invent a wildly different CLI convention.

## Styling details

- Prompt `$` in the accent green (whatever the current single accent color token is).
- The command text itself in a slightly dimmer/muted tone than body text — this is meta
  information, not primary content — similar dimness to how code comments look in a terminal.
- Any flag/argument portion (e.g. `--faq`, `--compare`) can get a subtle distinguishing color or
  just stay the same as the rest of the command — keep it simple, don't over-color this small
  element.
- Keep it on one line, small font size (similar to or slightly smaller than the current eyebrow
  text size), left-aligned above its heading exactly where the eyebrow sits today.
- Do NOT add a blinking cursor, typing animation, or any motion to these — they should read as
  static, already-executed commands, not new animations. (The one and only place with live
  typing/animation on the site should remain the hero terminal signature.)
- Remove the letter-spacing/uppercase treatment from the old eyebrow style for these — real
  terminal text isn't spaced out like that. Normal tracking, lowercase command text.

## Where NOT to apply this

- Don't touch the hero section (no eyebrow there today, keep it that way).
- Don't change the actual headings, body copy, or any content below the eyebrow — only the
  small label above each heading changes.
- Don't apply this to the terminal signature animation itself — that's a different, already
  fully-realized terminal component.

## Quality check

After implementing, verify: every section that currently has an eyebrow now has a
command-styled one instead (none left in the old spaced-caps style), the text stays legible at
mobile widths, and nothing overlaps or wraps awkwardly on narrow screens.
