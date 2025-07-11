# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal academic website for Dr. Kathryn Loosemore PhD, focusing on her research in International Relations, particularly regarding ETA (Euskadi Ta Askatasuna) terrorism studies. The site is built with Hugo static site generator and deployed via GitHub Pages.

## Tech Stack

- **Hugo**: Static site generator (minimum version 0.112.0)
- **Theme**: Salinger - a clean, minimalistic, mobile-first Hugo theme
- **CSS Framework**: TailwindCSS with DaisyUI components
- **CSS Processing**: PostCSS with Autoprefixer
- **Node.js**: v22.11.0 (for build tooling)

## Common Development Commands

### Initial Setup
```bash
# Install Hugo module dependencies
hugo mod npm pack

# Install npm dependencies
npm install
```

### Development
```bash
# Start development server
hugo server

# Start development server with drafts
hugo server --buildDrafts
```

### Build
```bash
# Build the static site (outputs to /public)
hugo
```

### Deployment
This is a GitHub Pages site. To deploy:
```bash
# Build the site
hugo

# Commit and push changes
git add .
git commit -m "Update site"
git push origin main
```

## Project Structure

### Content Organization
- `/content/`: All website content in Markdown format
  - `_index.md`: Homepage content
  - `/research/`: Academic research articles about ETA terrorism

### Theme Files
- `/themes/salinger/`: Theme directory (avoid modifying directly)
  - `/layouts/`: HTML templates
  - `/assets/`: CSS and JS source files
  - `/static/`: Theme static assets

### Static Assets
- `/static/`: Static files served directly
  - Excel database files (ETA victims list)
  - Research images (charts, graphs)
  - Site logo

### Generated Files
- `/public/`: Build output (do not edit directly)
- `/resources/_gen/`: Hugo's resource cache
- `hugo_stats.json`: CSS class usage for PurgeCSS optimization

## Architecture Notes

### Content Management
- All content is written in Markdown with Hugo front matter
- Research articles are in `/content/research/`
- Taxonomies: categories and tags are configured but not extensively used

### Styling Pipeline
1. TailwindCSS classes are used in templates
2. PostCSS processes the CSS through:
   - Tailwind compilation
   - Autoprefixer for browser compatibility
   - CSS imports resolution
3. Hugo's asset pipeline handles the final optimization

### Theme Customization
- The Salinger theme provides dark/light mode switching
- Custom styling should be added to theme overrides, not by modifying the theme directly
- Theme supports Twemoji, SEO optimization, and responsive design

## Important Considerations

- This is an academic/professional website - maintain formal tone in content
- Research content focuses on ETA terrorism studies and victim databases
- The site serves as both a portfolio and research repository
- When updating content, ensure proper academic citations and data accuracy
- The Excel database in `/static/` contains sensitive victim data - handle with care