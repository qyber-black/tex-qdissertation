# Qyber dissertation class and template

> SPDX-FileCopyrightText: 2026 Frank Langbein <frank@langbein.org>\
> SPDX-License-Identifier: LPPL-1.3c

The **qdissertation** class is a LaTeX class for dissertation reports (undergraduate and master's), plus ready-to-use templates. It provides a clean layout (A4, 12pt, single spacing), optional sans (default), serif, or hacker fonts, numeric or author--year citations, and a compact chapter style. The main template demonstrates the dissertation structure and can be filled with your own content.

The package also includes a short **initial plan / proposal** example (`plan.tex`) based on the separate `qproposal` class. This is an article-style layout for project plans with sections such as Project Description, Aims and Objectives, Feasibility, Work Plan, and References. It is generic enough to be adapted for different project modules and institutions.

Variations (degree, optional Reflection chapter) are selectable via commented options in `main.tex`. Confirm your institution's word limits and structure before submission.

## Getting started as an undergraduate or master's student

This directory is intended to be your main dissertation project, including both the dissertation report and an initial project plan, kept under version control in a git repository (typically as a fork on GitHub, GitLab, or your institution's Git service).

- **Fork the template**: on your hosting platform, fork the upstream repository that contains this directory into your own account or group. Then clone *your fork* to your machine so your local copy stays connected to your remote.
- **Build once**: in this directory, run:

  ```bash
  make          # builds main.pdf (dissertation) and plan.pdf (initial plan example)
  ```

  This checks that your LaTeX toolchain is working correctly.
- **Edit the dissertation**:
  - Put global metadata in `main.tex` using `\title`, `\author`, your degree or programme, institution, and `\date` (plus any options or commands described in the comments of `main.tex`).
  - Write your main chapters in the chapter files included by `main.tex` (for example `C1/chapter1.tex`, `C2/chapter2.tex`, and so on; adapt the structure to match your module's expectations).
  - Use any appendix files (for example in `AA/`, `AB/`) for supplementary material such as extra results, code listings, or data summaries, if your institution allows appendices.

While you are still close to the original template, you can occasionally bring in upstream updates to your fork if needed. Once you have made substantial local edits, treat upstream merges with care and only pull in specific changes you really need, reviewing and resolving any conflicts carefully.

## Compatibility

The default layout (12pt, single line spacing, suggested chapter structure) is
compatible with common institutional requirements for undergraduate and
master's dissertations. Always confirm your institution's word limits,
structure, and formatting rules before final submission.

Many institutions cap the main body (e.g.\ 10,000--12,000 for undergraduate,
15,000--20,000 for master's). Run `make wordcount`; caption words and front
matter are usually excluded---texcount reports them separately.

## Submission

For electronic submission, use `make` (lualatex, default) or `make ENGINE=pdf`;
both embed fonts by default. Do not encrypt the PDF. Verify the final PDF
before submitting.

## Build

The Makefile uses **latexmk** to run the LaTeX engine, bibliography, and cross-references as needed.

- **Build the dissertation and example plan:** `make` or `make all` (produces `main.pdf` and `plan.pdf`).
- **Build only the dissertation:** `make main`.
- **Build only the example initial plan:** `make plan` (produces `plan.pdf`).
- **Remove build artifacts:** `make clean`. Use `make distclean` to also remove `main.pdf`.
- **Word count:** `make wordcount` for per-file and total word count (caption words shown separately).

**Choose the LaTeX engine** with the `ENGINE` variable (default: `lua` = lualatex):

- `make` or `make ENGINE=lua` — LuaLaTeX
- `make ENGINE=pdf` — pdfLaTeX
- `make ENGINE=xe` — XeLaTeX

## Requirements

You need **latexmk**, **lualatex** (or pdflatex/xelatex if you switch engine), **makeglossaries** (for acronyms), and **bibtex** (for the bibliography). Install them via your distribution (TeX Live, MiKTeX, etc.).

## Fonts and obfuscation

- Class option **`obfuscate`** enables font obfuscation for any font (sans, serif, or hacker). Requires **LuaLaTeX**; with XeLaTeX or pdfLaTeX a warning is emitted and normal fonts are used.
- Generate obfuscated fonts with the build script. Default **`make hacker-font`** produces `fonts/hacker-obfuscated.otf` and `fonts/obfuscate-perm.lua` (use optional **`SEED=n`** for a reproducible permutation).
- To use obfuscation with **sans** or **serif**, run the script with the same **`--seed`** (e.g. same `SEED=` when using make), **`--font`** path to the base font (e.g. Source Sans Pro or Source Serif Pro), and **`--output-font sans-obfuscated.otf`** or **`serif-obfuscated.otf`**. Example: `python3 scripts/build-hacker-font.py --output-dir fonts --seed 42 --font /path/to/SourceSansPro-Regular.otf --output-font sans-obfuscated.otf`.
- For full obfuscation (including **\textbf**, **\textit**, and **\textsc** used in the class), generate all variants per family with the **same seed**: Regular, Bold, Italic, BoldItalic (e.g. `sans-obfuscated.otf`, `sans-obfuscated-Bold.otf`, `sans-obfuscated-Italic.otf`, `sans-obfuscated-BoldItalic.otf`). Optionally SmallCaps (used in newthought, headers, chapter titles) or Slanted if your font provides them. Expected files: `fonts/<base>.otf`, `fonts/<base>-Bold.otf`, `fonts/<base>-Italic.otf`, `fonts/<base>-BoldItalic.otf`, and `fonts/obfuscate-perm.lua` (shared).

## Quality checks

Run `make check` to run REUSE lint (license and copyright compliance; see [REUSE](https://reuse.software)). This project is REUSE-compliant. If the `reuse` tool is not installed, the target reports that.

## Working with git (recommended over Overleaf)

We recommend keeping this project in a git repository hosted on a service such as GitHub, GitLab, or your institution's Git platform, instead of editing the sources directly on Overleaf. A simple workflow for an undergraduate or master's dissertation is:

- **Edit, build, commit**:
  - Make changes to your `.tex` files for the dissertation (`main.tex` and chapter files) or the plan (`plan.tex` or a copy).
  - Run `make`, `make main`, or `make plan` to check that everything still compiles.
  - Use `git status` to see what changed, then `git commit` with a short message when you reach a stable point.
- **Use branches for bigger changes**: create a branch (for example `rewrite-methods` or `results-updates`) for substantial edits, and merge it back into your main branch once you are happy.
- **Sync with your remote fork**: push regularly to your fork on GitHub, GitLab, or your institutional Git service so your work is backed up and can be reviewed, commented on, or cloned to another machine.

If you are moving from Overleaf, copy your `.tex` and `.bib` files into this structure and commit them to your fork; from then on you can use git as your primary way of working.

## Where to put the class

The template expects `qdissertation.cls` in the same directory as `main.tex`. To use the class in other projects, either copy `qdissertation.cls` into that project or install it in your TEXMF tree.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to contribute.

If you use this template for your own dissertation and find ways it could be improved (for example clearer comments in `main.tex` or `plan.tex`, better example sections, or small documentation clarifications), you are encouraged to feed those improvements back upstream:

- Open an issue on the upstream project describing what was confusing or what you improved locally.
- Or, from your fork, create a pull/merge request with a focused change that would be useful to other students and supervisors as well.

Keep project- or module-specific customisations (such as particular marking schemes, institution-specific covers, or one-off formatting tweaks) in your fork; only propose upstream changes that are broadly applicable.

## License and copyright

Template and class: **LPPL-1.3c**, Copyright (C) 2026 Frank Langbein <frank@langbein.org>. The Current Maintainer of this work is Frank Langbein [frank@langbein.org](mailto:frank@langbein.org). See the [LaTeX Project Public License](https://www.latex-project.org/lppl/). The `LICENSE` file in this directory contains the short notice.
