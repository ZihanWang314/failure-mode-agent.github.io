# FAGEN Tutorial Site

Static site for the EMNLP 2026 tutorial **"Failure Modes in Agentic AI: Reproducible Triggers, Trace Diagnostics, and Verified Fixes"** (FAGEN).

Built with Astro 5, based on the `v1` template from [`RAGEN-AI/ragen-ai.github.io`](https://github.com/RAGEN-AI/ragen-ai.github.io). Layout mirrors the structure of academic tutorial sites such as [Foundation Models Meet Embodied Agents (ICCV 2025)](https://foundation-models-meet-embodied-agents.github.io/iccv2025_tutorial/).

## Layout

```
website/
├── astro.config.mjs        # Site URL / base path via SITE_URL, SITE_BASE
├── package.json            # astro 5.x only
├── public/                 # Static assets served at /
│   ├── favicon.svg
│   └── background-blurred.svg
└── src/
    ├── layouts/Layout.astro      # HTML shell, fonts, header / footer slots
    ├── pages/index.astro         # Composes the single-page site
    ├── styles/global.css         # Site-wide overrides only
    └── components/
        ├── Header.astro          # Sticky nav with section anchors
        ├── Hero.astro            # Title, venue, quick links, stats row
        ├── Abstract.astro        # Motivation, what you will learn, audience
        ├── Outline.astro         # 5 parts × (failure / diagnostic / fix) cards
        ├── Schedule.astro        # 3-hour slot, time-budgeted table
        ├── ReadingList.astro     # Curated refs, grouped by part
        ├── Speakers.astro        # 8 presenter cards with bios
        ├── Contact.astro         # Get-in-touch, contribute, mailing list
        └── Footer.astro          # Copyright, template attribution
```

## Develop

```bash
cd website
npm install
npm run dev
```

The dev server serves on http://localhost:4321 by default.

## Build

```bash
npm run build
```

Output goes to `dist/`. Preview the production build with `npm run preview`.

## Deploy

Designed to deploy to GitHub Pages at `https://failure-mode-agent.github.io`. Adjust the deployment target via env vars at build time:

```bash
SITE_URL="https://failure-mode-agent.github.io" SITE_BASE="/" npm run build
```

If the site is published under a subpath (e.g. `username.github.io/fagen-tutorial`), pass `SITE_BASE="/fagen-tutorial/"`.

## Editing content

All tutorial-specific content lives in the component frontmatter (the JS block at the top of each `.astro` file):

- **Title, venue, date, quick links:** `src/components/Hero.astro`
- **Abstract paragraphs and learning objectives:** `src/components/Abstract.astro`
- **The 5-part outline (failure / diagnostic / fix lists):** `parts` array at the top of `src/components/Outline.astro`
- **Schedule rows:** `rows` array at the top of `src/components/Schedule.astro`
- **Reading list entries:** `sections` array at the top of `src/components/ReadingList.astro`
- **Presenter cards:** `speakers` array at the top of `src/components/Speakers.astro`
- **Contact emails and companion-venue link:** `src/components/Contact.astro`

Styles for each section live in scoped `<style>` blocks at the bottom of the same file.

## Style rules

- No em-dashes (U+2014) or en-dashes (U+2013) anywhere in the source. Use commas, periods, semicolons, colons, parentheses, or hyphens instead. This is enforced project-wide.
- Brand color: `#2a2f6c` (deep indigo). Accent: `#4a56c9`.
- Typography: Inter, weights 400 / 500 / 600 / 700 / 800.

## Attribution

Template skeleton adapted from `RAGEN-AI/ragen-ai.github.io` (`src_v1_backup/`).
Tutorial content drawn from the EMNLP 2026 proposal draft and the companion FAGEN workshop proposal.
