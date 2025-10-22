# Repository Guidelines

## Project Structure & Module Organization
Source notebooks and pages live in `index.qmd`, `about.qmd`, and topic folders under `posts/` (one `.qmd` per article). The Quarto build emits static assets into `docs/`; edit those only via regeneration. Shared assets sit at repo root: `_quarto.yml` defines site metadata, `styles.css` holds custom styling, and `header-snippet.html` injects curated analytics. Keep new media in `posts/<slug>/images/` and reference them with relative paths.

## Build, Test, and Development Commands
Use Quarto for every build step:
```bash
quarto render            # rebuilds the full site into docs/
quarto preview           # live-reloads while editing .qmd files
quarto check             # validates project config and external links
```
Run `quarto preview` before committing layout-heavy changes so you can verify navigation, theming, and inline HTML snippets.

## Coding Style & Naming Conventions
Write content in Quarto Markdown with sentence-case headings and informative link text. YAML front matter should use two-space indentation and double quotes for strings touching special characters. Favor fenced code blocks with an info string (` ```python `) to enable syntax highlighting. Keep inline HTML minimal; when needed, format it compactly to match `header-snippet.html`. New post directories should follow `posts/<yyyy-mm-title>/` or another descriptive, kebab-case slug.

## Testing Guidelines
No automated test suite exists, so rely on manual verification. After editing, run `quarto render` and spot-check the generated `docs/` pages for broken layouts or stale scripts. Use `quarto check` to catch missing assets and dead links. For regression checks, search with `rg` to confirm that deprecated URLs or tracking pixels have not reappeared.

## Commit & Pull Request Guidelines
Compose commits in the imperative mood with concise summaries (≤72 characters) and optional detail bullets in the body; for example, `Remove CloudFront tracking script`. Group unrelated edits into separate commits to simplify review. Pull requests should outline the change scope, list verification steps (`quarto render`, manual checks), and include screenshots or GIFs when UI output shifts. Link relevant issues and call out any content requiring special review (e.g., third-party scripts).

## Security & Configuration Tips
Review any external scripts before inclusion; define them centrally in `header-snippet.html` so they can be audited and removed quickly. Keep `_quarto.yml` synchronized with navigation changes to avoid orphaned pages. When rotating analytics or CDN assets, search the `docs/` output to ensure no legacy references remain prior to deployment.
