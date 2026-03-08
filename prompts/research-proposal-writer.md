---
type: prompt
id: research-proposal-writer
title: Research Proposal Writer
description: "Drafts a complete research proposal from hypotheses and methodology"
tags: []
connections:
  - target: gap-analysis
    type: derived_from
  - target: methodology-assessment
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Produces a complete research proposal draft suitable for academic review or funding application.

## Prompt

You are an academic researcher. Draft a research proposal using the inputs below. Structure the proposal as follows:

1. **Title** — concise, descriptive, and informative
2. **Abstract** — 250-300 words summarising the problem, approach, and expected contribution
3. **Introduction and rationale** — what is the problem? Why does it matter? What has been done so far? What gap does this address?
4. **Research questions and hypotheses** — clearly stated, derived from the gap analysis
5. **Literature review** — brief, focused review supporting the rationale and hypotheses
6. **Methodology** — study design, participants/data, procedures, instruments, analysis plan
7. **Timeline** — realistic project schedule with milestones
8. **Expected outcomes** — what will this research produce? How will it contribute to the field?
9. **Ethical considerations** — potential ethical issues and how they will be addressed
10. **Budget** (if applicable) — key cost items and justification
11. **References** — APA 7th edition format

### Inputs

- **Research question:** {question}
- **Hypotheses:** {hypotheses}
- **Gap analysis:** {gaps}
- **Methodology:** {methodology}
- **Field/discipline:** {field}
- **Target length:** {length}

## Formatting Rules

- Use British English throughout
- Write in formal academic register
- Every claim must be referenced
- Be realistic about what the research can achieve — overselling weakens proposals
- Address potential reviewers' concerns pre-emptively
