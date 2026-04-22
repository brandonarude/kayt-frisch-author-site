# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Hugo static site for author Kayt Frisch. Uses the [hugo-profile](https://github.com/gurusabarish/hugo-profile) theme, vendored as a git submodule at `themes/hugo-profile`.

The repo was just scaffolded (`hugo new site`): `hugo.toml` still has placeholder `baseURL`/`title`, and `content/` is empty. Early customization work should focus on those.

## Commands

- `hugo server -D` — local dev server with drafts, live reload at `http://localhost:1313`.
- `hugo` — build production site into `public/` (already gitignored via `.hugo_build.lock` presence; `public/` is currently committed-as-untracked and should stay out of commits).
- `hugo new content/<section>/<slug>.md` — scaffold a new page from `archetypes/default.md`.
- After cloning: `git submodule update --init --recursive` to populate the theme.

## Architecture notes

- **Theme overrides via mirroring paths.** To customize the theme, copy the file from `themes/hugo-profile/layouts/...` (or `assets/...`, `static/...`, `i18n/...`) into the matching path at the repo root — Hugo's lookup order prefers the project over the theme. Don't edit files inside `themes/hugo-profile/` directly; it's a submodule and changes won't survive updates.
- **hugo-profile is data-driven.** Most of the homepage (hero, about, experience, projects, etc.) is configured through `params` in `hugo.toml` and/or files under `data/`, not by writing content pages. Before adding a new page, check whether the theme already has a section configured by params.
- **Content sections** live under `content/<section>/` with an `_index.md` for the section landing page. Front matter drives rendering; see theme docs for supported keys.
