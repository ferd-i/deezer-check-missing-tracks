# Repository Guidelines

This repository ships as a single-page utility for comparing Deezer playlists and tracking missing tracks. Keep contributions lean, documented, and easy to review so the tool stays quickly deployable.

## Project Structure & Module Organization
- `deezer_tri_webapp_proxy (1).html` is the only source file; it embeds HTML layout, scoped CSS, and vanilla JavaScript helpers for playlist loading, filtering, and export actions.
- Group future assets under `assets/` subfolders and update the HTML references accordingly.
- When extending the script, cluster related helpers together (theme, table pagination, CSV import) so reviewers can follow the flow that starts in `window.onload`.

## Build, Test, and Development Commands
- `open "deezer_tri_webapp_proxy (1).html"` opens the page in the default browser for quick smoke checks on macOS.
- `python3 -m http.server 8000` serves the file locally so `fetch` calls mimic production CORS behaviour; browse `http://localhost:8000/deezer_tri_webapp_proxy (1).html`.
- Clear local storage between runs with the browser devtools “Application → Storage → Local Storage” panel to validate first-run behaviour.

## Coding Style & Naming Conventions
- Use four-space indentation for HTML, CSS, and JavaScript to match the current file.
- Follow camelCase for JavaScript functions (`initTheme`, `applyFilter`) and kebab-case for CSS class names.
- Prefer `const`/`let`, keep DOM selectors cached when reused, and add short explanatory comments only where code intent is non-obvious.
- Place configuration constants (storage keys, focus size) near the top of the script and surface new UI controls via `data-*` attributes rather than hard-coding IDs.

## Testing Guidelines
- There is no automated test harness yet; rely on manual verification by loading the page, exercising playlist import, filter toggles, CSV export, and dark/light theme switching.
- Log browser console warnings and ensure network calls to Deezer endpoints resolve as expected; include screenshots or HAR files if you spot API regressions.
- If you introduce tooling (e.g., Jest for unit tests or Playwright for E2E), document the command in this guide and keep specs under a `tests/` directory.

## Commit & Pull Request Guidelines
- The project lacks an established Git history; adopt conventional commits (e.g., `feat: add bulk export validation`) to describe intent succinctly.
- Keep pull requests scoped: explain motivation, list impacted UI behaviours, and attach before/after captures when modifying the table or theme.
- Reference any related issue IDs, note manual test steps performed, and call out risks such as API rate limits or changes to local storage schema.
