---
type: prompt
id: identify-research-gaps
title: Identify Research Gaps
description: "Analyses existing literature to find gaps, contradictions, and opportunities for new research"
tags: [Production, Academic, Research]
inputs:
  research_topic:
    label: "Research Topic"
    description: "The research area or question to investigate"
    example: "Machine learning applications in early disease detection"
    required: true
    type: text
  literature_summary:
    label: "Literature Summary"
    description: "A summary of the existing literature on the topic"
    example: "Three meta-analyses have examined this relationship..."
    required: true
    type: text
  known_limitations:
    label: "Known Limitations"
    description: "Known limitations or constraints in the existing literature"
    example: "Most studies use self-reported data. Limited longitudinal evidence."
    required: true
    type: text
connections:
  - target: gap-analysis
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: analysis
---

## Purpose

Drives the research gap identification skill. Analyses the existing literature and field context to produce a structured gap analysis.

## Prompt

You are a research analyst specialising in literature gap analysis. Based on the research context below, identify gaps in the existing knowledge.

### Research Context

- **Field or topic:** {{input.research_topic}}
- **Literature summary:** {{input.literature_summary}}
- **Known limitations:** {{input.known_limitations}}

### Instructions

Analyse the provided literature and context to identify:

1. **Knowledge gaps** — specific questions the existing literature does not answer. For each gap, cite which studies come closest and explain what is missing.
2. **Methodological gaps** — approaches, populations, or settings that have not been studied. Explain why these gaps matter.
3. **Contradictions** — findings that conflict across studies. Note which studies disagree and what might explain the inconsistency.
4. **Emerging opportunities** — areas where recent developments (new methods, new data sources, shifting contexts) create openings for research that was previously impractical.
5. **Suggested research questions** — 3-5 specific, answerable research questions that directly address the most significant gaps.

### Output Format

Structure your analysis with clear headings for each section. For each gap or contradiction, reference the specific studies or findings involved. Prioritise gaps by significance — how much would answering this question advance the field?

## Formatting Rules

- Use British English throughout
- Reference specific studies by author and year where possible
- Keep each gap description to 2-3 sentences — concise, not exhaustive
- Order gaps by significance, most important first
