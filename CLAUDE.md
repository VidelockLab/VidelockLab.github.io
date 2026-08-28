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
- The CDN serves stale for a minute or two after a push. A page that looks
  unchanged is usually cache, not a failed deploy.
- **The Chemical Hygiene Plan's own Box link is login-walled.**
  `ucla.app.box.com/v/UCLA-Chemical-Hygiene-Plan` 302s to a Box login for an
  anonymous request, so it must never go on a QR code or a page a visitor
  reads. Link `ehs.ucla.edu/documents/Laboratory` instead, which lists it.
  Checked 25 Aug 2026; `/v/UCLA-Biosafety-Plan` and `/v/EHS-trainingmatrix`
  are both fine, so this is the CHP specifically, not a `/v/` problem.

## Adding a page

Create `<folder>/index.md` or `<folder>/<slug>.md` with front matter:

```yaml
---
layout: default
title: Human-readable title
nav_order: 3
permalink: /safety/<slug>/
---
```

`nav_order` does nothing under the current theme. Include it anyway — it is
what makes the just-the-docs switch a config change instead of a rewrite.

## Content rules

These are deliberate. Do not "helpfully" reverse them.

1. **Never re-host UCLA EH&S standard SOP PDFs.** EH&S revises them. Link to
   the official copies at https://ehs.ucla.edu/documents/Laboratory instead.
   This rule is about *EH&S's* documents. **The lab's own SOPs are a different
   case** — the five lab-written chemical SOPs are published here, because no
   EH&S copy exists to link to and they carry no personnel names or personal
   numbers. The lab-written *biosafety* SOPs do carry both, and stay off.
2. **Never publish container-level chemical inventory.** Hazard summaries,
   handling procedures and PPE requirements are fine. A public list of what
   is in Rm 1526 and in what quantity is not.
3. **No personal phone numbers, no personnel names, no equipment map.** The
   site carries only numbers UCLA already publishes: 9-1-1, EH&S
   (310) 825-9797, Facilities (310) 825-9236, Occupational Health, the ER.
   Everything else lives in the lab's Slack canvas and the safety manual.
4. **Never invent a phone number, a dose, an exposure limit, or a first-aid
   step.** On a safety page a plausible-looking wrong answer is the worst
   possible failure. Record it as an open issue instead.
5. **These paths are permanent.** They are printed on laminated QR labels on
   lab walls. Rewrite the content freely; never rename or move the path.

   `/safety/` · `/safety/exposure/` · `/safety/spill/` · `/safety/waste/` ·
   `/safety/sops/` · `/safety/training/`

   The lab-written SOP pages added 25 Aug 2026 are permanent too, though **not on
   any printed label** — the labels and the directory poster carry only the six
   router pages above: `/safety/sops/sensitizers/` · `/safety/sops/sodium-azide/` ·
   `/safety/sops/guanidinium/` · `/safety/sops/potent-compounds/`.
   `/safety/sops/glutaraldehyde/` was **deleted** 28 Aug 2026 when that SOP was
   folded into Chemical Sensitizers; nothing printed pointed at it. They live in flat files named
   `safety/sop-<slug>.md` — a real `safety/sops/` directory would collide with
   `safety/sops.md`, which owns the `/safety/sops/` permalink.

6. Keep the site root for general lab content. Safety lives under `/safety/`.

## The safety pages

`/safety/` is a router: emergency numbers, then five links. Each of the
others is one job, sized to be read on a phone by someone who is standing up.

- `exposure` — flush first, 15 minutes; where to go; the 2-hour lentivirus
  prophylaxis window
- `spill` — inside a cabinet / outside / shared space / dropped in transit
- `waste` — which container, plus the rules people forget
- `sops` — the router for procedures. Each of the 19 UCLA banded chemical
  SOPs is linked individually (URLs came from the lab's SOP coverage
  workbook, not from re-deriving them), plus the five lab-written chemical
  SOP pages, plus a reference block for the CHP and Institutional Biosafety
  Plan
- `training` — two parts (everyone, animal work) with Worksafe course IDs,
  plus how to log into CITI

## Source material

Lives outside this repo, at `~/Desktop/labstuff/LabSafety`, which has its
own CLAUDE.md covering the manual, the SOPs and the settled facts. Read that
before making substantive changes to a safety page — the room numbers,
containment levels and containment periods on this site all come from there.

## Style

Plain language, short sentences, scannable headings. The reader is often
standing at a bench with gloves on, or is a rotation student on day one, or
is a visitor who scanned a code in a corridor. Put the actionable thing
first and the background second. Assume no prior knowledge and no patience.
