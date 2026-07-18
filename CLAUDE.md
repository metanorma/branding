# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

Asset-only repository for the Metanorma product's visual brand (logos, symbols). There is no source code, no build system, no test suite — only graphic assets in `logo/`. The two PDFs (`metanorma-logo.pdf`, `metanorma-logo-horizontal-violet.pdf`) are Adobe Illustrator source artwork; everything else is derived output.

## Critical constraints

- **Never delete or overwrite any file in `logo/`.** Every asset here is source or canonical output. The global CLAUDE.md rule ("NEVER DELETE SOURCE FILES") applies absolutely — including the `-old` suffixed files, the PDFs, and the untracked `symbol.svg`. If cleanup seems warranted, flag to the user; do not act.
- **PNG and SVG come in pairs.** Each variant has matching raster + vector forms; do not regenerate one without the other.
- **`.DS_Store` is macOS noise.** Do not commit it. Suggest adding to `.gitignore` rather than deleting.

## Logo naming convention

Files follow `metanorma-logo_{variant}-{treatment}[-old].{ext}`:

- **variant**: `full` (symbol + wordmark) or `icon` (symbol alone)
- **treatment**: `light` / `dark` (logo color), `dark-bg` / `light-bg` (optimized for that background)
- **`-old` suffix**: superseded versions kept for historical/reference purposes — not disposable

`symbol.svg` is the standalone Metanorma "M" mark (a stylized letterform with radiating lines and a document motif) used as the basis for the icon variants.

## Workflow

- Default branch is `main` (local tracks `origin/main`); the old `master` skew was retired — there is no `master` branch.
- All changes go through a PR on a feature branch (per global rule: never commit/push directly to main, never push tags).
