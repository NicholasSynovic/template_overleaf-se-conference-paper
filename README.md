# Software Engineering Conference Paper Template

A ready-to-write LaTeX template for software engineering (SE) conference papers,
built on the ACM `acmart` class in `sigconf` mode. It ships with an opinionated
writing style guide, reusable figure/finding components, and a preconfigured
preamble so you can focus on content instead of setup.

Originally authored and exported from [Overleaf](https://www.overleaf.com).

## Features

- ACM `sigconf` layout via the vendored `acmart.cls` (no install required).
- Preprint mode by default (`nonacm`) — suppresses ACM copyright, DOI, and ISBN
  blocks; switch a single line for camera-ready submission.
- Modular preamble: all packages and custom macros live in `misc/typesetting.tex`.
- Reusable, self-contained components in `figures/` (placeholder figure and a
  numbered "Finding" callout box).
- Custom macros for inline section headers, LLM prompt callouts, and draft
  markers that can be toggled on/off.
- A detailed [`style_guide.md`](style_guide.md) describing the expected structure
  and prose conventions for every section of an empirical SE paper.

## Requirements

A LaTeX distribution that includes the packages used in the preamble (TeX Live,
MiKTeX, or MacTeX). The ACM class and bibliography files are vendored in this
repository, so no separate `acmart` installation is needed.

## Repository layout

```
main.tex                  Entrypoint — title, authors, abstract, and all sections
citations.bib             Bibliography database (BibTeX) — add your references here
style_guide.md            Authoritative writing/structure contract for the paper
misc/typesetting.tex      All package imports and custom macros
misc/data.tex             Global data/variable macros
figures/template_figure.tex   Placeholder figure pattern (reuse this)
figures/template_finding.tex  Numbered "Finding N." callout box (reuse this)
acmart.cls, acm*.bbx/.cbx/.dbx   Vendored ACM class and bibliography files
```

## Building

No build scripts or CI are included. Compile with the standard BibTeX cycle:

```bash
pdflatex main
bibtex main
pdflatex main
pdflatex main
```

Or let `latexmk` handle the passes automatically:

```bash
latexmk -pdf main.tex
```

## Usage

### Preprint vs. camera-ready

The default document class targets preprints (e.g., arXiv) and hides ACM
copyright/DOI/ISBN blocks:

```latex
\documentclass[sigconf,nonacm]{acmart}   % default (preprint)
% \documentclass[sigconf]{acmart}        % peer-reviewed camera-ready
```

For arXiv, swap `\bibliography{citations}` for `\input{main.bbl}` near the end of
`main.tex` (a commented hint is provided there).

### Draft markers

A `DEBUG` flag controls visibility of draft annotations. It is **off by default**
(`main.tex` sets `\DEBUGtrue` then immediately `\DEBUGfalse`). With it off,
`\TODO{}`, `\CITE{}`, and co-author note (`\NMS{}`) macros render as nothing. To
reveal them, comment out the `\DEBUGfalse` line.

### Custom macros

- `\myparagraph{...}` — bold inline mini-section header (preferred over
  `\subsubsection`).
- `\newfinding` — numbered "Finding N." marker for use inside a finding box.
- `\myprompt{title}{body}` — gray callout box for LLM prompts.
- `\ie` / `\eg` — pre-formatted italic Latin abbreviations.
- Use `cleveref`'s `\Cref{...}` with `sec:`/`subsec:`/`fig:` labels for all
  cross-references; never hardcode numbers.

### Bibliography

The active engine is **BibTeX + `natbib`** with the `ACM-Reference-Format` style.
Add entries to `citations.bib`. The bundled biblatex files (`acmauthoryear.bbx`,
`acmnumeric.bbx`, etc.) are not loaded by the current setup.

## Writing conventions

Before writing or restructuring prose, read [`style_guide.md`](style_guide.md).
It defines per-section paragraph counts, the six-paragraph introduction arc, the
standardized five-part research-question block, finding-box usage, and prose
rules (3–7 sentences per paragraph, explicit transitions, and avoidance of hype
words like "novel" or "significant").

## License

The vendored `acmart` class and ACM bibliography files are distributed under
their own LaTeX Project Public License (LPPL); see the file headers for details.
