# GEMINI.md — Mugdha Roy Personal Portfolio

## Project Overview
This repository contains the personal portfolio website for **Mugdha Roy** ("Two modes. One me."), showcasing both her career as a **Tech Analyst at HCLTech** and her work as the founder and event curator of **frekvncy** in Lucknow.

The site is built as a lightweight, zero-dependency, single-file static web application ([`index.html`](index.html)) with embedded CSS and vanilla JavaScript.

### Repository Files
- [`index.html`](index.html): Single-file portfolio web application (semantic HTML5, embedded CSS3, vanilla JS).
- [`README.md`](README.md): Public project overview, feature highlights, directory structure, and local preview instructions.
- [`SESSIONS.md`](SESSIONS.md): Chronological development session log tracking changes and decisions across sessions.
- [`GEMINI.md`](GEMINI.md): Workspace architecture, design tokens, and development guidelines.
- [`.agents/skills/update-project-docs/SKILL.md`](.agents/skills/update-project-docs/SKILL.md): Workspace skill for synchronizing `SESSIONS.md`, `GEMINI.md`, and `README.md`.
- [`og-image.jpg`](og-image.jpg): Square 1200×1200 Open Graph / social share image (`og:image`, `twitter:image` with `twitter:card=summary`).
- [`favicon.ico`](favicon.ico) (16/32/48), [`favicon-32.png`](favicon-32.png), [`apple-touch-icon.png`](apple-touch-icon.png) (180×180, full-bleed): Favicons based on the rotated `MR` logo mark on `#1b1020` with `#ff83c9` accent.
- [`LICENSE`](LICENSE): The Unlicense (public domain).

---

## Architecture & Key Patterns

### 1. Single-File Structure ([`index.html`](index.html))
- **HTML5 Semantic Layout**: Uses `<header>`, `<main>`, `<section>`, `<article>`, `<blockquote>`, and `<footer>` inside a centered `.shell` container (`max-width: 1192px`).
- **Embedded Styles (`<style>`)**: Compact, modern CSS using custom properties (CSS variables), CSS Grid, Flexbox, `clamp()` fluid typography, and keyframe animations (`float`, `twinkle`).
- **Vanilla JavaScript (`<script>`)**: An IIFE that manages interactive dual-mode switching (`tech` vs. `events`), ARIA states, theme colors, URL hash syncing (`#tech` / `#events`), and dynamic copyright year.

### 2. Dual-Mode Switching (`tech` & `events`)
The core interactive concept of the portfolio is switching between two personas controlled by `document.body.dataset.mode`:
- **`data-mode="tech"` (Default)**:
  - Highlights HCLTech Tech Analyst role, server/infrastructure credentials (CompTIA Server+, Windows Server), PowerShell/DSC, and DevOps foundations.
  - Primary external CTA points to LinkedIn (`https://www.linkedin.com/in/mugdha-roy-137a1520b`).
- **`data-mode="events"`**:
  - Highlights **frekvncy**, private-villa community gatherings in Lucknow, guest curation, and the featured Diwali Bash (`https://frekvncy.vercel.app/diwali-bash`).
  - Shifts the color palette to a warmer plum/magenta (`--bg: #2a1028`, `--accent: #ffafd9`).

#### How Mode Switching Works:
1. **CSS Visibility Toggles**:
   - Elements with `.tech-only` or `.event-only` are hidden by default (`display: none`) and revealed as block elements (`display: block`) via `body[data-mode="tech"] .tech-only` and `body[data-mode="events"] .event-only`.
   - Grid containers (`.cards`, `.lineup`) explicitly restore `display: grid` when their matching mode is active.
2. **JavaScript Content Map (`content` object)**:
   - Dynamic text nodes (hero eyebrow, title lines, subhead, orbit labels, section headings, and contact box copy/links) are updated via `setMode(mode, updateHash)`.
3. **Triggers**:
   - `#tech-button` and `#events-button` inside the `.mode-panel` switcher.
   - `#header-mode-toggle` pill button in the top navigation bar.
   - Initial URL hash detection (`#events` on page load switches to Events mode automatically).

---

## Design System & Styling

### Typography
Loaded from Google Fonts:
- **Display / Headings (`--display`)**: `'Space Grotesk', system-ui, sans-serif`
- **Body / UI (`--font`)**: `'DM Sans', system-ui, sans-serif`

### Color Tokens
| Token | `tech` Mode (Default) | `events` Mode (`body[data-mode="events"]`) | Purpose |
| :--- | :--- | :--- | :--- |
| `--bg` | `#1b1020` | `#2a1028` | Page background & `meta[name="theme-color"]` |
| `--fg` | `#fff7fc` | `#fff7fc` | Primary text color |
| `--muted` | `#d4b8ca` | `#e1bad6` | Secondary / body text color |
| `--surface` | `#2a1830` | `#431d3d` | Card & panel backgrounds |
| `--accent` | `#ff83c9` | `#ffafd9` | Primary brand accent, buttons, highlights |
| `--accent-deep` | `#742a62` | `#85356d` | Deep gradient stop for the hero orb |
| `--line` | `rgba(255,190,226,.20)` | `rgba(255,192,225,.22)` | Borders and subtle dividers |

### Responsive Breakpoints
- **`@media (max-width: 900px)`**: Adjusts hero grid spacing, scales down the `.orb`, hides `.mode-hint`, and switches `.cards` to a 2-column layout (with the 3rd card spanning 2 columns).
- **`@media (max-width: 650px)`**: Mobile layout—stacks `.hero-grid` vertically with `.hero-art` on top (`order: -1`), collapses `.cards` and `.lineup` to a single column, stacks `.mode-panel` and `.contact-box`, and simplifies navigation.
- **`@media (prefers-reduced-motion: reduce)`**: Disables animations, transitions, and smooth scrolling for accessibility.

---

## Development Guidelines

1. **Zero Build Step**:
   - Do not introduce bundlers, frameworks, or external JS libraries unless explicitly requested. Keep everything self-contained in [`index.html`](index.html) (or minimal static assets if expanded).
2. **Adding or Editing Mode-Specific Content**:
   - For **hero, section headers, or contact CTAs**, update both `content.tech` and `content.events` in the `<script>` block AND ensure the initial static HTML in `<main>` matches the `tech` default state.
   - For **cards or feature blocks**, add the appropriate `.tech-only` or `.event-only` class to the container or element.
3. **Accessibility (a11y)**:
   - Maintain `aria-pressed="true|false"` on `.mode-btn` toggles and dynamic `aria-label` updates on `#header-mode-toggle`.
   - Keep visible `:focus-visible` outlines (`outline: 3px solid var(--accent)`).
   - Ensure decorative elements (`.hero-art`, `.glyph`, `.bolt`, `.quote-mark`) retain `aria-hidden="true"`.
4. **External Links**:
   - Always include `target="_blank" rel="noopener noreferrer"` on external links (LinkedIn, frekvncy / Diwali Bash).
5. **Local Preview**:
   - Open [`index.html`](index.html) directly in any browser or serve the directory with a local static server (e.g., `npx serve .` or `python -m http.server`).
6. **Social Image & Favicons**:
   - `og:url`, `og:image`, `og:image:secure_url`, `twitter:image`, and `<link rel="canonical">` use absolute URLs on `https://frekvncy.github.io/Mugdha-Roy/`. Social scrapers (Facebook, LinkedIn, WhatsApp, X) ignore relative image paths, so keep them absolute.
   - Keep the OG image as a JPEG under ~300 KB (WhatsApp skips larger preview images).
   - Keep the OG image square (1200×1200) and `twitter:card` as `summary`; `summary_large_image` would crop a square image to 2:1.
7. **Documentation & Session Sync**:
   - Whenever features, styles, copy, or project structure change, use the [`update-project-docs`](.agents/skills/update-project-docs/SKILL.md) skill to update [`SESSIONS.md`](SESSIONS.md), [`GEMINI.md`](GEMINI.md), and [`README.md`](README.md).
