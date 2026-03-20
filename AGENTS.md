# AGENTS.md - Codebase Guidelines

## Project Overview

This is a personal blog website built with Jekyll, hosted on GitHub Pages. The site uses the Emerald theme with SCSS styling and vanilla JavaScript.

**Technology Stack:**
- Jekyll (static site generator)
- Liquid templating language
- SCSS (compiled to CSS)
- Vanilla JavaScript (ES5)
- HTML5

---

## Build Commands

### Local Development

```bash
# Install dependencies (requires Ruby and Bundler)
bundle install

# Serve site locally with live reload
bundle exec jekyll serve

# Serve on a different port
bundle exec jekyll serve --port 4000

# Build the site (outputs to ./_site)
bundle exec jekyll build

# Build for production (minified)
JEKYLL_ENV=production bundle exec jekyll build
```

### GitHub Pages Deployment

Push to `main` branch and GitHub Pages automatically builds via Jekyll.

---

## No Test Suite

This project has **no automated tests**. Manual testing is required:
- Test all pages render correctly
- Verify navigation works
- Check responsive layout on mobile
- Validate HTML/CSS in browser dev tools

---

## Code Style Guidelines

### General Principles
- KISS (Keep It Simple, Stupid)
- Minimal dependencies
- Mobile-first responsive design
- Semantic HTML

### HTML/Liquid Templates

**File Structure:**
- `_layouts/` - Page templates (default.html, post.html, page.html)
- `_includes/` - Reusable component snippets
- Templates use Liquid: tag markers for logic, double braces for output

**Formatting:**
```liquid
{% if condition %}
  <html>
{% else %}
  <other>
{% endif %}
```

**Front Matter Required:**
Every page/post must include YAML front matter:
```yaml
---
layout: post
title: My Title
---
```

### SCSS Styling

**Location:** `css/` directory with SCSS partials in `_sass/`

**Conventions:**
- Use existing color variables and mixins from `_sass/` files
- Follow BEM-like naming: `.block__element--modifier`
- Mobile-first media queries (base styles, then `@media (min-width: 940px)`)
- Avoid !important except as last resort

**Vendor Prefixes:**
Use mixins for cross-browser properties (border-radius, box-sizing)

### JavaScript

**Location:** `js/main.js`

**Conventions:**
- Vanilla JS only (no frameworks)
- Handle null checks before DOM operations
- Support IE10+ with addEventListener/attachEvent pattern
- Use `var` for variables (ES5 compatible)

**Example pattern:**
```javascript
var element = document.getElementById("id");
if (element !== null) {
  element.addEventListener('click', handler);
}
```

### File Naming

- Posts: `YYYY-MM-DD-title.md` format in `_posts/`
- Layouts: lowercase with hyphens `default.html`
- Includes: lowercase with hyphens `head.html`

---

## Jekyll Configuration

**Key settings in `_config.yml`:**
- `markdown: kramdown` - Markdown processor
- `permalink: /:title` - Post URL structure
- `paginate: 8` - Posts per page
- `gems: [jekyll-paginate]` - Plugins

**Site Variables:**
- `site.baseurl` - Relative path (use for all internal links)
- `site.url` - Full production URL

---

## Content Guidelines

### Posts
- Write in Markdown with YAML front matter
- Use `<!-- more -->` for excerpt separator on index
- Truncate with `| strip_html | truncatewords:50`

### Images
- Place in `/img/` directory
- Reference with absolute paths or `{{ site.baseurl }}/img/...`

---

## Git Workflow

1. Create feature branches for changes
2. Test locally before committing
3. Commit messages: clear, concise descriptions
4. No force pushes to main

---

## Common Issues

**Site not updating:**
- Clear `_site/` and rebuild: `rm -rf _site && jekyll build`
- Check front matter syntax

**SCSS changes not appearing:**
- Ensure `css/main.scss` is importing partials correctly
- Rebuild: `jekyll build`

**Port already in use:**
- Use `--port` flag to specify different port
