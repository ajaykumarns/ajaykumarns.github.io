# ajaykumarns.github.io

Personal blog built with Hugo, hosted on GitHub Pages.

## Quick Start

```bash
# Install Hugo (macOS)
brew install hugo

# Serve locally with drafts
hugo server -D

# Create new post
hugo new posts/my-post-title/index.md
```

## Publishing

### Automatic (GitHub Actions)
Push to `site` branch - GitHub Actions auto-builds and deploys.

### Manual
```bash
./publish.sh
cd public && git push origin master
```

## Project Structure

```
content/posts/    → Blog posts (Markdown)
content/about/    → About page
static/           → Images and assets
themes/arberia/   → Hugo theme
config.toml       → Site configuration
```

## Requirements

- **Hugo** (extended version): Install via `brew install hugo` or download from https://gohugo.io/
- **Git**: For version control

## Notes

- Source branch: `site` → Deploy branch: `master`
- Set `draft: false` to publish posts
- Theme is a git submodule - clone with `--recursive`

---

For detailed conventions, frontmatter reference, and development guidelines, see [AGENTS.md](AGENTS.md).