# 07 - Terminology And Glossary Handling

## 1. Purpose

This document instructs the Agent how to extract, validate, and maintain terminology. The Agent must not invent domain-specific terms, abbreviations, or jargon. Every specialized term in the SRS must be traceable to a source, an accepted industry standard, or a clearly marked `[ASSUMPTION]`.

## 2. Terminology Extraction Protocol

Before writing SRS content, scan source material for:

1. Domain-specific nouns and noun phrases.
2. Abbreviations and acronyms.
3. Explicit definitions from the client.
4. Terms used inconsistently across sources.
5. Undefined terms with multiple possible meanings.

## 3. Glossary Draft Format

Use this draft table while analyzing source material:

```markdown
| Term | Definition | Source Document | Source Location | Status |
|---|---|---|---|---|
| Active User | User who has logged in at least once in the past 30 days | Client Brief v2.1 | Section 2.3 | CONFIRMED |
| Workspace | [TBD: client uses this term without definition] | Client Brief v2.1 | Section 4.1 | PENDING |
```

## 4. Glossary Consistency Rules

### Rule 4.1 - One Term, One Meaning

Each glossary term must map to one definition. If a term has multiple meanings, mark `[CONFLICT]`, propose disambiguated labels, and halt for human decision.

### Rule 4.2 - One Concept, One Preferred Term

If multiple terms appear to refer to the same concept, the Agent must propose a canonical term and ask for confirmation.

Example:

```markdown
[TERMINOLOGY CLARIFICATION]
The following terms appear to refer to the same concept:
- "Client"
- "Customer"
- "End User"

Suggested canonical term: "Customer"
Please confirm or specify the preferred term.
```

### Rule 4.3 - No Invented Jargon

The Agent must not coin abbreviations or specialized labels unless:

1. The term appears in a source.
2. The term is an established industry term.
3. The term is proposed explicitly as `[ASSUMPTION]` for human approval.

## 5. Glossary Placement

The final SRS should include glossary content in:

- Section 1.4 - Definitions, Acronyms And Abbreviations.
- Appendix 18.1 - Glossary, when the glossary is long or needs supporting detail.

## 6. Final Glossary Format

```markdown
| Term | Type | Definition | First Used In | Source |
|---|---|---|---|---|
| Application Programming Interface | Acronym | A set of protocols and tools for software integration. | Section 10.2 | Industry standard |
```

## 7. Acronym Rules

- Expand an acronym at first use: `Application Programming Interface (API)`.
- Re-expand at the first use of each major section for long documents.
- Maintain an acronym table when more than five acronyms are used.

## 8. Client Terms Versus Industry Terms

| Scenario | Agent Action |
|---|---|
| Client defines a term | Use the client definition. |
| Client definition conflicts with industry meaning | Use the client definition, flag `[CONFLICT]` if risk exists, and note the difference. |
| Client uses an undefined common industry term | Use the standard meaning and mark `[ASSUMPTION]`. |
| Client uses an undefined novel term | Mark `[TBD]` and ask the human. |

## 9. Cross-References

- Source priority: `04-Source Priority.md`
- Human escalation: `06-Human Interaction Protocol.md`
- Output markers: `05-Output Rules.md`
- SRS template: `Context/SRS-Template.md`
