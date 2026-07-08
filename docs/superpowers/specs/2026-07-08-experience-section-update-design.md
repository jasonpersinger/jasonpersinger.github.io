# Experience Section & Site Refresh — Design

**Date:** 2026-07-08
**Scope:** `index.html`, `styles.css` (single-page static site, retro terminal design)

## Goal

Turn jasonpersinger.me into a self-contained CV/resume site: remove every
reference to the retired jasonpersinger.cv site, replace it with an on-page
experience timeline sourced from `PersingerJasonResume.pdf` (hosted in this
repo), and apply targeted visual polish.

## Requirements

### 1. Remove jasonpersinger.cv entirely
- Hero: "Resume site" button → "Resume PDF" linking to local
  `/PersingerJasonResume.pdf`.
- Delete the `jasonpersinger-cv` project card and its repo-index row.
- Replace the `#cv` strip section (see below).
- Nav link `cv` → `experience` (href `#experience`).

### 2. Experience section (replaces the cv strip, same slot after hero)
Same two-column evergreen panel layout (`360px | 1fr`, stacking at 860px).

**Left column:** eyebrow `professional experience`, heading updated to the
resume's framing (Technical Support Engineer — SaaS support, escalations,
implementations), buttons: **Download resume PDF** (local file, primary) and
**Email me**.

**Right column:** compact timeline — dates in Space Mono chocolate, role ·
company in bone, 1–2 line muted summary. Entries:

| Dates | Role | Summary |
|---|---|---|
| 2023 – 2026 | Software Support Analyst · AbsenceSoft (Remote) | Escalations & root cause analysis on enterprise leave management; built internal AI support tooling on the Claude API. |
| 2021 – 2022 | Support Team Lead · Binance.US (Remote) | Led ~8 analysts on a regulated US crypto exchange; cut average ticket resolution time 65%. |
| 2018 – 2021 | Implementation PM / Online Solution Specialist · PowerSchool | End-to-end SaaS implementations and training for K-12 school districts. |

**Exclusion:** Pixel Patcher must NOT appear anywhere on the site. It exists
only inside the resume PDF.

### 3. Projects section
- Heading "Selected GitHub projects" → "Projects".
- hollerworks card: remove the "Open site" (holler.works) link; keep
  "Repository" only. Card description text unchanged.
- Grid drops from 7 cards to 6 (cv card removed) — two clean rows of 3.

### 4. Homelab section
- Expand the section intro to properly cover home automation, the Home
  Assistant OS server, self-hosting, and the home network — a short paragraph
  (2–4 sentences), text only, no screenshots.
- Node cards unchanged.

### 5. Metadata & footer
- `<title>` and meta description updated to reflect portfolio + resume
  (mention experience/support engineering, drop nothing else).
- Footer: `// updated may 2026` → `// updated july 2026`.

### 6. Visual polish (same aesthetic, targeted)
- Unify card border-radius (currently mixes 3px and 4px) → 3px everywhere.
- Add hover border-color transition to `.project-card` and `.node-card`
  (matches existing `.repo-row` hover behavior).
- Remove the `.status` chip from project cards — it duplicates the
  `.project-tag` text. Delete the chip markup and its CSS.
- Timeline responsive behavior: date-beside-role on desktop, date stacked
  above role under 620px.

## Out of scope
- Pixel Patcher references (excluded by request).
- holler.works live link (site hosting being updated).
- Screenshots (`voidframe-homeassistant.png`, `Screenshot_20260517_111712.png`)
  stay out of the site; they remain untracked.
- No changes to node cards, TURBOTRAINER live link, or other project links.
- No JS; site stays static HTML + CSS.

## Verification
1. `grep -ri "jasonpersinger.cv\|pixelpatcher\|holler.works" index.html` →
   only acceptable hit is none (holler.works repo URL is
   github.com/jasonpersinger/hollerworks, which is fine).
2. Open the page in a browser: check hero, experience timeline, projects grid
   (6 cards, no status chips), homelab intro, footer — at desktop, ~800px,
   and ~400px widths.
3. Resume PDF link resolves to `/PersingerJasonResume.pdf` (file exists in
   repo root; must be committed).
