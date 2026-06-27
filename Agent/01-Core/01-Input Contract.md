# 01 - Input Contract

## 1. Purpose

This file defines the contract between the human user, source documents, and the Agent. It specifies the minimum information required before SRS generation and the required behavior when information is missing, ambiguous, or incomplete.

The rules are based on common requirements engineering practice and on ISO/IEC/IEEE 29148 concepts: requirements must be based on stakeholder needs, have clear attributes, and remain traceable through the life cycle.

## 2. Mandatory Inputs

Before generating a full SRS, the Agent must verify that these inputs exist in `Context/`, `Project/`, or the current user prompt:

1. **Problem Statement or Business Objective**: Why the software is being built and what problem it solves.
2. **Target Audience or User Classes**: Who will use, operate, administer, or integrate with the system.
3. **Core Feature List or Epic List**: What the system is expected to do at a high level.

## 3. Valuable Optional Inputs

When available, the Agent should use these inputs to improve precision:

- Technical constraints such as platform, runtime, hosting, technology stack, security policies, or compliance obligations.
- Current workflow or manual process.
- Target workflow or future-state process.
- External systems, APIs, data sources, or hardware dependencies.
- Competitor systems, reference products, or inspiration systems.
- Known non-functional targets such as performance, availability, usability, security, privacy, accessibility, or maintainability.

## 4. Missing Data Protocol

### Rule 4.1 - Fatal Gap

If the Problem Statement or Core Feature List is entirely absent, the Agent must halt and must not generate SRS content. Instead, it must produce a Requirements Gathering Questionnaire.

### Rule 4.2 - Partial Gap

If minor details are missing, the Agent may continue only when the gap does not prevent a coherent requirement. The Agent must mark the missing item at the exact location using:

- `[TBD: description]` when the information is required but unknown.
- `[ASSUMPTION]` when the Agent makes a defensible inference from available sources.

### Rule 4.3 - No Domain Guessing

The Agent must not assume standard industry features unless they are logically implied by the provided source material. For example:

- Valid assumption: an e-commerce checkout implies a cart or order review step.
- Invalid assumption: an e-commerce checkout implies a blockchain ledger without source evidence.

## 5. Entry Checklist

Before writing, the Agent must answer:

| Check | Required Result |
|---|---|
| Problem statement exists | Yes |
| At least one user class exists | Yes |
| At least one core feature exists | Yes |
| Source priority can be determined | Yes |
| Target output location is `Project/` | Yes |

If any mandatory check fails, follow `06-Human Interaction Protocol.md`.
