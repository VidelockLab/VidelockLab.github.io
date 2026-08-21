# Videlock Lab website — working notes

Public site for the Videlock Lab (UCLA DGSOM). Its main job is hosting lab
safety information that people reach by scanning QR codes posted in the lab.

## How this site works

- **Repo:** `VidelockLab/VidelockLab.github.io` (public, GitHub Pages)
- **Live at:** https://videlocklab.com — apex domain, `www` redirects to it
- **Engine:** Jekyll, built automatically by GitHub Pages. There is **no
  build step and no local toolchain.** Push to `main`, wait ~60 seconds,
  it's live. Do not add a build workflow, a `Gemfile`, or npm anything
  unless the theme genuinely requires it.
- **Theme:** `jekyll-theme-cayman`, set in `_config.yml`. The upgrade path
  to `just-the-docs` (sidebar + search) is documented in the comments there.

## Adding a page

Create `<folder>/index.md` or `<folder>/<slug>.md` with front matter:

```yaml
---
layout: default
title: Human-readable title
nav_order: 3
---
```

`nav_order` does nothing under the current theme. Include it anyway — it is
what makes the just-the-docs switch a config change instead of a rewrite.

Folder-with-`index.md` gives clean URLs (`/safety/`). Prefer it over
`safety.md` for anything that might grow subpages.

## Content rules

These are deliberate. Do not "helpfully" reverse them.

1. **Never re-host UCLA EH&S standard SOP PDFs.** EH&S revises them. Link to
   the official copies at https://ehs.ucla.edu/documents/Laboratory instead.
   Lab-authored SOPs (Custom, Biosafety) and factsheets DO belong here, as
   real HTML pages rather than PDF attachments.
2. **Never publish container-level chemical inventory.** Hazard summaries,
   handling procedures, and PPE requirements are fine. A public list of what
   is in Rm 1526 and in what quantity is not.
3. **Never invent a phone number, a dose, an exposure limit, or a first-aid
   step.** If a fact isn't in the source documents, leave a `TODO` marked in
   an HTML comment. On a safety page a plausible-looking wrong answer is the
   worst possible failure.
4. **`/safety/` is a permanent URL.** It is printed on QR codes on lab
   walls. Never rename, move, or restructure it away. Same for any deep link
   that ends up on printed material.
5. Keep the site root for general lab content. Safety lives under `/safety/`.

## Source material

Lives outside this repo, at `~/Desktop/labstuff/LabSafety`:

- `Custom SOPs/` — 5 lab-written SOPs → become pages here
- `Biosafety SOPs/` — 4 documents → become pages here
- `Factsheets/` — 2 documents → become pages here
- `UCLA Standard SOPs/` — 19 EH&S PDFs → **link out, do not copy**
- `Videlock Lab - SOP Coverage 2026-08-19.xlsx` — the chemical→SOP mapping,
  and the source of truth for which standard SOPs apply

## Style

Plain language, short sentences, scannable headings. The reader is often
standing at a bench with gloves on, or is a rotation student on day one.
Put the actionable thing first and the background second.
