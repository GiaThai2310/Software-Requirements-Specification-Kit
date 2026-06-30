# 01 - Analysis Workflow

## 1. Purpose

This document defines the standard workflow for analyzing source material and generating SRS content. It connects the core rules into an operational pipeline.

## 2. Workflow Overview

```text
INGEST -> ANALYZE -> STRUCTURE -> WRITE -> VALIDATE -> DELIVER
```

## 3. Phase 1 - Ingest

**Objective**: Load only the context needed for the current task.

| Step | Action |
|---:|---|
| 1.1 | Read the core files in the sequence defined by `AGENTS.md`. |
| 1.2 | Read `Context/SRS-TOC.md`. |
| 1.3 | Read all or part of `Context/SRS-Template.md` based on Run Mode. |
| 1.4 | Read or summarize source documents using `03-Context Rules.md`. |
| 1.5 | Read existing relevant output in `Project/`. |

**Exit criteria**: The Agent understands available data, missing data, existing output state, and the active Run Mode.

## 4. Phase 2 - Analyze

**Objective**: Extract requirements, terms, actors, rules, conflicts, and gaps.

| Step | Action |
|---:|---|
| 2.1 | Validate mandatory inputs. Halt if the fatal gap rule applies. |
| 2.2 | Extract terminology and build a glossary draft. |
| 2.3 | Identify stakeholders, actors, and external systems. |
| 2.4 | Extract business rules, constraints, data needs, conceptual entities, attributes, relationships, ownership, and non-functional targets. |
| 2.5 | Detect conflicts using `04-Source Priority.md`. |
| 2.6 | Mark gaps with `[TBD]` or `[ASSUMPTION]`. |
| 2.7 | Check TBD density and halt if it exceeds the threshold. |

**Exit criteria**: Requirements and gaps are structured enough to map into the SRS.

## 5. Phase 3 - Structure

**Objective**: Map extracted content to the SRS template.

| Step | Action |
|---:|---|
| 3.1 | Map each feature, rule, data artifact, and requirement to `Context/SRS-TOC.md`. |
| 3.2 | Assign IDs using `<TYPE>-<DOMAIN>-<NNN>`. |
| 3.3 | Build backward and forward traceability links for requirements and data artifacts. |
| 3.4 | In Draft / Outline Mode, generate only outline content and halt. |

**Exit criteria**: Each candidate requirement has an ID, section assignment, source trace, and verification direction.

## 6. Phase 4 - Write

**Objective**: Generate SRS content section by section.

| Step | Action |
|---:|---|
| 4.1 | Select the target section based on Run Mode. |
| 4.2 | Re-read source documents relevant to the section. |
| 4.3 | Write requirements using EARS syntax from `03-Requirement Writing Rules.md`. |
| 4.4 | Apply output format, markers, status labels, and traceability. |
| 4.5 | Set newly generated content to `DRAFT`. |
| 4.6 | Write only to `Project/`. |

**Exit criteria**: The target section is drafted with valid IDs, sources, statuses, and acceptance criteria.

## 7. Phase 5 - Validate

**Objective**: Verify local and global quality.

| Step | Action |
|---:|---|
| 5.1 | Run Micro Validation on every new or modified requirement. |
| 5.2 | Run relevant Macro Validation checks when a major section or draft is complete. |
| 5.3 | Fix formatting, atomicity, and clarity issues. |
| 5.4 | Do not resolve same-priority `[CONFLICT]` markers autonomously. |
| 5.5 | Update TBD and traceability records. |

**Exit criteria**: Critical validation issues are fixed or escalated.

## 8. Phase 6 - Deliver

**Objective**: Submit completed work for human review.

| Step | Action |
|---:|---|
| 6.1 | Set completed Agent-authored sections to `REVIEW`. |
| 6.2 | Summarize generated content, assumptions, conflicts, and TBDs. |
| 6.3 | Halt for human feedback in Incremental Mode. |
| 6.4 | Record human decisions as P1 source material. |
| 6.5 | Do not record `APPROVED` unless the human explicitly instructs approval recording. |

**Exit criteria**: The human has a clear review package and any unresolved issues are visible.

## 9. Cross-References

- Input contract: `Agent/01-Core/01-Input Contract.md`
- Run modes: `Agent/01-Core/02-Run Modes.md`
- Source priority: `Agent/01-Core/04-Source Priority.md`
- Output rules: `Agent/01-Core/05-Output Rules.md`
- Requirement writing: `Agent/02-SRS/03-Requirement Writing Rules.md`
- Traceability: `Agent/02-SRS/07-Traceability Workflow.md`
