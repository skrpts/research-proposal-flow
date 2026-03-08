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
  - target: anthropic-claude
    type: runs_on
  - target: openai-gpt4
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
