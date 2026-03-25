# AGENTS.md - Hugo Blog Repository

## Overview

Personal blog of Ajay Kumar (ajaykumarns), built with Hugo and deployed to GitHub Pages.

## Blog Post Workflow

1. Create/edit content in `content/posts/`
2. Use Hugo frontmatter:
   ```yaml
   ---
   title: "Your Post Title"
   date: YYYY-MM-DD
   draft: false
   tags: ["tag1", "tag2"]
   categories: ["Category"]
   description: "Brief description for SEO"
   ---
   ```
3. Preview locally with `hugo server`
4. When ready, set `draft: false`
5. Push to trigger GitHub Pages deployment

## Hugo Commands

- **Preview:** `hugo server -D` (includes drafts)
- **Build:** `hugo` (outputs to `public/`)
- **New post:** `hugo new posts/your-post-name.md`

## File Structure

```
content/posts/      → Blog posts (Markdown)
content/about.md    → About page
static/             → Static assets (images, files)
themes/             → Hugo theme (git submodule)
public/             → Built site (git subtree, pushed to gh-pages branch)
```

## Content Guidelines

- Write in clear, concise English
- Use code blocks with syntax highlighting
- Include relevant images in `static/` and reference with absolute paths
- Add appropriate tags and categories

## Deployment

Site auto-deploys via GitHub Pages on push to main branch.
