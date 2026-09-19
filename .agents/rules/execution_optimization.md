---
name: execution-optimization
description: Optimizations to avoid Windows command-line bottlenecks, consolidate execution scripts, and streamline report generation.
always_on: true
---

# Execution & Workflow Optimization Rules

## Process Execution
- Always write scripts to `.py` files on disk before executing them, rather than passing long inline commands via `python -c`.
- Avoid breaking tasks into multiple sequential shell calls. Combine data processing, plotting, and compilation into a single unified script.
- Keep execution fast and direct; do not prompt the user for permission when running standard generation tasks.
- Keep table syntax formatted with blank lines around pipe tables to ensure proper Pandoc compilation into DOCX.

## Report Standards (Moderna_Informe)
- Abstract must be concise, single-paragraph, and strictly contain NO algebraic formulas—only numerical values with uncertainties, confidence intervals, and percentages.
- Linearization for Snell's law: $Y = \sin(\theta_1), X = \sin(\theta_3)$ so the slope directly equals the refractive index ($m = n$).
- Produce separate, individual plots for each working liquid (linear fit with equation and residual plot with $\pm 1s$ band).
- Always deliver both `.md` and native `.docx` formats.
