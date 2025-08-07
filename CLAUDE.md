# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static website for KPBJ.FM, a radio station. The site is built using vanilla HTML/CSS/JS with Tailwind CSS for styling and uses a component-based architecture with environment variable substitution for templating.

## Build System

The project uses Just (justfile) as its build tool with the following key commands:

- `just` or `just build` - Full build process (clean, copy assets, compile Tailwind, inject components)
- `just dev` - Development mode with file watching and live server
- `just serve` - Serve the built site from dist/
- `just watch` - Watch files for changes and rebuild automatically
- `just tailwind-build` - Compile Tailwind CSS only

The build process:
1. Cleans the dist/ directory
2. Compiles Tailwind CSS from `assets/css/tailwind.css` to `dist/assets/css/output.css`
3. Copies assets (images, CSS) to dist/
4. Injects HTML components using environment variable substitution

## Component System

The site uses a simple templating system via `envsubst`:
- Components are stored in `components/` directory
- `components/footer.html` - Site footer
- `components/navbar.html` - Site navigation (header)
- Main pages use placeholders like `$NAVBAR` and `$FOOTER` that get replaced during build
- The `inject-components` command reads component files and substitutes them into HTML templates

## File Structure

- `index.html` - Main page template with component placeholders
- `assets/css/` - CSS files including Tailwind source and compiled output
- `assets/img/` - Static images
- `components/` - HTML component files
- `dist/` - Built output directory (generated)

## Dependencies

The project has minimal dependencies:
- Tailwind CSS for styling
- Just for build automation  
- `concurrently` and `serve` for development (implied by Justfile)
- `entr` and `fd` for file watching

## Development Workflow

1. Run `just dev` to start development server with file watching
2. Edit HTML files, components, or CSS
3. Changes trigger automatic rebuilds via the watch system
4. The development server serves from `dist/` directory
