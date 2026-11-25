# morf-site

The landing page for [morf](https://github.com/romivol/morf-source-code), a CLI that installs AI skills, agents, rules, prompts, hooks and MCP servers from any git repo into seven AI coding tools (Claude Code, OpenCode, Kilo, Codex, Cursor, Copilot, Windsurf), converting each into that tool's native format. Describes morf 2.0.0.

Live at **[morf.tools](https://morf.tools)**.

## What's here

A single static page. Vanilla HTML, CSS and JavaScript, no build step, no dependencies.

```
index.html      the whole site (styles and script inline)
404.html        branded not-found page
og-image.png    Open Graph / social preview (1200x630)
og-image.svg    source for the OG image
robots.txt      crawler directives and sitemap pointer
sitemap.xml     single-page sitemap
vercel.json     clean URLs, security headers, asset caching (Vercel)
netlify.toml    the same headers and caching for Netlify
specs/          design briefs used while building the page
```

Fonts (JetBrains Mono, Inter, Space Grotesk) load from Google Fonts. Everything else is self-contained.

### Notable pieces

- **Terminal animation.** Types the install command, runs a spinner, then reveals the per-tool output. Plays once on scroll into view, with a replay button. Honors `prefers-reduced-motion` by rendering the final frame instantly.
- **Before/after panel.** Tabs show how one source agent is reshaped into Cursor, Kilo and Copilot frontmatter.
- Copy-to-clipboard install bars, conversion matrix, comparison table, FAQ accordions, roadmap.

## Run locally

```sh
python -m http.server 8000
# or
npx serve .
```

Then open http://localhost:8000.

## Deploy

Fully static. The production site is on Vercel with no build command and the repo root as output. Netlify and GitHub Pages work the same way.

If the wordmark or tagline changes, regenerate `og-image.png` from `og-image.svg`, for example with `sharp(svg).resize(1200, 630).png()`.

## License

MIT.
