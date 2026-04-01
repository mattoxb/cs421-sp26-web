# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Quartz v4** static site generator instance for the CS 421 (Programming Languages) course website at University of Illinois. Quartz publishes Markdown content as a static website.

## Common Commands

```bash
# Development server with hot-reload (port 8080)
npx quartz build --serve

# Or use the shortcut script
./run

# Production build
npx quartz build

# Code quality
npm run check        # TypeScript checking + Prettier format verification
npm run format       # Auto-format with Prettier

# Run tests
npm test
```

## Tech Stack

- **Runtime:** Node.js 20.x
- **Language:** TypeScript (strict mode)
- **Framework:** Preact (React-like, server-rendered to static HTML)
- **Build Tool:** esbuild
- **Markdown:** remark/rehype pipeline with plugins for GFM, math (KaTeX), syntax highlighting (Shiki)

## Architecture

### Key Configuration Files

- `quartz.config.ts` - Site configuration: title, theme colors, fonts, plugins, analytics
- `quartz.layout.ts` - Page layout: component arrangement (header, sidebar, footer, content areas)

### Plugin System (Three-Tier)

1. **Transformers** (`quartz/plugins/transformers/`) - Process content: frontmatter parsing, syntax highlighting, link resolution, LaTeX rendering
2. **Filters** (`quartz/plugins/filters/`) - Select content: e.g., RemoveDrafts
3. **Emitters** (`quartz/plugins/emitters/`) - Generate output: HTML pages, RSS, sitemaps, search index

### Core Directories

- `content/` - Course Markdown content (lectures, exams, topics, staff info)
- `quartz/` - Framework code (components, plugins, utilities)
- `quartz/components/` - Preact components for page elements
- `public/` - Generated build output (git-ignored)

### Build Pipeline

1. Parse CLI args → 2. Transpile TS/SCSS → 3. Parse Markdown (parallel workers) → 4. Apply transformers → 5. Filter content → 6. Emit static files

### Content Ignore Patterns

These directories are excluded from builds: `private/`, `templates/`, `.obsidian/`

## CS 421 Specifics

- Custom color scheme defined in `quartz.config.ts`
- Plausible analytics integration
- Content authored in Obsidian-compatible Markdown
