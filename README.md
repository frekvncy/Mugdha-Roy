# Mugdha Roy — Personal Portfolio

> **Two modes. One me.**  
> Personal portfolio website for **Mugdha Roy** — showcasing her dual career as a **Tech Analyst at HCLTech** and the founder & event curator of **frekvncy** in Lucknow.

---

## ✨ Overview

Rather than splitting two distinct sides into separate profiles, this portfolio treats them as an interactive dual-mode experience inside a single, zero-dependency static web page ([`index.html`](index.html)):

- **⌘ Tech Analyst Mode (`#tech`, default)**
  - Highlights Mugdha's role at **HCLTech**, systems-thinking mindset, and infrastructure/automation foundations.
  - Showcases Skillsoft training credentials across **CompTIA Server+**, **Windows Server**, **PowerShell**, **Desired State Configuration (DSC)**, and **DevOps foundations**.
  - Connects directly to [LinkedIn](https://www.linkedin.com/in/mugdha-roy-137a1520b).
- **✳ Event Organizer Mode (`#events`)**
  - Highlights **frekvncy**, Mugdha's independent community-first event curation in **Lucknow**.
  - Showcases intimate private-villa gatherings, nostalgic icebreakers (2000s Bollywood Antakshari, Uno No-Mercy, Tambola), curated guest lists, and warm hospitality.
  - Features the [Diwali Bash](https://frekvncy.vercel.app/diwali-bash) and transitions the UI into a warmer plum-magenta palette.

---

## 🎨 Features & Design Highlights

- **Interactive Dual-Mode Switcher**: Toggle between *Tech Analyst* and *Event Organizer* from either the top navigation pill (`#header-mode-toggle`) or the hero switcher panel (`.mode-panel`), complete with URL hash syncing (`#tech` / `#events`) and dynamic `<meta name="theme-color">` updates.
- **Dynamic Theme & Visuals**: Smooth CSS custom property transitions (`--bg`, `--surface`, `--accent`, `--glow`) paired with a floating radial-gradient orb and rotating glassmorphic status badges.
- **Responsive Across Devices**: Fluid typography using `clamp()`, adaptive CSS Grid layouts at `900px` and `650px` breakpoints, and first-class mobile ergonomics.
- **Accessible by Default**: Semantic HTML5 landmarks, `aria-pressed` toggle states, dynamic `aria-label` updates, high-visibility `:focus-visible` outlines, and full `@media (prefers-reduced-motion: reduce)` support.
- **Zero Dependencies**: Built with pure HTML5, modern CSS3, and vanilla JavaScript in a single self-contained [`index.html`](index.html) file.

---

## 📁 Project Structure

```text
Mugdha-Roy/
├── .agents/
│   └── skills/
│       └── update-project-docs/
│           └── SKILL.md     # Agent skill to sync SESSIONS.md, GEMINI.md, and README.md
├── index.html               # Single-file portfolio application (HTML + CSS + JS)
├── GEMINI.md                # Workspace rules, design tokens, and architecture guide
├── README.md                # Project overview and usage documentation
├── SESSIONS.md              # Chronological log of development sessions and changes
└── LICENSE                  # The Unlicense (Public Domain)
```

---

## 🚀 Local Preview

Because the site has no build step or external runtime dependencies, you can preview it immediately:

1. **Open directly**: Double-click [`index.html`](index.html) to open it in any browser.
2. **Or serve locally**:
   ```bash
   # Using Python
   python -m http.server 8000

   # Or using Node.js
   npx serve .
   ```
   Then open `http://localhost:8000` (or `http://localhost:8000/#events` to launch directly into Event Organizer mode).

---

## 🔗 Links

- **LinkedIn**: [Mugdha Roy](https://www.linkedin.com/in/mugdha-roy-137a1520b)
- **frekvncy — Diwali Bash**: [frekvncy.vercel.app/diwali-bash](https://frekvncy.vercel.app/diwali-bash)

---

## 📄 License

Released into the public domain under [The Unlicense](LICENSE).
