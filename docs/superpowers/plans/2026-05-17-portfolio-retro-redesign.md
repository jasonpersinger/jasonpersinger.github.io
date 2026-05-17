# Portfolio Retro Terminal Redesign — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rewrite `index.html` and `styles.css` with a retro terminal/BBS aesthetic using a warm custom palette and Space Mono typography, while adding a new homelab section and removing three project cards and the Summary Method section.

**Architecture:** Two-file static site — complete rewrite of `styles.css` first (so the browser always has valid CSS), then surgical rewrite of `index.html` section by section. No build tooling, no JavaScript, no new files. Deployed directly to GitHub Pages.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, clamp, keyframes), Space Mono via Google Fonts

---

## Files

| File | Change |
|---|---|
| `styles.css` | Full rewrite |
| `index.html` | Full rewrite — new head (Google Fonts), updated nav, hero, projects, homelab section added, repo index pruned, footer updated |

---

## Task 1: Rewrite styles.css

**Files:**
- Modify: `styles.css`

- [ ] **Step 1: Replace styles.css with the complete new stylesheet**

Write the following as the entire contents of `styles.css`:

```css
:root {
  --pitch-black: #171511;
  --evergreen:   #233225;
  --tea-green:   #bfdbc3;
  --bone:        #eae1cf;
  --chocolate:   #cf6604;
  --muted:       #7a8f7c;
  --border:      #2d3f2f;
  --panel:       #1d1f1a;
  color-scheme: dark;
}

* { box-sizing: border-box; }
html { scroll-behavior: smooth; }

body {
  margin: 0;
  min-height: 100vh;
  background: var(--pitch-black);
  color: var(--bone);
  font-family: ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  line-height: 1.6;
}

a { color: inherit; }
h1, h2, h3, p { margin-top: 0; }

/* ── NAV ── */
.site-header {
  position: sticky;
  top: 0;
  z-index: 10;
  background: rgba(23, 21, 17, .92);
  border-bottom: 1px solid var(--border);
  backdrop-filter: blur(12px);
}

.nav {
  width: min(1120px, calc(100% - 32px));
  height: 60px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 24px;
}

.brand {
  font-family: 'Space Mono', monospace;
  font-size: .82rem;
  font-weight: 700;
  color: var(--chocolate);
  text-decoration: none;
  letter-spacing: .06em;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 20px;
  font-family: 'Space Mono', monospace;
  font-size: .72rem;
  color: var(--muted);
}

.nav-links a {
  text-decoration: none;
  color: var(--muted);
}
.nav-links a:hover { color: var(--tea-green); }

/* ── MAIN CONTAINER ── */
main {
  width: min(1120px, calc(100% - 32px));
  margin: 0 auto;
}

/* ── HERO ── */
.hero {
  min-height: calc(100vh - 60px);
  display: grid;
  grid-template-columns: minmax(0, 1fr) 340px;
  align-items: center;
  gap: 48px;
  padding: 56px 0;
}

.eyebrow {
  font-family: 'Space Mono', monospace;
  margin: 0 0 12px;
  font-size: .72rem;
  font-weight: 400;
  letter-spacing: .14em;
  text-transform: uppercase;
  color: var(--muted);
}
.eyebrow::before {
  content: '// ';
  color: var(--chocolate);
}

h1 {
  font-family: 'Space Mono', monospace;
  max-width: 720px;
  margin-bottom: 20px;
  font-size: clamp(1.7rem, 4vw, 3.2rem);
  line-height: 1.1;
  color: var(--bone);
}

.cursor {
  display: inline-block;
  width: .55em;
  height: .82em;
  background: var(--chocolate);
  vertical-align: bottom;
  margin-left: .1em;
  animation: blink .9s step-end infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50%       { opacity: 0; }
}

.intro {
  max-width: 580px;
  color: var(--muted);
  font-size: 1.05rem;
}

.hero-actions {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
  margin-top: 28px;
}

/* ── BUTTONS ── */
.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 40px;
  padding: 0 16px;
  border: 1px solid var(--border);
  border-radius: 3px;
  color: var(--bone);
  text-decoration: none;
  font-family: 'Space Mono', monospace;
  font-size: .75rem;
  font-weight: 700;
}
.button:hover { border-color: var(--tea-green); }
.button.primary {
  background: var(--chocolate);
  border-color: var(--chocolate);
  color: var(--pitch-black);
}
.button.primary:hover { opacity: .88; }

/* ── PROFILE CARD ── */
.profile-card {
  background: var(--evergreen);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 24px;
}

.avatar {
  width: 88px;
  height: 88px;
  border-radius: 50%;
  border: 2px solid var(--chocolate);
  margin-bottom: 16px;
  display: block;
}

.profile-name {
  font-family: 'Space Mono', monospace;
  font-weight: 700;
  font-size: 1rem;
  color: var(--bone);
}

.profile-meta {
  font-family: 'Space Mono', monospace;
  font-size: .72rem;
  color: var(--muted);
  margin-bottom: 18px;
}

.stats {
  display: grid;
  gap: 12px;
  margin: 0;
}

.stats div {
  padding-top: 12px;
  border-top: 1px solid var(--border);
}

.stats dt {
  font-family: 'Space Mono', monospace;
  color: var(--muted);
  font-size: .68rem;
  text-transform: uppercase;
  letter-spacing: .1em;
}

.stats dd {
  margin: 4px 0 0;
  font-size: .9rem;
  color: var(--tea-green);
}

/* ── SECTIONS ── */
.section {
  padding: 56px 0;
  border-top: 1px solid var(--border);
}

.section-heading {
  display: flex;
  align-items: end;
  justify-content: space-between;
  gap: 24px;
  margin-bottom: 24px;
}

.section-intro {
  color: var(--muted);
  font-size: .98rem;
  max-width: 640px;
  margin-bottom: 24px;
  line-height: 1.65;
}

h2 {
  font-family: 'Space Mono', monospace;
  margin-bottom: 0;
  font-size: clamp(1.35rem, 3vw, 1.9rem);
  line-height: 1.15;
  color: var(--bone);
}

/* ── CV STRIP ── */
.cv-strip {
  display: grid;
  grid-template-columns: 360px minmax(0, 1fr);
  gap: 40px;
  align-items: start;
  background: var(--evergreen);
  border: 1px solid var(--border);
  border-radius: 4px;
  padding: 28px;
  margin-bottom: 56px;
}

.cv-copy p {
  color: var(--muted);
  margin-bottom: 20px;
}

.cv-actions {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}

/* ── PROJECT GRID ── */
.project-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 12px;
}

.project-card {
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 3px;
  min-height: 240px;
  padding: 18px;
  display: flex;
  flex-direction: column;
}

.project-card.featured { background: var(--evergreen); }

.project-topline {
  display: flex;
  justify-content: space-between;
  gap: 12px;
  margin-bottom: 14px;
  align-items: center;
}

.project-tag {
  font-family: 'Space Mono', monospace;
  font-size: .68rem;
  color: var(--chocolate);
  letter-spacing: .02em;
}

.status {
  font-family: 'Space Mono', monospace;
  display: inline-flex;
  align-items: center;
  min-height: 22px;
  padding: 0 8px;
  border-radius: 2px;
  font-size: .65rem;
  font-weight: 700;
  color: var(--tea-green);
  border: 1px solid rgba(191, 219, 195, .28);
  white-space: nowrap;
}

h3 {
  font-family: 'Space Mono', monospace;
  margin-bottom: 8px;
  font-size: 1rem;
  color: var(--bone);
}

.project-card p {
  color: var(--muted);
  font-size: .9rem;
  flex: 1;
}

.project-links {
  display: flex;
  gap: 14px;
  flex-wrap: wrap;
  margin-top: auto;
  padding-top: 14px;
  border-top: 1px solid var(--border);
}

.project-links a {
  font-family: 'Space Mono', monospace;
  font-size: .72rem;
  color: var(--tea-green);
  font-weight: 700;
  text-decoration: none;
}
.project-links a:hover { color: var(--bone); }

/* ── HOMELAB ── */
.homelab-top { margin-bottom: 12px; }

.homelab-bottom {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
}

.node-card {
  background: var(--evergreen);
  border: 1px solid var(--border);
  border-radius: 3px;
  padding: 18px;
}

.node-header {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 12px;
  padding-bottom: 12px;
  border-bottom: 1px solid var(--border);
}

.node-name {
  font-family: 'Space Mono', monospace;
  font-size: 1rem;
  font-weight: 700;
  color: var(--chocolate);
}

.node-spec {
  font-family: 'Space Mono', monospace;
  font-size: .68rem;
  color: var(--muted);
}

.service-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
  margin-bottom: 12px;
}

.service-tag {
  font-family: 'Space Mono', monospace;
  font-size: .65rem;
  background: rgba(191, 219, 195, .05);
  border: 1px solid var(--border);
  color: var(--tea-green);
  padding: 2px 8px;
  border-radius: 2px;
}

.node-card p {
  color: var(--muted);
  font-size: .9rem;
  line-height: 1.65;
}

/* ── REPO LIST ── */
.repo-list {
  border: 1px solid var(--border);
  border-radius: 3px;
  overflow: hidden;
}

.repo-row {
  min-height: 50px;
  display: grid;
  grid-template-columns: minmax(0, 1fr) 120px;
  align-items: center;
  gap: 16px;
  padding: 0 16px;
  background: var(--panel);
  border-bottom: 1px solid var(--border);
  text-decoration: none;
}
.repo-row:last-child { border-bottom: 0; }
.repo-row:hover { background: var(--evergreen); }

.repo-row span:first-child {
  font-family: 'Space Mono', monospace;
  font-size: .8rem;
  font-weight: 700;
  color: var(--tea-green);
}
.repo-row span:last-child {
  font-family: 'Space Mono', monospace;
  font-size: .72rem;
  color: var(--muted);
  text-align: right;
}

/* ── FOOTER ── */
.footer {
  width: min(1120px, calc(100% - 32px));
  margin: 0 auto;
  padding: 28px 0 44px;
  color: var(--muted);
  display: flex;
  justify-content: space-between;
  gap: 16px;
  border-top: 1px solid var(--border);
  font-family: 'Space Mono', monospace;
  font-size: .72rem;
}
.footer a { color: var(--muted); text-decoration: none; }
.footer a:hover { color: var(--tea-green); }

/* ── RESPONSIVE ── */
@media (max-width: 860px) {
  .hero {
    grid-template-columns: 1fr;
    min-height: auto;
  }
  .cv-strip {
    grid-template-columns: 1fr;
  }
  .homelab-bottom {
    grid-template-columns: 1fr;
  }
  .profile-card {
    max-width: 440px;
  }
  .project-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (max-width: 620px) {
  .nav {
    height: auto;
    min-height: 60px;
    align-items: flex-start;
    flex-direction: column;
    justify-content: center;
    padding: 10px 0;
  }
  .nav-links {
    width: 100%;
    overflow-x: auto;
    padding-bottom: 2px;
  }
  .project-grid {
    grid-template-columns: 1fr;
  }
  .repo-row {
    grid-template-columns: 1fr;
    gap: 2px;
    padding: 10px 14px;
  }
  .repo-row span:last-child {
    text-align: left;
  }
  .footer {
    flex-direction: column;
  }
}
```

- [ ] **Step 2: Verify CSS loads without errors**

Open `index.html` in a browser (e.g. `firefox index.html` or `xdg-open index.html`).

The page will look broken because the HTML classes haven't been updated yet — that's expected. Check the browser console (F12) for any CSS parse errors. There should be none.

- [ ] **Step 3: Commit**

```bash
git add styles.css
git commit -m "Rewrite styles.css with retro terminal palette and Space Mono typography"
```

---

## Task 2: Update index.html head and nav

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace the `<head>` block**

Replace everything between `<head>` and `</head>` with:

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="GitHub portfolio for Jason Persinger: hardware dashboards, self-hosted assistants, command-line tools, web apps, and Linux customization projects.">
  <title>Jason Persinger | GitHub Portfolio</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
```

- [ ] **Step 2: Replace the `<header>` / nav block**

Replace the existing `<header class="site-header">...</header>` with:

```html
<header class="site-header">
  <nav class="nav" aria-label="Primary">
    <a class="brand" href="/">JASON PERSINGER</a>
    <div class="nav-links">
      <a href="#projects">projects</a>
      <a href="#homelab">homelab</a>
      <a href="#cv">cv</a>
      <a href="#repo-index">repos</a>
      <a href="https://github.com/jasonpersinger">github</a>
    </div>
  </nav>
</header>
```

- [ ] **Step 3: Verify in browser**

Reload `index.html`. The nav should now show `JASON PERSINGER` in chocolate/orange on the left and lowercase monospace links on the right. Space Mono should be loading (check Network tab if unsure).

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "Update head (Space Mono font) and nav markup"
```

---

## Task 3: Rewrite hero section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace the hero section**

Replace the existing `<section class="hero" ...>...</section>` with:

```html
<section class="hero" aria-labelledby="page-title">
  <div class="hero-copy">
    <p class="eyebrow">github portfolio</p>
    <h1 id="page-title">Practical software, hardware, and self-hosted tools.<span class="cursor" aria-hidden="true"></span></h1>
    <p class="intro">
      I build compact dashboards, command-line utilities, embedded projects, and personal web apps that solve specific jobs without extra ceremony.
    </p>
    <div class="hero-actions" aria-label="Profile links">
      <a class="button primary" href="https://github.com/jasonpersinger">GitHub profile</a>
      <a class="button" href="https://jasonpersinger.cv">Resume site</a>
    </div>
  </div>
  <aside class="profile-card" aria-label="Profile summary">
    <img class="avatar" src="https://avatars.githubusercontent.com/u/22330057?v=4" alt="Jason Persinger GitHub avatar">
    <div>
      <div class="profile-name">Jason Persinger</div>
      <div class="profile-meta">Roanoke, VA</div>
    </div>
    <dl class="stats">
      <div>
        <dt>Focus</dt>
        <dd>Web, hardware, CLI</dd>
      </div>
      <div>
        <dt>Tools</dt>
        <dd>Docker · Bash · Git · AI APIs</dd>
      </div>
      <div>
        <dt>Tinkering in</dt>
        <dd>JS · Python · C++ · Rust</dd>
      </div>
    </dl>
  </aside>
</section>
```

- [ ] **Step 2: Verify in browser**

Reload `index.html`. Check:
- Hero headline renders in Space Mono, bone/cream color
- Chocolate/orange blinking block cursor appears after "tools."
- Profile card has `--evergreen` background, chocolate avatar border
- Stats show "Tools" and "Tinkering in" rows (not "Languages")
- `// github portfolio` eyebrow with chocolate `//` prefix

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Rewrite hero and profile card — updated stat rows, cursor blink"
```

---

## Task 4: Rewrite CV strip and projects section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace the CV strip**

Replace `<section class="section cv-strip" id="cv" ...>...</section>` with:

```html
<section class="section cv-strip" id="cv" aria-labelledby="cv-title">
  <div>
    <p class="eyebrow">professional profile</p>
    <h2 id="cv-title">Support systems specialist and technical operator</h2>
  </div>
  <div class="cv-copy">
    <p>
      My CV site covers the non-code side of the same work: SaaS support, escalations, implementations, technical documentation, support operations, SSO/SAML/OAuth troubleshooting, Linux, Bash, Salesforce, and JIRA.
    </p>
    <div class="cv-actions">
      <a class="button primary" href="https://jasonpersinger.cv">Open CV site</a>
      <a class="button" href="https://jasonpersinger.cv/PersingerJasonResume.pdf">Download resume PDF</a>
      <a class="button" href="mailto:jason.persinger@gmail.com">Email me</a>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Replace the entire projects section**

Replace `<section class="section" id="projects" ...>...</section>` with the following. This removes Sloplocks, emarx, and GrowSeason, keeps 7 cards, and updates all tags to `[ lang · type ]` format:

```html
<section class="section" id="projects" aria-labelledby="featured-title">
  <div class="section-heading">
    <div>
      <p class="eyebrow">featured work</p>
      <h2 id="featured-title">Selected GitHub projects</h2>
    </div>
  </div>

  <div class="project-grid">
    <article class="project-card featured">
      <div class="project-topline">
        <span class="project-tag">[ html · job-board ]</span>
        <span class="status">Job board</span>
      </div>
      <h3>hollerworks</h3>
      <p>Moderated tech and tech-adjacent job board for Appalachia. The static frontend is backed by Firebase, Cloud Functions, Algolia search, Netlify redirects, Cloudflare Turnstile, structured job pages, and required compensation fields.</p>
      <div class="project-links">
        <a href="https://holler.works">Open site</a>
        <a href="https://github.com/jasonpersinger/hollerworks">Repository</a>
      </div>
    </article>

    <article class="project-card featured">
      <div class="project-topline">
        <span class="project-tag">[ js · bookmarklet ]</span>
        <span class="status">Bookmarklet</span>
      </div>
      <h3>TURBOTRAINER</h3>
      <p>GemStone IV skill trainer helper that injects bulk rank controls into the browser page. It is a client-side JavaScript bookmarklet, so it stores no login data, sends nothing to a server, and works directly on the existing trainer UI.</p>
      <div class="project-links">
        <a href="https://turbotrainer.gamemasters.lol">Open tool</a>
        <a href="https://github.com/jasonpersinger/TURBOTRAINER">Repository</a>
      </div>
    </article>

    <article class="project-card">
      <div class="project-topline">
        <span class="project-tag">[ c++ · voice-ai ]</span>
        <span class="status">Voice AI</span>
      </div>
      <h3>Peambot</h3>
      <p>Self-hosted AI desktop buddy built around a Waveshare ESP32-S3 AMOLED robot face and a Raspberry Pi server stack. The plan combines xiaozhi-esp32 firmware, Docker services, wake word, ASR, LLM, TTS, memory, and MCP automation.</p>
      <div class="project-links">
        <a href="https://github.com/jasonpersinger/peambot">Repository</a>
      </div>
    </article>

    <article class="project-card">
      <div class="project-topline">
        <span class="project-tag">[ html · storefront ]</span>
        <span class="status">Storefront</span>
      </div>
      <h3>NIXKEY</h3>
      <p>Premium static storefront for bootable Linux USB drives. The site pairs a dark teal/orange brand system with a curated distro catalog, Snipcart commerce wiring, product metadata, and operational scripts for USB flashing workflows.</p>
      <div class="project-links">
        <a href="https://github.com/jasonpersinger/NIXKEY">Repository</a>
      </div>
    </article>

    <article class="project-card">
      <div class="project-topline">
        <span class="project-tag">[ html · resume ]</span>
        <span class="status">Resume</span>
      </div>
      <h3>jasonpersinger-cv</h3>
      <p>Static resume site for support systems work: experience at Pixel Patcher, AbsenceSoft, Binance.US, and PowerSchool, plus skills around escalation handling, documentation, implementations, SSO, Salesforce, JIRA, Linux, and Bash.</p>
      <div class="project-links">
        <a href="https://jasonpersinger.cv">Open CV</a>
        <a href="https://jasonpersinger.cv/PersingerJasonResume.pdf">Resume PDF</a>
        <a href="https://github.com/jasonpersinger/jasonpersinger-cv">Repository</a>
      </div>
    </article>

    <article class="project-card">
      <div class="project-topline">
        <span class="project-tag">[ shell · distro ]</span>
        <span class="status">Distro</span>
      </div>
      <h3>NOKENIX</h3>
      <p>Early-stage Debian stable KDE distribution project with a live-build ISO scaffold, QEMU smoke tests, build scripts, decision logs, package policy, release checklist, and branding system for a maintainable community desktop.</p>
      <div class="project-links">
        <a href="https://github.com/jasonpersinger/NOKENIX">Repository</a>
      </div>
    </article>

    <article class="project-card">
      <div class="project-topline">
        <span class="project-tag">[ c++ · esp32 ]</span>
        <span class="status">ESP32</span>
      </div>
      <h3>CYD ESP32 Pi-hole Dashboard</h3>
      <p>Pi-hole v6 stats display for the ESP32-2432S028R Cheap Yellow Display. It polls the local Pi-hole API, rotates through three TFT slides, and presents block rate, query totals, cached traffic, clients, and gravity list size.</p>
      <div class="project-links">
        <a href="https://github.com/jasonpersinger/CYD-ESP32-PIHOLE-DASHBOARD">Repository</a>
      </div>
    </article>
  </div>
</section>
```

- [ ] **Step 3: Delete the Summary Method section**

Remove the entire block:

```html
<section class="section split" aria-labelledby="craft-title">
  <div>
    <p class="eyebrow">Summary method</p>
    <h2 id="craft-title">AI-assisted blurbs, grounded in repo context</h2>
  </div>
  <p>
    Each project summary is written from repository descriptions, README notes, and visible implementation details. The goal is to make the portfolio useful to a technical reader without forcing them to open every repo first.
  </p>
</section>
```

- [ ] **Step 4: Verify in browser**

Reload `index.html`. Check:
- CV strip renders in `--evergreen` panel with `// professional profile` eyebrow
- Exactly 7 project cards visible (no Sloplocks, emarx, or GrowSeason)
- hollerworks and TURBOTRAINER have `--evergreen` featured background
- All cards show `[ lang · type ]` tag in chocolate, status badge in tea-green
- Summary Method section is gone

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "Rewrite CV strip and projects — remove 3 cards, remove Summary Method, update tags"
```

---

## Task 5: Add homelab section

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Insert the homelab section**

Insert the following block directly after the closing `</section>` of the projects section and before `<section class="section" id="repo-index" ...>`:

```html
<section class="section" id="homelab" aria-labelledby="homelab-title">
  <div class="section-heading">
    <div>
      <p class="eyebrow">homelab</p>
      <h2 id="homelab-title">HOMELAB</h2>
    </div>
  </div>
  <p class="section-intro">Running self-hosted infrastructure on hardware I control — because owning your stack teaches you things SaaS never will. The "void" network spans a daily driver, a Pi Docker host, and a dedicated Home Assistant machine.</p>

  <div class="homelab-top">
    <div class="node-card">
      <div class="node-header">
        <span class="node-name">voidbox</span>
        <span class="node-spec">Custom (MSI MS-7C87) · Ryzen 7 5700G · 32 GB · 480 GB btrfs</span>
      </div>
      <div class="service-tags">
        <span class="service-tag">CachyOS</span>
        <span class="service-tag">KDE Plasma 6</span>
        <span class="service-tag">KWin (Wayland)</span>
        <span class="service-tag">fish</span>
        <span class="service-tag">ghostty</span>
        <span class="service-tag">Docker</span>
        <span class="service-tag">Btrfs</span>
        <span class="service-tag">Tailscale</span>
        <span class="service-tag">AUR</span>
      </div>
      <p>The daily driver and project bench. CachyOS on Plasma 6 / Wayland, fish in ghostty with BigBlueTerm Nerd Font. Ryzen 7 5700G APU driving a 1440p / 100 Hz panel on integrated Vega; a discrete RDNA card is queued as the next upgrade. Btrfs root, Tailscale-attached — where most projects originate before pieces migrate out to voidberry or voidframe.</p>
    </div>
  </div>

  <div class="homelab-bottom">
    <div class="node-card">
      <div class="node-header">
        <span class="node-name">voidberry</span>
        <span class="node-spec">Raspberry Pi 4B · 4 GB</span>
      </div>
      <div class="service-tags">
        <span class="service-tag">Pi-hole</span>
        <span class="service-tag">Nginx Proxy Manager</span>
        <span class="service-tag">Homepage</span>
        <span class="service-tag">Uptime Kuma</span>
        <span class="service-tag">Paperless-ngx</span>
        <span class="service-tag">Actual Budget</span>
        <span class="service-tag">Tailscale</span>
        <span class="service-tag">rclone</span>
      </div>
      <p>Docker stack running on a USB SSD. Tailscale punches through CGNAT for remote access; rclone + systemd timers handle automated Google Drive backups.</p>
    </div>

    <div class="node-card">
      <div class="node-header">
        <span class="node-name">voidframe</span>
        <span class="node-spec">Dell Inspiron 3650</span>
      </div>
      <div class="service-tags">
        <span class="service-tag">Home Assistant OS</span>
        <span class="service-tag">Zigbee2MQTT</span>
        <span class="service-tag">SLZB-06p7u</span>
        <span class="service-tag">HACS</span>
        <span class="service-tag">T-Higrow sensors</span>
        <span class="service-tag">Tuya Zigbee</span>
      </div>
      <p>Dedicated Home Assistant machine with a Zigbee coordinator, LILYGO T-Higrow plant sensors (soil moisture, conductivity, light, temp) on solar panels, and a Tuya device fleet. Roadmap: HA MCP server integration for Claude Desktop and a self-hosted voice assistant.</p>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Verify in browser**

Reload `index.html`. Check:
- Homelab section appears between projects and repo index
- `// homelab` eyebrow with chocolate prefix, `HOMELAB` h2 in Space Mono
- voidbox card spans full width with all 9 service tags
- voidberry and voidframe sit side by side below voidbox
- Intro paragraph visible in muted color above node cards
- `homelab` nav link scrolls to the section

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Add homelab section — voidbox, voidberry, voidframe node cards"
```

---

## Task 6: Rewrite repo index and footer

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace the repo index section**

Replace `<section class="section" id="repo-index" ...>...</section>` with the following (removes sloplocks, emarx, growseason):

```html
<section class="section" id="repo-index" aria-labelledby="repo-title">
  <div class="section-heading">
    <div>
      <p class="eyebrow">repository index</p>
      <h2 id="repo-title">Quick links</h2>
    </div>
  </div>

  <div class="repo-list">
    <a class="repo-row" href="https://github.com/jasonpersinger/hollerworks">
      <span>hollerworks</span>
      <span>HTML</span>
    </a>
    <a class="repo-row" href="https://github.com/jasonpersinger/TURBOTRAINER">
      <span>TURBOTRAINER</span>
      <span>JavaScript</span>
    </a>
    <a class="repo-row" href="https://github.com/jasonpersinger/peambot">
      <span>peambot</span>
      <span>C++</span>
    </a>
    <a class="repo-row" href="https://github.com/jasonpersinger/NIXKEY">
      <span>NIXKEY</span>
      <span>HTML</span>
    </a>
    <a class="repo-row" href="https://github.com/jasonpersinger/jasonpersinger-cv">
      <span>jasonpersinger-cv</span>
      <span>HTML</span>
    </a>
    <a class="repo-row" href="https://github.com/jasonpersinger/NOKENIX">
      <span>NOKENIX</span>
      <span>Shell</span>
    </a>
    <a class="repo-row" href="https://github.com/jasonpersinger/CYD-ESP32-PIHOLE-DASHBOARD">
      <span>CYD-ESP32-PIHOLE-DASHBOARD</span>
      <span>C++</span>
    </a>
  </div>
</section>
```

- [ ] **Step 2: Replace the footer**

Replace `<footer class="footer">...</footer>` with:

```html
<footer class="footer">
  <span>// updated may 2026</span>
  <a href="https://github.com/jasonpersinger">github.com/jasonpersinger</a>
</footer>
```

- [ ] **Step 3: Verify in browser**

Reload `index.html`. Check:
- Repo list shows exactly 7 rows — no sloplocks, emarx, or growseason
- Repo names in tea-green, language labels in muted on the right
- Rows highlight to `--evergreen` on hover
- Footer shows `// updated may 2026` in Space Mono

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "Rewrite repo index (remove 3 entries) and footer"
```

---

## Task 7: Responsive check and final commit

**Files:**
- Modify: `styles.css` (only if fixes needed)
- Modify: `index.html` (only if fixes needed)

- [ ] **Step 1: Check 860px breakpoint**

In browser dev tools (F12 → responsive mode), set width to 860px. Verify:
- Hero collapses to single column (copy above profile card)
- CV strip collapses to single column
- Project grid becomes 2-column
- Homelab bottom row (voidberry + voidframe) stacks to single column

- [ ] **Step 2: Check 620px breakpoint**

Set width to 375px (iPhone). Verify:
- Nav stacks brand above links; links row scrolls horizontally if needed
- Project grid is single column
- Repo rows stack (name above language)
- Footer stacks vertically

- [ ] **Step 3: Fix any layout issues found**

If any responsive issues appear, fix them in `styles.css` within the existing `@media` blocks. Common issues to watch for:
- `node-spec` text overflowing the node-header row on narrow screens (add `flex-direction: column` to `.node-header` at 620px if needed)
- Hero `h1` font size too large on mobile (`clamp` handles this but verify visually)

- [ ] **Step 4: Smoke-check all nav links**

Click each nav link and verify it scrolls to the correct section:
- `projects` → Featured Work
- `homelab` → HOMELAB
- `cv` → Professional profile strip
- `repos` → Quick links

- [ ] **Step 5: Final commit**

```bash
git add styles.css index.html
git commit -m "Responsive fixes and final polish — portfolio retro terminal redesign complete"
```

---

## Self-Review Checklist

Before executing, verified:

- [x] **Spec coverage:** All spec requirements have a task — palette, typography, cursor blink, eyebrow format, 7 cards, 3 removals, Summary Method removed, profile card stat rows, homelab section with layout A, repo index pruned, footer format
- [x] **No placeholders:** All steps contain actual HTML/CSS code
- [x] **Type consistency:** CSS class names used in HTML match classes defined in styles.css — `.project-tag`, `.service-tags`, `.service-tag`, `.node-card`, `.node-header`, `.node-name`, `.node-spec`, `.homelab-top`, `.homelab-bottom`, `.section-intro`, `.cursor` all defined in Task 1 CSS and referenced in Tasks 3–6 HTML
- [x] **Google Fonts:** `<link>` added in Task 2 head before `styles.css` link, matching the `'Space Mono'` font-family references throughout the CSS
