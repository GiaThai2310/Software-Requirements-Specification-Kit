# 03 - Context Rules

## 1. Purpose

This document governs how the Agent reads, summarizes, and refreshes documents during SRS work. Context is a limited resource. Loading irrelevant material increases the risk of omissions, stale reasoning, and accidental instruction drift.

## 2. Bootstrap Reading Order

When initializing a session or starting a major SRS task, read files in this order:

| Step | File | Action |
|---:|---|---|
| 1 | `Agent/AGENTS.md` | Read in full. |
| 2 | `Agent/01-Core/01-Input Contract.md` | Read in full. |
| 3 | `Agent/01-Core/02-Run Modes.md` | Read in full. |
| 4 | `Agent/01-Core/03-Context Rules.md` | Read in full. |
| 5 | `Agent/01-Core/04-Source Priority.md` | Read in full. |
| 6 | `Agent/01-Core/05-Output Rules.md` | Read in full. |
| 7 | `Agent/01-Core/06-Human Interaction Protocol.md` | Read in full. |
| 8 | `Agent/01-Core/07-Terminology-Glossary Handling.md` | Read in full. |
| 9 | `Context/SRS-TOC.md` | Read in full. |
| 10 | `Context/SRS-Template.md` | Read in full or read the relevant section by mode. |
| 11 | `Agent/02-SRS/*` | Read only the workflow needed for the active mode. |

## 3. Read Versus Summarize

| Condition | Action |
|---|---|
| Core instruction file | Read in full. |
| SRS template in Draft or Full Generation Mode | Read in full. |
| SRS template in Incremental Mode | Read the target section and shared conventions. |
| Large client source document | Summarize first, then re-read relevant passages before writing. |
| Existing `Project/` SRS output | Read the target section in full before editing. |

## 4. Required Summary Format

When summarizing a source document, use this structure:

```markdown
## Summary Of: [Document Name]

- **Key Decisions**:
- **Stated Requirements**:
- **Constraints / Restrictions**:
- **Open Questions / Ambiguities**:
- **Conflicts Detected**:
```

Summaries support triage only. The Agent must re-read relevant source content before writing or modifying requirements.

## 5. When To Re-Read

The Agent must re-read source content when:

- It is about to write or modify a section that depends on that source.
- A `[CONFLICT]` marker involves that source.
- A change request references that source.
- A previous summary is more than two task cycles old.
- The user challenges or updates the meaning of a previous source.

## 6. Files To Avoid During Normal SRS Generation

| Path | Rule |
|---|---|
| `Human/*` | Do not read unless the user asks to maintain or audit the kit. |
| `.git/*` | Do not read for requirements analysis. |
| Unlisted files outside `Agent/`, `Context/`, and `Project/` | Do not read unless the user explicitly references them. |

## 7. Context Budget Guidance

Use the context window deliberately:

| Zone | Approximate Allocation |
|---|---:|
| Operating instructions | 15-20 percent |
| Source data | 40-50 percent |
| Reasoning and validation | 20-30 percent |
| Output buffer | 10-15 percent |

If context becomes saturated, summarize completed material and re-read only the specific source passages needed for the next write.
