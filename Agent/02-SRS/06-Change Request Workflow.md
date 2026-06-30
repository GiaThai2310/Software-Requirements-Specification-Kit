# 06 - Change Request Workflow

## 1. Purpose

This document defines how the Agent handles change requests without regenerating the full SRS. Every change must be logged, analyzed, approved by the human when required, patched narrowly, validated, and closed.

## 2. Lifecycle

```text
RECEIVED -> ANALYZING -> AWAITING_DECISION -> AUTHORIZED -> APPLYING -> APPLIED -> REVIEW -> CLOSED
                                      -> REJECTED
                                      -> DEFERRED
```

`AUTHORIZED` means the human allowed the Agent to apply a patch. It is not the same as requirement approval.

## 3. Step 1 - Receive And Log

Assign a CR ID using the canonical ID pattern:

```text
CR-GEN-001
```

Log:

```markdown
| Field | Value |
|---|---|
| CR-ID | CR-GEN-001 |
| Date Received | YYYY-MM-DD |
| Source | Direct Prompt / Meeting Notes / Updated Document |
| Description | [Brief change description] |
| Priority | P1-Critical / P2-High / P3-Medium / P4-Low |
| Status | RECEIVED |
```

## 4. Step 2 - Impact Analysis

Before patching, the Agent must:

1. Re-read the source material referenced by the CR.
2. Consult the SRS traceability matrix or dependency records.
3. Identify directly affected requirements.
4. Identify indirectly affected requirements.
5. Check for conflicts with approved or review-bound content.
6. Identify validation checks required after the patch.

Impact report format:

```markdown
## Impact Analysis - CR-GEN-001

### Change Description
[What is changing and why]

### Directly Affected Items

| ID | Section | Current State | Required Change |
|---|---|---|---|

### Indirectly Affected Items

| ID | Section | Relationship | Potential Impact |
|---|---|---|---|

### Conflict Assessment
[CONFLICT findings or "None"]

### Risk Assessment

| Risk | Likelihood | Impact |
|---|---|---|
```

## 5. Step 3 - Human Decision

The Agent must halt after impact analysis when:

- Approved content is affected.
- Scope is ambiguous.
- Same-priority sources conflict.
- The CR would deprecate content.
- The change has material business, legal, security, or architectural impact.

The human may authorize, modify, reject, or defer the CR.

## 6. Step 4 - Apply Patch

After authorization, the Agent must:

1. Modify only affected items.
2. Set changed Agent-authored items to `REVIEW`.
3. Add a change annotation:

```markdown
> [CHANGE] Changed by CR-GEN-001 (YYYY-MM-DD): [Brief description].
```

4. Retain deprecated requirements with `DEPRECATED` status and a replacement reference when applicable.
5. Assign new IDs using `<TYPE>-<DOMAIN>-<NNN>`.

## 7. Step 5 - Validate Patch

Run:

- Micro Validation on all changed requirements.
- Traceability checks for changed links.
- Consistency checks for affected sections.
- Status checks to ensure the Agent did not set `APPROVED`.

## 8. Step 6 - Close Or Submit For Review

After patching:

1. Update CR status to `APPLIED`.
2. Update revision history.
3. Present summary to the human.
4. Keep affected requirements in `REVIEW`.
5. Record `APPROVED` only if the human explicitly instructs the Agent to record approval.

## 9. Cross-References

- Source priority: `Agent/01-Core/04-Source Priority.md`
- Human interaction: `Agent/01-Core/06-Human Interaction Protocol.md`
- Micro validation: `Agent/02-SRS/04-Micro Validation.md`
- Macro validation: `Agent/02-SRS/05-Macro Validation.md`
- Traceability: `Agent/02-SRS/07-Traceability Workflow.md`
