# Failure Modes in Agentic AI: Tutorial Site

Static site for the EMNLP 2026 tutorial **"Failure Modes in Agentic AI: From Reproducible Triggers and Diagnostics to Reliable Fixes"**, served at https://failure-mode-agent.github.io.

Built with Astro 5, based on the `v1` template from [`RAGEN-AI/ragen-ai.github.io`](https://github.com/RAGEN-AI/ragen-ai.github.io). Layout mirrors the structure of academic tutorial sites such as [Foundation Models Meet Embodied Agents (ICCV 2025)](https://foundation-models-meet-embodied-agents.github.io/iccv2025_tutorial/).

## Layout

```
.
├── .github/workflows/deploy.yml  # Build and deploy to GitHub Pages on push to main
├── astro.config.mjs        # Site URL / base path via SITE_URL, SITE_BASE
├── package.json            # astro 5.x only
├── public/                 # Static assets served at /
│   ├── favicon.svg
│   └── speakers/           # Presenter headshots
└── src/
    ├── layouts/Layout.astro      # HTML shell, meta tags, fonts, design tokens, header / footer slots
    ├── pages/index.astro         # Composes the single-page site (section order)
    ├── styles/global.css         # Shared section scaffolding (.wrap, .section, .label, .split)
    └── components/               # One per section, in page order
        ├── Header.astro          # Sticky nav with section anchors
        ├── Hero.astro            # Title, subtitle, venue, quick-link buttons
        ├── Abstract.astro        # Tutorial abstract
        ├── Schedule.astro        # Time-budgeted table for the 3.5-hour slot
        ├── Outline.astro         # 5 parts: Part 1 overview, Parts 2-5 failure / diagnostic / fix cards
        ├── ReadingList.astro     # Reading list, grouped by part
        ├── Speakers.astro        # Presenter cards (photo, affiliation, homepage)
        ├── Contact.astro         # Per-presenter email list
        └── Footer.astro          # Copyright, template attribution
```

## Develop

```bash
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

`.github/workflows/deploy.yml` builds the site and publishes it to GitHub Pages at `https://failure-mode-agent.github.io` on every push to `main`. Adjust the deployment target via env vars at build time:

```bash
SITE_URL="https://failure-mode-agent.github.io" SITE_BASE="/" npm run build
```

If the site is published under a subpath (e.g. `username.github.io/agent-failure-modes`), pass `SITE_BASE="/agent-failure-modes/"`.

## Editing content

Site content follows the EMNLP 2026 tutorial proposal (`acl_latex.tex` and its `custom.bib`). When the proposal changes, update the matching component. All tutorial-specific content lives in the component frontmatter (the JS block at the top of each `.astro` file):

- **Title, subtitle, venue, quick links:** `src/components/Hero.astro`. Set `slidesUrl` to turn the inactive "Slides" button into a live link.
- **Page title and meta description:** `src/pages/index.astro` and `src/layouts/Layout.astro`.
- **Abstract:** `src/components/Abstract.astro` (proposal abstract).
- **Schedule rows:** `rows` array in `src/components/Schedule.astro` (proposal schedule table).
- **Outline:** `parts` array in `src/components/Outline.astro` (proposal Tutorial Outline). Part 1 supplies its own `columns`; Parts 2-5 use `failures`, `diagnostics`, `fixes`, and optional `challenges`.
- **Reading list:** `sections` array in `src/components/ReadingList.astro` (proposal Reading List; titles, venues, and links from `custom.bib`). `recommended: true` adds the star; `label` adds a short-name tag when the paper title lacks the name the tutorial uses (e.g. VeRL for HybridFlow).
- **Presenter cards:** `speakers` array in `src/components/Speakers.astro`. Photos are the proposal headshots in `public/speakers/`; optional `zoom` and `shift` reproduce the proposal's per-photo framing.
- **Contact emails:** `contacts` array in `src/components/Contact.astro`, and the Contact button `mailto` in `Hero.astro`.
- **Section order:** `src/pages/index.astro`. Keep the nav links in `Header.astro` in the same order. Every section uses the shared `.section`, `.wrap`, and `.section-head` classes from `src/styles/global.css`; sections are separated by hairline rules, not background colors.

Styles for each section live in scoped `<style>` blocks at the bottom of the same file.

## Style rules

- No em-dashes (U+2014) or en-dashes (U+2013) anywhere in the source. Use commas, periods, semicolons, colons, parentheses, or hyphens instead. This is enforced project-wide.
- Design context (audience, personality, principles) lives in `.impeccable.md`. The direction is rigorous and editorial: typography, hairline rules, and whitespace instead of cards, gradients, or pill buttons.
- Color: OKLCH tokens in `Layout.astro`. Neutrals are tinted toward the brand indigo (`--brand`, about `#2a2f6c`); the vermilion `--rubric` marks part numbers, stars, and failure labels only. Every text color clears WCAG AA on both paper tones.
- Typography: Archivo semi-condensed (`--font-display` / `--font-heading`) for the hero, section, part, session, and reading-list titles; Archivo (`--font-sans`) for navigation, labels, metadata, and times with tabular numerals; Literata (`--font-serif`) for reading text and italic subtitles. No monospace.

## Attribution

Template skeleton adapted from `RAGEN-AI/ragen-ai.github.io` (`src_v1_backup/`).
Tutorial content follows the EMNLP 2026 tutorial proposal.
