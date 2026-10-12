# AGENTS.md

Hugo static site for **Simply Learn AI**, using the `introduction` theme (`config.toml:2`) and published to GitHub Pages at `https://simply-learn-ai.github.io/` (`config.toml:1`). There is no application code, only content, config and layout overrides (no root `package.json`, `go.mod` or `Makefile`).

## Do not commit unless asked

- Do not commit, amend or push unless the user explicitly requests it. Make local changes only.

## Build and preview

- Install the theme's PostCSS toolchain once: `cd themes/introduction && npm ci --ignore-scripts` (same as CI, `.github/workflows/deploy.yml:38-40`).
- Production build: `PATH="$PWD/themes/introduction/node_modules/.bin:$PATH" hugo --minify --gc` (CI adds `--baseURL`, `.github/workflows/deploy.yml:54-55`).
- Production builds need Hugo **0.165.0 extended** (`.github/workflows/deploy.yml:45-46`) and the `postcss` binary from `themes/introduction/node_modules/.bin`.
- `hugo server -D` skips PostCSS: server mode takes the `hugo.IsServer` branch in `layouts/partials/head/css.html:3-6` (plain `css.Sass`), while the production branch runs Sass + PostCSS + fingerprint (`layouts/partials/head/css.html:7-10`).
- Local gotcha (observed, environment-specific): the snap Hugo at `/snap/bin/hugo` failed with `POSTCSS: ... binary with name "postcss" not found` even with `themes/introduction/node_modules/.bin` on `PATH`. The standalone gohugoio `0.165.0 extended` binary built the site successfully.

## Deploy

- Pushing to `main` runs `.github/workflows/deploy.yml` (`.github/workflows/deploy.yml:3-5`): it builds and uploads `./public` (`.github/workflows/deploy.yml:60`) with `actions/deploy-pages` (`.github/workflows/deploy.yml:71`).
- This requires the repo's Pages source to be **GitHub Actions** (not "Deploy from a branch"); the workflow depends on `actions/configure-pages` and `actions/deploy-pages` (`.github/workflows/deploy.yml:48-50,69-71`).

## Theme is a submodule

- `themes/introduction` is a git submodule (`.gitmodules:1-3`). Git tracks only the gitlink (`git ls-files themes/introduction` prints `themes/introduction`).
- Never edit files under `themes/introduction/`; those changes are not tracked by this repo, so they are not committed or deployed. Override in the project root instead:
  - `layouts/` (Hugo prefers project layouts over theme layouts)
  - `assets/` (Sass/CSS bundled by Hugo)
  - `static/` (copied verbatim)
  - `config.toml` (params)

Existing project overrides and their intent:

- `layouts/blog/single.html:2`: page heading is the post title. The theme used the section title "Blog" (`themes/introduction/layouts/blog/single.html:1-4`) and repeated the title in an `<h2>` (`themes/introduction/layouts/blog/single.html:9-11`); the override drops the `<h2>`.
- `layouts/blog/single.html:64`: blog body wrapper adds the `blog-content` class used by `assets/css/custom.css`.
- Per-post dates are intentionally hidden by these overrides (the theme shows them at `themes/introduction/layouts/blog/single.html:24`, `themes/introduction/layouts/blog/list.html:10`, `themes/introduction/layouts/partials/blog/li.html:3-4`, `themes/introduction/layouts/partials/blog/archive.html:19-20`, `themes/introduction/layouts/partials/home/blog.html:9`, `themes/introduction/layouts/_default/list.html:10`, `themes/introduction/layouts/_default/taxonomy.html:11`):
  - `layouts/blog/list.html`, `layouts/partials/blog/li.html`, `layouts/partials/home/blog.html`, `layouts/_default/list.html`, `layouts/_default/taxonomy.html`
  - `layouts/partials/blog/archive.html` (still groups posts under a year heading, `layouts/partials/blog/archive.html:5-14`)
- `layouts/partials/head/css.html:16-17` fingerprints `custom.css` (the theme does not, `themes/introduction/layouts/partials/head/css.html:16-17`), so CSS edits reach browsers despite the fixed URL.

## Content model

- English content lives in `content/en/` (`config.toml:89`). Add languages under `[languages]` (`config.toml:85`).
- Homepage template `themes/introduction/layouts/index.html`:
  - Hero renders the `/home` page, i.e. `content/en/home/index.md` (`themes/introduction/layouts/index.html:14-28`).
  - Then renders the `/home` page resources plus `/blog` (and `/projects` when present), sorted by `weight` (`themes/introduction/layouts/index.html:45-57`).
  - `contact.md` is excluded from that loop and rendered last (`themes/introduction/layouts/index.html:58`, `themes/introduction/layouts/index.html:100`).
- Current `weight` values: `content/en/home/about.md:4` = 8, `content/en/blog/_index.md:3` = 20.
- The nav is built from the same pages (`themes/introduction/layouts/nav.html:44-96`), so deleting a section's content also removes its menu entry.
- Raw HTML in Markdown is allowed: `config.toml:72` sets `markup.goldmark.renderer.unsafe = true`, used for the homepage QR `<img>` in `content/en/home/index.md`.
- Homepage QR image: `static/img/simply-learn-ai.png`.

## Styling

- Custom CSS is `assets/css/custom.css`, enabled by `customCSS = ["css/custom.css"]` (`config.toml:17`) and linked via `layouts/partials/head/css.html:16-17`. Do not edit theme Sass for font or colour changes.
- Current conventions there: Abril Fatface for headings, bold and `.bold-title` (`assets/css/custom.css:3-15`); post `## ` (h2) section headings such as `## Introduction` use Playfair Display (weight 800) via `.blog-content h2`; blog body and other post headings use Nunito Sans.

## Housekeeping

- Gitignored build output: `public/`, `resources/_gen/`, `.hugo_build.lock` (`.gitignore:2-4`). Do not commit them.
- `static/.nojekyll` stops GitHub Pages from running Jekyll.
- No tests, linters or formatters are configured for the site. The theme submodule has its own tests (`themes/introduction/package.json`), which this repo does not run.

## Writing

- Do not use Oxford commas in prose.
- Keep the two versions of the AI article in sync: `content/en/blog/ai-without-the-mystery-dot-points.md` is the bullet-point version and `content/en/blog/ai-without-the-mystery-full-article.md` is the prose version. Whenever the dot-point version changes, update the full-article version to match, keeping its prose style.

### Two voices

The dot-point version of the AI article (`content/en/blog/ai-without-the-mystery-dot-points.md`) is written as an even, turn-taking exchange between two complementary perspectives rather than a single narrator. Each bullet is wrapped in a `<span>` that carries the speaker's colour, so the two voices read as a balanced back-and-forth in roughly equal measure. The prose version (`content/en/blog/ai-without-the-mystery-full-article.md`) is plain text with no colour.

- `<span class="voice-teal">` is the analysis-first voice that carries the deeper, higher-value explanation.
- `<span class="voice-maroon">` is the plain-language voice that keeps the everyday framing accessible.

Both classes are defined in `assets/css/custom.css` (teal `#0f766e`, maroon `#800000`); the `li:has(...)::marker` rules colour the matching bullet markers. When editing the dot-point version, keep the two voices close to half and half and give the teal voice the more substantial technical points. No speaker names are shown to readers.
