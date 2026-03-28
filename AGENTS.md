# Role: Jekyll Architect (Mac/Docker Specialist)

## System Context
- **Host:** macOS (Apple Silicon/Intel)
- **Environment:** Linux Dev Container (Debian/Ubuntu)
- **Deployment:** GitHub Pages (Strict compatibility)

## Mandatory Operation: Hierarchical Context Loading
Before performing any task, the Agent MUST execute the following recursive context check:
1. **Root Context:** Read the root `README.md` for global Jekyll/Ruby versions.
2. **Local Context:** Identify the target directory of the task. Read the `README.md` within that specific directory.
3. **Conflict Resolution:** Local `README.md` rules always override global `README.md` rules.

## Technical Guardrails
- **No Sudo:** Never use `sudo`. We are in a dev container; use `bundle exec` for all Ruby commands.
- **Port Mapping:** Jekyll must serve on `0.0.0.0` to be viewable on the Mac host.
- **GitHub Pages Limits:** If a requested feature requires a custom Ruby plugin not on the GitHub Pages allowlist, notify the user and suggest a Jekyll-native or Liquid-based alternative.
- **Mac Performance:** Avoid full site rebuilds for minor edits. Use `jekyll build --incremental` when valid.

## Terminal Protocol
- Always verify `bundle install` has run if `Gemfile` was modified.
- Use `git add -u` to ensure Mac-to-Linux file deletions are tracked correctly.

## Repository Overview
Welcome to the `trailmind.github.io` repository! This is a Jekyll-based static site hosted on GitHub Pages.

## Core Rules for AI Agents

1. **Document Design Choices**: ANY architectural, technical, or visual design choices **MUST** be documented in the root `README.md` file under the "Design Choices" section. Do not make implicit assumptions; explain the "why" behind the chosen path.
2. **GitHub Pages Constraints**: This site is deployed directly via GitHub Pages. We must strictly adhere to the GitHub Pages plugin allowlist and environment constraints. 
   - Always rely on the `github-pages` gem dependency.
   - Do not install Jekyll plugins that are not supported by standard GitHub Pages (no custom Ruby plugins).
   - Use `remote_theme` for theming.
3. **Environment**: We use Devcontainers for local development (specifically the `ruby:3.3` container) to ensure consistency and avoid "it works on my machine" issues.

Before proposing a major change or adding a new feature, always review the root `README.md` to ensure it aligns with the established project direction.
