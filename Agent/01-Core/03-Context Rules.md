# 03 — Context Rules

## 1. Purpose

This document governs **how the Agent reads, prioritizes, and manages documents** within its context window during SRS generation. Improper context loading leads to token waste, the "Lost in the Middle" effect (where LLMs ignore information placed in the middle of long inputs), and hallucination from stale or irrelevant data.

> [!IMPORTANT]
> The Agent must treat its context window as a **finite budget**. Every file loaded consumes tokens. Loading irrelevant files directly competes with the space available for reasoning and output generation.

---

## 2. Document Reading Order (Bootstrap Sequence)

When initializing a session or beginning a new Run Mode, the Agent must load files in the following **strict order**. This order is designed to place the most critical behavioral constraints at the boundaries of the context (beginning and end) where LLM attention is highest.

| Step | File | Action | Rationale |
|------|------|--------|-----------|
| 1 | `Agent/01-Core/01-Input Contract.md` | **READ in full** | Establishes what data is mandatory before any work begins. |
| 2 | `Agent/01-Core/02-Run Modes.md` | **READ in full** | Determines the execution strategy for the current session. |
| 3 | `Agent/01-Core/03-Context Rules.md` | **READ in full** | This file. Governs all subsequent reading behavior. |
| 4 | `Agent/01-Core/04-Source Priority.md` | **READ in full** | Establishes the hierarchy of truth for conflict resolution. |
| 5 | `Agent/01-Core/05-Output Rules.md` | **READ in full** | Defines formatting, markers, and output targets. |
| 6 | `Agent/01-Core/06-Human Interaction Protocol.md` | **READ in full** | Defines when to halt and escalate to the Human. |
| 7 | `Agent/01-Core/07-Terminology-Glossary Handling.md` | **READ in full** | Governs term extraction and glossary consistency. |
| 8 | `Context/SRS-TOC.md` | **READ in full** | Provides the structural skeleton for the SRS output. |
| 9 | `Context/SRS-Template.md` | **READ or SUMMARIZE** | See §3 for summarization rules. |
| 10 | `Agent/02-SRS/*` (workflow files) | **READ on demand** | Load only the specific workflow file relevant to the active Run Mode. |

---

## 3. READ vs. SUMMARIZE Decision Matrix

Not all documents need to be loaded verbatim. The Agent must apply the following rules to decide whether to **read in full** or **summarize** a document.

### 3.1 Rules

| Condition | Action | Rationale |
|-----------|--------|-----------|
| File is an `Agent/01-Core/*` instruction file | **Always READ in full** | These are behavioral constraints. Summarization risks losing critical rules. |
| File is `Context/SRS-Template.md` and Run Mode is **Full Generation** or **Draft/Outline** | **READ in full** | The Agent needs the complete template structure. |
| File is `Context/SRS-Template.md` and Run Mode is **Incremental** | **READ only the target section** | Extract only the section boundaries relevant to the current task. Skip all other sections. |
| File is a client-provided document (meeting notes, briefs) | **SUMMARIZE first, then re-read on demand** | Client documents are often verbose. Extract key decisions, requirements, and constraints first. |
| File is in `Project/` (previously generated SRS output) | **READ the target section in full** | The Agent must verify the current state of the section it is about to modify. |

### 3.2 Summarization Protocol

When summarizing a document, the Agent must produce a structured extraction — not a free-form paragraph. Use this format:

```
## Summary of: [Document Name]
- **Key Decisions**: [Bulleted list]
- **Stated Requirements**: [Bulleted list]
- **Constraints / Restrictions**: [Bulleted list]
- **Open Questions / Ambiguities**: [Bulleted list with [TBD] markers]
- **Conflicts Detected**: [Bulleted list with [CONFLICT] markers, if any]
```

---

## 4. When to RE-READ a Document

The Agent must **re-read** (reload the full content of) a document under the following conditions:

| Trigger | Action |
|---------|--------|
| The Agent is about to **write or modify** a section that references a specific source document | Re-read that source document in full to ensure accuracy. |
| A `[CONFLICT]` marker has been flagged between two sources | Re-read **both** conflicting sources in full before escalating to the Human. |
| The Human provides a **Change Request** that references a specific document | Re-read the referenced document to verify the CR's scope and impact. |
| The Agent's previous summary is **more than 2 task cycles old** in the current session | Re-read to refresh stale context and prevent drift. |

> [!WARNING]
> The Agent must **never** rely solely on a summary when making a write decision. If a summary was used for initial triage, the Agent must re-read the relevant sections of the source document before generating output.

---

## 5. Files the Agent Must NEVER Read

The following directories and files are **off-limits** to the Agent. Loading them wastes context and risks instruction pollution.

| Path | Reason |
|------|--------|
| `Human/*` | Contains human-facing onboarding materials and tutorials. Not relevant to Agent operations. Explicitly prohibited in `AGENTS.md`. |
| `.git/*` | Version control metadata. No analytical value. |
| Any file not listed in the `Context/` or `Agent/` directories | The Agent must not speculatively load files outside its designated workspace. |

---

## 6. Context Window Budget Allocation

The Agent should mentally partition its context window into the following zones:

| Zone | Approximate Allocation | Contents |
|------|----------------------|----------|
| **System Instructions** | ~15–20% | All `Agent/01-Core/*` files (behavioral rules). |
| **Source Data** | ~40–50% | Client documents, `Context/` files, and relevant `Project/` sections. |
| **Working Memory** | ~20–30% | Intermediate reasoning, draft output, validation results. |
| **Output Buffer** | ~10–15% | The final generated text for the current task. |

> [!TIP]
> If the Agent detects that its context is becoming saturated (e.g., multiple large client documents loaded simultaneously), it should **offload** completed sections by summarizing them and retaining only the summary, freeing space for the next task.

---

## 7. Cross-Reference to Other Core Files

- **Reading order enforcement** → `AGENTS.md` §3 (Execution Sequence)
- **What to do when data is missing** → `01-Input Contract.md` §5
- **Which source wins in a conflict** → `04-Source Priority.md`
- **Where and how to write output** → `05-Output Rules.md`
- **When to stop and ask the Human** → `06-Human Interaction Protocol.md`
