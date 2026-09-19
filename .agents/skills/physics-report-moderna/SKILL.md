---
name: physics-report-moderna
description: Generate a two-column, English-language physics lab report as a real .docx Word document from a professor's guide and raw experimental data. Enforces three mandatory phases in order — an interview (materials gathering plus anomaly detection), a RAG conceptual-framework prompt, and final document generation (abstract, results, linear fits, discussion, conclusions, and fully worked LaTeX appendices) — plus a publication-style matplotlib plotting script. Use whenever the user asks for a physics lab report ("informe de laboratorio", "lab report", "physics report") and wants a Word deliverable, not a Markdown file.
---

# SKILL: Physics_report_moderna

This skill must NOT jump straight into drafting the report. It has three mandatory phases, in this order: (0) Initial interview, (0.1) Conceptual-framework prompt via RAG, and (1) Generation of the final .docx document.

---

## PHASE 0 — INITIAL INTERVIEW (mandatory, before writing anything)

Before generating any part of the report, the assistant must **ask the user**, interview-style, for the following. Do not assume, do not invent, do not fill in with generic values.

### 0.1 Materials to explicitly request

1. **Professor's guide**: pasted or attached (full text or image/PDF).
2. **Data table(s)**: raw, exactly as taken in the lab.
3. **Deviations from the guide / special notes**: any parameter set by the professor in class (e.g. a different number of oscillations than the guide specifies, a restricted range of distances, etc.).
4. **Reference/theoretical value(s)** (optional): if the user wants a statistical comparison against a literature value.

If the user has not provided one or more of these, the assistant **must stop and request them** before continuing — it must not generate the report based on assumptions.

### 0.2 Anomaly detection (mandatory logic)

Upon receiving the guide and the data, the assistant must actively review and ask about any of the following, instead of ignoring them or silently "fixing" them:

- **Dimensional inconsistencies or omissions in the guide** (e.g. formulas missing a factor of $2\pi$, incoherent units): flag them and ask whether the user wants the corrected version used (dimensionally justified) or the guide's literal version.
- **Outliers or anomalous values in the raw data** (e.g. a time reading that deviates strongly from the rest at the same point): point out which data point looks anomalous and ask whether it was a measurement error, whether it should be excluded, or whether it should be kept as-is.
- **Missing or incomplete data** (e.g. missing repetitions at some point, missing system mass, missing instrument resolution): list them explicitly and request them.
- **Procedural ambiguity**: if it is unclear which variable is independent/dependent, or how the center of mass was determined, etc., ask directly instead of assuming.

### 0.3 What the assistant must NOT do in this phase

- Must not generate derived tables, fits, graphs, or text for any report section yet.
- Must not invent numerical values of any kind (already prohibited by the user's standing preferences).
- Must not go beyond what the specific guide covers, unless the user gives an explicit instruction to the contrary.

Only once the user has answered what's needed (complete materials + anomalies resolved) does the process move to Phase 0.1.

---

## PHASE 0.1 — CONCEPTUAL FRAMEWORK PROMPT (RAG system)

Before drafting the Introduction, the assistant must generate (not execute) a prompt that the user can paste into their RAG system to obtain the conceptual/theoretical framework. The assistant hands this prompt to the user and **waits for the RAG's output** before writing Section I (Introduction) with equations and derivations — it must not invent the theoretical framework itself while the user is going to use the RAG.

Prompt template (the assistant must adapt the brackets to the specific experiment, without going beyond what the guide states):

```
I need the conceptual/theoretical framework for a physics lab report on
[topic of the experiment, e.g. "physical pendulum and moment of inertia"].

Instructions:
- Derive the physical model from first principles (Newton's laws / rotational
  dynamics / simple harmonic oscillator, as applicable), showing every
  algebraic step.
- Do not skip intermediate steps.
- Justify each relation dimensionally.
- Stick strictly to the scope of the lab guide I am attaching/describing
  below: [paste or summarize the guide]. Do not introduce models,
  corrections, or generalizations the guide does not cover, unless I
  explicitly request it.
- Provide the equations numbered sequentially: (1), (2), (3)...
- Explicitly state the model's assumptions and simplifications (small
  oscillations, rigid body, negligible friction, etc., as applicable).
- Do not generate the results section or the statistical analysis yet —
  only the conceptual/theoretical framework.
```

Rules for this prompt:

- It must stay within the scope of the guide; it must not request "extra" theoretical content unless the user specifies it.
- It must not request calculations with the user's data yet (that is Phase 1).

---

## PHASE 1 — FINAL DOCUMENT GENERATION

### General output rules

- **Output language: English.** All report content (text, tables, figure captions, appendices) is written in English, regardless of the language the user speaks with the assistant.
- **File format: .docx** (Word), NOT Markdown. The final deliverable must be an actual Word document, generated using the corresponding docx skill.
- **Layout: two-column**, scientific-article / IEEE style, applied throughout the entire document — including every Appendix (A, B, C, D). Appendices are NOT single-column exceptions: derivations, equations, and tables in Appendices A–D must flow and wrap within the same two-column layout as the rest of the report.
- **In-text Citations (verified, not optional):** The Introduction (Section I) must contain actual in-text citations ([1], [2], etc.) woven into the prose next to the theoretical claims, laws, or derivations they support — not just listed at the end in References. Before finishing the document, check that Section I has at least one in-text citation per major theoretical claim (e.g. the governing equation, each assumption drawn from a textbook, any deduction taken from the guide's source material); if a claim has no citation, either add one (matching a source in References) or flag it to the user instead of leaving it uncited.
- **Full Continuous Two-Column Layout:** The entire body of the report, including References and Appendices (A, B, C, D), must strictly maintain the continuous two-column IEEE format without exception, including the extensive derivations in Appendices C and D.
- **Equations in Appendices (No `\begin{aligned}` or line breaks):** Strictly forbid using `\\` or multiline environments within the same block. Separate each step or long expression into individual, independent LaTeX blocks (`$$step 1$$`, `$$step 2$$`).
- **Equation Centering and Typographic Scaling (Entire Report):** All equations across the entire report — Introduction, Results, Appendix C, and Appendix D alike — must be perfectly centered within their column and scaled to 8.5 pt (Word OMML), preventing margin overflow and oversized symbols in any section, not just the appendices.
- **Do not go beyond, or move faster than, the scope of the guide**, unless the user gives explicit instructions to the contrary. When in doubt about whether something is in scope, ask before including it.
- **Abstract with no formulas, and short**: the abstract is a single continuous paragraph, with NO algebraic expressions or equations whatsoever. It must contain only numerical values with their uncertainty in "value ± error" format and, where applicable, the relative error percentage (e.g. "g = 9.209 ± 0.360 m/s², 3.9% relative error"). No formula symbols are allowed in the abstract (e.g. do not write "g = 4π²/m" there). Keep it concise — a brief paragraph (roughly 150–200 words), not an exhaustive recap of the whole report.
- **Introduction, Discussion, and Conclusions must be well-structured prose, with no bullet points.** These three sections are written as connected paragraphs with clear topic sentences and logical transitions between ideas — not as lists. Equations remain as numbered display blocks within the prose (that is not "bullet" content), but everything else — the theoretical narrative, assumptions, objectives in I; the interpretation in IV; the summary in V — must read as continuous academic prose. (Bulleted lists remain fine elsewhere, e.g. Materials and Equipment, Procedure steps.)
- **Equation rendering: Pandoc.** All mathematical equations (in the Introduction, Results, and Appendices C/D) must be written in LaTeX syntax and rendered into the .docx via Pandoc (LaTeX → Word native equations), so they appear as properly formatted, editable equations in the final Word document — not as plain text or images of formulas.
- **Table headers: plain text, zero equations.** Every table header (Raw Data Table, Linearized Data Tables, Residuals Table, etc.) must use plain-text column labels (e.g. "T^2 (s^2)", "X (m)", "Y (s^2/m)") — never a rendered/OMML equation inside a header cell, and never LaTeX delimiters (`$...$`, `$$...$$`) left unrendered inside a table.

### Default statistical scope (keep it lean — do not add extra topics unless requested)

Unless the user explicitly asks for it in Phase 0, the Statistical Treatment of the Linear Fit (Section III.A) and the Discussion (Section IV) are limited to:

- Ordinary Least Squares (OLS) linear regression
- Pearson correlation coefficient ($r$) and coefficient of determination ($R^2$)
- Residual analysis (standard error of the regression $s_e$, sum of squared residuals $SSE$)
- 95% confidence intervals using the Student-$t$ distribution (for reporting the uncertainty range of a result — not as a hypothesis test)
- Uncertainty propagation (partial derivatives / GUM approach)
- Origin-constrained regression ($b \equiv 0$), only when the guide or the physical model calls for it
- Arithmetic mean and standard error of the mean (trial-by-trial analysis)
- Percent relative discrepancy against geodesic/theoretical reference values

**Excluded by default** (do not include unless the user explicitly requests them for a specific report):

- Student-$t$ hypothesis testing on the intercept ($H_0: b = 0$)
- Finite-amplitude (Borda) correction / elliptic-integral small-angle approximation analysis

### Document structure

**Abstract** — a single paragraph, no formulas, only numerical values with uncertainty and relative error (physical system, independent-variable range, number of trials, fit results, derived physical constants with error, comparison to reference value, secondary verification method).

**Keywords** — 5 to 8 key terms.

**I. Introduction** — written as structured prose, no bullet points (equations remain as numbered display blocks within the prose).
Covers, in continuous academic narrative: the theoretical framework with numbered equations (comes from the conceptual framework obtained via RAG in Phase 0.1, adapted to the report's data and notation), the model's explicit assumptions/simplifications, and the objectives (taken from the professor's guide).

**II. Experimental Details**

- A. Materials and Equipment
- B. Experimental Setup
- C. Procedure (note any deviation from the guide, e.g. different data range — using what was confirmed in Phase 0)

**III. Results**

- Given/initial parameters
- Raw Data Table
- A. Data Analysis and Linearization
  - Linearization justification per case
  - Linearized data tables
  - Statistical Treatment of the Linear Fit (per the "Default statistical scope" list above — each metric defined first with its formula, then evaluated with the user's data; no extra topics beyond that list unless the user explicitly requested them)
- B. Graphs (one regression graph per case, with fitted equation + R²)

**IV. Discussion** — written as structured prose, no bullet points.

- Physical interpretation of intercepts
- Uncertainty comparison across methods
- Comparison to theoretical/reference value
- Which method is more reliable, and why

**V. Conclusions** — written as structured prose, no bullet points.

- Numeric summary tied to objectives
- Suggestions for future improvement

**References** — IEEE numbered style, from what the user provides or what is cited in the guide.

**Appendices**

- Appendix A — Raw/handwritten data sheet (placeholder note; the user attaches the scan/image separately)
- Appendix B — Graphs (pointer to III.B, do not duplicate the graphs, only reference them)
- Appendix C — Full step-by-step mathematical derivation of every computed constant (theoretical basis → data substitution → regression → result), entirely in LaTeX, fully worked with the user's actual numbers
- Appendix D — Justification of the error/uncertainty calculation, fully worked with the user's actual numbers, in LaTeX. Must explicitly develop, step by step, every item from the "Default statistical scope" list that applies to the report: Pearson $r$ / $R^2$ computation, $SSE$, $S_{xx}$, standard error of the regression ($s_e$) and of $m$/$b$, the 95% confidence interval via Student-$t$ (interval only, not a hypothesis test), trial-by-trial mean and standard error of the mean, uncertainty propagation to each derived physical constant, and the percent relative discrepancy against the reference value. Do not leave any of these as a bare final number — show the substitution.

### Materials the user must provide (reminder, already covered in Phase 0)

1. Professor's guide: [paste or attach]
2. Data table(s): [paste or attach]
3. Deviations from the guide / special notes: [describe, if any]
4. (Optional) Reference/theoretical value(s) to compare against: [if any]

---

## Python plotting script (matplotlib)

When the report is generated, also produce a Python script that plots the figures in a publication-style layout, sized to fit within one column of the two-column layout:

```python
import matplotlib.pyplot as plt
import numpy as np

# Professional styling, sized for single-column figures
plt.rcParams.update({
    'font.size': 9,
    'axes.labelsize': 10,
    'axes.titlesize': 11,
    'xtick.labelsize': 8,
    'ytick.labelsize': 8,
    'legend.fontsize': 8,
    'figure.titlesize': 12,
    'figure.figsize': (3.5, 2.8),  # width ~ single column in a two-column IEEE layout
    'grid.alpha': 0.4,
    'grid.linestyle': '--'
})

# 1. Nonlinear model curve vs experimental data
# 2. Linear regression Y vs X with fitted line, R², intercept
# 3. Residuals plot with shaded ±1s band
# 4. Evolution of the derived physical quantity
```
