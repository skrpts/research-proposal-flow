---
type: workflow
id: research-proposal-flow
title: Research Proposal Flow
description: "Gap analysis, hypothesis generation, methodology design, and proposal drafting"
tags: [Draft]
connections:
  - target: gap-analysis
    type: uses
  - target: methodology-assessment
    type: uses
  - target: identify-research-gaps
    type: uses
  - target: assess-methodology
    type: uses
  - target: hypothesis-generator
    type: uses
  - target: research-proposal-writer
    type: uses
  - target: llm-service
    type: runs_on
metadata:
  estimated_duration: "30-60 minutes"
  trigger: manual
---

## Overview

This workflow guides the development of a research proposal from initial gap analysis through to a complete, submission-ready document. Each stage builds on the previous one, with the methodology assessment providing quality assurance before the final draft.

## Pipeline Stages

### Stage 1: Gap Analysis

**Input:** Existing literature review or summary, research field description

Invoke the **gap-analysis** skill via the **identify-research-gaps** prompt to systematically identify what existing research has not covered. Produces categorised gaps with evidence and suggested research questions.

**Output:** Structured gap analysis with prioritised opportunities.

### Stage 2: Hypothesis Generation

**Input:** Gap analysis from Stage 1, existing findings from the literature

Invoke the **hypothesis-generator** prompt to produce testable hypotheses that address the identified gaps. Each hypothesis includes rationale, variables, and expected outcomes.

**Output:** 3-5 testable hypotheses ranked by promise and feasibility.

### Stage 3: Methodology Design

**Input:** Selected hypothesis from Stage 2, field-specific standards

Design the methodology, then invoke the **methodology-assessment** skill via the **assess-methodology** prompt to evaluate it. Iterate on the design based on the assessment feedback.

**Gate:** Methodology must be rated "adequate" or "strong" before proceeding.

**Output:** Assessed and refined methodology.

### Stage 4: Proposal Drafting

**Input:** All outputs from Stages 1-3

Invoke the **research-proposal-writer** prompt to produce a complete proposal covering introduction, literature review, methodology, timeline, and expected outcomes.

**Output:** Complete research proposal draft.

## Error Handling

- If gap analysis finds no significant gaps, the research question may be too narrow or the field may be saturated — broaden the scope or consider a replication study
- If hypotheses are not testable with available resources, revise the scope or suggest collaboration
- If methodology assessment identifies critical weaknesses, return to Stage 3 before drafting
- If the proposal exceeds the target length, prioritise methodology and rationale sections — these are what reviewers scrutinise most

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.existing_literature_review_or}}` | Yes | Existing literature review or summary | `Paste the relevant brief, notes, source material, or dataset here.` |
| `{{input.research_field_description}}` | Yes | research field description | `Paste a short brief describing the goal, audience, and constraints.` |
| `{{input.existing_findings_from_the}}` | Yes | existing findings from the literature | `Paste the relevant brief, notes, source material, or dataset here.` |
| `{{input.field_specific_standards}}` | No | field-specific standards | `Paste the relevant brief, notes, source material, or dataset here.` |

## Outputs

| Name | Description |
|------|-------------|
| Structured gap analysis | Structured gap analysis with prioritised opportunities |
| 3-5 testable hypotheses ranked by promise and feasibility | 3-5 testable hypotheses ranked by promise and feasibility |
| Assessed and refined methodology | Assessed and refined methodology |
| Complete research proposal draft | Complete research proposal draft |

## Setup

Before running this workflow:

1. No external services required — paste your content directly and provide any supporting context as inputs or source nodes.
2. Review the included documents, assets, or source nodes and customise them to match your team, brand, or domain conventions where needed.
3. No specific AI provider or API key is required beyond your configured skrptiq LLM provider.

## Provider Notes

- Most stages work with any capable model; stronger models usually improve synthesis, judgement, and writing quality.
- Extraction, classification, and formatting steps generally run well on smaller or faster models.
- Because there are no vendor-specific integrations here, provider choice is mostly a trade-off between speed, quality, and cost.

## Example Input

To test this workflow immediately after import:

```
Existing Literature Review Or: "Paste the relevant brief, notes, source material, or dataset here."
Research Field Description: "Paste a short brief describing the goal, audience, and constraints."
Existing Findings From The: "Paste the relevant brief, notes, source material, or dataset here."
Field Specific Standards: "Paste the relevant brief, notes, source material, or dataset here."
```

