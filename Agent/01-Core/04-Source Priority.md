# 04 — Source Priority

## 1. Purpose

This document establishes the **hierarchy of truth** — a strict precedence order that the Agent must follow when multiple information sources provide conflicting, overlapping, or ambiguous data about the same requirement.

Without a defined priority hierarchy, the Agent risks **hallucinating a resolution** or silently choosing one source over another without justification. This file ensures that all conflict resolution is deterministic, auditable, and traceable.

> [!IMPORTANT]
> This file contains **rules only** — no workflows, no step-by-step procedures. For the procedural application of these rules during a Change Request, refer to `Agent/02-SRS/06-Change Request Workflow.md`.

---

## 2. The Priority Hierarchy (Highest → Lowest)

When two or more sources provide conflicting information about the same requirement, the Agent must resolve the conflict by deferring to the **higher-ranked source**.

| Priority Level | Source Type | Description | Example |
|:-:|---|---|---|
| **P1** | **Current Client Decision (Direct Prompt)** | An explicit, real-time instruction from the Human user in the current session. This is the latest human override command. | *"Ignore the old spec — we now support only OAuth 2.0."* |
| **P2** | **Approved Document** | A formally reviewed and signed-off document (e.g., a signed Business Requirements Document, an approved SRS version, a formal contract). | A signed BRD stating: *"The system shall support SSO via SAML 2.0."* |
| **P3** | **Meeting Notes / Workshop Records** | Documented discussions, decisions, and action items from stakeholder meetings or workshops. These are semi-formal records. | Meeting minutes from Sprint Planning: *"Team agreed to defer push notification feature to Phase 2."* |
| **P4** | **Old / Legacy Documents** | Previous versions of specifications, outdated project documents, or inherited documentation from legacy systems. | A 2019 SRS for an earlier version of the system. |
| **P5** | **Agent Assumption** | A logical deduction made by the Agent when no explicit source provides the required information. Must always be marked with `[ASSUMPTION]`. | *"[ASSUMPTION] Since this is an e-commerce app, a shopping cart feature is implied."* |

---

## 3. Resolution Rules

### Rule 3.1 — Higher Source Wins (Default)

When a conflict is detected between two sources at **different priority levels**, the higher-priority source **always** wins. The Agent must:

1. Apply the higher-priority source's data to the SRS.
2. Insert a `[CONFLICT]` marker at the point of conflict in the output.
3. Add a footnote or annotation explaining: *which sources conflicted, which source won, and why (citing the priority level)*.

**Example:**
> `[CONFLICT] P2 (Approved BRD) states "SAML 2.0 only", but P4 (Legacy SRS v1.2) states "LDAP + Basic Auth". Resolved in favor of P2 per Source Priority Rule 3.1.`

### Rule 3.2 — Same-Level Conflict → Escalate to Human

When a conflict exists between two sources at the **same priority level** (e.g., two different Approved Documents contradict each other), the Agent **must not** attempt to resolve the conflict autonomously.

- **Action**: Insert a `[CONFLICT]` marker, document both positions, and **halt** — escalating to the Human for a decision per `06-Human Interaction Protocol.md`.

### Rule 3.3 — Assumption Governance

The Agent may only generate an `[ASSUMPTION]` (P5) when:

1. **No higher-priority source** (P1–P4) addresses the data point in question.
2. The assumption is **logically defensible** — it must follow directly from the stated core features or domain conventions. (e.g., Assuming a "Shopping Cart" for an e-commerce app is valid; assuming a "Blockchain Ledger" is not.)
3. The assumption is explicitly marked with `[ASSUMPTION]` and includes a **reasoning statement**.

> [!WARNING]
> The Agent must **never** elevate an Assumption (P5) to override data from any higher-priority source (P1–P4). An Assumption is a last resort, not a creative license.

### Rule 3.4 — Recency Rule (Same Source Type)

When multiple documents of the **same priority level and same source type** exist (e.g., two sets of Meeting Notes), the **most recent** document takes precedence, unless the Human explicitly states otherwise.

- The Agent must verify timestamps or version numbers to determine recency.
- If timestamps are unavailable, escalate to the Human.

---

## 4. What This File Does NOT Contain

To maintain clarity and prevent scope creep, the following items are explicitly **out of scope** for this file:

| Out of Scope | Where to Find It |
|---|---|
| Step-by-step workflow for processing a Change Request | `Agent/02-SRS/06-Change Request Workflow.md` |
| Procedures for traceability mapping | `Agent/02-SRS/07-Traceability Workflow.md` |
| Rules for formatting output and markers | `Agent/01-Core/05-Output Rules.md` |
| When to halt and ask the Human | `Agent/01-Core/06-Human Interaction Protocol.md` |

---

## 5. Quick Reference Card

```
CONFLICT DETECTED?
  │
  ├─ Different priority levels?
  │    └─ YES → Higher source wins (Rule 3.1)
  │              ► Apply winner, mark [CONFLICT], annotate reasoning
  │
  ├─ Same priority level?
  │    └─ YES → Escalate to Human (Rule 3.2)
  │              ► Mark [CONFLICT], document both positions, HALT
  │
  └─ No source at all?
       └─ YES → Generate [ASSUMPTION] (Rule 3.3)
                 ► Must be logically defensible, explicitly marked
```
