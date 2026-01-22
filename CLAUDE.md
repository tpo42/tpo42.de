# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

tpo42.de is the official website for the tpo42 Framework - a Technical Product Owner documentation framework that
integrates arc42 (architecture documentation) and req42 (requirements engineering) into a unified "Documentation as
Code" approach.

**Tech Stack**: Jekyll 4.4, Ruby, AsciiDoc (via jekyll-asciidoc), docToolchain, SCSS/Sass

## Common Commands

```bash
# Install dependencies
bundle install

# Serve locally with live reload (port 4000)
bundle exec jekyll serve

# Build for production
bundle exec jekyll build

# Generate PDF documentation via docToolchain
dtcw docker generatePDF
```

### AsciiDoc Container (adcw)

For quick AsciiDoc operations, there's a lightweight container at
`~/data/Projects/OSS/container/tpo42-asciidoc-container/`:

```bash
# Build the container first
./bin/adcbw

# Flatten includes for LLM context (resolve all include:: directives)
./bin/adcw flatten -i requirements.adoc -o build/requirements-flat.adoc

# Syntax validation
./bin/adcw validate -i architecture.adoc

# Extract diagram sources
./bin/adcw extract-diagrams -i overview.adoc -o build/diagrams/

# Direct asciidoctor commands
./bin/adcw asciidoctor mydoc.adoc
./bin/adcw asciidoctor-pdf mydoc.adoc

# Interactive shell
./bin/adcw shell
```

## Architecture

### Content Structure

- **Primary markup**: AsciiDoc (`.adoc` files)
- **Main pages**: `index.adoc`, `overview.adoc`, `about.adoc`, `getting-started.adoc`
- **Documentation frameworks**: `doc/arc42.adoc` (12 chapters in `doc/arc42-chapters/`) and `doc/req42.adoc` (12
  chapters in `doc/req42-chapters/`)
- **Diagrams**: PlantUML diagrams rendered via asciidoctor-diagram

### Jekyll Layout

- `_layouts/default.html` - Main Liquid template
- `_includes/header.html`, `_includes/footer.html` - Navigation components
- `_sass/_tpo42.scss` - Custom theme with tpo42 branding colors
- `_config.yml` - Jekyll configuration with AsciiDoc processor settings

### Build Pipeline

- **Local**: Jekyll serve on port 4000
- **CI/CD**: GitHub Actions (`.github/workflows/pages.yml`) deploys to GitHub Pages on push to `main`
- **docToolchain**: Configured in `docToolchainConfig.groovy` for PDF/HTML generation to `doc/build/`

## Code Quality

### Commit Message Format

Conventional commits required: `fix:`, `feat:`, `chore:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:`, `revert:`,
`ci:`, `build:`

- Title max 52 chars
- Body max 120 chars per line

### Branch Protection

- Protected branch: `main`
- Allowed patterns: `feature/*`, `hotfix/*`, `release/*`, `ng`

## Development Environment

DevContainer available (`.devcontainer/devcontainer.json`) using `tpo42/jekyll-docker:4.4.1` image with VS Code
extensions for AsciiDoc, Markdown, and YAML.

## Theme Colors

Primary palette defined in `_sass/_tpo42.scss`:

- Primary teal: `#2E7D84`
- Accent red: `#C5504B`
- Link colors optimized for accessibility on dark backgrounds
