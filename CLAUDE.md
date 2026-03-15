```
# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.
```

## 入口说明

- 先读 README.md（公共真源）
- 本文件仅保留工具差异项
- 与 README 冲突时以 README 为准

## 执行顺序

1. README.md
2. 命中的 `doc/ai-skills/` 的 `SKILL.md`
3. 本文件差异项

## Project Overview

This is a **Jekyll-based static blog website** for "小张的读书会" (Xiao Zhang's Reading Club), focused on book reviews and reading notes. It's a customized fork of the Hux Blog theme with modern web technologies and PWA support.

## Key Technologies & Stack

- **Static Site Generator:** Jekyll 3.x with GFM (GitHub Flavored Markdown)
- **Build Tools:** Grunt (CSS/JS compilation and minification)
- **CSS:** Less preprocessor, Bootstrap 3.x
- **JavaScript:** Vanilla JS, Service Worker for PWA
- **Comments:** Gitalk (GitHub Issues-based commenting system)
- **Analytics:** Google Analytics and Baidu Analytics
- **Syntax Highlighting:** Rouge
- **Pagination:** Jekyll Paginate plugin

## Build & Development Commands

### Jekyll Commands

```bash
# Local development server (with auto-regeneration)
jekyll serve

# Build static site to _site/ directory
jekyll build
```

### Grunt Commands

```bash
# Install dependencies
npm install

# Compile Less to CSS, minify JS
grunt

# Watch for changes in JS/Less files and auto-recompile
grunt watch

# Compile Less only
grunt less

# Minify JavaScript only
grunt uglify
```

### Package.json Scripts

```bash
# Preview built site with Python 2
npm run preview

# Preview built site with Python 3
npm run py3view

# Watch for changes + preview + Jekyll serve (Python 2)
npm run watch

# Watch for changes + preview + Jekyll serve (Python 3)
npm run py3wa
```

## High-Level Architecture

### Core Structure

```
enilu-en.github.io/
├── _posts/              # Blog posts (Markdown, organized by year)
├── _layouts/            # Jekyll templates (default.html, post.html, page.html, keynote.html)
├── _includes/           # Reusable components (head.html, nav.html, footer.html)
├── _config.yml          # Jekyll configuration
├── css/                 # Compiled stylesheets
├── less/                # Less source files
├── js/                  # JavaScript files
├── img/                 # Images
├── fonts/               # Web fonts
├── pwa/                 # Progressive Web App files
├── index.html           # Homepage (with pagination)
├── about.html           # About page
├── tags.html            # Tags/cloud page
├── 404.html             # Error page
├── offline.html         # Offline fallback page
├── feed.xml             # RSS feed
├── sitemap.xml          # SEO sitemap
└── CNAME                # Custom domain configuration (reading.enlu.cn)
```

### Key Features

1. **Responsive Design:** Bootstrap 3.x-based mobile-friendly layout
2. **Progressive Web App (PWA):** Service Worker for offline mode and add-to-home-screen functionality
3. **Gitalk Comments:** GitHub Issues-based commenting system with Chinese URL support
4. **Tag-Based Categorization:** Browse posts by tags
5. **SEO Optimization:** Sitemap, RSS feed, and metadata
6. **Syntax Highlighting:** Rouge for code blocks
7. **Social Integration:** GitHub, Facebook, Twitter, and other social media links

### Customizations

This is a fork of the Hux Blog theme with specific customizations for "小张的读书会":
- Modified Gitalk to handle long Chinese URLs by truncating to 40 characters
- Content focused on book reviews and reading notes
- Custom domain configuration (reading.enlu.cn)
- Updated social media profiles

## Configuration

### Jekyll (_config.yml)

Key settings:
- Site title, description, and URLs
- Sidebar and social media profiles
- Build settings (markdown engine, highlighter, pagination)
- Gitalk comments configuration
- Analytics (Google Analytics)
- Featured tags
- PWA settings

### Grunt (Gruntfile.js)

Handles:
- Less compilation to CSS (expanded and minified versions)
- JavaScript minification
- Auto-recompilation on file changes
- Banner comments for compiled files

## Deployment

The blog is hosted on GitHub Pages. Key deployment files:
- `CNAME`: Specifies custom domain (reading.enlu.cn)
- `_config.yml`: Configures base URLs and build settings
- `package.json`: Contains deployment scripts (push, boil, cafe)
