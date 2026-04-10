# AGENTS.md

## Stack

Hugo static site using the [hextra](https://github.com/imfing/hextra) theme, pulled via Go modules (not in `themes/`). Requires **Hugo extended** (for Dart Sass).

## Commands

- `hugo server` — local dev server with live reload
- `hugo build --gc --minify` — production build (output to `public/`)

## Architecture

- `hugo.yaml` — site config (menus, params, markup settings)
- `content/` — page content as markdown; homepage is `content/_index.md`
- `layouts/shortcodes/` — custom shortcodes (`banner` for homepage hero)
- `static/img/` — static assets (logo, images)
- `go.mod` / `go.sum` — Hugo module deps (hextra theme); run `hugo mod get -u` to update theme

## Key conventions

- Goldmark `unsafe: true` is enabled — raw HTML in markdown is rendered
- `security.enableInlineShortcodes: true` is set
- CI (`.github/workflows/hugo.yaml`) deploys to GitHub Pages on push to `main`
- CI pins specific versions: Hugo 0.156.0, Go 1.26.0, Dart Sass 1.97.3, Node 24.13.1

## Gotchas

- `themes/` is empty locally — theme is resolved at build time via Go modules
- The banner shortcode uses `.Page.Resources.GetMatch`, so banner images must be page bundles (in the same directory as `_index.md`), not in `static/`