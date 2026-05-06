# AGENTS.md

## Project
MkDocs static blog → GitHub Pages. Simple: just Markdown + YAML.

## Commands

```bash
# Dev (live reload)
mkdocs serve

# Validate before commit (fails on warnings/broken links)
mkdocs build --strict

# Check YAML syntax
python -c "import yaml; yaml.safe_load(open('mkdocs.yml'))"
```

## Deployment
- Push to `master` → auto-deploys via GitHub Actions
- See `.github/workflows/deploy.yml`

## Adding Content

1. **New article**: `docs/articles/your-title.md`
2. **Front matter** (required):
   ```yaml
   ---
   title: Title
   date: 2024-01-01
   tags: [tag1]
   ---
   ```
3. **Register in nav**: Edit `nav:` in `mkdocs.yml`

## Config Location
- `mkdocs.yml` - site name, theme (Material), nav, plugins

## Gotchas
- YAML keys must be lowercase (e.g., `site_name`, not `siteName`)
- Use relative links within the project
- Images go in `docs/assets/images/`