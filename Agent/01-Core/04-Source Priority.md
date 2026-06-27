# 04 - Source Priority

## 1. Purpose

This file defines the hierarchy of truth used when sources conflict. The Agent must not silently choose a convenient interpretation. Conflict handling must be deterministic, documented, and traceable.

## 2. Priority Hierarchy

When two or more sources conflict, apply the highest available priority:

| Priority | Source Type | Description |
|---:|---|---|
| P1 | Current Client Decision | A direct instruction from the user in the current session. |
| P2 | Approved Document | A formally approved SRS, BRD, contract, security policy, or signed decision record. |
| P3 | Meeting Notes / Workshop Records | Documented stakeholder discussion, decisions, and action items. |
| P4 | Legacy Document | Old, inherited, superseded, or explicitly unapproved material. |
| P5 | Agent Assumption | A defensible inference used only when no higher-priority source covers the point. |

## 3. Resolution Rules

### Rule 3.1 - Higher Source Wins

If sources conflict at different priority levels, the higher-priority source wins. The Agent must:

1. Apply the higher-priority source.
2. Insert `[CONFLICT]` at the affected output location.
3. Add a concise annotation stating which sources conflicted, which source won, and why.

Example:

```markdown
[CONFLICT] P2 Approved BRD states "SAML 2.0 only"; P4 Legacy SRS states "LDAP and Basic Auth". Resolved in favor of P2 by Source Priority Rule 3.1.
```

### Rule 3.2 - Same-Level Conflict Requires Human Decision

If conflicting sources have the same priority level, the Agent must not resolve the conflict. The Agent must:

1. Mark the issue with `[CONFLICT]`.
2. Document both positions and their sources.
3. Halt using `06-Human Interaction Protocol.md`.

### Rule 3.3 - Assumption Governance

The Agent may use `[ASSUMPTION]` only when:

1. No P1-P4 source addresses the data point.
2. The inference is directly supported by the project domain or stated feature set.
3. The reasoning is written next to the assumption.

Assumptions never override P1-P4 sources.

### Rule 3.4 - Recency Within Same Source Type

If two sources have the same priority and same source type, use the most recent source when timestamps or version numbers are available. If recency cannot be determined, halt and ask the human.

## 4. Quick Reference

```text
Conflict detected?
  Different priority levels -> apply higher source, mark [CONFLICT].
  Same priority level       -> mark [CONFLICT], halt for human decision.
  No source covers it       -> use [ASSUMPTION] only if defensible.
```

## 5. Out Of Scope

This file defines priority rules only. Procedures live in:

- `Agent/02-SRS/06-Change Request Workflow.md`
- `Agent/02-SRS/07-Traceability Workflow.md`
- `Agent/01-Core/06-Human Interaction Protocol.md`
