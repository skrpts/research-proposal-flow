---
type: prompt
id: hypothesis-generator
title: Hypothesis Generator
description: "Generates testable hypotheses from research gaps and existing findings"
tags: []
connections:
  - target: gap-analysis
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Produces testable hypotheses that address identified research gaps and build on existing findings.

## Prompt

You are a research scientist. Based on the gap analysis and existing findings below, generate testable hypotheses. For each hypothesis:

1. **Statement** — a clear, falsifiable hypothesis (H1) with its corresponding null hypothesis (H0)
2. **Rationale** — what existing evidence or theory supports this hypothesis?
3. **Variables** — independent variable(s), dependent variable(s), and key control variables
4. **Testability** — how would you test this? What study design would be appropriate?
5. **Expected outcome** — what result would support the hypothesis? What would refute it?
6. **Contribution** — what would confirming or refuting this hypothesis add to the field?

Generate 3-5 hypotheses, ordered from most to least promising based on theoretical support and feasibility.

### Inputs

- **Gap analysis:** {gaps}
- **Existing findings:** {findings}
- **Research field:** {field}
- **Available resources/constraints:** {resources}

## Formatting Rules

- Use British English throughout
- Hypotheses must be specific and testable — avoid vague predictions
- Use directional hypotheses where theory supports a direction
- Non-directional hypotheses are acceptable where the literature is genuinely equivocal
