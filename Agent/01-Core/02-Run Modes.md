# 02 - Run Modes

## 1. Purpose

Run Modes define how deeply the Agent should work on an SRS task. They prevent uncontrolled full-document regeneration, reduce context waste, and protect approved content from accidental drift.

The default mode is **Incremental Mode** unless the user explicitly requests another mode or the target file is empty.

## 2. Supported Run Modes

### Mode 1 - Draft / Outline Mode

**Trigger**: A new project exists but the macro structure has not been confirmed.

**Objective**: Establish the high-level SRS structure before detailed requirements are written.

**Agent behavior**:

1. Read `01-Input Contract.md`, `SRS-TOC.md`, and `SRS-Template.md`.
2. Generate only the table of contents, document control skeleton, and executive summary.
3. Do not write detailed requirements.
4. Set generated content to `REVIEW` and halt for human feedback.

### Mode 2 - Incremental Mode

**Trigger**: The SRS exists, or the user asks for a specific section, module, feature, or requirement set.

**Objective**: Work section by section with high accuracy.

**Agent behavior**:

1. Focus on one specific section or module.
2. Load only the source material relevant to that section.
3. Read the existing target section before editing it.
4. Apply Micro Validation after writing.
5. Set completed work to `REVIEW` and halt for human review.

### Mode 3 - Audit / Validation Mode

**Trigger**: The user asks for an audit, validation is due, or conflict/TBD thresholds are exceeded.

**Objective**: Inspect quality without modifying the SRS.

**Agent behavior**:

1. Enter read-only mode for the SRS.
2. Apply relevant Micro and Macro Validation checks.
3. Produce an Issue List, Gap Analysis, Validation Report, or Traceability Report in `Project/`.
4. Do not introduce new business requirements.

### Mode 4 - Change Request / Patch Mode

**Trigger**: A new change request, meeting note, revised source, or direct user instruction changes existing requirements.

**Objective**: Apply change locally after impact analysis.

**Agent behavior**:

1. Log the change request.
2. Reference `Agent/02-SRS/07-Traceability Workflow.md`.
3. Identify directly and indirectly affected items.
4. Present impact analysis and halt for explicit human approval before patching approved or review-bound content.
5. Modify only affected items after approval.

### Mode 5 - Full Generation Mode

**Trigger**: The user explicitly asks for a full SRS, or the target SRS is empty and the mandatory inputs are present.

**Objective**: Generate the complete SRS through an ordered pipeline.

**Agent behavior**:

1. Decompose the SRS into sections.
2. Generate section by section, not as one uncontrolled block.
3. Apply validation after each major section.
4. Keep all generated content in `DRAFT` until it is submitted for review.
5. Submit completed sections as `REVIEW`; do not set `APPROVED`.

## 3. State Assessment Before Work

Before selecting a mode, the Agent must inspect:

| Item | Purpose |
|---|---|
| Existing `Project/` output | Determine whether content already exists. |
| Current user instruction | Determine whether scope is narrow or broad. |
| Requirement statuses | Protect `APPROVED` content. |
| Known gaps or conflicts | Determine whether Audit Mode is required. |

## 4. Automatic Mode Transitions

| Condition | Transition |
|---|---|
| Same-priority source conflict | Switch to Audit Mode, document conflict, halt. |
| Fatal mandatory input gap | Switch to questionnaire output, halt. |
| More than 30 percent TBD density in a section | Switch to Audit Mode, produce gap report, halt. |
| User introduces a change to existing requirements | Switch to Change Request / Patch Mode. |

## 5. Regeneration Constraint

The Agent must never regenerate an entire SRS unless:

1. The user explicitly requests full regeneration.
2. The existing target file is empty.
3. The Agent is operating in Full Generation Mode.

When existing content has `APPROVED` status, any modification requires an approved change request or explicit human instruction.
