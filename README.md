# ajaykumarns.github.io

Personal blog built with Hugo, hosted on GitHub Pages.

## 🚀 Quick Start

### Running Locally

```bash
# Serve the site locally (with live reload)
hugo server -D

# Or build for production
hugo
```

### Creating New Posts

```bash
# Create a new post (replace 'my-post-title' with your title)
hugo new posts/my-post-title/index.md
```

Posts are created in `content/posts/`. Edit the front matter in each post:
- `title`: Post title
- `date`: Publication date
- `draft`: Set to `false` to publish

## 📝 Publishing Blogs

### Option 1: Using the publish script (recommended)

```bash
# Make sure you're on the main branch with all changes committed
git status  # Should be clean

# Run the publish script
./publish.sh
```

The script will:
1. Check for uncommitted changes (exits if any)
2. Create a git worktree with the `master` branch
3. Build the Hugo site to `public/`
4. Commit the built files to master

**Important:** After running `./publish.sh`, you MUST manually push:

```bash
cd public
git push origin master
```

### Option 2: Manual publish

```bash
# Build the site
hugo

# The generated files are in the `public/` directory (if you ran hugo with -d public)
# Or if using the worktree approach:
cd public
git add --all
git commit -m "Publishing blog"
git push origin master
```

## 📁 Project Structure

```
├── content/          # Your content (posts, about, etc.)
│   ├── posts/        # Blog posts
│   ├── about/        # About page
│   └── bookshelf.md  # Books page
├── layouts/          # Hugo templates
├── static/           # Static assets (images, etc.)
├── themes/           # Hugo themes
├── config.toml       # Site configuration
└── publish.sh        # Publishing script
```

## 🔧 Requirements

- **Hugo**: Install via `brew install hugo` (macOS) or download from https://gohugo.io/
- **Git**: For version control

## ⚠️ Notes

- The site uses GitHub Pages with the `master` branch as the publishing source
- Posts in `content/posts/` with `draft: false` will be published
- The `publish.sh` script uses git worktrees to keep source and built files separate

## 🔄 CI/CD (Optional)

The repo includes GitHub Actions workflows in `.github/` for automatic builds. If enabled:
- Push to `main` branch triggers automatic build
- Built files pushed to `master` branch

## 📝 Updating "About" Page

Edit: `content/about/index.md`

To mark projects as retired, use the strikethrough format:
```markdown
- ~~https://example.com~~ - 🏁 Retired - Description
```