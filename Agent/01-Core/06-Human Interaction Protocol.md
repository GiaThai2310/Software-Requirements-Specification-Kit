# 06 — Human Interaction Protocol

## 1. Purpose

This document defines **when, why, and how** the Agent must pause its autonomous execution and defer a decision to the Human user. The goal is to strike the correct balance between Agent autonomy and Human oversight — the Agent should not halt for trivial decisions (which destroys throughput), nor should it silently resolve ambiguities that carry significant risk (which destroys trust).

> [!IMPORTANT]
> The default stance of the Agent is: **"When in doubt, halt and ask."** It is always safer to pause and present options than to silently make a wrong decision.

---

## 2. Mandatory Halt Conditions

The Agent **MUST** halt execution and escalate to the Human in all of the following situations. There are no exceptions.

### 2.1 Source Conflict at the Same Priority Level

- **Trigger**: Two or more sources at the **same priority level** (per `04-Source Priority.md`) contradict each other.
- **Example**: Two Approved Documents (both P2) state different authentication methods.
- **Agent Behavior**:
  1. Insert a `[CONFLICT]` marker at the point of contradiction.
  2. Document both positions clearly, citing the exact source and passage.
  3. **HALT**. Present the conflict to the Human with a structured prompt:
     ```
     [CONFLICT ESCALATION]
     ► Source A (P2 — Approved BRD §3.1): "System shall use SAML 2.0"
     ► Source B (P2 — Approved Security Policy §2.4): "System shall use OAuth 2.0 + PKCE"
     ► Action Required: Please confirm which authentication protocol to adopt, or provide a hybrid approach.
     ```

### 2.2 Fatal Data Gap

- **Trigger**: A Mandatory Input (as defined in `01-Input Contract.md` §3) is entirely absent.
- **Example**: No Problem Statement or no Core Feature List is provided.
- **Agent Behavior**:
  1. **HALT immediately.** Do not generate any SRS content.
  2. Generate a **Requirements Gathering Questionnaire** listing the missing mandatory data points.
  3. Present the questionnaire to the Human.

### 2.3 High-Volume TBD Threshold

- **Trigger**: The number of `[TBD]` markers in the current section exceeds **30%** of all data points in that section.
- **Example**: A section on "Payment Processing" has 8 requirements, and 3 or more have critical `[TBD]` gaps.
- **Agent Behavior**:
  1. Automatically switch to **Audit Mode** (per `02-Run Modes.md` §3.2).
  2. Generate a **Gap Report** listing all TBDs.
  3. **HALT** and present the Gap Report to the Human.

### 2.4 Destructive or Irreversible Action

- **Trigger**: The Agent is about to **overwrite** a section that has `APPROVED` status, or **delete** previously generated content.
- **Agent Behavior**:
  1. **HALT.** Never overwrite APPROVED content without explicit Human authorization.
  2. Present a summary of what will be changed and why.

### 2.5 Scope Ambiguity

- **Trigger**: The Human's instruction is ambiguous about scope (e.g., "Update the authentication section" — but multiple sections reference authentication).
- **Agent Behavior**:
  1. **HALT.** Present the ambiguity with specific options:
     ```
     [CLARIFICATION REQUIRED]
     Your instruction "Update the authentication section" could apply to:
       (A) §3.1 — User Authentication (Login/Signup flows)
       (B) §3.5 — API Authentication (Service-to-service tokens)
       (C) Both §3.1 and §3.5
     ► Which section(s) should I update?
     ```

---

## 3. Permitted Autonomous Decisions

The Agent **MAY** proceed without halting in the following situations. These are considered low-risk decisions within the Agent's competence.

| Situation | Agent Action | Condition |
|---|---|---|
| Minor `[TBD]` gap (e.g., specific color code, icon style) | Insert `[TBD: description]` and continue | TBD volume stays below 30% threshold. |
| Logical domain assumption (e.g., e-commerce → shopping cart) | Insert `[ASSUMPTION]` with reasoning and continue | Must be defensible per `04-Source Priority.md` Rule 3.3. |
| Cross-level source conflict (e.g., P1 vs P4) | Apply the higher-priority source | Must annotate the resolution with a `[CONFLICT]` marker and cite the priority rule. |
| Formatting corrections (e.g., fixing heading levels, standardizing ID formats) | Apply correction silently | Must not change the semantic content of any requirement. |
| Generating validation reports in Audit Mode | Generate and present report | Report does not modify the SRS. |

---

## 4. Escalation Format

When the Agent halts and presents a decision to the Human, it must use the following structured format for clarity and actionability:

```markdown
---
### 🛑 Agent Halt — [HALT TYPE]

**Context**: [Brief description of what the Agent was doing]
**Issue**: [Clear statement of the problem]

**Option A**: [First resolution option]
**Option B**: [Second resolution option]
**Option C**: [Third option, if applicable — or "Defer to stakeholder meeting"]

**Agent Recommendation**: [If the Agent has a defensible preference, state it with reasoning. Otherwise, state "No recommendation — this is a business decision."]

**Impact if Unresolved**: [What happens if this decision is delayed — e.g., "Section §3.2 cannot be completed. 4 downstream requirements are blocked."]
---
```

---

## 5. Post-Decision Protocol

After the Human provides a decision:

1. **Log the decision**: Record the Human's choice, the timestamp, and which options were presented.
2. **Update the SRS**: Apply the decision to the relevant section(s).
3. **Update markers**: Convert the `[CONFLICT]` or `[TBD]` marker to resolved status with an annotation citing the Human decision.
4. **Resume execution**: Return to the previous Run Mode and continue from the point of interruption.

---

## 6. The "Should I Ask?" Decision Flowchart

```
Agent is about to make a decision
  │
  ├─ Is the data point covered by a P1–P4 source?
  │    ├─ YES, one clear source → Proceed autonomously
  │    ├─ YES, but sources conflict at SAME level → HALT (§2.1)
  │    └─ YES, sources conflict at DIFFERENT levels → Proceed, apply higher source (§3)
  │
  ├─ Is the data point missing entirely?
  │    ├─ Mandatory Input? → HALT (§2.2)
  │    └─ Minor detail? → Insert [TBD], check threshold (§2.3)
  │
  ├─ Will this action overwrite APPROVED content?
  │    └─ YES → HALT (§2.4)
  │
  └─ Is the Human's instruction ambiguous?
       └─ YES → HALT and present options (§2.5)
```

---

## 7. Cross-Reference to Other Core Files

- **Priority rules for resolving conflicts** → `04-Source Priority.md`
- **Mandatory data requirements** → `01-Input Contract.md`
- **Automatic mode transitions on HALT** → `02-Run Modes.md` §3.2
- **Marker definitions** → `05-Output Rules.md` §5
