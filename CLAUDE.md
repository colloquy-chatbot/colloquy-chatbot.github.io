# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Jekyll Commands
- Build and serve site locally: `bundle exec jekyll serve`
- Build without serving: `bundle exec jekyll build`
- Clean build: `bundle exec jekyll clean && bundle exec jekyll build`

## Ruby and Jekyll Guidelines
- Indentation: 2 spaces
- Follow Jekyll's Liquid template conventions
- Document front matter should be at top of file with layout, title, permalink
- Use markdown for content formatting where possible
- Use HTML only when necessary for complex layouts

## Documentation Style
- Use tabs component for TypeScript/Python implementation examples
- Follow consistent structure in API documentation
- Keep code examples concise and demonstrative
- Use proper heading hierarchy (H1 > H2 > H3)
- Organize related content in separate documentation pages