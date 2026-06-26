# 02 — Run Modes

## 1. Purpose

This document defines the execution strategies (**Run Modes**) for the AI Agent when working on a Software Requirements Specification (SRS). Its primary objectives are to:

- Optimize the **Context Window** usage
- Prevent unnecessary token consumption and cost
- Avoid **hallucination** and generation of uncontrolled "walls of text"
- Prevent schema drift and loss of prior approved states

> [!IMPORTANT]
> The Agent is **strictly prohibited** from automatically regenerating the entire SRS document in any circumstance, unless explicitly operating in **Full Generation Mode** or when the target file is completely empty.

Before initiating any writing task, the Agent **MUST** assess the current project state and select the appropriate Run Mode — either by determining it autonomously or by asking the Human user for clarification.

---

## 2. Supported Run Modes

There are **5 execution modes**. The Agent must identify or confirm the active mode with the Human before beginning any work.

---

### Mode 1: Draft / Outline Mode

- **Trigger**: Start of a new project; the macro structure of the system has not yet been confirmed.
- **Objective**: Lock down the high-level architecture before any detailed analysis begins.
- **Agent Behavior**:
  1. Read `01-Input Contract.md` and `SRS-Template.md`.
  2. Generate only a **Table of Contents (TOC)** and a high-level **Executive Summary**.
  3. **Do NOT** write any detailed requirements at this stage.
  4. Halt and request **Human approval** (Human-in-the-loop checkpoint) before proceeding.

---

### Mode 2: Incremental Mode *(Default)*

- **Trigger**: The SRS already exists and work needs to proceed section by section; or the Human instructs the Agent to focus on a specific isolated feature (e.g., *"Only draft the User Authentication requirements"*).
- **Objective**: Concentrate LLM resources on one specific module at a time to achieve maximum analytical depth, based on the *Incremental Generation with Verification* pattern.
- **Agent Behavior**:
  1. Focus exclusively on **one specific section** of the SRS (e.g., only User Roles, or only the API Authentication flow).
  2. Isolate the context — retrieve only source documents relevant to the specified section and write output exclusively within that section's boundary.
  3. Apply micro-validation rules from `04-Micro Validation.md` immediately upon completing that section.
  4. Halt and **await Human review** before moving on to the next section or module.
- **Constraint**: Do not attempt to output the complete SRS in a single generation block. Use tool calls to incrementally build the output structure to avoid all-or-nothing failures and context limit breaches.

---

### Mode 3: Audit / Validation Mode

- **Trigger**: A draft section has been generated, or the Agent is executing `04-Micro Validation.md` / `05-Macro Validation.md`.
- **Objective**: Inspect the quality of and identify gaps in the existing SRS document **without modifying the source**, analogous to the concept of *Verifiable Rewards* in Agent training.
- **Agent Behavior**:
  1. Activate **Read-Only** state — no writes to the SRS file.
  2. Load the existing SRS content and cross-reference it against the Input Contract.
  3. Apply the "Reflection Pattern" — the Agent enters a self-review loop, evaluating its own output against formatting rules and domain constraints.
  4. Run all checks defined in `05-Macro Validation.md`.
  5. Output an **Issue List**, **Gap Analysis**, or **Traceability Report**.
- **Constraint**: Do **not** directly modify the SRS file. Do **not** introduce new business requirements during this mode. Focus solely on resolving `[CONFLICT]` flags, clarifying `[ASSUMPTION]` tags, and improving syntactic quality.

---

### Mode 4: Change Request / Patch Mode

- **Trigger**: New information is introduced via Change Requests (CR), new Meeting Notes, or revised Input Contracts.
- **Objective**: Handle change requests in a targeted, localized manner — avoid regenerating the entire document.
- **Agent Behavior**:
  1. Receive a **Change Request** from the Human.
  2. Reference `08-Traceability Workflow.md` to identify which Requirement IDs are **directly and indirectly** affected by the CR.
  3. Generate a **patch draft** — modified content only for the impacted items — and submit it to the Human for review.
- **Constraint**: Treat the SRS as a **"Living Spec"**. The Agent is strictly prohibited from modifying sections of the document that are not explicitly impacted by the incoming change context.

---

### Mode 5: Full Generation Mode

- **Trigger** *(Restricted)*: Activated **only** when:
  1. The project is in its initial kick-off phase and the target `SRS-Template.md` is completely empty, **OR**
  2. The Input Contract is extremely small (within the permitted token budget), **OR**
  3. There is an **explicit override command** from the Human (e.g., *"Generate the entire SRS"*).
- **Objective**: Generate the complete SRS document from start to finish in a single, sequential pipeline run.
- **Agent Behavior**:
  1. Apply the **Planning Pattern (Plan-Act)** — decompose SRS creation into sequential tasks and generate the document section by section.
  2. Run all pipelines sequentially: from analysis through to final validation.
- **Constraint**: Do not attempt to output the full SRS in one generation block. Build the output structure incrementally via tool calls to prevent context limit failures.

---

## 3. State Management & Transition Rules

### 3.1 Pre-Execution Assessment Protocol

1. **Assess State First**: The Agent must read the target output file and the change request *before* selecting a Run Mode.
2. **Bidirectional Sync**: Treat finalized implementation metrics and operational learnings as a feedback loop to continuously refine the spec.

### 3.2 Automatic Mode Transitions

| Condition | Automatic Action |
|---|---|
| Logic conflict (`[CONFLICT]`) detected | Switch to **Mode 3 (Audit Mode)** — enumerate all errors and halt execution, deferring all decisions to the Human. |
| Excessive missing data (`[TBD]` volume too high) | Switch to **Mode 3 (Audit Mode)** — produce a gap report and await Human clarification before resuming. |

> [!WARNING]
> When the Agent automatically transitions to Audit Mode, it **must not** attempt to resolve conflicts or fill in missing data autonomously. All resolution authority belongs to the Human.