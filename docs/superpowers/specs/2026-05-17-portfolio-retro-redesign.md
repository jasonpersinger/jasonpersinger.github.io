# Portfolio Redesign — Retro Terminal Aesthetic

**Date:** 2026-05-17
**Status:** Approved

---

## Overview

Full visual and content rewrite of `index.html` and `styles.css`. The goal is a retro terminal/BBS aesthetic using modern CSS — Space Mono typography, a warm custom palette, and structural chrome that reads "terminal" while keeping body prose fully legible. No build tooling; the site remains static HTML/CSS deployable directly to GitHub Pages.

---

## Visual System

### Palette

```css
--pitch-black: #171511;   /* page background */
--evergreen:   #233225;   /* panel / card background */
--tea-green:   #bfdbc3;   /* secondary text, links, service tags */
--bone:        #eae1cf;   /* primary headings and body text */
--chocolate:   #cf6604;   /* accent — nav brand, eyebrow prefix, cursor, tag brackets */

/* derived */
--muted:  #7a8f7c;        /* prose body, muted labels */
--border: #2d3f2f;        /* all borders and dividers */
--panel:  #1d1f1a;        /* non-featured card background */
```

### Typography

- **Space Mono** (Google Fonts, 400 + 700) — all headings (`h1`–`h3`), nav, eyebrows, labels, project tags, node names, repo names, footer. Loaded via `<link>` in `<head>`.
- **System sans-serif** (`ui-sans-serif, system-ui, sans-serif`) — all body prose (card descriptions, intro paragraph, homelab node descriptions, CV copy). Fast, readable, no extra request.

### Decorative conventions

- Section eyebrows: `// section-name` — the `//` prefix is rendered in `--chocolate` via `::before`
- Project tags: `[ lang · type ]` in Space Mono, `--chocolate` color
- Hero headline: block cursor (`▌`) after the last word, CSS `@keyframes blink` (step-end, 0.9s)
- Nav brand: `JASON PERSINGER` in Space Mono, `--chocolate`
- No scanlines, no marquee, no `<blink>` — retro signal comes from typeface and palette, not gimmicks
- Footer: `// updated may 2026` format

---

## Page Structure

Single-page layout, top to bottom:

```
nav           sticky, backdrop-filter blur
hero          two-column: copy left, profile card right
cv-strip      two-column banner
projects      section — 7 cards in 3-col grid
homelab       section — new (see below)
repo-index    section — directory-style list
footer
```

---

## Content Changes

### Projects section

**Remove from Featured Work:**
- Sloplocks
- emarx
- GrowSeason

**Remaining cards (7 total):**

| Card | Lang tag | Status tag |
|---|---|---|
| hollerworks | HTML | Job board |
| TURBOTRAINER | JavaScript | Bookmarklet |
| Peambot | C++ | Voice AI |
| NIXKEY | HTML | Storefront |
| jasonpersinger-cv | HTML | Resume |
| NOKENIX | Shell | Distro |
| CYD ESP32 Pi-hole Dashboard | C++ | ESP32 |

Featured cards (darker `--evergreen` bg): hollerworks, TURBOTRAINER.

Project tags use `[ lang · type ]` format, e.g. `[ c++ · esp32 ]`.

### Removed section

The entire "Summary Method" section (`<section class="section split">`) is removed.

### Profile card — Languages row

Replace the single `Languages` stat row with two rows:

| Label | Value |
|---|---|
| Tools | Docker · Bash · Git · AI APIs |
| Tinkering in | JS · Python · C++ · Rust |

This accurately frames operational fluency vs. exploratory / AI-assisted use.

### Repo index

Remove `sloplocks`, `emarx`, and `growseason` entries to match the project card removals.

---

## Homelab Section (New)

Inserted between the projects section and the repo index. Anchor: `id="homelab"`. Add `homelab` link to nav.

### Section heading

```
eyebrow: // homelab
h2:      HOMELAB
```

### Intro paragraph

> Running self-hosted infrastructure on hardware I control — because owning your stack teaches you things SaaS never will. The "void" network spans a daily driver, a Pi Docker host, and a dedicated Home Assistant machine.

### Layout

voidbox spans full width on top. voidberry and voidframe sit in a two-column row below.

```
┌──────────────────────────────────────────┐
│                 voidbox                  │
└──────────────────────────────────────────┘
┌─────────────────────┐ ┌──────────────────┐
│      voidberry      │ │    voidframe     │
└─────────────────────┘ └──────────────────┘
```

### Node cards

Each node card contains:
- **Header row:** node name (`--chocolate`, Space Mono 700) + hardware spec (Space Mono 9px, `--muted`)
- **Service tag row:** flex-wrapped `[ service ]` tags (`--tea-green`, `--evergreen` bg, `--border` border)
- **Description paragraph:** body text in system sans-serif, `--muted`

#### voidbox
- **Spec:** Custom (MSI MS-7C87) · Ryzen 7 5700G · 32 GB · 480 GB btrfs
- **Tags:** CachyOS · KDE Plasma 6 · KWin (Wayland) · fish · ghostty · Docker · Btrfs · Tailscale · AUR
- **Description:** The daily driver and project bench. CachyOS on Plasma 6 / Wayland, fish in ghostty with BigBlueTerm Nerd Font. Ryzen 7 5700G APU driving a 1440p / 100 Hz panel on integrated Vega; a discrete RDNA card is queued as the next upgrade. Btrfs root, Tailscale-attached — where most projects originate before pieces migrate out to voidberry or voidframe.

#### voidberry
- **Spec:** Raspberry Pi 4B · 4 GB
- **Tags:** Pi-hole · Nginx Proxy Manager · Homepage · Uptime Kuma · Paperless-ngx · Actual Budget · Tailscale · rclone
- **Description:** Docker stack running on a USB SSD. Tailscale punches through CGNAT for remote access; rclone + systemd timers handle automated Google Drive backups.

#### voidframe
- **Spec:** Dell Inspiron 3650
- **Tags:** Home Assistant OS · Zigbee2MQTT · SLZB-06p7u · HACS · T-Higrow sensors · Tuya Zigbee
- **Description:** Dedicated Home Assistant machine with a Zigbee coordinator, LILYGO T-Higrow plant sensors (soil moisture, conductivity, light, temp) on solar panels, and a Tuya device fleet. Roadmap: HA MCP server integration for Claude Desktop and a self-hosted voice assistant.

---

## CSS Architecture

`styles.css` is a full rewrite. Key structural decisions:

- All values via CSS custom properties (defined in `:root`)
- Layout via CSS Grid (`grid-template-columns`, `gap`) — no floats, no flexbox hacks
- Responsive: single breakpoint at `860px` collapses hero, cv-strip, homelab bottom row to single column; `620px` collapses project grid and repo rows
- `clamp()` for fluid hero `h1` font size
- Space Mono loaded via Google Fonts `<link>` (two weights: 400, 700)
- Cursor blink: CSS-only `@keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }` with `animation-timing-function: step-end`
- Sticky nav: `position: sticky; top: 0; backdrop-filter: blur(10px)`
- No JavaScript

---

## Files Modified

| File | Change |
|---|---|
| `index.html` | Full rewrite — content changes, new homelab section, updated nav, updated profile card |
| `styles.css` | Full rewrite — new palette, Space Mono typography, terminal chrome |

No new files. No build step. No dependencies beyond the Google Fonts `<link>`.

---

## Out of Scope

- No JS animations (typing effect deferred — can be added later)
- No changes to `CNAME`, `README.md`, or `.nojekyll`
- No changes to linked external sites (hollerworks, jasonpersinger.cv, etc.)
