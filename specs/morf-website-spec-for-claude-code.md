# morf — Website Build Spec (for Claude Code)

> **Audience:** Claude Code. Build the complete landing page for **morf** from this spec alone.
> A working single-file HTML reference implementation is attached (`morf-site-preview.html`) — match its look, feel and behavior, then improve on it where this spec says so.

---

## 1. What morf is (product context — read first)

**morf** is an open-source CLI (MIT, zero runtime dependencies, Node >= 18) that installs AI agent primitives from any git repo into **every AI coding tool at once** — and, critically, **converts** each primitive into each tool's native format rather than just copying files.

### The problem it solves
Every AI coding tool speaks its own dialect. A skill, an agent, a rule — each tool wants a different folder, a different file extension, different frontmatter fields. Developers who use more than one tool (most of them) copy files around and hand-fix each one, for every tool, every time.

### What morf does
```
$ morf install github.com/acme/bug-finder
  ✓ cloning  bug-finder  done

  morphing bug-finder →

  ✓  claude     ~/.claude/agents/bug-finder.md
  ✓  cursor     .cursor/rules/bug-finder.mdc
  ✓  kilo       ~/.kilo/agent/bug-finder.md
  ±  copilot    .github/agents/bug-finder.md   (tools mapped)
  ✓  windsurf   .devin/rules/bug-finder.md
  ✓  opencode   ~/.opencode/agent/bug-finder.md

  morfed 1 agent → 6 tools
```

### Key facts
- **Tagline:** `one agent, every tool`
- **Secondary line:** `Write once. morf it everywhere.`
- **Positioning one-liner:** *"Ruler does rules. APM does packaging. morf does all of it — and it's the only one that actually converts your agents."*
- **6 supported tools:** Claude Code, Cursor, Kilo, GitHub Copilot, Windsurf, OpenCode.
- **6 primitive types:** skills, agents, rules, prompts/commands, hooks, MCP servers.
- **Conversion vs routing:** skills & MCP are near-universal formats → *routed* (right folder, unchanged). Agents, rules, prompts, hooks genuinely differ per tool → *converted* (frontmatter/permissions/event names rewritten). **Agent conversion is the moat — no competitor does it.**
- Works with **any git host** (GitHub, GitLab, self-hosted, public or private), by URL or by short name from a registry.
- **Zero config:** no manifest required, unlike APM.
- Never modifies source repos; never overwrites local edits (skip + `--force` hint).

### Audience for the site (two at once)
1. **Developers** — must see the install one-liner and understand the product within 3 seconds.
2. **Recruiters / hiring managers** — the site owner is job-hunting (DevOps + AI); the site must read as a real, polished product with market awareness. The comparison table and roadmap exist largely for this audience.

---

## 2. Brand & visual direction

**Vibe: terminal / hacker, dark.** Deliberately dark and mono-first — it stands out against the light polished dev-tool sites of 2026 and signals "lives in the terminal."

**Restraint rule:** the violet→cyan gradient is the ONE expressive element (it literally embodies conversion — color morphing from hue to hue). Everything else stays quiet and disciplined. Gradient is allowed ONLY on: the wordmark, the logo mark, `morphing`/`morfed` words in the terminal, highlighted table rows, the CTA band background, and small accents (feature-card icon chips, active tab borders). Nowhere else.

### Design tokens (use exactly)
```css
--bg:#0A0C10;        /* page background */
--bg-elev:#12151C;   /* terminal, install bar */
--bg-card:#0F131A;   /* cards */
--border:#1E2430;    /* hairline borders */
--text:#E6E9EF; --text-dim:#8B93A3; --text-faint:#5A6172;
--grad-a:#7C3AED;    /* violet */
--grad-b:#22D3EE;    /* cyan  */
--ok:#27C93F; --warn:#E3B341; --err:#FF5F56;
```
Gradient: `linear-gradient(120deg, var(--grad-a), var(--grad-b))`.
Ambient: one fixed radial violet glow behind the hero (`radial-gradient`, blurred, low opacity). Subtle.

### Typography
- **Mono (headings + all code/terminal):** JetBrains Mono (Google Fonts), fallback `ui-monospace, 'Cascadia Code', monospace`.
- **Sans (body prose):** Inter, fallback `system-ui, sans-serif`.
- Hero H1 `clamp(2.4rem, 6vw, 4.2rem)`, weight 800, letter-spacing −0.04em. Section H2 ~1.9rem. Body 1rem/1.6.
- Brand voice: lowercase, terse, developer-native (npm/vite tone). No corporate filler.

### Logo (SVG, build inline)
Mark = a square that transforms into a circle in 4 steps (square → increasingly rounded → circle), all filled with the gradient, opacity ramping .5 → 1. This IS the product story: one shape becoming another.
```svg
<svg viewBox="0 0 210 60">
  <defs><linearGradient id="h" x1="0" y1="0" x2="1" y2="1">
    <stop offset="0" stop-color="#7C3AED"/><stop offset="1" stop-color="#22D3EE"/></linearGradient></defs>
  <rect x="6"  y="12" width="36" height="36" rx="3"  fill="url(#h)" opacity=".5"/>
  <rect x="52" y="12" width="36" height="36" rx="10" fill="url(#h)" opacity=".72"/>
  <rect x="98" y="12" width="36" height="36" rx="15" fill="url(#h)" opacity=".88"/>
  <circle cx="180" cy="30" r="18" fill="url(#h)"/>
</svg>
```
Wordmark: `morf` lowercase, mono, weight 800, gradient text. Small icon-only variant (shrunk mark) for nav + favicon + footer.

---

## 3. Page structure (single page, this exact order)

1. **Sticky nav** — icon + gradient wordmark left; links right: conversion · how it works · compare · faq · `GitHub ★` button. Backdrop blur; bottom border appears on scroll.
2. **Hero** — logo mark (~210px), H1 `one agent,` / `every tool` (second line gradient), sub-paragraph, **copy-paste install bar** (`$ npx morf install <git-url>` + working copy button), `View on GitHub →` link, then a strip of the 6 tool names with tiny gradient dots.
3. **Signature: the morph terminal** ← the star. Full spec in §4.
4. **The problem** — eyebrow `the problem`; H2 `Every AI tool speaks its own dialect.`; short lead paragraph ending "morf is the translator: one command, converted for every tool you use."
5. **Before/after conversion (interactive)** — eyebrow `real conversion, not copying`; H2 `The same agent, reshaped for each tool.` Two code cards side by side: left = fixed source agent (`bug-finder.md` with name/description/tools/model frontmatter), right = the converted output. **Tabs above (→ cursor / → kilo / → copilot)** switch the right card's content, showing genuinely different frontmatter per target (cursor: `globs`+`alwaysApply` in `.mdc`; kilo: `mode`+`permission`+`color`; copilot: tools-mapped comment) and the destination path as the last line. Gradient arrow between cards; stacks vertically on mobile (arrow rotates 90°).
6. **Features** — 6 cards, 3×2 grid (1-col mobile): Real format conversion / Every major tool / Every primitive / Zero config / Any git host / Open source. Small gradient-tinted icon chip per card.
7. **How it works** — 4-step flow: clone → parse → convert → route (numbered chips with arrows), followed by the **conversion matrix table**: rows = 6 primitives, columns = 6 tools, cells = ✓ (converted, green) / ↝ (routed, cyan) / — (n/a, faint). **Agents row highlighted** with a subtle gradient background. Legend below. Matrix values:
   | | claude | cursor | kilo | copilot | windsurf | opencode |
   |---|---|---|---|---|---|---|
   | Skills | ↝ | ↝ | ↝ | ↝ | ↝ | ↝ |
   | **Agents** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
   | Rules | ✓ | ✓ | ↝ | ✓ | ✓ | ↝ |
   | Prompts | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
   | Hooks | ✓ | — | ✓ | — | ✓ | ✓ |
   | MCP | ↝ | ↝ | ↝ | ↝ | ↝ | ↝ |
8. **The CLI** — 6 command cards, 2-col grid: `install <url>` / `search <query>` / `list` / `update --all` / `publish` / `config default <tool>`, each with a one-line description.
9. **Use cases** — 3 cards, each an italic quote + answer: "built it in Claude, want it in Cursor" / "team uses three tools, config drifts" / "personal library of skills reused everywhere".
10. **Comparison table** — morf vs APM vs Ruler vs copy-paste-by-hand. Columns: multi-tool / **converts agents** / all primitives / zero-config / any git host. morf row highlighted, only one fully checked. Below it, the positioning one-liner with `morf does all of it` in gradient.
11. **Quick start** — 3 numbered steps: `npx morf install <git-url>` → `morf config default <tool>` → `morf list`.
12. **FAQ** — native `<details>` accordions, 6 items: does it change my files (no) / unsupported primitive (skips just that, marks it) / need a manifest (no) / which git hosts (any) / overwrite local edits (no, `--force`) / really free (MIT, zero deps).
13. **Roadmap** — tagged rows: `shipped` (green) skills+agents for Claude/OpenCode/Kilo · `in progress` (amber) Cursor/Copilot/Windsurf + rules/prompts/hooks/MCP · `next` (faint) public registry & search · lockfile & `morf sync` · versioning & `morf publish`.
14. **CTA band** — faint gradient background strip: `Write once. morf it everywhere.` + repeated install bar.
15. **Footer** — small icon, links `GitHub · LinkedIn · npm` (placeholder `#`), `Built by [ your name ]` (**keep as visible placeholder**, amber), `open source · MIT`, tag line `built for people who use more than one AI tool.`

---

## 4. The morph terminal (signature element — build this well)

A macOS-style terminal window (traffic-light dots, title `morf — install`, `--bg-elev`, hairline border, soft shadow). Plays once when scrolled into view (IntersectionObserver, threshold ~0.4), with a `↻ replay` button below.

**Sequence:**
1. Type `$ morf install github.com/acme/bug-finder` char-by-char (~36ms/char) with a blinking cyan block cursor.
2. Spinner line: a **Braille spinner** (`⠋⠙⠹⠸⠼⠴⠦⠧`, 80ms/frame) next to `cloning  bug-finder`, running ~1.25s, then resolving to `✓  cloning  bug-finder done`.
3. Blank line, then `morphing bug-finder →` (gradient on "bug-finder").
4. Six result lines revealed staggered (~125ms apart) — exactly the output shown in §1, with `✓` green, `±` amber.
5. Blank line, then `morfed 1 agent → 6 tools` (gradient on "morfed").

**Status symbols everywhere on the site (unicode, not ASCII):** `✓` ok/green · `±` adapted/amber · `✗` error/red · `—` not supported/faint · `↝` routed/cyan.

**Reduced motion:** if `prefers-reduced-motion: reduce`, render the entire final frame instantly — no typing, no spinner.

---

## 5. Interactions & behavior checklist
- Install-bar **copy button** actually copies `npx morf install <git-url>` (clipboard API), flips to `copied ✓` for ~1.4s.
- Nav gains a bottom border once `scrollY > 10`.
- Before/after **tabs** switch content client-side, active tab gets cyan border.
- FAQ uses native `<details>`/`<summary>`, custom +/– indicator, no JS needed.
- Smooth-scroll anchors from nav.
- Terminal plays once on scroll-into-view; replay restarts it cleanly (cancel pending timers).

---

## 6. Quality bar (non-negotiable)
- **Responsive, mobile-first.** Grids collapse to 1 column ≤760px; nav links hide (keep GitHub button) ≤600px; before/after stacks with rotated arrow; tables get horizontal scroll wrappers.
- **Accessibility:** semantic headings hierarchy, alt/aria-label on logo SVGs, visible keyboard focus, color contrast ≥ 4.5:1 for text, `prefers-reduced-motion` honored everywhere.
- **Performance:** no frameworks needed — vanilla HTML/CSS/JS is fine (reference is a single file). If you prefer to scaffold (e.g. Vite + vanilla or Astro) for deployability, keep output static and dependency-light. Fonts via Google Fonts with `preconnect`.
- **SEO/meta:** `<title>morf — one agent, every tool</title>`, meta description, Open Graph tags (og:title, og:description; generate a simple og-image if easy), favicon from the icon-only logo mark.
- No console errors. Lighthouse-clean (90+ across the board is the target).

---

## 7. Deliverables
1. The site, ready to deploy on Vercel/Netlify/GitHub Pages (static output).
2. A `README.md` for the site repo: what it is, how to run locally, how to deploy.
3. Favicon (SVG) generated from the logo mark.
4. Keep all outbound links (`GitHub`, `LinkedIn`, `npm`, repo URLs) as `#` placeholders and the footer name as `[ your name ]` — the owner fills these in.

## 8. What NOT to do
- Don't add sections beyond §3 (no testimonials, no pricing, no newsletter).
- Don't use the gradient outside the allowed list in §2.
- Don't replace the terminal animation with a static image or video.
- Don't invent stats, star counts, download numbers, or fake testimonials — everything on the page must be true to the product as described here.
- Don't switch to a light theme.

— end of spec —
