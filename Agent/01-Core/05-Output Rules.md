# 05 - Output Rules

## 1. Purpose

This document defines where the Agent writes output, which format it must use, which markers it must embed, and which status labels it must apply. These rules make SRS output consistent, machine-readable, auditable, and easier to validate.

## 2. Output Targets

| Output Type | Target Location | Rule |
|---|---|---|
| SRS document content | `Project/` | The Agent may create or modify only files in `Project/`. |
| Validation reports | `Project/` | Use separate files such as `Project/Validation-Report-YYYY-MM-DD.md`. |
| Traceability matrices | `Project/` | Use the SRS Section 16 or `Project/Traceability-Matrix.md`. |
| Change request artifacts | `Project/` | Use `Project/Change-Requests/` or a clearly named CR file. |

During normal SRS generation, the Agent must not modify `Agent/`, `Context/`, or `Human/`.

## 3. Requirement Statement Format

Every individual requirement must follow this structure:

```markdown
#### [REQ-ID] Requirement Title

- **Priority**: [Must / Should / Could / Won't] (MoSCoW)
- **Status**: [DRAFT | REVIEW | APPROVED | DEPRECATED]
- **Source**: [Source document name and section/page, or "Direct Prompt"]
- **Rationale**: [Why this requirement exists]
- **Acceptance Criteria**:
  1. [Testable criterion 1]
  2. [Testable criterion 2]
- **Dependencies**: [Related requirement IDs, or "None"]
- **Notes**: [Markers, assumptions, conflicts, or review notes]
```

## 4. Canonical ID Convention

All IDs use this canonical pattern:

```text
<TYPE>-<DOMAIN>-<NNN>
```

| Type | Meaning | Example |
|---|---|---|
| `FR` | Functional Requirement | `FR-AUTH-001` |
| `NFR` | Non-Functional Requirement | `NFR-PERF-001` |
| `BR` | Business Rule | `BR-ORDER-001` |
| `UC` | Use Case | `UC-PAY-001` |
| `CON` | Constraint | `CON-SEC-001` |
| `F` | Feature | `F-AUTH-001` |
| `AC` | Acceptance Criterion | `AC-AUTH-001` |
| `PF` | Product Function Group | `PF-GEN-001` |
| `STK` | Stakeholder | `STK-GEN-001` |
| `ACT` | Actor | `ACT-GEN-001` |
| `EXT` | External System | `EXT-INTG-001` |
| `BG` | Business Goal | `BG-GEN-001` |
| `SC` | Success Criterion | `SC-GEN-001` |
| `ENT` | Data Entity | `ENT-DATA-001` |
| `REL` | Data Relationship | `REL-DATA-001` |
| `DMR` | Data Modeling Rule | `DMR-DATA-001` |
| `TBL` | Physical Table | `TBL-DATA-001` |
| `COL` | Table Column | `COL-DATA-001` |
| `ATTR` | Entity Attribute | `ATTR-DATA-001` |
| `DATA` | Data Item | `DATA-DATA-001` |
| `VAL` | Data Validation Rule | `VAL-DATA-001` |
| `CDC` | Cross-Domain Constraint | `CDC-DATA-001` |
| `MIG` | Data Migration Item | `MIG-DATA-001` |
| `UI` | User Interface Requirement | `UI-GEN-001` |
| `IF` | Interface | `IF-INTG-001` |
| `SEC` | Security Or Access Control Requirement | `SEC-AUTH-001` |
| `STATE` | State | `STATE-GEN-001` |
| `TR` | State Transition | `TR-GEN-001` |
| `ERR` | Error | `ERR-GEN-001` |
| `EDGE` | Edge Case | `EDGE-GEN-001` |
| `DIA` | Diagram | `DIA-GEN-001` |
| `REF` | Reference | `REF-GEN-001` |
| `ASM` | Assumption | `ASM-GEN-001` |
| `DEP` | Dependency | `DEP-GEN-001` |
| `OQ` | Open Question | `OQ-GEN-001` |
| `DEC` | Decision | `DEC-GEN-001` |
| `RISK` | Risk | `RISK-GEN-001` |

Rules:

- `<TYPE>` is a short uppercase item type.
- `<DOMAIN>` is a stable uppercase domain or category code such as `AUTH`, `PAY`, `ORDER`, `PERF`, `SEC`, or `GEN`.
- `<NNN>` is a three-digit zero-padded sequence.
- IDs must be unique across the full SRS.
- IDs are permanent. Do not reuse an ID after deprecation.
- Use `GEN` for general document items without a natural domain.

## 5. Section Metadata

Each major SRS section must begin with:

```markdown
## [Section Number] Section Title

**Last Updated**: YYYY-MM-DD
**Status**: [DRAFT | REVIEW | APPROVED | DEPRECATED]
**Author**: [Agent | Human | Collaborative]
```

## 6. Canonical Status Labels

| Status | Meaning | Setter |
|---|---|---|
| `DRAFT` | Initial or revised content not yet submitted for review. | Agent |
| `REVIEW` | Submitted for human review or awaiting decision. | Agent |
| `APPROVED` | Explicitly accepted by a human approver. | Human only |
| `DEPRECATED` | Replaced or retired but retained for audit history. | Agent after human instruction or approved CR |

The Agent must never set a requirement, section, or change request result to `APPROVED` unless the human explicitly instructs it to record an approval decision.

## 7. Markers

Markers are inline tags used to flag gaps, conflicts, and assumptions.

| Marker | Usage | Required Behavior |
|---|---|---|
| `[TBD]` | A required detail is missing. | Place at the exact location and add to the TBD list. |
| `[TBD: description]` | A specific missing detail. | Prefer this over bare `[TBD]`. |
| `[ASSUMPTION]` | A defensible inference by the Agent. | Include reasoning immediately after the marker. |
| `[CONFLICT]` | Sources contradict each other. | Cite source priority handling and halt for same-priority conflicts. |
| `[REVIEW]` | Low confidence or human attention needed. | Explain what needs review. |
| `[DEPRECATED]` | Retained item no longer active. | Keep for audit history; do not delete. |

## 8. TBD Tracking List

The Agent must maintain a TBD list when any `[TBD]` markers exist:

```markdown
| TBD-ID | Location | Description | Assigned To | Target Date | Status |
|---|---|---|---|---|---|
| TBD-GEN-001 | FR-AUTH-003 | Maximum password length | Human | TBD | OPEN |
```

## 9. Formatting Standards

- Use ATX-style headings (`#`, `##`, `###`).
- Do not skip heading levels.
- Use numbered lists for ordered steps.
- Use bullets for unordered lists.
- Use fenced code blocks for schemas, APIs, data models, and examples.
- Use markdown tables for structured data.
- Use descriptive markdown links instead of bare URLs.
- Keep final project output in English ASCII unless the user requests localization.

## 10. Prohibited Formatting

| Prohibited | Reason |
|---|---|
| HTML tags inside markdown | Reduces portability across markdown renderers. |
| Bare URLs | Reduces readability and audit quality. |
| Emoji in IDs or statuses | Breaks predictable parsing. |
| Mixed status vocabularies | Breaks lifecycle validation. |
| Mixed ID patterns | Breaks traceability and impact analysis. |

## 11. Cross-References

- Conflict resolution: `04-Source Priority.md`
- Human escalation: `06-Human Interaction Protocol.md`
- Micro validation: `Agent/02-SRS/04-Micro Validation.md`
- Macro validation: `Agent/02-SRS/05-Macro Validation.md`
- Traceability: `Agent/02-SRS/07-Traceability Workflow.md`
