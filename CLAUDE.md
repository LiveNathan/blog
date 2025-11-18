# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a personal blog repository built with Jekyll and hosted on GitHub Pages. The blog documents Nathan Lively's
journey building micro-SaaS products, with technical posts covering audio physics, software development (Java, Vaadin,
Spring), and entrepreneurship. Posts are written in a stream-of-consciousness style, often via dictation, then organized
with AI assistance before final edits.

## GitHub Repository

- **Repository:** LiveNathan/blog
- **GitHub URL:** https://github.com/LiveNathan/blog
- **Published Site:** https://livenathan.github.io/blog

**GitHub API Access:**
You can access repository contents via the GitHub API:

- Images: `https://api.github.com/repos/LiveNathan/blog/contents/assets/images`
- Posts: `https://api.github.com/repos/LiveNathan/blog/contents/_posts`
- Audio: `https://api.github.com/repos/LiveNathan/blog/contents/assets/audio`
- Root: `https://api.github.com/repos/LiveNathan/blog/contents/`

## Repository Structure

```
blog/
├── _posts/           # Blog posts in markdown format
├── assets/
│   ├── images/       # Images referenced in posts (PNG, SVG)
│   │   └── 2025/     # Organized by year
│   └── audio/        # Audio samples (.wav files)
├── _config.yml       # Jekyll configuration
└── index.md          # Home page
```

## Jekyll Configuration

**Site Details:**

- Theme: minima
- Markdown processor: kramdown
- Base URL: `/blog`
- Published URL: https://livenathan.github.io/blog
- Plugins: jekyll-feed

**Post Defaults:**

- Layout: `post`
- Comments: enabled

## Blog Post Format

All posts must follow this naming convention: `YYYY-MM-DD-slug-title.md`

**Front Matter Template:**

```yaml
---
layout: post
title: "Your Post Title"
date: YYYY-MM-DD HH:MM:SS -0000
categories: [category1, category2, category3]
---
```

**Common Categories:**

- micro-saas, directories, validation, entrepreneurship, building-in-public
- audio-physics, dsp, convolution, filtering
- java, vaadin, spring, tdd, hexagonal-architecture
- power, electrical, av-production, live-events, production-av

## Asset Management

**Images:**

- Store in `assets/images/` or `assets/images/YYYY/` for year-specific content
- Supported formats: PNG, SVG
- Reference in posts using relative paths: `/blog/assets/images/filename.png`

**Audio Files:**

- Store in `assets/audio/`
- Supported format: WAV
- Used for demonstrating audio processing concepts

## Development Workflow

**Local Development:**
Since there's no Gemfile in the repository, you'll need to set up Jekyll manually:

```bash
# Install Jekyll and bundler
gem install jekyll bundler

# Create a Gemfile if needed for local development
bundle init
bundle add jekyll minima jekyll-feed

# Serve the site locally
bundle exec jekyll serve --baseurl ''
```

**Preview:**
The site will be available at `http://localhost:4000`

**Building:**

```bash
bundle exec jekyll build
```

Generated files appear in `_site/` (ignored by git).

## Git Workflow

Main branch: `main`

The repository is clean and deployment happens automatically via GitHub Pages when pushing to main.

## Content Guidelines

**Writing Style:**

- Stream-of-consciousness brain dumps, typically via dictation
- Organized with AI assistance (usually Claude)
- Final human edits for clarity and tone
- Conversational, personal, and transparent about the process
- Posts often include personal anecdotes and humor

**Technical Content:**

- Deep dives into audio DSP concepts (overlap-save convolution, comb filtering, sample-accurate kernel switching)
- Software architecture discussions (Java, Spring Boot, Vaadin)
- Infrastructure and deployment topics (Railway, Coolify, Docker, PostgreSQL, Redis)
- LLM experimentation and benchmarking
- Power distribution and electrical systems for AV production

**Visual Content:**

- Technical diagrams and illustrations to explain complex concepts
- Screenshots and demo images
- Charts and comparison tables

## Notes for Future Development

- The blog has no Gemfile currently; local development requires manual Jekyll setup
- Posts are date-prefixed with future dates (2025) as this represents planned content
- The site uses GitHub Pages' automatic deployment (no manual build/deploy needed)
- Social links are configured in `_config.yml` for GitHub, Twitter/X, and LinkedIn
