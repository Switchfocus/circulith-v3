# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Circulith-v3 is a static landing page for a Luxembourg-based tyre recycling company. The entire site lives in a single `index.html` file — no build tools, no package manager, no frameworks.

## Running Locally

Use VS Code's Live Server extension (configured for port 5502):

```bash
# Or use any static server:
python -m http.server 5502
npx serve .
```

No build step required.

## Architecture

Everything is in `index.html`:
- **CSS** — embedded in `<style>` tag (~772 lines)
- **JS** — embedded in `<script>` tag (~68 lines)

**Page sections (in order):**
1. `<nav>` — fixed header with mobile hamburger toggle
2. `.hero` — headline with breathing orb CSS animation
3. `.numbers-bar` — stats with count-up animation on scroll
4. `.section-about` — 2-column about + process layout
5. `.section-outputs` — 3-column output stream cards
6. `.section-why` — 4-row comparison table
7. `.section-cta` — email signup call-to-action
8. `<footer>` — SVG logo and links

## CSS System

CSS custom properties defined in `:root`:
- `--bg`: #f7f5f0 (cream background)
- `--ink`: #141412 (near-black text)
- `--green`: #1a9e5c (brand primary)
- `--green-l`: #d4f0e2 (light green accent)
- `--mid`: #6b6b66 (muted text)
- `--faint` / `--rule`: overlay and border colors

**Fonts** (Google Fonts): Fraunces (serif, headings) + Geist Mono (monospace, body)

**Breakpoints:** 960px (tablet), 480px (mobile)

## JavaScript Patterns

- **Intersection Observer** (`revealObs`) — adds `.visible` class to trigger CSS fade-in/translate-Y animations as elements enter the viewport
- **Intersection Observer** (`numObs`) — fires `countUp()` on `.numbers-bar` once
- **`countUp(el, target, duration)`** — animates a number from 0 to target using `requestAnimationFrame`
- **`toggleNav()`** — hamburger ↔ X toggle for mobile menu
