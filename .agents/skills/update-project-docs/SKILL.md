---
name: update-project-docs
description: >-
  Use this skill to log development progress and synchronize SESSIONS.md, GEMINI.md,
  and README.md whenever features, styles, content, or project structure change,
  or when the user asks to record a session or update project documentation.
---

# Update Project Docs (`SESSIONS.md`, `GEMINI.md`, & `README.md`)

Follow this workflow to keep the repository's documentation and session history accurate and synchronized.

---

## 1. Inspect Recent Changes
Before editing documentation files, inspect what changed in the workspace:
1. Run `git status` and `git diff` (or check recent commits with `git log -n 5 --stat`) to identify all modified, added, or removed files.
2. Review [`index.html`](../../../index.html) if UI structure, CSS tokens, breakpoints, mode-switching logic, or external links were updated.

---

## 2. Update `SESSIONS.md`
Record the current session or update today's session entry in [`SESSIONS.md`](../../../SESSIONS.md):
- **Header Format**: `## Session <N> — YYYY-MM-DD`
- **Summary**: A concise 1–2 sentence overview of the session's goal.
- **Changes Made**: Bullet points describing concrete changes (features added, copy updated, styles refined, bugs fixed).
- **Files Touched**: Markdown file links to every file created or modified during the session.
- If multiple tasks happen on the same day within the same session, append to the latest session entry rather than creating duplicate headers, unless the user explicitly asks for a new session entry.

---

## 3. Update `GEMINI.md`
Review [`GEMINI.md`](../../../GEMINI.md) and update any sections affected by the changes:
- **Project Overview & Repository Structure**: Update if new files, assets, or skills are added.
- **Architecture & Dual-Mode Switching**: Update if new mode-specific classes, DOM IDs, `content` keys, or interactive behaviors are introduced.
- **Design System & Styling**: Keep the **Color Tokens** table, **Typography**, and **Responsive Breakpoints** (`900px`, `650px`, `prefers-reduced-motion`) strictly in sync with `<style>` in [`index.html`](../../../index.html).
- **Development Guidelines**: Add any new conventions or constraints established during the session.

---

## 4. Update `README.md`
Review [`README.md`](../../../README.md) and ensure user-facing documentation reflects the latest state:
- **Overview & Features**: Reflect any new portfolio sections, personas, interactive features, or credentials.
- **Project Structure**: Keep the directory tree accurate whenever files or folders are added/removed.
- **Links & Preview Instructions**: Update external URLs or local preview instructions if changed.

---

## 5. Verification Checklist
Before finishing:
- [ ] All file links in `SESSIONS.md`, `GEMINI.md`, and `README.md` resolve to valid paths in the repository.
- [ ] CSS variables, breakpoints, and mode behavior documented in `GEMINI.md` match [`index.html`](../../../index.html).
- [ ] The directory tree in `README.md` matches the actual workspace layout.
