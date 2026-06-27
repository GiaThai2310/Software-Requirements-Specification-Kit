# 04 - Micro Validation

## 1. Purpose

Micro Validation checks each individual requirement immediately after writing or modifying it. A requirement that fails a critical check must be rewritten before delivery.

## 2. Quality Characteristics

| ID | Characteristic | Check | Severity |
|---|---|---|---|
| C1 | Necessary | Does the requirement define a real need? | Critical |
| C2 | Unambiguous | Does it have one clear interpretation? | Critical |
| C3 | Complete | Is enough information present to implement and test it? | Critical |
| C4 | Atomic | Does it express one obligation? | Critical |
| C5 | Verifiable | Can it be checked by test, analysis, inspection, or demonstration? | Critical |
| C6 | Feasible | Is it achievable within known constraints? | Warning |
| C7 | Correct | Does it match the source? | Critical |
| C8 | Conforming | Does it follow format, status, and ID rules? | Warning |
| C9 | Appropriate | Is it at the right abstraction level? | Warning |

## 3. EARS Syntax Checks

| Check | Rule | Severity |
|---|---|---|
| Uses `shall` | Requirement body uses exactly one mandatory `shall` for one obligation. | Critical |
| Has explicit subject | The system or actor performing the action is named. | Critical |
| Matches EARS | Uses a valid EARS pattern or simple valid variant. | Warning |
| No dangling clauses | Every `when`, `if`, `while`, or `where` clause is complete. | Critical |
| No excessive nesting | More than three clauses requires decomposition. | Warning |

## 4. Linguistic Checks

Check for:

- Forbidden vague terms from `03-Requirement Writing Rules.md`.
- Passive voice that hides responsibility.
- Vague quantifiers such as `some`, `many`, `usually`, or `normally`.
- Open-ended lists such as `etc.`.
- Undefined pronouns.
- Ambiguous timing.
- Double negatives.

## 5. Structural Checks

| ID | Check | Rule | Severity |
|---|---|---|---|
| S1 | ID | Uses `<TYPE>-<DOMAIN>-<NNN>`. | Critical |
| S2 | Status | Uses `DRAFT`, `REVIEW`, `APPROVED`, or `DEPRECATED`. | Critical |
| S3 | Source | Has a backward source trace. | Critical |
| S4 | Acceptance criteria | Functional requirements have at least one criterion. | Critical |
| S5 | Priority | Has MoSCoW priority. | Warning |
| S6 | Rationale | Explains why the requirement exists. | Warning |
| S7 | Dependencies | Lists related IDs or `None`. | Warning |

## 6. Failure Handling

For each failed check:

1. Add `[REVIEW]` only when human attention is needed.
2. Rewrite critical failures before delivery.
3. Keep warnings visible in notes or validation reports.
4. Do not convert any item to `APPROVED`.

Example:

```markdown
> [REVIEW] Micro Validation: C4 Atomicity failed. This statement includes validation and notification; split into two requirements.
```

## 7. Cross-References

- Requirement writing rules: `Agent/02-SRS/03-Requirement Writing Rules.md`
- Output rules: `Agent/01-Core/05-Output Rules.md`
- Macro validation: `Agent/02-SRS/05-Macro Validation.md`
