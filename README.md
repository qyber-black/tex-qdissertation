# Qyber dissertation class and template

> SPDX-FileCopyrightText: 2026 Frank Langbein <frank@langbein.org>\
> SPDX-License-Identifier: LPPL-1.3c

The **qdissertation** class is a LaTeX class for dissertation reports (undergraduate and master's), plus a ready-to-use template. It provides a clean layout (A4, 12pt, single spacing), optional sans/serif/mixed fonts, numeric or author--year citations, and a compact chapter style. The template demonstrates the structure and can be filled with your own content.

Variations (degree, optional Reflection chapter) are selectable via commented options in `main.tex`. Confirm your institution's word limits and structure before submission.

## Compatibility

The default layout (12pt, single line spacing, suggested chapter structure) is compatible with common institutional requirements for undergraduate and master's dissertations. Always confirm your institution's word limits, structure, and formatting rules before final submission.

Many institutions cap the main body (e.g.\ 10,000--12,000 for undergraduate, 15,000--20,000 for master's). Run `make wordcount`; caption words and front matter are usually excluded---texcount reports them separately.

## Submission

For electronic submission, use `make` (lualatex, default) or `make ENGINE=pdf`; both embed fonts by default. Do not encrypt the PDF. Verify the final PDF before submitting.

## Build

The Makefile uses **latexmk** to run the LaTeX engine, bibliography, and cross-references as needed.

- **Build the dissertation:** `make` or `make all` (produces `main.pdf`).
- **Remove build artifacts:** `make clean`. Use `make distclean` to also remove `main.pdf`.
- **Word count:** `make wordcount` for per-file and total word count (caption words shown separately).

**Choose the LaTeX engine** with the `ENGINE` variable (default: `lua` = lualatex):

- `make` or `make ENGINE=lua` — LuaLaTeX
- `make ENGINE=pdf` — pdfLaTeX
- `make ENGINE=xe` — XeLaTeX

## Requirements

You need **latexmk**, **lualatex** (or pdflatex/xelatex if you switch engine), **makeglossaries** (for acronyms), and **bibtex** (for the bibliography). Install them via your distribution (TeX Live, MiKTeX, etc.).

## Quality checks

Run `make check` to run REUSE lint (license and copyright compliance; see [REUSE](https://reuse.software)). This project is REUSE-compliant. If the `reuse` tool is not installed, the target reports that.

## Where to put the class

The template expects `qdissertation.cls` in the same directory as `main.tex`. To use the class in other projects, either copy `qdissertation.cls` into that project or install it in your TEXMF tree.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to contribute.

## License and copyright

Template and class: **LPPL-1.3c**, Copyright (C) 2026 Frank Langbein <frank@langbein.org>. The Current Maintainer of this work is Frank Langbein [frank@langbein.org](mailto:frank@langbein.org). See the [LaTeX Project Public License](https://www.latex-project.org/lppl/). The `LICENSE` file in this directory contains the short notice.
