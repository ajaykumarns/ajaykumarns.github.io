# AGENTS.md - Hugo Blog Repository

## Overview

Personal blog of Ajay Kumar (ajaykumarns), built with Hugo and deployed to GitHub Pages. Source code lives on the `site` branch; deployed content goes to `master` branch via GitHub Actions.

## Repository Structure

| Branch | Purpose |
|--------|---------|
| `site` | Source content (Hugo files, markdown, config) |
| `master` | Deployed/built site (GitHub Pages serves from here) |

## File Structure

```
content/posts/     → Blog posts (Markdown with frontmatter)
content/about/     → About page
content/bookshelf.md → Books page
content/fav-quotes.md → Quotes page
static/            → Static assets (images, files) - reference with absolute paths
themes/arberia/    → Hugo theme (git submodule)
public/            → Built site (git worktree pointing to master branch)
config.toml        → Hugo configuration
publish.sh         → Manual deployment script
.github/workflows/ → GitHub Actions CI/CD
```

## Git Workflow

### Branch Naming
- Source branch: `site`
- Deploy branch: `master`

### Standard Workflow
```bash
# 1. Make changes to content
# 2. Preview locally
hugo server -D

# 3. Commit to site branch
git add .
git commit -m "Add new blog post"
git push origin site

# 4. GitHub Actions auto-deploys on push to site branch
```

### Manual Deployment (Alternative)
```bash
# Ensure working directory is clean
git status

# Run publish script (builds to public/ and commits to master)
./publish.sh

# Manually push from the public worktree
cd public && git push origin master
```

## Blog Post Workflow

### Creating New Posts

```bash
hugo new posts/my-post-title/index.md
```

This creates `content/posts/my-post-title/index.md` with default frontmatter.

### Frontmatter Reference

```yaml
---
title: "Your Post Title"
subtitle: "Optional subtitle"
date: 2024-04-07T10:30:00+05:30
lastmod: 2024-04-07T10:30:00+05:30
draft: false
type: standard-view
weight: 1

featured: true
sidebar: true
toc: true
math:
  enable: false
lightgallery: false
license: ""

hiddenFromHomePage: false
hiddenFromSearch: false

author: Ajay Nadathur
description: "Brief description for SEO and social sharing"

tags:
  - Tag1
  - Tag2
categories:
  - blog
  - tech

resources:
  - name: featured-image
    src: blog-posts.jpg
---
```

### Key Frontmatter Fields

| Field | Required | Description |
|-------|----------|-------------|
| `title` | Yes | Post title |
| `date` | Yes | Publication date (ISO 8601 format) |
| `draft` | Yes | Set to `false` to publish |
| `description` | Recommended | SEO description (150-160 chars) |
| `tags` | Recommended | Array of tags for categorization |
| `categories` | Recommended | Array of categories |
| `featured` | Optional | Show on homepage featured section |
| `toc` | Optional | Enable table of contents |
| `subtitle` | Optional | Subtitle displayed below title |

### Draft vs Published

- `draft: true` - Post is hidden in production
- `draft: false` - Post is published
- Use `hugo server -D` to preview drafts locally

## Hugo Commands

```bash
# Local development server (with drafts)
hugo server -D

# Local development server (production mode)
hugo server

# Build for production
hugo

# Build with minification (what CI uses)
hugo --gc --minify

# Create new post
hugo new posts/post-slug/index.md

# Create new page
hugo new page-name.md
```

## Content Guidelines

### Writing Style
- Write in clear, concise English
- Use proper markdown formatting
- Include meaningful headings (h2, h3 hierarchy)
- Break long content into sections

### Code Blocks
Use syntax-highlighted code blocks:

````markdown
```python
def hello():
    print("Hello, World!")
```
````

### Images
- Place images in `static/img/posts/` or post folder
- Reference with absolute paths: `/img/posts/image.jpg`
- Use `resources` in frontmatter for featured images

### Links
- Internal links: `/posts/my-post/` (relative to site root)
- External links: Full URL with `https://`

### About Page
- Edit: `content/about/index.md`
- Mark retired projects with strikethrough: `~~https://example.com~~ - 🏁 Retired - Description`

## Deployment

### Automatic (GitHub Actions)
- Triggered on push to `site` branch
- Workflow file: `.github/workflows/hugo.yml`
- Uses Hugo version specified in workflow (0.136.5)
- Automatically builds and deploys to GitHub Pages

### Manual (publish.sh)
Use when GitHub Actions is disabled or for manual control:
```bash
./publish.sh
cd public && git push origin master
```

## Configuration

### config.toml Key Settings

| Setting | Value |
|---------|-------|
| baseURL | `https://nadathurx.com/` |
| theme | `arberia` |
| title | `NadathurX` |
| summaryLength | `30` |
| permalinks.posts | `/:title/` |

### Theme-Specific Features
- Table of contents (tocMinWordCount: 100)
- Reading time display
- Social sharing buttons
- Google Analytics (ID in config)
- Disqus comments support

## Common Tasks

### Add New Tag
Tags are auto-generated from frontmatter. Just add to tags array in post.

### Modify Site Navigation
Edit `[[menu.main]]` sections in `config.toml`.

### Change Theme Settings
Edit `[Params]` section in `config.toml`.

### Add Social Links
Edit `[Params.social]` in `config.toml`.

## Troubleshooting

### Site Not Updating
1. Check GitHub Actions workflow succeeded
2. Verify `draft: false` in frontmatter
3. Check build logs for errors

### Posts Not Appearing
1. Verify date is in the past (not future dated)
2. Check `hiddenFromHomePage` is not `true`
3. Ensure proper `categories` taxonomy

### Theme Issues
```bash
# Update theme submodule
git submodule update --init --recursive
```

## Important Notes

- Never edit `public/` directly - it's a worktree
- Always commit to `site` branch only
- Theme is a git submodule - use `--recursive` when cloning
- Images in `static/` use absolute paths from site root