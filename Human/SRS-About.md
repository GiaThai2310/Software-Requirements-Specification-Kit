---
title: About SRS
aliases:
  - SRS Overview
  - Software Requirements Specification Overview
tags:
  - srs
  - requirements-engineering
  - software-documentation
status: completed
---

# About SRS

This page explains what a Software Requirements Specification (SRS) is and how this kit uses it.

Detailed writing guidance is in `Human/SRS-Guide.md`.
The operational template is in `Context/SRS-Template.md`.

## 1. What Is An SRS?

A Software Requirements Specification is a structured document that describes what a software system shall do and the conditions it shall satisfy. It should make stakeholder needs clear enough for analysis, design, implementation, verification, validation, and change control.

An SRS answers questions such as:

- Why is this software being built?
- What is in scope and out of scope?
- Who uses, operates, or integrates with the system?
- What features and behaviors are required?
- What business rules and constraints apply?
- What data is created, processed, stored, exchanged, retained, or deleted?
- What quality attributes must be met?
- How will each requirement be verified?

An SRS should focus on required behavior and measurable constraints. It should avoid design or implementation detail unless that detail is itself a required constraint.

## 2. Why Use An SRS?

### 2.1 Shared Understanding

An SRS gives stakeholders, analysts, designers, developers, testers, and approvers a shared baseline for scope and behavior.

### 2.2 Scope Control

An SRS separates:

- In-scope work.
- Out-of-scope work.
- Future-scope work.
- Open questions.
- Assumptions.
- Dependencies.

### 2.3 Development Input

An SRS gives technical teams a reliable basis for design and implementation. It does not replace design documentation; it defines what the design must satisfy.

### 2.4 Verification Input

Requirements should be testable by test, analysis, inspection, or demonstration. Acceptance criteria and traceability links help testers derive evidence from requirements.

### 2.5 Change Control

When requirements change, an SRS helps determine impact. Traceability shows affected features, use cases, business rules, data, interfaces, tests, and risks.

## 3. What Good Requirements Look Like

Good requirements are:

- Necessary.
- Unambiguous.
- Complete enough to implement and test.
- Atomic.
- Verifiable.
- Feasible.
- Traceable.
- Consistent with source material.

This kit uses EARS-style requirement statements and a canonical ID/status model to make those qualities easier to check.

## 4. Kit Conventions

### 4.1 ID Format

All SRS item IDs use:

```text
<TYPE>-<DOMAIN>-<NNN>
```

Examples:

- `FR-AUTH-001`
- `NFR-PERF-001`
- `BR-ORDER-001`
- `UC-PAY-001`
- `OQ-GEN-001`

### 4.2 Status Format

The canonical statuses are:

| Status | Meaning |
|---|---|
| `DRAFT` | Created or revised but not yet submitted for review. |
| `REVIEW` | Ready for human review or awaiting decision. |
| `APPROVED` | Explicitly accepted by a human approver. |
| `DEPRECATED` | Retained for history but no longer active. |

The Agent may not independently approve content.

### 4.3 Markers

| Marker | Meaning |
|---|---|
| `[TBD]` | Required information is missing. |
| `[ASSUMPTION]` | The Agent made a documented inference. |
| `[CONFLICT]` | Sources contradict each other. |
| `[REVIEW]` | Human attention is needed. |
| `[DEPRECATED]` | Item is no longer active but retained for audit. |

## 5. Reference Basis

This kit is informed by:

- ISO/IEC/IEEE 29148:2018 for requirements engineering concepts, requirement attributes, and traceability.
- EARS for constrained natural-language requirement syntax.
- MoSCoW prioritisation for Must / Should / Could / Won't priority labels.
- INCOSE-style requirement quality characteristics for requirement review.

See `Project/Refactor-Log-2026-06-26.md` for the source links used during the English refactor.
