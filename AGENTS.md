# Agent Guidelines for al-folio

A simple, clean, and responsive [Jekyll](https://jekyllrb.com/) theme for academics.

---

## Project Overview

**al-folio** is a Jekyll-based static site generator template designed for academics, researchers, and professionals to create portfolio and blog websites. It provides rich features for displaying publications, CV, projects, blog posts, and teaching materials.

**Key Features:**

- CV display with RenderCV/JSONResume format support
- Publication bibliography with BibTeX integration (via jekyll-scholar)
- Blog posts with related posts, categories, and archives
- Projects showcase with masonry layout
- News/announcements section
- Course listings and teaching materials
- Book reviews
- Dark/light mode toggle
- Search functionality
- Responsive design

---

## Technology Stack

### Core Technologies

| Technology  | Version                            | Purpose                                 |
| ----------- | ---------------------------------- | --------------------------------------- |
| **Jekyll**  | v4.x                               | Static site generator (Ruby-based)      |
| **Ruby**    | 3.3.5 (CI), 3.2.2 (some workflows) | Primary runtime                         |
| **Python**  | 3.13                               | Jupyter notebook conversion (nbconvert) |
| **Node.js** | Latest                             | Prettier formatting, PurgeCSS           |
| **Docker**  | -                                  | Local development environment           |

### Key Jekyll Plugins

| Plugin                    | Purpose                             |
| ------------------------- | ----------------------------------- |
| `jekyll-scholar`          | Bibliography management from BibTeX |
| `jekyll-archives-v2`      | Archive page generation             |
| `jekyll-paginate-v2`      | Pagination support                  |
| `jekyll-minifier`         | CSS/JS minification                 |
| `jekyll-terser`           | JavaScript minification             |
| `jekyll-imagemagick`      | Responsive image generation         |
| `jekyll-jupyter-notebook` | Jupyter notebook embedding          |
| `jekyll-tabs`             | Tab UI components                   |
| `jekyll-toc`              | Table of contents generation        |
| `jekyll-feed`             | RSS feed generation                 |
| `jekyll-sitemap`          | XML sitemap generation              |
| `classifier-reborn`       | Related posts calculation           |
| `jemoji`                  | Emoji support                       |

### Code Quality Tools

- **Prettier** v3.8.0+ with `@shopify/prettier-plugin-liquid` – Code formatting (mandatory for PRs)
- **PurgeCSS** – CSS optimization for production builds
- **pre-commit** – Git hooks for basic validation

---

## Project Structure

```
.
├── _bibliography/          # BibTeX bibliography files
│   └── papers.bib
├── _books/                 # Book review entries
├── _data/                  # YAML data files
│   ├── citations.yml       # Citation metrics
│   ├── coauthors.yml       # Co-author information
│   ├── cv.yml              # CV content (RenderCV format)
│   ├── repositories.yml    # GitHub repository listings
│   ├── socials.yml         # Social media links
│   └── venues.yml          # Publication venues
├── _includes/              # Reusable Liquid components
│   ├── figure.liquid       # Responsive images
│   ├── head.liquid         # HTML head section
│   ├── header.liquid       # Site navigation
│   ├── footer.liquid       # Site footer
│   ├── scripts.liquid      # Global scripts
│   ├── projects.liquid     # Project display
│   ├── citation.liquid     # Bibliography entry
│   └── ...
├── _layouts/               # Page layout templates
│   ├── about.liquid        # About/home page
│   ├── post.liquid         # Blog posts
│   ├── page.liquid         # Static pages
│   ├── bib.liquid          # Bibliography
│   ├── distill.liquid      # Distill.pub-style articles
│   ├── cv.liquid           # CV page
│   └── ...
├── _news/                  # News/announcement entries
├── _pages/                 # Static pages
│   ├── about.md
│   ├── blog.md
│   ├── cv.md
│   ├── projects.md
│   ├── publications.md
│   └── ...
├── _plugins/               # Custom Jekyll plugins (Ruby)
├── _posts/                 # Blog posts (YYYY-MM-DD-title.md)
├── _projects/              # Project showcase entries
├── _sass/                  # SCSS stylesheets
├── _scripts/               # JavaScript files
│   ├── search.liquid.js    # Search data generation
│   ├── photoswipe-setup.js # Gallery initialization
│   └── ...
├── _site/                  # Generated site (build output)
├── _teachings/             # Course and teaching entries
├── assets/                 # Static assets
│   ├── css/                # Stylesheets
│   ├── js/                 # JavaScript files
│   ├── img/                # Images
│   ├── pdf/                # PDF files
│   ├── json/               # JSON data
│   ├── jupyter/            # Jupyter notebooks
│   └── bibliography/       # Bibliography details
├── bin/                    # Utility scripts
│   └── entry_point.sh      # Docker entry point
├── .github/
│   ├── workflows/          # GitHub Actions CI/CD
│   └── instructions/       # Detailed file-type instructions
├── _config.yml             # Main Jekyll configuration
├── docker-compose.yml      # Docker Compose config
├── Dockerfile              # Docker image definition
├── Gemfile                 # Ruby dependencies
├── package.json            # Node.js dependencies
└── purgecss.config.js      # PurgeCSS configuration
```

---

## Build and Development Commands

### Local Development (Recommended: Docker)

**Prerequisites:** Docker and Docker Compose installed

```bash
# Pull prebuilt image and start development server
docker compose pull && docker compose up
# Site runs at http://localhost:8080 with live reload

# Rebuild after changing dependencies or Dockerfile
docker compose up --build

# Stop containers and free port 8080
docker compose down

# Use slim Docker image (smaller footprint)
docker compose -f docker-compose-slim.yml up
```

### Legacy: Bundle/Jekyll (Not Recommended)

```bash
# Install Ruby gems
bundle install

# Install Python dependencies
pip install jupyter

# Run development server
bundle exec jekyll serve --port 4000
# Site runs at http://localhost:4000
```

### Production Build

```bash
# Set environment variable
export JEKYLL_ENV=production

# Build site
bundle exec jekyll build

# Output is in _site/ directory
```

---

## Code Style Guidelines

### Prettier Formatting (Mandatory)

All files must be formatted with Prettier before committing:

```bash
# First-time setup
npm install --save-dev prettier @shopify/prettier-plugin-liquid

# Format all files
npx prettier . --write

# Check formatting (CI does this)
npx prettier . --check
```

**Prettier Configuration** (`.prettierrc`):

- Plugins: `@shopify/prettier-plugin-liquid`
- Print width: 150
- Trailing comma: ES5

### Exclusions from Prettier

The following files/directories are excluded (`.prettierignore`):

- `_scripts/*.js` – Mixed Liquid/JavaScript syntax not supported by Prettier

### YAML Style Guidelines

- Use 2 spaces for indentation (never tabs)
- Quote strings containing special characters (`:`, `&`, `#`, `|`, `>`)
- Use `>` for multi-line strings (ignore newlines)
- Use `|` for multi-line strings (preserve newlines)

### Liquid Style Guidelines

- Use 2 spaces for indentation
- Single quotes around strings in Liquid tags
- Use `{%- -%}` (with hyphens) to control whitespace

---

## Testing Instructions

### Pre-Commit Checklist

Before every commit, you **must** run these steps:

1. **Format Code:**

   ```bash
   npx prettier . --write
   ```

2. **Build Locally & Verify:**

   ```bash
   docker compose down
   docker compose up --build
   # Wait for "Server running" message (30-60 seconds)
   # Visit http://localhost:8080
   # Check navigation, pages, images, dark mode toggle
   ```

3. **Verify YAML Syntax:**
   - Check for parse errors in terminal output
   - Common error: `YAML parse error` from special characters

### Build Validation

**Successful build indicators:**

- `Server running...` message appears
- No `Liquid Exception` errors
- No `YAML parse error` messages
- Site accessible at http://localhost:8080

### Common Build Issues

| Issue                                  | Cause                 | Solution                                  |
| -------------------------------------- | --------------------- | ----------------------------------------- |
| `Permission denied` on `.jekyll-cache` | File permissions      | Uncomment USER args in Dockerfile         |
| `Unknown tag 'toc'`                    | Plugin not loading    | Check gh-pages branch deployment settings |
| Port already in use                    | Existing process      | `docker compose down` or kill process     |
| CSS/JS not loading                     | Wrong `url`/`baseurl` | Check `_config.yml` settings              |

---

## CI/CD and Deployment

### GitHub Actions Workflows

Located in `.github/workflows/`:

| Workflow               | Purpose                         | Trigger                |
| ---------------------- | ------------------------------- | ---------------------- |
| `deploy.yml`           | Main deployment to GitHub Pages | Push/PR to main/master |
| `prettier.yml`         | Code formatting validation      | Push/PR to main/master |
| `broken-links.yml`     | Link validation                 | Schedule/manual        |
| `axe.yml`              | Accessibility testing           | Schedule/manual        |
| `codeql.yml`           | Security scanning               | Schedule               |
| `update-citations.yml` | Auto-update citation counts     | Schedule               |
| `render-cv.yml`        | CV PDF generation               | Push to cv.yml         |

### Deployment Process

1. **Build Job** (runs on Ubuntu latest):
   - Sets up Ruby 3.3.5 with bundler cache
   - Sets up Python 3.13
   - Installs ImageMagick
   - Installs/upgrade nbconvert
   - Runs `bundle exec jekyll build` with `JEKYLL_ENV=production`
   - Runs PurgeCSS for CSS optimization
   - Deploys `_site/` to `gh-pages` branch

2. **Prettier Check** (parallel):
   - Runs `npx prettier . --check`
   - Fails PR if formatting issues found
   - Generates HTML diff artifact on failure

### Deployment Configuration

**Critical `_config.yml` settings:**

```yaml
# Personal site (username.github.io)
url: https://username.github.io
baseurl:  # leave empty

# Project site (username.github.io/repo-name/)
url: https://username.github.io
baseurl: /repo-name/
```

---

## Content File Types and Guidelines

### Markdown Content

Content files are in `_books/`, `_news/`, `_pages/`, `_posts/`, `_projects/`, `_teachings/`.

**Frontmatter Examples:**

```yaml
# Blog Post (_posts/YYYY-MM-DD-title.md)
---
layout: post
title: Post Title
date: 2024-01-15
categories: research
description: Brief description
---
# Project (_projects/project-name.md)
---
layout: page
title: Project Name
description: Short description
img: /assets/img/project-image.jpg
importance: 1
---
# Page (_pages/page-name.md)
---
layout: page
title: Page Title
permalink: /pathname/
description: Brief description
---
```

### BibTeX Bibliography

File: `_bibliography/papers.bib`

Standard BibTeX format with al-folio custom keywords:

- `pdf` – Path to PDF file
- `code` – URL to source code
- `preview` – Preview image path
- `doi` – DOI identifier
- `selected` – Boolean to feature on publications page
- `abstract` – Full abstract text

Example:

```bibtex
@article{smith2023,
  title={Important Research},
  author={Smith, John},
  journal={Nature},
  year={2023},
  pdf={smith2023.pdf},
  code={https://github.com/example/repo},
  selected={true}
}
```

### YAML Configuration

Main config: `_config.yml`
Data files: `_data/*.yml`

**Key sections in `_config.yml`:**

- Site settings (title, name, description, url, baseurl)
- Feature flags (enable\_\* options)
- Plugin configurations
- Third-party library URLs and versions

### Liquid Templates

Templates in `_includes/` and `_layouts/`:

- Use Liquid syntax for conditionals and loops
- Processed by Jekyll during build
- Can access `site` and `page` variables

### JavaScript Files

Files in `_scripts/`:

- `.liquid.js` files: Processed by Jekyll Liquid engine first
- `.js` files: Passed through as-is
- Use frontmatter with `permalink` to specify output path

Example:

```javascript
---
permalink: /assets/js/my-script.js
---
// JavaScript code here
console.log('Hello');
```

---

## Security Considerations

1. **Dependencies:**
   - Keep Ruby gems updated via `bundle update`
   - Keep Node.js packages updated via `npm update`
   - Check for security advisories regularly

2. **Third-party Libraries:**
   - Libraries loaded from CDN with SRI hashes
   - Integrity hashes defined in `_config.yml`
   - Never load external scripts without integrity checks

3. **Sensitive Data:**
   - Never commit secrets to repository
   - Use GitHub Secrets for CI/CD sensitive values
   - `_site/` directory is in `.gitignore`

4. **User Content:**
   - Jekyll processes user-provided content (Markdown)
   - Use `| escape` filter when outputting user content in templates
   - Be cautious with HTML in Markdown

---

## Quick Reference

### Essential File Locations

| Purpose       | Location                                |
| ------------- | --------------------------------------- |
| Main config   | `_config.yml`                           |
| Site metadata | `_config.yml` (title, description, url) |
| Social links  | `_data/socials.yml`                     |
| CV content    | `_data/cv.yml`                          |
| Publications  | `_bibliography/papers.bib`              |
| Blog posts    | `_posts/*.md`                           |
| Projects      | `_projects/*.md`                        |
| Static pages  | `_pages/*.md`                           |
| Styles        | `_sass/*.scss`                          |
| Layouts       | `_layouts/*.liquid`                     |
| Includes      | `_includes/*.liquid`                    |
| Scripts       | `_scripts/*.js`                         |

### Common Commands

```bash
# Start development server
docker compose up

# Format code
npx prettier . --write

# Build for production
export JEKYLL_ENV=production && bundle exec jekyll build

# Check formatting
npx prettier . --check
```

### Feature Flags (in `_config.yml`)

| Flag                        | Description                 |
| --------------------------- | --------------------------- |
| `enable_darkmode`           | Light/dark mode toggle      |
| `enable_math`               | MathJax for equations       |
| `enable_publication_badges` | Altmetric/Dimensions badges |
| `enable_masonry`            | Masonry layout for projects |
| `enable_medium_zoom`        | Image zoom on click         |
| `search_enabled`            | Site search functionality   |

---

## Troubleshooting Resources

- **Setup/Deployment Help:** [INSTALL.md](INSTALL.md)
- **Customization Guide:** [CUSTOMIZE.md](CUSTOMIZE.md)
- **Troubleshooting:** [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
- **FAQ:** [FAQ.md](FAQ.md)
- **GitHub Issues:** https://github.com/alshedivat/al-folio/issues

---

## File-Type Specific Instructions

For detailed guidance on specific file types, see:

| File Type           | Instruction File                                                                                                       |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Markdown content    | [`.github/instructions/markdown-content.instructions.md`](.github/instructions/markdown-content.instructions.md)       |
| YAML configuration  | [`.github/instructions/yaml-configuration.instructions.md`](.github/instructions/yaml-configuration.instructions.md)   |
| BibTeX bibliography | [`.github/instructions/bibtex-bibliography.instructions.md`](.github/instructions/bibtex-bibliography.instructions.md) |
| Liquid templates    | [`.github/instructions/liquid-templates.instructions.md`](.github/instructions/liquid-templates.instructions.md)       |
| JavaScript          | [`.github/instructions/javascript-scripts.instructions.md`](.github/instructions/javascript-scripts.instructions.md)   |

---

_This document is intended for AI coding agents working on the al-folio project. For human contributors, see the README.md and other documentation files._
