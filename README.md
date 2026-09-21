# 805 Outdoors — Squarespace Custom Code

Plain CSS/JS for the 805 Outdoors Squarespace site, hosted on GitHub and
served through the [jsDelivr](https://www.jsdelivr.com/) CDN, then linked
into Squarespace's Code Injection settings. No build step — just edit the
files and push.

## Files

- `style.css` — site-wide custom styles
- `script.js` — site-wide custom scripts

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

## Workflow going forward

1. Edit `style.css` / `script.js` locally.
2. Commit and push to GitHub.
3. If using a branch URL, purge the jsDelivr cache (see above) so changes
   go live immediately; if using a version tag, bump the tag.
