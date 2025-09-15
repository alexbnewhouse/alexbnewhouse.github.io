# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal academic website built with **Quarto**, a scientific publishing system. The site belongs to Alex Newhouse, a PhD candidate in Political Science specializing in computational analysis of political violence and extremism.

## Architecture

**Quarto Website Structure:**
- `_quarto.yml` - Main configuration file defining website structure, theme (lumen), and navbar
- `*.qmd` - Quarto markdown files that generate the website pages
- `docs/` - Output directory where rendered HTML files are published (GitHub Pages)
- `posts/` - Directory containing blog post subdirectories
- `profpic.jpeg` - Profile image used on the main page

**Key Pages:**
- `index.qmd` - Homepage with personal bio and research overview
- `cv.qmd` - Academic CV
- `research.qmd` - Research projects and publications
- `teaching.qmd` - Teaching experience and tutorial links
- `posts.qmd` - Blog listing page
- `tutorial*.qmd` - Educational content for quantitative methods

## Development Commands

**Build and Preview:**
```bash
quarto render          # Build the entire website to docs/
quarto preview         # Live preview with auto-reload during development
quarto render <file>   # Render specific file
```

**Publishing:**
The site automatically publishes from the `docs/` directory to GitHub Pages when changes are pushed to the main branch.

## Content Guidelines

**Academic Focus:** Content should maintain an academic tone appropriate for a PhD candidate's professional website. The site showcases research on political violence, extremism, and computational social science.

**Teaching Materials:** Tutorial files (tutorial1.qmd, tutorial2-pipe.qmd, etc.) contain educational content for quantitative methods courses. These should be pedagogically sound and accessible to undergraduate students.

**Blog Posts:** Located in `posts/` subdirectories, focused on research, technology, and academia.

## File Naming

- Use lowercase with hyphens for multi-word filenames
- Tutorial files: `tutorial[number]-[topic].qmd`
- Blog posts: `posts/YYYY-MM-DD-[title]/index.qmd`

## Website Features

- Search functionality enabled
- RSS feed for blog posts
- Responsive design with trestles template on homepage
- Social media links (LinkedIn, Bluesky, GitHub, Email)
- Category filtering and sorting for blog posts