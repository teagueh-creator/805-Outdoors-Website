# 805 Outdoors — Squarespace Custom Code

Plain CSS/JS for the 805 Outdoors Squarespace site, hosted on GitHub and
served through the [jsDelivr](https://www.jsdelivr.com/) CDN, then linked
into Squarespace's Code Injection settings. No build step — just edit the
files and push.

## Files

- `style.css` — site-wide custom styles: brand colors/fonts (as CSS
  variables) plus the `.eo-*` classes and `.book-lesson-btn` used by the
  page sections below
- `script.js` — site-wide custom scripts (empty for now)
- `assets/logo.png` — the 805 Outdoors logo, served via jsDelivr for use
  in `<img>` tags (see Section snippets below)
- `sections/` — reference copies of the HTML you paste into Squarespace
  Code Blocks; not served by jsDelivr, just kept here for version control

## 1. Push this repo to GitHub

This folder is already a git repo with an initial commit and its remote set
to `https://github.com/teagueh-creator/805-Outdoors-Website.git`. Make sure
that repository exists on GitHub (public — jsDelivr needs a public repo),
then push:

```bash
git push -u origin main
```

## 2. Get jsDelivr URLs

jsDelivr serves any file straight from a public GitHub repo. URL format:

```
https://cdn.jsdelivr.net/gh/teagueh-creator/805-Outdoors-Website@<branch-or-tag>/<file>
```

For example, pointing at the `main` branch:

```
https://cdn.jsdelivr.net/gh/teagueh-creator/805-Outdoors-Website@main/style.css
https://cdn.jsdelivr.net/gh/teagueh-creator/805-Outdoors-Website@main/script.js
```

**Important — caching:** jsDelivr aggressively caches files pulled from a
branch (like `@main`) for up to 24 hours (sometimes longer), so edits won't
show up on the live site right away. Two ways to deal with this:

- **For active development:** use the branch URL (`@main`) and purge the
  cache after each push by visiting:
  `https://purge.jsdelivr.net/gh/teagueh-creator/805-Outdoors-Website@main/style.css`
  (and the same for `script.js`).
- **For production/stability:** tag a release (e.g. `git tag v1.0.0 && git
  push origin v1.0.0`) and use the tag in the URL instead of `@main`. Tagged
  versions are immutable and cache-friendly — bump the tag when you want the
  live site to pick up changes.

## 3. Add to Squarespace Code Injection

In Squarespace: **Settings → Advanced → Code Injection** (exact path may
vary slightly by plan/version).

**Header** — add the CSS:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/teagueh-creator/805-Outdoors-Website@main/style.css">
```

**Footer** — add the JS:

```html
<script src="https://cdn.jsdelivr.net/gh/teagueh-creator/805-Outdoors-Website@main/script.js"></script>
```

Save. Squarespace injects these on every page site-wide.

## 4. Add the page sections

`sections/` has one HTML file per homepage section:

1. `hero.html`
2. `about.html`
3. `history.html`
4. `services.html`
5. `partners.html`

On the Squarespace page, add a **Code Block** for each one, in that order,
and paste its contents in. They rely entirely on the classes and variables
already defined in `style.css`, so nothing else needs to be pasted in
per-block. Squarespace's own site header/footer and navigation stay as-is —
these sections are just the page content in between.

Each file has `[bracketed placeholders]` for copy that only you can write
(bio, milestones, real certification names, partner details, etc.) — swap
those out directly in the Code Block. To add another activity or partner,
duplicate the relevant card `<div>` (marked with an HTML comment) inside its
grid.

## Retheming later

Every color and font lives once, at the top of `style.css`, in `:root`:

```css
:root {
  --eo-navy: #1b2a3b;
  --eo-accent: #d98b3b;
  --eo-forest: #4b6b4a;
  --eo-cta: #1a7a3c;
  /* …etc */
}
```

Change a value there, push, purge/bump the cache (below), and it updates
everywhere on the site at once — headings, buttons, badges, backgrounds.
There's no need to touch the section HTML files for a color or font change.

## Workflow going forward

1. Edit `style.css` / `script.js` / a file in `sections/` locally.
2. Commit and push to GitHub.
3. If using a branch URL, purge the jsDelivr cache (see above) so changes
   go live immediately; if using a version tag, bump the tag. Section HTML
   pasted directly into Squarespace Code Blocks updates instantly since it
   isn't loaded from jsDelivr — only `style.css`/`script.js`/`logo.png`
   changes need a cache purge.
