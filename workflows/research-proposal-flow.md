---
type: workflow
id: research-proposal-flow
title: Research Proposal Flow
description: "Gap analysis, hypothesis generation, methodology design, and proposal drafting"
tags: [Production, Academic, Research, Risk]
connections:
  - target: hypothesis-generation
    type: uses
  - target: proposal-drafting
    type: uses
  - target: methodology-assessment
    type: uses
  - target: language-polish
    type: uses
  - target: llm-service
    type: runs_on
  - target: research-ethics-framework
    type: references
  - target: ethics-checklist
    type: references
  - target: research-protocol-template
    type: references
  - target: brief-compliance-check
    type: uses
  - target: input-gap-check
    type: uses
  - target: gap-analysis
    type: uses
metadata:
  estimated_duration: "30-60 minutes"
  trigger: manual
output_step: "language-polish"
composite_steps:
  - "gap-analysis"
  - "hypothesis-generation"
  - "methodology-assessment"
  - "proposal-drafting"
  - "language-polish"
  - "brief-compliance-check"
  - "input-gap-check"
execution:
  - skill: "gap-analysis"
    step_type: "synthesis"
    prompt: "identify-research-gaps"
    output: { name: "research_gaps", type: "text" }
  - skill: "hypothesis-generation"
    prompt: "hypothesis-generator"
    step_type: "generation"
    output: { name: "hypotheses", type: "text" }
  - skill: "methodology-assessment"
    prompt: "assess-methodology"
    step_type: "review"
    output: { name: "methodology_assessment", type: "text" }
  - skill: "proposal-drafting"
    prompt: "research-proposal-writer"
    step_type: "generation"
    output: { name: "proposal_draft", type: "text" }
  - skill: "language-polish"
    prompt: "polish-language"
    step_type: "content"
    output: { name: "polished_proposal", type: "text" }
    context:
      voice_profile: "Neutral professional tone"
      grammar_strictness: "Professional"
    bindings:
      source:
        from_step: "Proposal Drafting"
        field: output
  - parallel:
    - skill: "brief-compliance-check"
      prompt: "check-brief-compliance"
      step_type: "review"
      output: { name: "compliance_verdict", type: "decision" }
      context:
        audience_profile: "General professional audience"
        compliance_brief: "No specific compliance requirements"
        compliance_depth: "Standard"
      bindings:
        source:
          from_step: "Language Polish"
          field: output
    - skill: "input-gap-check"
      prompt: "check-input-gaps"
      step_type: "validation"
      output: { name: "input_gaps", type: "decision" }
---

## Overview

This workflow guides the development of a research proposal from initial gap analysis through to a complete, submission-ready document. Each stage builds on the previous one, with the methodology assessment providing quality assurance before the final draft.

## Pipeline Stages

### Stage 1: Gap Analysis

**Input:** Existing literature review or summary, research field description

Invoke the **gap-analysis** skill via the **identify-research-gaps** prompt to systematically identify what existing research has not covered. Produces categorized gaps with evidence and suggested research questions.

**Output:** Structured gap analysis with prioritized opportunities.

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
- If the proposal exceeds the target length, prioritize methodology and rationale sections — these are what reviewers scrutinise most

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.existing_literature_review_or}}` | Yes | Existing literature review or summary of the field | `Paste your literature review or summary of existing research here.` |
| `{{input.research_field_description}}` | Yes | Description of the research field or discipline | `Educational technology in UK higher education` |
| `{{input.existing_findings_from_the}}` | Yes | Existing findings from the literature and known limitations | `Studies show X but have not examined Y...` |
| `{{input.field_specific_standards}}` | No | Field-specific methodological standards | `CONSORT for RCTs, PRISMA for systematic reviews` |
| `{{input.available_resources}}` | No | Available resources and constraints for the proposed research | `12-month timeline, access to 3 secondary schools, no external funding` |
| `{{input.target_length}}` | No | Target length for the proposal | `3000 words` |

## Outputs

| Name | Description |
|------|-------------|
| Structured gap analysis | Structured gap analysis with prioritized opportunities |
| 3-5 testable hypotheses ranked by promise and feasibility | 3-5 testable hypotheses ranked by promise and feasibility |
| Assessed and refined methodology | Assessed and refined methodology |
| Complete research proposal draft | Complete research proposal draft |

## Setup

Before running this workflow:

1. No external services required — paste your content directly and provide any supporting context as inputs or source nodes.
2. Review the included documents, assets, or source nodes and customize them to match your team, brand, or domain conventions where needed.
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

