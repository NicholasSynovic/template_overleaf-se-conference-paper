## 1. Global Prose & Typography Rules

* **Paragraph Architecture:** Every paragraph must target **3–7 sentences**. Avoid single-sentence paragraphs (which disrupt narrative flow) and dense walls of text exceeding 8 sentences.
* **Rhetorical Singularity:** Each paragraph must serve exactly *one* functional goal (e.g., establishing context, identifying a gap, introducing a method, presenting a factual finding, or defining a threat).
* **Explicit Signposting:** Maintain visible logical progression across paragraph and section boundaries using explicit structural transition words (e.g., *However*, *Consequently*, *In contrast*, *Furthermore*, *As a result*).
* **Micro-Formatting:** Use the custom `\myparagraph{...}` macro to denote inline bold headers for named mini-paragraphs (e.g., specific contributions or baseline metrics). Avoid abusing standard `\subsubsection`.

---

## 2. Section-by-Section Structural Blueprint

### Abstract (Target: 6–8 Sentences)

Must be a self-contained, three-part narrative block with **no** citations or raw statistical tables:

1. **Context & Problem (Sentences 1–3):** State the broader software engineering domain, why it matters, and the core friction point or consequence.
2. **Approach & Scope (Sentences 4–5):** Explicitly state *"In this paper, we..."* and summarize the design, method, and evaluation scale (e.g., data size, system types).
3. **Impact & Insights (Sentences 6–8):** Deliver the headline qualitative/quantitative outcome and its concrete implication for future research or practice.

### Section 1: Introduction (The 6-Paragraph Arc)

* **Paragraph 1 (Context):** Establish the broad domain and provide a hook demonstrating why the field is non-trivial.
* **Paragraph 2 (The Gap):** Pivot sharply (*"However, current practices..."*) to isolate the precise technical or empirical gap.
* **Paragraph 3 (The Core Insight):** Introduce your goal and high-level approach. Provide plain-language intuition for why your method solves the gap.
* **Paragraph 4 (Contributions):** Use `\myparagraph{Contributions}` followed by an unnumbered bulleted list (**3–4 items**). Each bullet must be one sentence plus a short clarifying clause detailing an artifact, empirical insight, or open-science replication package. Do not use unquantified hype words like "novel" or "significant."
* **Paragraph 5 (Significance):** Provide a brief, high-level preview of the headline results and explicitly state the bounds of your scope.
* **Paragraph 6 (Roadmap):** Detail the paper's organization using lowercase section names mapped to their respective `\Cref` macros (e.g., `\Cref{sec:background}`).

### Section 2: Background and Related Work

* **Entry Block:** A 3–5 sentence paragraph re-contextualizing the problem space with deeper technical maturity before splitting into subsections.
* **Subsection 1 (Domain Overview):** Establish technical definitions, entities (e.g., pipelines, registries), and standard workflows. Connect constraints to specific domain challenges using cause-and-effect transitions (*"Consequently..."*).
* **Subsection 2 (Existing Approaches):** Group literature by thematic categories rather than chronological order. Contrast what they achieve against where they fall short.
* **Subsection 3 (Conceptual Foundation):** Define the theoretical lens (e.g., socio-technical, reliability frameworks) used to reason about the problem, bridging directly into the operational variables of your methodology.

### Section 3: Research Questions (The Structural Bridge)

* An introductory 1–3 sentence paragraph anchoring the RQs to the core gap.
* A formal enumerated list using the `[label=\textbf{RQ\arabic*}:]` format. Each question must be a single sentence prefaced by a bolded dimensional anchor (e.g., **[Prevalence]**, **[Patterns]**, **[Impact]**).
* A final mapping paragraph explicitly detailing which sections, datasets, and pipelines answer which question.

### Sections 4–6: Evaluation of RQs (Standardized 5-Part Block)

Every research question evaluation section must adhere to the exact same subsection structure:

1. **Overview Paragraph:** Restate the RQ verbatim, justify its role in the study's progression, and explain why the dimension matters.
2. **Methodology Subsection:** Break down the specific study design, data sources/sampling rules, execution procedure, and metrics/analysis plan. Include a 2–3 sentence `\myparagraph{Threats to Validity for RQ_x}` block targeting question-specific biases.
3. **Empirical Findings Subsection:** Present data preprocessing/descriptive statistics, followed by core results.
* *Rule:* Every table and figure must be explicitly cited and described textually (*"As shown in Figure 2..."*). Stay strictly descriptive; omit qualitative interpretation here.


4. **Formal Answer Box:** Use the centered `template_finding` input to deliver a 2–3 sentence, neutral synthesis answering the question text.
5. **Pointer Sentence:** Conclude with a single sentence routing the reader to the Discussion section for qualitative implications.

### Section 7: Discussion (The Funnel Arc)

Moves from narrow, data-adjacent interpretations to broad, high-level implications:

* **Subsection 1 (Interpretation of RQs):** Use dedicated `\myparagraph` headers for each RQ. Structure each block exactly as: *Interpretation (2–3 sentences) $\rightarrow$ Mechanism/Why (2–3 sentences) $\rightarrow$ Relation to prior work (2–3 sentences) $\rightarrow$ Scoped actionable action or limitation (2–3 sentences).*
* **Subsection 2 (Wider Implications):** Split into distinct paragraphs covering *Theoretical Implications* (how this refines existing engineering models) and *Practical/Industrial Implications* (concrete changes for engineering teams or tools).
* **Subsection 3 (Limitations & Alternative Explanations):** Openly analyze structural weaknesses in your data/measures and present plausible alternative interpretations of your findings.
* **Subsection 4 (Future Directions):** Propose immediate follow-up studies, methodological refinements, and new questions opened by this work.
* **Take-Home Message:** End the section with a confident `\myparagraph{Take-Home Message}` summarizing what the study ultimately proves.

### Section 8: Threats to Validity

Systematically classify vulnerabilities into three distinct subsections:

* **Internal Validity:** Address confounding variables, instrumentation quirks, and how missing data/attrition patterns were handled.
* **External Validity:** Clearly boundary the context, project types, or participant demographics to define exactly where results do and do not generalize.
* **Construct Validity:** Justify that your indirect metrics accurately capture the target theoretical constructs. Address potential measurement errors or technical tool biases.

### Section 9: Conclusion

* **Paragraph 1:** Synthesize the overarching problem and findings across all RQs using fresh, non-repetitive prose.
* **Paragraph 2:** Enumerate the concrete engineering artifacts and insights generated.
* **Paragraph 3:** Highlight the primary future trajectory and close with a powerful, authoritative statement. *Style Rule: The final sentence must be a confident declaration of impact, never an apology or a list of limitations.*

---

## 3. LaTeX Compilation & Cross-Referencing Syntax

* **Preprint vs. Camera-Ready:** Use `\documentclass[sigconf,nonacm]{acmart}` for arXiv or preprint servers to suppress ACM copyright blocks, DOI lines, and price footers. Switch to `\documentclass[sigconf]{acmart}` only for peer-reviewed, camera-ready submission.
* **Draft Tracking:** Toggle visibility of internal project alerts, comments, and tracking notes using the boolean debug flags:
```latex
\DEBUGtrue   % Activates visibility of draft/todo files
\DEBUGfalse  % Strips all draft metadata for clean compilation

```


* **Referencing Engine:** Never hardcode section, figure, or table numbers. Always use uppercase-managed smart macros provided by the `cleveref` configuration package:
* Sections: `\Cref{sec:introduction}` $\rightarrow$ **Section 1**
* Subsections: `\Cref{subsec:subsection-1}` $\rightarrow$ **Section 2.1**
* Figures: `\Cref{fig:template_figure}` $\rightarrow$ **Figure 1**