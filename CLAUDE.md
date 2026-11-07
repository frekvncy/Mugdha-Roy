# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Personal portfolio for Mugdha Roy: one static page with two "modes" — **Tech Analyst** (HCLTech, default, `#tech`) and **Event Organizer** (frekvncy, Lucknow, `#events`). Everything (HTML, CSS, JS) lives in `index.html`. No build step, no package manager, no dependencies beyond Google Fonts (Space Grotesk, DM Sans). There are no tests or linters. Static assets at the root: a square 1200×1200 `og-image.jpg` (kept under ~300 KB for WhatsApp) and a favicon set (`favicon.ico`, `favicon-32.png`, `apple-touch-icon.png`).

The site is deployed to GitHub Pages at https://frekvncy.github.io/Mugdha-Roy/ (via a GitHub Actions workflow on push to `main`). `og:url`, `og:image`, `twitter:image` and `canonical` must be absolute URLs on that domain, because social scrapers ignore relative image paths.

## Preview

```bash
python -m http.server 8000      # or: npx serve .
# http://localhost:8000          → tech mode
# http://localhost:8000/#events  → event mode
```

Opening `index.html` directly in a browser also works.

## How dual-mode works

Mode switching spans three places in `index.html` that must stay in sync:

1. **`<body data-mode="tech|events">`** drives theming. `:root` holds the tech-mode CSS tokens (`--bg`, `--surface`, `--accent`, `--accent-deep`, `--glow`, etc.); `body[data-mode="events"]` overrides them with a warmer plum/magenta palette. Prefer changing tokens over hardcoding colors.
2. **`.tech-only` / `.event-only` classes** show/hide whole blocks per mode. The active rule sets `display:block`, with explicit `display:grid` overrides for `.cards` and `.lineup`. Don't use `display:initial` here (it turned a `<blockquote>` inline and broke the layout). If you add a new grid/flex container that toggles, add a matching override.
3. **The `content` object in the `<script>`** holds per-mode copy for elements whose text changes rather than being hidden (hero text, CTAs, orbit labels, work-section heading, contact box). `setMode()` writes these into elements by ID. Adding a mode-swapped string means adding the key to **both** `content.tech` and `content.events` and adding a line in `setMode()`.

Other `setMode()` details:
- The static HTML is the tech-mode content; keep it identical to `content.tech`, since `setMode('tech')` is never called on load.
- It updates `aria-pressed` on `#tech-button`/`#events-button`, the label and `aria-label` of `#header-mode-toggle`, and `<meta name="theme-color">` (hex values hardcoded to match each mode's `--bg`).
- The hash is read only once on load (`#events` → event mode). Button clicks update it via `history.replaceState`. There is no `hashchange` listener.

Responsive breakpoints are `900px` and `650px`, plus a `prefers-reduced-motion` block. The CSS is minified onto a few very long lines, so use targeted search/replace rather than whole-line edits.

## Documentation sync

The repo keeps `README.md`, `GEMINI.md`, and `SESSIONS.md` in sync with `index.html` (workflow in `.agents/skills/update-project-docs/SKILL.md`). When you change features, tokens, breakpoints, mode behavior, links, or file structure:
- Add to `SESSIONS.md` using `## Session <N> — YYYY-MM-DD` with Summary / Changes Made / Files Touched. Append to the current day's entry instead of creating a duplicate.
- Keep the color tokens table, typography, and breakpoints in `GEMINI.md` matching the `<style>` block.
- Keep the README directory tree and links accurate.
