# Suggestions to Improve Awesome-CV

This document collects concrete, low‑friction improvements to make the project easier to use, more robust, and friendlier for contributors. Items are grouped by theme and roughly prioritized from quickest wins to deeper changes.

## Quick wins (docs, discoverability)
- Add a quick “TL;DR build” block to README with common commands for macOS/Linux/Windows, including `latexmk` usage and minimal TeX packages.
- Document troubleshooting section: common XeLaTeX errors (fonts, missing packages), and how to fix them.
- Link to this SUGGESTIONS.md from README (done in this change) and invite PRs to append ideas.
- Add badges for CTAN (if published) and Overleaf template versions, clarifying version parity.

## Project hygiene and contributor experience
- Add CONTRIBUTING.md: guidelines for PRs, style for `.cls` and `.tex`, how to run local builds, and how to add new example sections.
- Add a lightweight CODE_OF_CONDUCT.md (Contributor Covenant).
- Provide Issue/PR templates: bug report, feature request (e.g., new section type), question.
- Add EditorConfig (.editorconfig) to normalize indentation (2 spaces) and line endings.

## Build and tooling
- Provide a Dockerfile/runtime for reproducible builds (tiny TeX Live subset), and a `make docker-build` target.
- Enhance Makefile:
  - `make all` builds resume, cv, and cover letter with `latexmk -xelatex -quiet` for incremental builds.
  - `make watch` uses `latexmk -pvc` to auto-rebuild on change.
  - `make clean` removes aux files in `examples/` (aux, fdb_latexmk, fls, log, out, synctex.gz) while keeping PDFs by default; add `make distclean` to remove PDFs too.
- Add optional lint step (ChkTeX or lacheck) and a `make lint` target.

## Continuous Integration (CI)
- GitHub Actions workflow that:
  - Sets up TeX Live cache.
  - Runs `make all` for examples to ensure class compiles.
  - Uploads built PDFs as artifacts for quick review.
  - Runs `make lint` if present.
- Nightly CI to build with the latest TeX Live to catch upstream breakages early.

## Templates and examples
- Provide minimal, commented example for each document type:
  - Minimal CV, minimal résumé, minimal cover letter (one page each), with inline comments explaining commands like `\cventry`, `\cvsection`, and `\cvitems`.
- Add a “kitchen sink” example showcasing all section types and options.
- Offer localized examples (EN, DE, ES, FR, ZH) showing hyphenation, date formats, and right‑to‑left snippet for completeness.

## Class (.cls) enhancements (backward‑compatible)
- Add class options switches:
  - `color=<name>` to select a built‑in palette (blue, teal, indigo, grayscale).
  - `mono` to force monospaced body for ATS parsing.
  - `compact` to trim vertical spacing for strict one‑page résumés.
- Provide a single file for user overrides (e.g., `awesome-cv-user.sty`) so updates don’t require editing the class.
- Expose spacing lengths as lengths (e.g., `\cvSectionSep`, `\cvItemSep`) for user customization.

## Fonts and assets
- Document how to swap fonts (system vs included) and provide optional fallback to Latin Modern if Roboto/Source Sans not installed.
- Include a script or doc snippet that auto‑installs needed fonts on macOS/Linux.

## Accessibility and ATS
- Add guidance for ATS‑friendly output: avoid multi‑column where harmful, ensure text is text (not outlines), color contrast meets WCAG AA, include basic PDF metadata.
- Provide a `highcontrast` class option and a grayscale palette.

## Versioning and releases
- Keep a CHANGELOG.md using Keep a Changelog. Tag releases on Git.
- If publishing to CTAN, include CTAN metadata and update instructions.

## Community
- Add Discussions tab for Q&A and template sharing. Create a “showcase” issue for users to link their variants.

## Nice‑to‑have (later)
- A small CLI scaffold (Python or Node) or Make target to duplicate an example into a personal working directory with a chosen palette.
- A script to convert structured data (YAML/JSON) into `.tex` snippets (e.g., work experience list).

---
Contributions welcome! If you’d like to pick an item, open an issue to discuss scope and then submit a PR.
