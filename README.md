# Orthogonal Thoughts by Trailmind

Welcome to the source repository for `trailmind.github.io`.

---

## Design Choices

This section tracks all significant architectural, technical, and styling choices made in this project. 
As per the rules in `AGENTS.md`, any new design choices, deviations, or significant updates must be recorded here.

## 1. Architecture & Environment
* **Framework**: Jekyll (Static Site Generator)
* **Hosting Pipeline**: GitHub Pages
* **Local Environment**: VS Code Devcontainers with `ruby:3.3`. Why? Because GitHub Pages uses Ubuntu runners with specific Ruby versions. We mirror this environment to catch dependency issues locally rather than during CI/CD.

## 2. Dependency Strategy
* **Strict Versioning**: We use the `github-pages` gem directly instead of the generic `jekyll` gem. 
* **Why**: GitHub's build servers run a tightly restricted ecosystem of allowed plugins and theme versions. Installing the `github-pages` gem enforces this state locally; preventing us from hallucinating plugins (like `jekyll-archives` or `jekyll-picture-tag`) that will break the production site.

## 3. Theming & Plugins
* **Theme Installation**: Because of GitHub Pages restrictions, we will utilize `remote_theme` in `_config.yml` instead of downloading theme gems locally. If we build a custom theme from scratch, we will place layouts in `_layouts` rather than a separate gem.
* **Plugins**: Confined strictly to the GitHub Pages allowlist (e.g. `jekyll-feed`, `jekyll-seo-tag`).

## 4. Build Optimization
* **Ignored Folders**: We exclude `_site` and `.devcontainer` from Jekyll's build cycle via `_config.yml`.
* **Why**: When Docker Desktop (especially on macOS) maps local system paths to a container, high I/O folders like `_site` cause massive CPU spikes and slow down the Jekyll regeneration loop. By excluding them from Jekyll's watcher and adding `.DS_Store` to our `.gitignore`, we retain optimal performance.

*(Future choices regarding typography, color palettes, and component structures will be appended here.)*
