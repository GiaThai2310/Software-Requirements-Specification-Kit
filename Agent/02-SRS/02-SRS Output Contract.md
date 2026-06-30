# 02 - SRS Output Contract

## 1. Purpose

This document defines which SRS sections are required by project scale. `Context/SRS-TOC.md` defines structure. `Context/SRS-Template.md` defines section formatting. This file defines tailoring rules.

## 2. Project Scale Classification

| Tier | Criteria | Typical Projects |
|---|---|---|
| Tier 1 - Small | Up to 3 user classes, up to 10 features, single platform, no regulatory burden | Internal tools, MVPs, prototypes |
| Tier 2 - Medium | 4-8 user classes, 11-30 features, integrations or multiple platforms | SaaS products, e-commerce, mid-size enterprise apps |
| Tier 3 - Large | 9 or more user classes, more than 30 features, compliance or multi-system integration | Healthcare, fintech, government, ERP |

If scale is unclear, default to Tier 2 and add `[REVIEW]` asking the human to confirm.

## 3. Section Requirements By Tier

Legend:

- `R` = Required.
- `C` = Conditional or recommended.
- `O` = Optional.
- `X` = Skip unless the human requests it.

| Section | Tier 1 | Tier 2 | Tier 3 |
|---|:-:|:-:|:-:|
| 0. Document Control | O | R | R |
| 1. Introduction | R | R | R |
| 2. Overall Description | R | R | R |
| 3. Stakeholders, Actors and External Systems | C | R | R |
| 4. Business Context | C | R | R |
| 5. Product Features | R | R | R |
| 6. Use Case Specifications | O | R | R |
| 7. Business Rules | O | R | R |
| 8. Functional Requirements | R | R | R |
| 9. Data Requirements And Data Model | O | R | R |
| 10. External Interface Requirements | C | R | R |
| 11. Non-functional Requirements | C | R | R |
| 12. Access Control Requirements | O | R | R |
| 13. State Models | X | C | R |
| 14. Error Handling and Edge Cases | O | R | R |
| 15. Acceptance Criteria and Verification | C | R | R |
| 16. Requirements Traceability | X | R | R |
| 17. Open Questions, Decisions and Risks | R | R | R |
| 18. Appendices | O | R | R |
| 19. Requirement Identification Convention | R | R | R |
| 20. Requirement Status Convention | R | R | R |
| 21. SRS Review Checklist | X | C | R |
| 22. Approval | X | C | R |

## 4. Universal Mandatory Sections

All SRS outputs must include:

1. Purpose.
2. Scope.
3. Definitions, acronyms, and abbreviations.
4. Product functions.
5. User classes.
6. Assumptions and dependencies.
7. Problem statement.
8. Product features.
9. Functional requirements.
10. Data requirements and data model when the system stores, processes, exchanges, reports on, migrates, or retains business data.
11. Open questions and risks.
12. Requirement identification convention.
13. Requirement status convention.

## 5. Skipped Section Protocol

When a section is skipped by tier:

1. Do not silently omit it if the section number is part of the selected output structure.
2. Add a short placeholder:

```markdown
## [Section Number] Section Title

**Last Updated**: YYYY-MM-DD
**Status**: REVIEW
**Author**: Agent

This section is omitted for this project tier. Revisit if scope expands.
```

3. Log the omission in Section 17 if it could affect stakeholder expectations.

## 6. Status And Approval

The Agent may draft, submit for review, or deprecate after approved change control. The Agent must not independently approve content.
