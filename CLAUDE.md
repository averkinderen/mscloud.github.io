# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based blog website hosted on GitHub Pages, focused on Azure cloud management and Microsoft technologies. The site uses the Minimal Mistakes theme and is published at https://mscloud.be.

## Development Environment

### Prerequisites
- Ruby (with Bundler)
- Node.js (for JavaScript asset compilation)
- Jekyll and dependencies via Bundler

### Building and Running

**Local development server:**
```bash
bundle exec jekyll serve
```
The site will be available at `http://localhost:4000` with live reload enabled.

**Build the site:**
```bash
bundle exec jekyll build
```
The compiled site will be in the `_site` directory.

**JavaScript asset compilation:**
```bash
npm run build:js
```
This uglifies JavaScript files and adds banners. The watch command is:
```bash
npm run watch:js
```

### Installing Dependencies

**Ruby dependencies:**
```bash
bundle install
```

**Node dependencies:**
```bash
npm install
```

## Site Architecture

### Content Structure

**Blog posts:** `_posts/`
- Named with format: `YYYY-MM-DD-post-title.md`
- Include YAML front matter with: title, author, categories, tags, header (optional)
- Use markdown format
- Images referenced from `/assets/images/` or `/wp-content/uploads/`

**Static pages:** `_pages/`
- Contains about, categories, tags, year-archive, and 404 pages
- Use layout and permalink in front matter

**Drafts:** `_drafts/`
- Work-in-progress posts without dates in filename
- Not published to the live site

### Configuration Files

**_config.yml:** Main Jekyll configuration
- Site metadata and author info
- Theme configuration (using remote_theme: "mmistakes/minimal-mistakes")
- Plugin settings (jekyll-paginate, jekyll-sitemap, jekyll-feed, etc.)
- Default layouts and front matter
- Analytics, comments (Disqus), and social sharing settings
- Permalink structure: `/:categories/:title/`
- Pagination: 5 posts per page
- Timezone: Australia/Sydney

**_data/navigation.yml:** Site navigation menu structure
- Defines main navigation: Categories, Tags, About me

**_data/authors.yml:** Author profiles for multi-author support

### Theme Customization

**_includes/:** Custom includes and theme overrides
- Analytics providers, comments providers
- Custom author profile links
- Feature rows, galleries, and other UI components

**_sass/:** Custom styles (if present)

**assets/:** Static assets
- Images in `/assets/images/`
- JavaScript in `/assets/js/`
- Legacy content in `/wp-content/uploads/`

## Blog Post Guidelines

### Front Matter Template
```yaml
---
title: "Post Title Here"
author: Author Name
categories:
  - Azure
tags:
  - Azure DevOps
  - PowerShell
header:
  og_image: /assets/images/image-name.PNG
---
```

### Content Conventions
- Use liquid tags for image references: `![Description]({{ site.url }}/assets/images/filename.png)`
- Code blocks use triple backticks with language identifiers
- Images typically stored in `/assets/images/` with date prefix (e.g., `2020-07-11-filename.PNG`)

## Writing Style Guide

When creating or editing blog posts, follow these established writing patterns:

### Structure and Organization

**Standard post structure:**
1. **Opening with context** - Start with a real-world scenario, customer need, or practical problem
   - Example: "One of my customers is on a journey to re-architect old on-premises web applications..."
   - Example: "We use ARM outputs quite extensively in our Azure DevOps pipelines..."

2. **Problem statement** - Clearly define the challenge or issue
   - Use section headers like `## Issue`, `## Challenge`, or `## Introduction`
   - Explain the "why" before diving into the "how"

3. **Solution walkthrough** - Step-by-step implementation
   - Use numbered lists for sequential steps
   - Break complex processes into subsections with `##` or `###` headers
   - Common section names: `## Setup`, `## Requirements`, `## Configuration`

4. **Results/verification** - Show the outcome
   - Section often titled `## Running the pipeline`, `## Result`, or `## Conclusion`

5. **Closing** - End with conclusion section and sign-off
   - Use `## Conclusion` header
   - Sign with "Alex", "Alexandre", or "Hope this helps, Alex"

### Tone and Voice

**Conversational and inclusive:**
- Use "we" frequently to include the reader: "We will add...", "We can now..."
- Share personal experiences: "I got a few requests", "I struggled a bit with..."
- Keep it approachable and practical, not overly formal
- Use casual transitions: "Let's give it a try now", "That's it for the application gateway"

**Direct and honest:**
- Mention when things didn't work initially: "I was getting error message when..."
- Share workarounds: "A work around for this was to..."
- Credit others who helped: "I want to thank [Person] to help me out when I got stuck"
- Include personal opinions when relevant: "this doesn't make sense at all to me, but anyway 😉"

### Content Patterns

**Emphasis techniques:**
- Use *italics* for key takeaways or summary statements
  - Example: *"If we have continuous deployments for our webApps, we want continuous deployments for our APIM as well."*
- Use **bold** for UI elements, actions, and important terms
  - Example: "Click on **Extensions** and **Add**"
  - Example: **My recommendation is to avoid this as much as you can.**

**Notes and warnings:**
- Use blockquotes (>) for notes, warnings, and important callouts
  - `> Note: Although in Microsoft's documentation...`
  - `> **NOTE** I'm not going to explain how to setup...`

**Code and technical content:**
- Always specify language for code blocks (yml, json, powershell, xml, bash)
- Include actual variable/resource names from implementations (makes it more concrete)
- Provide complete, working examples rather than pseudo-code
- Link to GitHub repos when sharing scripts: `https://github.com/averkinderen/...`

**External references:**
- Link to Microsoft documentation: `[found here](https://docs.microsoft.com/...)`
- Reference blog posts and articles that provide additional context
- Link to Azure DevOps marketplace extensions when mentioned

**Visual aids:**
- Use screenshots extensively to illustrate each major step
- Reference images with descriptive text: `![Descriptive text]({{ site.url }}/assets/images/...)`
- Name image files with date prefix: `2020-06-10-AzureAPI-WAFRules.png`

### Technical Writing Approach

**Problem-solution format:**
- Lead with the real-world scenario or customer requirement
- Explain why existing solutions are insufficient
- Walk through the implementation step-by-step
- Show the results/proof it works

**Practical recommendations:**
- Make clear recommendations in bold when sharing best practices
- Example: **"My recommendation is to avoid this as much as you can."**
- Advocate for modern approaches (IaC, Configuration as Code)
- Share lessons learned from real implementations

**Troubleshooting insights:**
- Include common pitfalls encountered: "This step is one of many that we have not being able to..."
- Explain workarounds when official methods don't work
- Document which approaches were tried and didn't work (saves readers time)

### Formatting Standards

**Lists and bullets:**
- Use bullet points (`*` or `-`) for non-sequential items
- Use numbered lists for sequential steps
- Nest sub-items when explaining complex concepts

**Headers:**
- Use `##` for major sections (Introduction, Setup, Conclusion)
- Use `###` for subsections
- Use descriptive header text that summarizes the section

**Inline formatting:**
- Code/commands in backticks: `` `bundle exec jekyll serve` ``
- File paths in backticks: `` `_config.yml` ``
- UI elements in **bold**: **Custom Script Extension**
- Emphasis with *italics* for key concepts

### Sign-off Patterns

Common closings:
- "Hope this helps, Alex"
- "Thanks, Alex"
- "Alex"
- "Hope this helps, Alexandre"

## GitHub Pages Deployment

- Site automatically builds and deploys on push to `master` branch
- GitHub Pages uses Jekyll with `--safe` flag (whitelisted plugins only)
- Domain: mscloud.be (configured in CNAME file)
- Travis CI configuration present in `.travis.yml`

## Jekyll Plugins

Configured plugins (GitHub Pages compatible):
- jekyll-paginate
- jekyll-sitemap
- jekyll-gist
- jekyll-feed
- jemoji
- jekyll-include-cache
- jekyll-seo-tag
- jekyll-algolia (for search)

## Theme Information

- Theme: Minimal Mistakes (via remote_theme)
- Documentation: https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/
- Skin: default (options: air, aqua, contrast, dark, dirt, neon, mint, plum, sunrise)
- Layout: wide (set in defaults)

## Common Tasks

**Create a new blog post:**
1. Create file in `_posts/` with format `YYYY-MM-DD-title.md`
2. Add front matter with title, author, categories, tags
3. Write content in markdown
4. Test locally with `bundle exec jekyll serve`

**Update navigation:**
Edit `_data/navigation.yml`

**Modify site configuration:**
Edit `_config.yml` (requires server restart to see changes)

**Add images:**
Place in `/assets/images/` and reference with `{{ site.url }}/assets/images/filename`
