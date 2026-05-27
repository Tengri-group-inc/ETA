# Tengri Group — Company Website

This repo is the **public marketing website for Tengri Group Inc.**, live at
**https://tengrigroupinc.com**. It is a single static page — no build step, no
framework, no dependencies. What you see in `index.html` is exactly what ships.

## How it's built

- **`index.html`** — the entire site. HTML, all CSS (in one `<style>` block in the
  `<head>`), and a tiny bit of JavaScript (mobile nav + sticky header) at the bottom.
  Everything lives here. There is no React, no Tailwind, no bundler.
- **`assets/`** — images. Currently just `tengri-logo.png`. Reference images with
  **relative paths** (`assets/foo.png`), never absolute (`/assets/foo.png`) — absolute
  paths break on the GitHub Pages preview URL.
- **`CNAME`** — tells GitHub Pages to serve the site on `tengrigroupinc.com`. Do not
  delete or rename this file.

## How it's deployed

- Hosted on **GitHub Pages** from the `main` branch of `Tengri-group-inc/ETA`.
- **Every push to `main` automatically redeploys** the live site within ~1–2 minutes.
  There is nothing else to run or click.
- Custom domain `tengrigroupinc.com` is configured in repo **Settings → Pages**.

## Editing guide (for Claude Code)

The page is organized as labeled `<section>` blocks, each with an `id`. To change
content, find the matching section:

| Section | `id` | What's in it |
|---|---|---|
| Hero | `hero` | Headline, subhead, location line |
| The Thesis | `thesis` | The investment thesis prose |
| The Platform | `platform` | The 5 capability layers (`layer-card` blocks) |
| Portfolio | `portfolio` | Tengri Development / Capital / Field Services cards |
| For Sellers | `sellers` | Acquisition criteria + process |
| For Investors | `investors` | ETA model, deal structure, disclaimers |
| For Operators | `operators` | Hiring / subcontractor pitch |
| Leadership | `leadership` | Founder bio |
| How We Operate | `principles` | The 6 operating principles |
| Contact | `contact` | Email addresses + phone |
| Footer | `footer` | Logo, links, legal text |

### Conventions to follow when editing
- **Colors and fonts** are defined as CSS variables in `:root` near the top of the
  `<style>` block (e.g. `--accent`, `--gold`, `--bg`). Use these variables instead of
  hardcoding hex values, so the design stays consistent.
- **Two fonts**: `Inter` (sans, body/UI) and `Cormorant Garamond` (serif, used for the
  thesis prose). Loaded from Google Fonts in the `<head>`.
- The nav menu (`<nav id="main-nav">`) and the footer "Quick Links" list both link to
  section `id`s. **If you add or rename a section, update both menus** so links don't
  break.
- Keep contact emails consistent: `acquisitions@`, `investors@`, `work@`, `info@`,
  and the founder's `araev@tengrigroupinc.com`.

## Common tasks
- **Change wording**: edit the text inside the relevant `<section>`.
- **Add a portfolio item**: copy an existing `.portfolio-card` block in `#portfolio`.
- **Add a platform layer**: copy a `.layer-card` block in `#platform`, bump the number.
- **Replace the logo**: drop the new file in `assets/`, keep the filename
  `tengri-logo.png` (or update the two `<img src="assets/...">` references + the favicon
  link in `<head>`).

## Before pushing
- Open `index.html` in a browser and confirm the logo shows in the header and footer,
  the mobile menu opens, and nav links jump to the right sections.
- Commit with a short message describing the content change, then push to `main`.
  The live site updates automatically.
