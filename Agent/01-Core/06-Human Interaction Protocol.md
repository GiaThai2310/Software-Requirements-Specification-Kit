# 06 - Human Interaction Protocol

## 1. Purpose

This document defines when, why, and how the Agent must pause autonomous execution and defer a decision to the human user. The Agent should not halt for trivial details, but it must never silently resolve decisions that carry approval, scope, legal, security, or business risk.

## 2. Mandatory Halt Conditions

The Agent must halt in these situations.

### 2.1 Same-Priority Source Conflict

**Trigger**: Two or more sources at the same priority level contradict each other.

**Required behavior**:

1. Insert `[CONFLICT]` at the affected output location.
2. Document both positions with exact source references.
3. Halt and ask the human to choose or provide a combined resolution.

### 2.2 Fatal Data Gap

**Trigger**: A mandatory input from `01-Input Contract.md` is absent.

**Required behavior**:

1. Do not generate SRS content.
2. Produce a Requirements Gathering Questionnaire.
3. Halt until the human provides the missing context.

### 2.3 High TBD Density

**Trigger**: More than 30 percent of the meaningful data points in a section would require `[TBD]`.

**Required behavior**:

1. Switch to Audit / Validation Mode.
2. Produce a Gap Report.
3. Halt until the human provides clarification.

### 2.4 Approved Content Change

**Trigger**: The Agent is about to modify content with `APPROVED` status.

**Required behavior**:

1. Halt before editing.
2. Present the proposed change and impact.
3. Require explicit human authorization or an approved change request.

### 2.5 Deletion Or Deprecation

**Trigger**: The Agent is about to delete, remove, or deprecate existing SRS content.

**Required behavior**:

1. Do not delete approved or historical requirements.
2. Use `DEPRECATED` only after human instruction or an approved change request.
3. Retain audit annotations.

### 2.6 Scope Ambiguity

**Trigger**: The user instruction can reasonably affect multiple sections or modules.

**Required behavior**:

1. Identify the ambiguous scope.
2. Present specific options.
3. Halt until the user confirms the intended scope.

## 3. Permitted Autonomous Decisions

The Agent may proceed without halting for low-risk decisions:

| Situation | Agent Action |
|---|---|
| Minor missing detail | Insert `[TBD: description]` and continue if under the TBD threshold. |
| Defensible domain inference | Insert `[ASSUMPTION]` with reasoning. |
| Cross-priority conflict | Apply the higher-priority source and annotate `[CONFLICT]`. |
| Formatting correction | Correct format without changing meaning. |
| Validation report generation | Generate a report in `Project/` without modifying the SRS. |

## 4. Escalation Format

When halting, use this structure:

```markdown
---
### Agent Halt - [HALT TYPE]

**Context**: [What the Agent was doing]
**Issue**: [Clear statement of the problem]

**Option A**: [Resolution option]
**Option B**: [Resolution option]
**Option C**: [Optional deferral or combined option]

**Agent Recommendation**: [Recommendation with reasoning, or "No recommendation; this is a business decision."]

**Impact If Unresolved**: [Blocked sections, requirements, or risks]
---
```

## 5. Post-Decision Protocol

After the human provides a decision:

1. Record the decision in the SRS Decisions table or in the relevant change request log.
2. Cite the human decision as a P1 source.
3. Apply the decision only to affected sections.
4. Update markers from `[TBD]` or `[CONFLICT]` to resolved annotations where appropriate.
5. Set affected Agent-edited items to `REVIEW` unless the human explicitly instructs the Agent to record `APPROVED`.

## 6. Approval Rule

The Agent may record `APPROVED` only when the human explicitly approves and instructs the Agent to record that approval. A statement such as "looks good" may be treated as review feedback, but not as formal approval unless the user clearly asks to approve or mark approved.

## 7. Decision Flow

```text
Agent is about to decide:
  Covered by one clear P1-P4 source?       -> Proceed.
  Same-level source conflict?              -> Halt.
  Missing mandatory input?                 -> Halt.
  Minor missing detail?                    -> Mark TBD and continue if below threshold.
  Would modify APPROVED content?           -> Halt.
  Would set APPROVED status?               -> Halt unless human explicitly instructed approval recording.
  Ambiguous user scope?                    -> Halt.
```

## 8. Cross-References

- Source priority: `04-Source Priority.md`
- Input contract: `01-Input Contract.md`
- Run modes: `02-Run Modes.md`
- Output rules: `05-Output Rules.md`
