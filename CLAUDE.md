# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a general-purpose LaTeX template repository designed for Japanese academic documents, specifically for the Shimokawa Lab (下川研). It uses the Japanese LaTeX typesetting system with `jsarticle` document class for lightweight and versatile document creation.

This is a general-purpose template intended to be used with the [Shimokawa Lab LaTeX environment](https://github.com/smkwlab/latex-environment). For specialized documents, dedicated templates are available:
- [Thesis template](https://github.com/smkwlab/sotsuron-template) for graduation theses
- [Weekly report template](https://github.com/smkwlab/wr-template) for weekly reports

## Build Commands

The repository uses GitHub Actions for automated builds, but for local development:

```bash
# Using uplatex (Japanese LaTeX)
uplatex main.tex
dvipdfmx main.dvi

# Or if latexmk is configured for Japanese LaTeX
latexmk main.tex

# Clean build artifacts
rm -f *.aux *.log *.dvi *.toc *.lof *.lot

# View PDF (example)
open main.pdf  # macOS
xdg-open main.pdf  # Linux
```

Note: The build requires a Japanese LaTeX distribution (like TeX Live with Japanese support).

## Key Architecture

- **main.tex**: The primary LaTeX source file using `jsarticle` document class
- **GitHub Actions**: Automated build and release workflow using `ghcr.io/smkwlab/texlive-ja-textlint:2025b` Docker container via `smkwlab/latex-release-action@v2.2.0`
- **Output**: Generates `main.pdf` (which is gitignored)

## Release Workflow

The repository automatically builds and releases PDFs when:
- Tags are pushed (creates GitHub releases with attached PDF)
- Pull requests are opened (builds PDF and uploads as workflow artifact for review)

## Important Configuration

The template uses:
- `jsarticle` document class (lightweight Japanese article format)
- `uplatex` engine with Unicode support
- `dvipdfmx` driver for graphics (standard for Japanese LaTeX)
- A4 paper with 25mm margins on all sides
- Essential packages: graphicx, amsmath, amssymb, url, enumitem, otf

## Working with the Template

When modifying `main.tex`:
- The document class `jsarticle` provides a lightweight structure with section/subsection organization
- Use `uplatex` engine for Unicode-based Japanese text processing
- Graphics should be compatible with `dvipdfmx` driver (PDF, PNG, JPEG formats)
- The template includes basic math support via `amsmath` and `amssymb` packages
- Structure your content using `\section{}` and `\subsection{}` commands
- Pull requests automatically generate PDF artifacts for review

## Use Cases

This template is ideal for:
- Research notes and documentation
- Experiment reports and lab records
- Course assignments and reports
- Personal academic documents
- Prototyping larger LaTeX documents