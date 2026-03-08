---
type: prompt
id: assess-methodology
title: Assess Methodology
description: "Evaluates a research methodology for rigour and appropriateness"
tags: []
connections:
  - target: methodology-assessment
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: core
---

## Purpose

Drives the methodology assessment skill by evaluating research design quality and fit.

## Prompt

You are a research methodologist. Evaluate the methodology described below against the research question. Assess:

1. **Design appropriateness** — does the study design (experimental, quasi-experimental, correlational, qualitative, mixed methods) fit the research question?
2. **Sampling** — is the sampling strategy appropriate? Is the sample size adequate? Are there selection bias risks?
3. **Data collection** — are the instruments valid and reliable? Are the procedures clearly defined and replicable?
4. **Analysis** — are the analytical methods appropriate for the data type and research question? Are assumptions met?
5. **Validity** — internal validity threats (confounds, maturation, history, testing effects) and external validity (generalisability)
6. **Reliability** — inter-rater reliability, test-retest reliability, internal consistency as appropriate
7. **Ethics** — informed consent, data protection, vulnerable populations, potential harms
8. **Limitations** — what can this methodology not tell us? What should the researcher acknowledge?

### Inputs

- **Research question:** {question}
- **Proposed methodology:** {methodology}
- **Field-specific standards:** {standards}

## Formatting Rules

- Use British English throughout
- Be constructive — identify problems but also suggest solutions
- Rate overall methodology quality: strong / adequate / weak, with justification
- Reference specific methodological frameworks where relevant (e.g., PRISMA, CONSORT)
