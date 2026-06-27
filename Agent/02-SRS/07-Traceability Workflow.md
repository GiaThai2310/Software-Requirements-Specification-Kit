# 07 - Traceability Workflow

## 1. Purpose

Traceability links each requirement backward to its source and forward to verification. It is the mechanism that prevents orphan requirements, uncontrolled scope growth, and unverifiable SRS content.

## 2. ID Assignment Rules

Use the canonical pattern:

```text
<TYPE>-<DOMAIN>-<NNN>
```

Examples:

| Type | Example |
|---|---|
| Functional Requirement | `FR-AUTH-001` |
| Non-Functional Requirement | `NFR-PERF-001` |
| Business Rule | `BR-ORDER-001` |
| Use Case | `UC-PAY-001` |
| Constraint | `CON-SEC-001` |
| Feature | `F-AUTH-001` |
| Acceptance Criterion | `AC-AUTH-001` |
| Change Request | `CR-GEN-001` |
| Data Entity | `ENT-DATA-001` |
| Data Relationship | `REL-DATA-001` |
| Physical Table | `TBL-DATA-001` |
| Table Column | `COL-DATA-001` |
| Entity Attribute | `ATTR-DATA-001` |
| Data Item | `DATA-DATA-001` |
| Data Validation Rule | `VAL-DATA-001` |
| Data Migration Item | `MIG-DATA-001` |

Rules:

1. Assign IDs when the item is created.
2. Never reuse or reassign IDs.
3. Sequence numbers increment within each type-domain pair.
4. Deprecated IDs remain in the document.
5. Domain codes must remain stable.

## 3. Recommended Domain Codes

| Code | Domain |
|---|---|
| `AUTH` | Authentication |
| `USR` | User management |
| `PAY` | Payment |
| `NOTIF` | Notifications |
| `PROD` | Product or catalog |
| `ORDER` | Order lifecycle |
| `RPT` | Reporting |
| `ADMIN` | Administration |
| `INTG` | Integration |
| `SRCH` | Search |
| `DATA` | Data management |
| `SEC` | Security |
| `PERF` | Performance |
| `GEN` | General or document-level item |

If a new domain is needed, propose it and mark `[REVIEW]` unless the human already specified it.

## 4. Traceability Link Types

| Link Type | Direction | From | To |
|---|---|---|---|
| Source Trace | Backward | Requirement | Source document or decision |
| Parent Trace | Backward | Requirement | Feature, goal, or use case |
| Derivation Trace | Forward | Feature or use case | Requirements |
| Verification Trace | Forward | Requirement | Acceptance criteria, test case, or evidence |
| Dependency Trace | Lateral | Requirement | Related requirement |

## 5. Minimum Traceability

| Item Type | Source Trace | Parent Trace | Verification Trace |
|---|:-:|:-:|:-:|
| FR | Required | Recommended | Required |
| NFR | Required | Optional | Required |
| BR | Required | Optional | Recommended |
| UC | Required | Recommended | Required |
| CON | Required | Optional | Recommended |
| ENT | Required | Recommended | Recommended |
| REL | Required | Recommended | Recommended |
| TBL | Required | Recommended | Recommended |
| COL | Required | Recommended | Recommended |
| ATTR | Required | Recommended | Recommended |
| DATA | Required | Recommended | Recommended |
| VAL | Required | Optional | Recommended |
| MIG | Required | Optional | Recommended |

## 6. Requirements Traceability Matrix

Maintain an RTM in SRS Section 16 or `Project/Traceability-Matrix.md`.

```markdown
| ID | Title | Source | Source Location | Parent | Related Feature/UC | Verification | Status |
|---|---|---|---|---|---|---|---|
| FR-AUTH-001 | Email format validation | Client Brief v2.1 | Section 3.1 | F-AUTH-001 | UC-AUTH-001 | AC-AUTH-001 | DRAFT |
| NFR-PERF-001 | Search response time | Direct Prompt | Session YYYY-MM-DD | None | F-SRCH-001 | AC-PERF-001 | DRAFT |
```

Maintain data traceability in SRS Section 9.11 when data artifacts are present.

```markdown
| Data Item | Source | Entity/Table | Used By Feature | Used By Requirement | Validation Rule | Retention Rule | Migration Rule |
|---|---|---|---|---|---|---|---|
| DATA-DATA-001 | Client Brief v2.1 | ENT-DATA-001 / TBL-DATA-001 | F-DATA-001 | FR-DATA-001 | VAL-DATA-001 | Retain 7 years | MIG-DATA-001 |
```

## 7. RTM Maintenance Rules

- Update the RTM whenever a requirement is created, changed, deprecated, or renumbered.
- Do not remove deprecated IDs from the RTM.
- Record change request IDs when a CR modifies a requirement.
- During validation, compare the RTM against the actual SRS body.

## 8. Orphan Detection

| Orphan Type | Definition | Severity |
|---|---|---|
| No Source | Requirement lacks a backward source trace. | Critical |
| No Verification | Requirement lacks acceptance criteria or test evidence. | Warning |
| No Parent | Functional requirement lacks feature, goal, or use case trace. | Warning |
| Dead Link | Referenced ID does not exist or is deprecated without replacement. | Critical |
| Unmapped Data | Data item lacks entity/table, source, or related requirement trace. | Warning |

## 9. Orphan Resolution

1. No Source: ask the human for a source or mark as `[ASSUMPTION]` if defensible.
2. No Verification: write or request acceptance criteria.
3. No Parent: map to a feature or mark `[REVIEW]`.
4. Dead Link: repair the reference or document deprecation replacement.

## 10. Source Reference Format

Use this format:

```markdown
- **Source**: [Document Name], [Section/Page/Item Number]
```

Examples:

| Source Type | Format |
|---|---|
| Client Brief | `Client Brief v2.1, Section 3.1` |
| Meeting Notes | `Meeting Notes 2026-06-26, Item 4` |
| Direct Prompt | `Direct Prompt, session YYYY-MM-DD` |
| Approved Document | `Approved BRD v1.0, Section 5.2` |
| Agent Assumption | `[ASSUMPTION] Domain inference with reasoning` |

## 11. Cross-References

- Output rules: `Agent/01-Core/05-Output Rules.md`
- Source priority: `Agent/01-Core/04-Source Priority.md`
- Change request workflow: `Agent/02-SRS/06-Change Request Workflow.md`
- Macro validation: `Agent/02-SRS/05-Macro Validation.md`
