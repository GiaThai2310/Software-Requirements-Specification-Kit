# 05 — Output Rules

## 1. Purpose

This document defines **where** the Agent writes its output, **what format** it must use, **which markers** it must embed, and **what status labels** it must apply to each requirement or section. These rules ensure structural consistency, machine-readability, and auditability across all SRS deliverables.

> [!IMPORTANT]
> The Agent must **never** output requirements in free-form prose without proper structure. Every requirement must have an ID, a status, and full traceability metadata.

---

## 2. Output Target (Where to Write)

| Output Type | Target Location | Rule |
|---|---|---|
| **SRS document content** (requirements, sections, narratives) | `Project/` directory | The Agent may only create or modify files within `Project/`. |
| **Validation reports** (Issue Lists, Gap Analysis) | `Project/` directory | Output as separate files (e.g., `Project/Validation-Report-YYYY-MM-DD.md`). |
| **Traceability matrices** | `Project/` directory | Output as a dedicated file (e.g., `Project/Traceability-Matrix.md`). |
| **Change Request patches** | `Project/` directory | Output as a diff-style patch file or inline edits within the target SRS section. |

> [!WARNING]
> The Agent must **NEVER** write to or modify files in `Agent/`, `Context/`, or `Human/` directories. These are immutable. Violation of this rule is a critical failure. See `AGENTS.md` §2.

---

## 3. Output Format (How to Write)

### 3.1 Requirement Statement Format

Every individual requirement must follow this template:

```markdown
#### [REQ-ID] Requirement Title

- **Priority**: [Must / Should / Could / Won't] (MoSCoW)
- **Status**: [DRAFT | REVIEW | APPROVED | DEPRECATED]
- **Source**: [Source document name + section/page, or "Direct Prompt"]
- **Rationale**: [Why this requirement exists]
- **Acceptance Criteria**:
  1. [Testable criterion 1]
  2. [Testable criterion 2]
- **Dependencies**: [List of related REQ-IDs, or "None"]
- **Notes**: [Any additional context, markers, or annotations]
```

### 3.2 Requirement ID Convention

| Component | Format | Example |
|---|---|---|
| **Functional Requirement** | `FR-[Module]-[NNN]` | `FR-AUTH-001` |
| **Non-Functional Requirement** | `NFR-[Category]-[NNN]` | `NFR-PERF-003` |
| **Business Rule** | `BR-[NNN]` | `BR-012` |
| **Use Case** | `UC-[Module]-[NNN]` | `UC-PAY-002` |
| **Constraint** | `CON-[NNN]` | `CON-005` |

- `[Module]` = a short code for the feature area (e.g., `AUTH`, `PAY`, `USR`, `NOTIF`).
- `[NNN]` = a three-digit, zero-padded sequential number.
- IDs must be **unique across the entire SRS**. The Agent must never reuse or reassign an ID.

### 3.3 Section Structure

Each major SRS section must begin with:

```markdown
## [Section Number] Section Title

**Last Updated**: [YYYY-MM-DD]
**Status**: [DRAFT | REVIEW | APPROVED]
**Author**: [Agent | Human | Collaborative]
```

---

## 4. Status Labels

Every requirement and every section must carry a **status label**. The Agent must set and update these labels according to the following lifecycle:

| Status | Meaning | Who Sets It |
|---|---|---|
| `DRAFT` | Initial generation by the Agent. Not yet reviewed by a Human. | Agent |
| `REVIEW` | Submitted to the Human for review. Awaiting feedback. | Agent (when submitting for review) |
| `APPROVED` | Explicitly approved by the Human. Locked from further Agent modification unless a Change Request is filed. | Human only |
| `DEPRECATED` | Superseded or removed by a Change Request. Retained for audit trail but not active. | Agent (upon Human instruction) |

> [!IMPORTANT]
> The Agent must **never** set a requirement's status to `APPROVED`. Only the Human can approve. The Agent may propose `REVIEW` status and halt.

---

## 5. Markers (Inline Annotations)

Markers are inline tags that the Agent must embed directly in the SRS text to flag information gaps, conflicts, and assumptions. These markers are machine-searchable and must follow consistent formatting.

### 5.1 Marker Definitions

| Marker | Usage | Agent Behavior |
|---|---|---|
| `[TBD]` | **To Be Determined**. A specific detail is missing from the client input but is required for the SRS. | Insert at the exact location of the missing data. Add an entry to the TBD tracking list (see §5.2). |
| `[TBD: description]` | A TBD with a short inline description of what information is needed. | Preferred over bare `[TBD]` for clarity. Example: `[TBD: maximum file upload size in MB]` |
| `[ASSUMPTION]` | The Agent has made a logical deduction to proceed. | Must include a reasoning statement immediately after. Example: `[ASSUMPTION] Since this is an e-commerce platform, a product catalog is implied.` |
| `[CONFLICT]` | Two or more sources contradict each other on the same data point. | Must include a resolution annotation citing `04-Source Priority.md`. If same-level conflict, Agent must HALT and escalate per `06-Human Interaction Protocol.md`. |
| `[REVIEW]` | The Agent is uncertain about the accuracy or completeness of this content. | Flag for Human attention. Does not imply a conflict — just low confidence. |
| `[DEPRECATED]` | This requirement or section has been superseded. | Retained in the document for audit trail. Must not be deleted. |

### 5.2 TBD Tracking List

The Agent must maintain a **TBD Tracking List** as an appendix in the SRS output file. Each entry must include:

```markdown
| TBD-ID | Location (REQ-ID / Section) | Description | Assigned To | Target Date | Status |
|--------|----------------------------|-------------|-------------|-------------|--------|
| TBD-001 | FR-AUTH-003 | Maximum password length | [TBD] | [TBD] | OPEN |
| TBD-002 | §3.2 | Payment gateway provider selection | [TBD] | [TBD] | OPEN |
```

> [!TIP]
> The goal is to **resolve all TBDs before implementation begins**. The TBD list serves as a punch list for the Human to work through with stakeholders.

---

## 6. Formatting Standards

### 6.1 General Markdown Rules

- Use **ATX-style headers** (`#`, `##`, `###`) — not Setext (underlines).
- Use **numbered lists** for sequential/ordered items (steps, acceptance criteria).
- Use **bulleted lists** for unordered items (features, notes).
- Use **fenced code blocks** (`` ``` ``) for any technical specifications, API schemas, or data models.
- Use **tables** for structured data (traceability matrices, TBD lists, comparison charts).

### 6.2 Prohibited Formatting

| Prohibited | Reason |
|---|---|
| HTML tags inside markdown | Breaks portability across markdown renderers. |
| Bare URLs without link text | Reduces readability. Always use `[descriptive text](URL)`. |
| Emoji in requirement IDs or status labels | Non-standard; breaks machine parsing. |
| Inconsistent heading levels (skipping from `##` to `####`) | Breaks document outline and TOC generation. |

---

## 7. Cross-Reference to Other Core Files

- **Where conflicts in sources arise** → `04-Source Priority.md`
- **When to halt and ask the Human** → `06-Human Interaction Protocol.md`
- **How to validate output quality** → `Agent/02-SRS/04-Micro Validation.md`, `Agent/02-SRS/05-Macro Validation.md`
- **Structural alignment for the SRS** → `Context/SRS-TOC.md`, `Context/SRS-Template.md`
