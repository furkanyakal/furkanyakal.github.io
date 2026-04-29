# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal portfolio/academic website for Furkan Yakal, built on the [al-folio](https://github.com/alshedivat/al-folio) Jekyll theme. Deployed automatically to GitHub Pages (`gh-pages` branch) whenever changes are pushed to `main`.

## Local development

**Recommended (Docker):**
```bash
docker compose pull
docker compose up
# → http://localhost:8080
```

**Slim image (~100MB):**
```bash
docker compose -f docker-compose-slim.yml up
```

**Native Ruby (legacy):**
```bash
bundle install
pip install jupyter
bundle exec jekyll serve
# → http://localhost:4000
```

**Format Liquid/HTML templates:**
```bash
npx prettier --write .
```

## Content architecture

All personal content lives in these locations — these are the files to edit when updating the site:

| Location | Purpose |
|---|---|
| `_pages/about.md` | Homepage (bio, profile photo, announcements toggle) |
| `_data/cv.yml` | CV page structured data (education, experience, etc.) |
| `assets/json/resume.json` | JSON Resume format (drives the `/cv` page alongside `cv.yml`) |
| `_news/` | Announcements shown on the homepage |
| `_projects/` | Project cards (`1_project.md`, `2_project.md`, …) |
| `_bibliography/papers.bib` | Publications (BibTeX, rendered by jekyll-scholar) |
| `assets/img/` | Images (auto-converted to WebP at build time by imagemagick) |
| `_config.yml` | Site-wide settings: name, URL, feature flags, plugin config |

## Key config patterns

- **Feature flags** in `_config.yml` follow the `enable_*` naming pattern (e.g. `enable_darkmode`, `enable_math`).
- **Third-party library versions** are centrally managed under `third_party_libraries:` in `_config.yml` — do not hardcode CDN URLs in templates.
- The CV page uses both `_data/cv.yml` (for the `/cv` layout) and `assets/json/resume.json` (loaded at build time via `jekyll-get-json`). Keep them in sync.

## Deployment

Pushing to `main` triggers a GitHub Actions workflow that builds the site and pushes the result to the `gh-pages` branch. Do **not** manually edit the `gh-pages` branch.
