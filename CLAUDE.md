# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based personal blog hosted on GitHub Pages. The site uses the Hacker theme and automatically builds when changes are pushed to the main branch.

## Key Commands

Since this site uses GitHub Pages, all building happens automatically on GitHub's servers. Local development is not required, but if needed:

## Site Structure

- **Posts**: Must be placed in `_posts/` directory with naming format `YYYY-MM-DD-title.md`
- **Pages**: Root-level `.md` files (about.md, contact.md, etc.)
- **Config**: `_config.yml` contains site configuration
- **Theme**: Uses `pages-themes/hacker@v0.2.0` remote theme

## Content Guidelines

**Blog Post Format:**
```yaml
---
layout: post
title: "Post Title"
description: "Brief description"
date: YYYY-MM-DD
categories: [category1, category2]
tags: [tag1, tag2, tag3]
author: "Manikandaraj Srinivasan"
---
```

**Important Configuration:**
- `github.is_project_page: false` removes the "View on GitHub" button
- Remote theme is configured for GitHub Pages compatibility
- Site automatically lists recent posts on homepage

## Deployment

- Pushes to `main` branch trigger automatic GitHub Pages builds
- No manual deployment or CI/CD setup required
- Site available at configured GitHub Pages URL
