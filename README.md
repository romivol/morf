# morf — landing page

The marketing site for **morf**, an open-source CLI that installs AI agent primitives
(agents, skills, rules, prompts, hooks, MCP servers) from any git repo into every AI
coding tool at once — **converting** each into that tool's native format rather than
just copying files.

> Tagline: *one agent, every tool* · *Write once. morf it everywhere.*

## What's here

A single static, dependency-free page — vanilla HTML/CSS/JS, no build step.

```
index.html      the whole site (styles + script inline)
404.html        branded not-found page
favicon.svg     icon-only logo mark
og-image.png    Open Graph / social preview (1200×630, raster — scrapers need PNG/JPG)
og-image.svg    source for the OG image
robots.txt      crawler directives + sitemap pointer
sitemap.xml     single-page sitemap
vercel.json     clean URLs, security headers, asset caching (Vercel)
netlify.toml    same headers/caching for Netlify
```

Fonts (JetBrains Mono + Inter) load from Google Fonts. Everything else is self-contained.

### Highlights
- Signature **morph terminal** — types the install command, runs a Braille spinner,
  then reveals the per-tool conversion output. Plays once on scroll into view; `↻ replay`
  restarts it. Honors `prefers-reduced-motion` (renders the final frame instantly).
- Interactive **before/after** panel — tabs reshape a source agent into cursor / kilo /
  copilot native frontmatter.
- Copy-to-clipboard install bars, conversion matrix, comparison table, FAQ accordions.
- Dark terminal aesthetic; the violet→cyan gradient is the only expressive accent.

## Run locally

It's a static file — open `index.html` directly, or serve it for correct relative paths:

```bash
# any static server works
python -m http.server 8000
# or
npx serve .
```

Then visit http://localhost:8000.

## Deploy

Fully static — drop the folder on any host.

- **Vercel** — `vercel` (or import the repo; no build command, output = root).
- **Netlify** — drag the folder into the dashboard, or connect the repo with an empty
  build command and publish directory `.`.
- **GitHub Pages** — push to `main`, enable Pages from the repo root.

## Before you ship

Replace the placeholders:

- outbound links: `GitHub`, `LinkedIn`, `npm`, and the `View on GitHub` / nav CTA hrefs (all `#`)
- the footer name — `[ your name ]`
- the domain: `morf.dev` appears in the `<head>` canonical/OG tags, `robots.txt`, and
  `sitemap.xml`. Swap it for your real production domain so social previews and the
  sitemap resolve correctly.

If you change the wordmark or tagline, regenerate the OG image from `og-image.svg`
(the repo shipped it via `sharp`: `sharp(svg).resize(1200,630).png()`).

## License

MIT.
