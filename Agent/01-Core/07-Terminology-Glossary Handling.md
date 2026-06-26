# 07 — Terminology-Glossary Handling

## 1. Purpose

This document instructs the Agent on how to **extract, validate, and maintain terminology** from client-provided documents. The Agent must never invent domain-specific terms, abbreviations, or jargon. All terminology used in the SRS must be traceable to a client source or explicitly marked as an `[ASSUMPTION]`.

> [!IMPORTANT]
> The Agent is **strictly forbidden** from fabricating terminology. If a term appears in the SRS that does not exist in any client document or industry-standard glossary, the Agent has hallucinated. This is a critical failure.

---

## 2. Terminology Extraction Protocol

When the Agent ingests a client document (from `Context/` or via direct prompt), it must perform a terminology scan before writing any SRS content.

### 2.1 Extraction Steps

1. **Scan for domain-specific terms**: Identify nouns, noun phrases, abbreviations, and acronyms that carry specialized meaning in the client's business domain.
2. **Scan for defined terms**: Look for explicit definitions provided by the client (e.g., *"'Active User' means a user who has logged in at least once in the past 30 days"*).
3. **Scan for inconsistent usage**: Detect cases where the client uses multiple terms for the same concept (e.g., "Customer" vs. "Client" vs. "End User" — do they mean the same thing?).
4. **Flag ambiguous terms**: Mark any term that has multiple possible interpretations with `[TBD]` and escalate to the Human for clarification.

### 2.2 Extraction Output Format

The Agent must compile extracted terms into a structured **Glossary Draft Table**:

```markdown
| Term | Definition | Source Document | Source Page/Section | Status |
|------|-----------|-----------------|---------------------|--------|
| Active User | A user who has logged in at least once in the past 30 days | Client Brief v2.1 | §2.3 | CONFIRMED |
| SKU | Stock Keeping Unit — unique identifier for each product variant | Meeting Notes 2024-03-15 | Item 4 | CONFIRMED |
| Workspace | [TBD: Client uses this term but does not define it] | Client Brief v2.1 | §4.1 | PENDING |
```

---

## 3. Glossary Consistency Rules

### Rule 3.1 — Single Term, Single Meaning

Each term in the Glossary must map to **exactly one definition**. If the client uses the same term with different meanings in different contexts, the Agent must:

1. Flag the inconsistency with `[CONFLICT]`.
2. Propose disambiguated terms (e.g., *"User (End User)"* vs. *"User (Admin User)"*).
3. **HALT** and escalate to the Human for a decision per `06-Human Interaction Protocol.md`.

### Rule 3.2 — Single Concept, Single Term

If the client uses **multiple terms** for the same concept (synonyms), the Agent must:

1. Identify all variants (e.g., "Client", "Customer", "End User").
2. Propose a **canonical term** — the single preferred term to use throughout the SRS.
3. Present the proposal to the Human:
   ```
   [TERMINOLOGY CLARIFICATION]
   The following terms appear to refer to the same concept:
     - "Client" (used in BRD §1.2)
     - "Customer" (used in Meeting Notes 2024-03-15)
     - "End User" (used in Legacy SRS §3.1)
   ► Proposed canonical term: "Customer"
   ► Please confirm or specify your preferred term.
   ```
4. Once confirmed, use **only** the canonical term in all SRS output. Add the synonyms to the Glossary as "See also" references.

### Rule 3.3 — No Invented Terms

The Agent must **never** coin new terms, create abbreviations, or introduce jargon that does not appear in:

- The client's provided documents (any priority level per `04-Source Priority.md`), **OR**
- A widely recognized industry standard (e.g., IEEE, ISO, OWASP, W3C).

If the Agent needs to refer to a concept that has no established term, it must:

1. Use a plain, descriptive phrase.
2. Mark it with `[ASSUMPTION]` and propose a term for the Human's approval.

---

## 4. Glossary Placement in the SRS

### 4.1 Location

The Glossary must appear in the SRS at the location specified by `Context/SRS-Template.md` — typically in:

- **Section 1.4 — Definitions, Acronyms, and Abbreviations** (per IEEE 830 / IEEE 29148 template structure), **AND**
- Optionally as an **Appendix** if the glossary exceeds 30 entries.

### 4.2 Glossary Entry Format

Each entry in the final SRS Glossary must follow this format:

```markdown
| Term | Abbreviation | Definition | First Used In |
|------|-------------|-----------|---------------|
| Application Programming Interface | API | A set of protocols and tools for building software applications. | §3.2 |
| Stock Keeping Unit | SKU | A unique alphanumeric identifier assigned to each product variant for inventory tracking. | §4.1 |
```

---

## 5. Abbreviation and Acronym Rules

### Rule 5.1 — First Use Expansion

The first time an abbreviation or acronym appears in the SRS, it must be **written in full with the abbreviation in parentheses**:

- ✅ *"The Application Programming Interface (API) shall support RESTful endpoints."*
- ❌ *"The API shall support RESTful endpoints."* (first use without expansion)

### Rule 5.2 — Subsequent Uses

After the first expansion, the abbreviation may be used alone for the remainder of the section. If the SRS is long (10+ sections), re-expand at the first use in each major section for readability.

### Rule 5.3 — Acronym Table

Maintain a dedicated **Acronyms Table** in the Glossary section:

```markdown
| Acronym | Full Form |
|---------|-----------|
| API | Application Programming Interface |
| SRS | Software Requirements Specification |
| SSO | Single Sign-On |
| RBAC | Role-Based Access Control |
```

---

## 6. Handling Client-Specific vs. Industry-Standard Terms

| Scenario | Agent Action |
|----------|-------------|
| Client defines a term that matches an industry standard | Use the client's definition. Note the industry standard definition in the Glossary for reference. |
| Client defines a term that **conflicts** with an industry standard | Flag with `[CONFLICT]`. Use the client's definition (P2 > general knowledge) but add a note: *"Note: This differs from the standard industry definition of [term]."* |
| Client uses a term without defining it, but it has a clear industry-standard meaning | Adopt the industry-standard definition. Mark as `[ASSUMPTION]` with reasoning. |
| Client uses a completely novel term with no definition and no standard meaning | Insert `[TBD]` and escalate to the Human. Do not guess. |

---

## 7. Cross-Reference to Other Core Files

- **Source of truth for term definitions** → `04-Source Priority.md` (client definitions are P2–P3)
- **When to halt for terminology conflicts** → `06-Human Interaction Protocol.md`
- **Where to place the Glossary in the SRS** → `Context/SRS-Template.md`
- **Marker usage** → `05-Output Rules.md` §5
