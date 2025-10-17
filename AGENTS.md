# AGENTS.md

GitHub Pages (Jekyll) site. No build/test/lint tooling, no package manifest, no CI in the repo.

- `_config.yml` is empty. The `default` layout is not in the repo, so it comes from the GitHub Pages default theme. `_layouts/page.html` and `post.html` extend it.
- `_includes/head-custom.html` is the theme's head hook. It currently includes `copy-button.html`, which adds the code-block copy button.
- Pages are Markdown with front matter (`layout: default`, `title: <filename>`). Follow this for new pages, such as `docs/*.md`.
- `webadb-tool/` is a prebuilt static bundle with hashed asset names under `assets/`. Do not hand-edit it. Replace it as a whole from a build elsewhere.
- `markdown-preview/index.html` is a standalone static page.
- There is no local preview setup. Changes are verified only after pushing to GitHub Pages.
