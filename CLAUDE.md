# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A TypeScript learning path documentation project. The source of truth is `typescript.md` — an 8-phase structured learning path tailored for full-stack developers using React, Next.js, Express, and Drizzle ORM.

## Primary workflow

HTML documentation pages are generated from `typescript.md` using the `/create-typescript-doc` skill:

```
/create-typescript-doc Phase 1   # generates phase-1.html
/create-typescript-doc Phase 6   # generates phase-6.html
```

Generated files are saved as `phase-N.html` in this directory. Each HTML file is fully self-contained (no external dependencies) with a dark theme, sticky sidebar, and deep-dive concept panels per topic.

## Phase list

| Phase | Title |
|---|---|
| Phase 1 | TypeScript Foundations |
| Phase 2 | Intermediate TypeScript |
| Phase 3 | Object-Oriented TypeScript |
| Phase 4 | Advanced TypeScript |
| Phase 5 | TypeScript Design Patterns |
| Phase 6 | TypeScript with Backend Development |
| Phase 7 | TypeScript with React |
| Phase 8 | Expert-Level TypeScript |

## Source file format

`typescript.md` is a curriculum outline structured as:
- 8 top-level `# PHASE N — Title` headings
- Modules within each phase: `## Module N: Title`
- Each module has a bulleted `Topics:` list and a `Project:` mini-project
- No tables — the HTML skill generates topic tables and all deep-dive content

When editing `typescript.md`, preserve the bullet list format and module headings — the `/create-typescript-doc` skill parses them structurally.
