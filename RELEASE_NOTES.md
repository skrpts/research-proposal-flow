# Release Notes

## v1.1.32
GH#1100 consumer wave batch 6 — declare the data flow these steps were resolving positionally. 3 binding(s) added.

Two slots take declared inputs. `identify-research-gaps` ("Prior Analysis") sits at position 1 with nothing upstream — new required `prior_literature`. `check-input-gaps` ("Inputs Provided") reports what the user omitted, so it cannot come from a step — new required `inputs_provided`.

**This flow now requires input it did not require before.** That is the fix: previously the user supplied nothing for these slots and the step silently received whatever the binding pointed at.

`assess-methodology` (slot "Research Gap Analysis") binds Research Gap Identification rather than its positional predecessor, which emits hypotheses — the label names the step exactly.

## v1.1.31
GH#1044 — the last of the required-but-undocumented inputs, resolved by testing whether the existing table name is itself required by a prompt rather than by how similar the names look. Renamed existing_literature_review_or to the name the prompt consumes; documented literature_summary, research_topic. Rows generated from the requiring prompt's own declared description, example and required flag. No behaviour change; documentation only.

## v1.1.30
GH#1044 — document the inputs this workflow's prompts REQUIRE but its Inputs table never listed. A user supplying exactly what the table asked for was running with required parameters unsatisfied — a silent wrong run, not a documentation nicety. Renamed 1 row(s) (existing_literature_review_or) to the name the prompt actually consumes; documented 3 input(s): known_limitations, literature_summary, research_topic. Every row is generated from the requiring prompt's own declared description, example and required flag — none invented. No behaviour change; documentation only.

## v1.1.29
GH#818 Phase 1 (Tier 1) — fix intent-vs-output: the pipeline promised a drafted proposal but ran gap-analysis + methodology-assessment → polish (it polished the ANALYSIS). The `hypothesis-generator` and `research-proposal-writer` prompts were shipped but never wired in. Wire both on dedicated local skills (`hypothesis-generation` → "Hypothesis Generator", `proposal-drafting` → "Proposal Drafting"): gap-analysis → hypothesis → methodology → **research-proposal-writer(draft)** → polish. Re-point the proposal-writer's gap refs to `{{steps.Research Gap Identification.output}}` (resolvable title). Polish binds `source` `from_step "Proposal Drafting"`; coherent-lock all deps to current published (repin `polish-language` → 1.0.5, `check-brief-compliance` → 1.0.3 with its new `source` binding). contents skills 0→2.

## v1.1.28
GH#745 — declare per-step `output: {name, type}` on every execution step (research_gaps/text, compliance_verdict/decision, input_gaps/decision, methodology_assessment/text, polished_proposal/text). Lights up the #744 rich flow-map with named, typed outputs. **Also corrects the input-gap-check step to its intended `validation` type** — its `step_type` was mis-indented (outside the parallel item) and dropped at parse time, so the step previously ran untyped; it is now a validation gate. Content + structural fix (GH#748); no bindings changes.

## v1.1.27
GH#645 Row 3b — migrate to K-037 dep-referenced schema. Strip 13 inline shared-content files and declare 13 hub-shared deps (UUID id + slug name + version + checksum from `gen-dep-checksums.mjs`). Closes pre-Step-3 inline-vendoring for this bundle.

## v1.1.26
Wave 2: re-signed with canonical engine signing pipeline.

## v1.1.25
Tags migrated inline into manifest (GH#586). tags.yaml retired.

## v1.1.24
Bundle re-signed with canonical engine signing pipeline (Wave 2 migration).

## v1.1.23
Signature fix — RELEASE_NOTES.md now included in integrity checksum.

## v1.1.22
Initial catalog release with full structural and content-quality validation. All scanner checks pass.
