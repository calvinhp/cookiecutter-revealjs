# Repository Guidelines

## Project Structure & Module Organization
This repo is a Cookiecutter template. The root `cookiecutter.json` defines prompts (title, event, year, slug, keywords, author info), and all scaffolded assets live in `{{cookiecutter.presentation_slug}}/`. Inside that directory:

- `slides.md` — Pandoc Markdown source with YAML front matter and Jinja2 template variables.
- `images/` — presentation media (tracked with Git LFS in generated projects).
- `themes/` — SCSS themes (`wildclouds`, `wildclouds_night`, `wildclouds_white`, `minions_white`). During builds, the active theme is copied to `css/theme/` and compiled via Vite.
- `tricks.yaml` — watchdog config for `make watch`.
- `Makefile` — orchestrates Reveal.js fetch, npm install, plugin copying, Pandoc rendering, and dev server.
- `.github/workflows/static.yml` — GitHub Actions workflow (wrapped in `{% raw %}`/`{% endraw %}` Jinja tags) that builds and deploys to GitHub Pages using Pandoc 3.8.2 with LFS support.

The default theme is `wildclouds`, set via the `slide-theme` variable at the top of the Makefile.

## Build, Test, and Development Commands
- `cookiecutter .` scaffolds a new presentation locally; pass the GitHub URL for remote use.
- `nvm install --lts` aligns Node with the expected Reveal.js toolchain.
- `make index.html` fetches Reveal.js (if not present), runs `npm install`, copies built plugins to `plugin/` paths expected by Pandoc's revealjs template, and renders slides via Pandoc.
- `make start` builds then launches the Reveal.js dev server with live reload.
- `make watch` (requires `watchmedo` / `watchdog`) rebuilds whenever Markdown changes; configured via `tricks.yaml`.
- `npm run build:styles` regenerates theme CSS if you touch SCSS sources (the Makefile calls this automatically for the active theme).
- `make clean` removes all Reveal.js artifacts (js/, css/, dist/, node_modules/, etc.) to reset the working directory.
- `make help` prints available Make targets with descriptions.

## Coding Style & Naming Conventions
Author slides in Markdown with Pandoc attributes; prefer fenced blocks and explicit IDs (`# Slide Title {.class}`). Use fenced divs with colons for credits and speaker notes (`::: notes`). Indent YAML front matter with two spaces. Follow SCSS conventions already present: 2-space indentation, descriptive `$variable` names, and import ordering (`@import` template files before custom rules). Name new template files with lowercase-hyphenated or lowercase-underscore patterns to match existing assets (e.g., `wildclouds_night.scss`).

When editing the GitHub Actions workflow, keep the `{% raw %}`/`{% endraw %}` wrapper intact so Jinja2 doesn't interpret GitHub Actions expressions like `${{ }}`.

## Testing Guidelines
There is no automated test suite; rely on manual verification. After edits, run `make index.html` to ensure Pandoc completes without warnings, then use `make start` to review behavior in the browser. If you adjust themes, confirm `dist/theme/<theme>.css` regenerates via `npm run build:styles` and inspect slides for visual regressions. For GitHub Actions changes, verify the workflow YAML is valid and that the `{% raw %}` wrapper is preserved. Document any required manual checks in the generated project's README when you introduce nonstandard behavior.

## Commit & Pull Request Guidelines
Adopt Conventional Commit prefixes (`feat:`, `fix:`, `docs:`) as seen in the history (`feat: enable Git LFS…`). Scope template-only changes with clear descriptions (e.g., `feat: add keynote-style layout`). For pull requests, include: summary of template impact, sample command output or screenshots from a generated project, and links to related issues. Run the relevant `make` targets before submission and note any manual verification performed to help reviewers reproduce results quickly.
