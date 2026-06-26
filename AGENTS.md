# AGENTS.md

ACM `sigconf` (acmart) LaTeX conference-paper template, imported from Overleaf. Single document; `main.tex` is the only entrypoint. The bulk of the value here is the writing style contract and the LaTeX wiring, not code.

## Build

No build scripts, Makefile, or CI exist. Compile with the standard BibTeX (not biblatex) cycle:

```
pdflatex main
bibtex main
pdflatex main
pdflatex main
```

- `latexmk -pdf main.tex` also works and handles the passes automatically.
- `acmart.cls` and the bundled `acm*.bbx/.cbx/.dbx` files are vendored in-repo; do not edit or delete them.

## Bibliography (read before touching citations)

- The active engine is **BibTeX + `natbib`**, via `\bibliographystyle{ACM-Reference-Format}` + `\bibliography{citations}` (`main.tex:891-892`) and `\usepackage{natbib}[numbers]` (`misc/typesetting.tex:41`).
- The bundled biblatex files (`acmauthoryear.bbx`, `acmnumeric.bbx`, etc.) are **not** loaded by the current setup. Ignore them unless deliberately switching engines.
- `citations.bib` is currently empty — add entries there.
- For arXiv: switch `\bibliography{citations}` to `\input{main.bbl}` (commented hint at `main.tex:893`).

## Document wiring

- `main.tex` `\input`s `misc/data.tex` (global data macros, currently near-empty) and `misc/typesetting.tex` (all package imports + custom macros).
- Figures/findings live as standalone files in `figures/` and are pulled in with `\input{figures/...}` (no extension). Reuse `figures/template_figure.tex` and `figures/template_finding.tex` as the canonical patterns.
- `template_finding.tex` depends on `\newfinding` defined in `misc/typesetting.tex` (its inline comment wrongly says `typeset/misc.tex`) — the finding counter is shared/global, so reordering finding boxes renumbers them. The template calls `\newfinding` three times to demo numbering; a real box typically uses one.

## Preprint vs camera-ready

- Default is preprint: `\documentclass[sigconf,nonacm]{acmart}` (`main.tex:6`) — suppresses ACM copyright/DOI/ISBN blocks.
- For peer-reviewed camera-ready, switch to `\documentclass[sigconf]{acmart}` (commented at `main.tex:5`).

## DEBUG flag (counterintuitive)

`main.tex:27-28` sets `\DEBUGtrue` then immediately `\DEBUGfalse`, so **debug is OFF by default**. When off, `\TODO{}`, `\CITE{}`, and `\NMS{}` (co-author notes) render as nothing. To see draft markers, comment out line 28.

## Custom macros (use these, don't reinvent)

- `\myparagraph{...}` — bold inline mini-section header. Preferred over `\subsubsection` per the style guide.
- `\newfinding` — numbered "Finding N." marker; use inside a finding box.
- `\myprompt{title}{body}` — gray callout box for LLM prompts.
- `\ie` / `\eg` — pre-formatted italic abbreviations.
- Cross-references: always use `cleveref` `\Cref{...}` with `sec:`/`subsec:`/`fig:` labels. Never hardcode numbers.

## Writing conventions

`style_guide.md` is the authoritative content contract: per-section paragraph counts, the 6-paragraph intro arc, the standardized 5-part RQ block, finding-box usage, and prose rules (3–7 sentences/paragraph, explicit transitions, no hype words like "novel"/"significant"). Read it before writing or restructuring prose.
