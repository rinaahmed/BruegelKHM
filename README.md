# Bruegel im KHM / Bruegel at the KHM

A mobile-first, bilingual (Deutsch / English) single-page companion for visiting the
Pieter Bruegel the Elder collection at the **Kunsthistorisches Museum Vienna** — the
largest and most important Bruegel collection in the world.

The whole app is one self-contained `index.html` file: vanilla HTML, CSS, and
JavaScript, no frameworks, no build step, no dependencies. Just open it in a browser.

> Unofficial, educational fan project. Not affiliated with or endorsed by the
> Kunsthistorisches Museum Vienna.

---

## Features

The app is organised into sections, reached from the sticky bottom navigation bar.
A **Mehr / More** popover holds the secondary sections to keep the bar to five icons.

- **Hintergrund / Background** — collapsible cards on Bruegel's life, a visual timeline,
  the historical context (Habsburg rule, the Reformation, proverbs and allegory), and
  *the four threads* that run through every painting.
- **Vorbereitung / Prepare** — active-recall tools to use *before* your visit: a timeline
  test, paraphrasing the four threads in your own words, a free-write reflection, and a
  Netherlandish-proverbs hunt list.
- **Gemälde / Paintings** — the 12 paintings, each as a card with a thumbnail, a
  "what to look for" guide, historical context, and an inline space for your own
  observations (see below).
- **Checkliste / Checklist** — tick off each painting as you stand in front of it, with
  a progress bar.
- **Notizen / Notes** — an aggregated view of everything you've written, with export.
- **Über / About** — practical info and a recap of the four threads.

### The four threads

A reading lens applied across every painting:

1. **The Crowd as Protagonist** — no heroes; everyone is equal, small against the landscape.
2. **Landscape as Emotional State** — the landscape is an argument, not a backdrop.
3. **What Is Always Happening in the Background** — the most important thing is often at the edge.
4. **Where Is God?** — the sacred is never announced; it hides.

### Your own observations

Each painting card has a "My Observations" block with two fields — a **first impression**
(before reading the guide notes) and an **after reading** reflection. Notes:

- **save automatically** as you type (no save button),
- **persist on your device** via `localStorage`, so notes written before your visit are
  still there when you arrive,
- are gathered in the **Notes** section, where you can **export them to a `.txt` file** or
  **copy them to the clipboard**. The export also includes your Prepare *Free Write*.

If `localStorage` is unavailable (e.g. private browsing), the app falls back to
in-memory notes for the session and warns you to export them.

---

## Running locally

No build or install. Either open the file directly:

```bash
open index.html        # macOS
xdg-open index.html    # Linux
```

…or serve it over HTTP (recommended, so relative behaviour matches production):

```bash
python3 -m http.server 8000
# then visit http://127.0.0.1:8000/
```

---

## Deployment

The app is deployed as an **Azure Static Web App**. Because the entire app is a single
file at the repository root, deployment is just publishing that root — no build output.

A GitHub Actions workflow (`.github/workflows/azure-static-web-apps-*.yml`) builds and
deploys automatically:

- **app location:** `/` (repository root)
- **api / output location:** none

Every push to `main` deploys to production; pull requests get preview environments.

---

## Tech & design

- **Single file** — `index.html` contains all markup, styles, and logic.
- **No dependencies** — vanilla HTML/CSS/JS; nothing to install, nothing to build.
- **Mobile-first** — centred, max width 480px; sticky header and bottom nav.
- **Bilingual** — DE/EN toggle in the header switches *all* text instantly; default is DE.
- **Typography** — Georgia (serif) for reading content, system UI sans-serif for labels
  and chrome.
- **Offline-friendly** — painting thumbnails are embedded directly in the file as
  base64, so the app works without a network connection in the gallery.
- **Privacy** — no analytics, no cookies, no external requests at runtime. Your notes
  never leave your device unless you export them yourself.

---

## Image credits

The 12 painting thumbnails are downscaled reproductions sourced from
[Wikimedia Commons](https://commons.wikimedia.org/) and are in the **public domain**
(Pieter Bruegel the Elder, d. 1569). For high-resolution details of the KHM paintings,
see [insidebruegel.net](https://insidebruegel.net).

---

## Repository layout

```
index.html   # the entire application
.github/     # Azure Static Web Apps deploy workflow
README.md    # this file
```
