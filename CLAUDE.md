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

## Git workflow

Keep the history clean and professional — these commits are public on the company's
GitHub.

**Before committing**
- Open `index.html` in a browser and confirm the logo shows in the header and footer,
  the mobile menu opens, and nav links jump to the right sections.
- Make sure the commit contains **one logical change**. Don't bundle unrelated edits
  (e.g. a content rewrite and a color change) into the same commit.

**Commit messages**
- Short, imperative subject line, ≤ ~60 chars, no trailing period.
  Good: `Update hero headline`, `Add Tengri Capital portfolio card`, `Fix footer link`.
  Avoid: `update`, `changes`, `stuff`.
- If the change needs context, add a blank line then 1–2 sentences explaining **why**.
- **Never** add Claude as author or co-author — no `Co-Authored-By: Claude` trailer and
  no Claude/AI mention. Commits are authored solely by the user.
- Don't commit secrets, API keys, or large unnecessary files.

**Pushing = publishing**
- Every push to `main` goes **live within ~1–2 minutes**. Push only when the change is
  ready for the public to see.
- Want to preview or iterate before going live? Work on a branch, then merge to `main`
  when it's ready.
- If a push is rejected with a "fast-forward" / "fetch first" error, run
  `git pull --rebase origin main` and push again. (GitHub occasionally auto-commits the
  `CNAME` file, which puts a commit on the remote you don't have locally.)

## Using Context7 (live documentation lookup)

Context7 is an MCP tool that fetches **current** docs for libraries, frameworks, SDKs,
APIs, CLIs, and cloud services — useful because model knowledge can be out of date.

- This site is plain HTML/CSS/JS with **no libraries or build step**, so Context7 is
  **rarely needed for routine content edits**. Don't reach for it just to change text.
- **Do** use it when a task brings in something external, e.g.: adding an analytics
  snippet (Google Analytics, Plausible), embedding a form/booking service, pulling in a
  JS library, or questions about **GitHub Pages** behavior or the **`gh` CLI**. In those
  cases, fetch the latest docs via Context7 instead of relying on memory.

## Gotchas & lessons learned

**If a task took several tries or threw confusing errors before you got it working, add
an entry here** — symptom, cause, fix — so the same mistake isn't repeated next time.
Keep entries short. Treat this section as the project's memory.

- **Images must use relative paths, never absolute.** The original site referenced the
  logo as `/assets/tengri-logo.png`, but no file lived at that path, so it 404'd in the
  header and footer. Use `assets/tengri-logo.png`. Absolute `/assets/...` also breaks on
  the GitHub Pages preview URL.
- **DNS lives in Wix, not a normal registrar.** Nameservers are `*.wixdns.net`. Edit
  records at **Wix → Domains → Manage DNS Records**, not at a registrar control panel.
- **In Wix, the root/apex domain = a _blank_ Host name.** Wix's "Add Record" form
  rejects `@` and only creates subdomains. To point the apex (`tengrigroupinc.com`),
  leave the Host name field empty. The four GitHub Pages IPs are
  `185.199.108.153`, `.109.153`, `.110.153`, `.111.153`. `www` is a CNAME →
  `tengri-group-inc.github.io`.
- **NEVER touch the email DNS records.** `araev@tengrigroupinc.com` runs on
  **Microsoft 365**. Leave the MX records and the `autodiscover`, `enterpriseenrollment`,
  `enterpriseregistration`, `lyncdiscover`, and `sip` CNAMEs alone — editing or deleting
  any of them breaks company email. Only ever touch the website's A and `www` records.
- **The HTTPS certificate lag after a DNS change is normal.** GitHub takes anywhere from
  a few minutes to an hour to issue the SSL cert once DNS is correct. A
  `NET::ERR_CERT_COMMON_NAME_INVALID` browser warning during that window is expected, not
  a bug — it clears itself. Don't repeatedly re-trigger the Pages API; that can slow
  issuance. Just wait, then turn on "Enforce HTTPS."
