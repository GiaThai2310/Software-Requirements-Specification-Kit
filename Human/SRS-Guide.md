---
title: SRS Guide
aliases:
  - Software Requirements Specification Guide
tags:
  - srs
  - requirements-engineering
  - software-documentation
status: completed
template: "Context/SRS-Template.md"
overview: "Human/SRS-About.md"
---

# Software Requirements Specification Guide

This guide explains how to use the SRS kit. It is written for humans. The Agent's executable operating rules live in `Agent/`.

## 1. Reference Basis

The guide is based on widely used requirements engineering practices, including:

- ISO/IEC/IEEE 29148:2018 for requirements engineering and requirements specification structure.
- EARS for clear "shall" statements.
- MoSCoW prioritisation for priority labels.
- INCOSE-style quality characteristics such as necessary, unambiguous, complete, singular, feasible, verifiable, and traceable.

The kit is not a verbatim copy of any standard. It is a practical workflow derived from those references.

## 2. Recommended Workflow

1. Put client briefs, meeting notes, approved source documents, and project context in `Context/`.
2. Ask the Agent to run Draft / Outline Mode if the project is new.
3. Review and approve the outline direction.
4. Generate sections incrementally.
5. Review each generated section.
6. Use Change Request / Patch Mode for new information.
7. Run Audit / Validation Mode before baselining the SRS.

## 3. Required Inputs

A full SRS should not be generated until the project has:

- A problem statement or business objective.
- User classes or target audience.
- Core features or epics.

If these are missing, the Agent should ask requirements-gathering questions instead of writing a speculative SRS.

## 4. Project Scale

Use the output contract to tailor the document:

| Tier | Description |
|---|---|
| Tier 1 - Small | Small internal tool, MVP, or prototype. |
| Tier 2 - Medium | Product with integrations, several user classes, or multiple feature areas. |
| Tier 3 - Large | Compliance, many actors, many features, or multi-system integration. |

When uncertain, start with Tier 2 and trim after review.

## 5. Writing Requirements

Use EARS-style statements:

| Pattern | Example |
|---|---|
| Ubiquitous | The system shall retain audit logs for 365 days. |
| Event-driven | When the user submits valid credentials, the system shall create an authenticated session. |
| State-driven | While an account is locked, the system shall reject password login attempts. |
| Unwanted behavior | If payment authorization fails, then the system shall display the payment failure reason. |
| Optional feature | Where multi-factor authentication is enabled, the system shall require a verification code. |

Keep each requirement atomic. If a sentence contains two obligations, split it.

## 6. Priority

Use MoSCoW priorities:

| Priority | Meaning |
|---|---|
| Must | Required for the release or baseline. |
| Should | Important but not mandatory for the release. |
| Could | Desirable if capacity allows. |
| Won't | Explicitly excluded from the current scope. |

Priority is recorded in the requirement metadata, not by replacing `shall` with weaker verbs.

## 7. Status

Use only these statuses:

| Status | Meaning |
|---|---|
| DRAFT | Agent-created or revised, not yet submitted. |
| REVIEW | Ready for human review or awaiting decision. |
| APPROVED | Explicitly approved by a human. |
| DEPRECATED | Retained for history but no longer active. |

The Agent should not mark content as `APPROVED` unless the human explicitly instructs it to record approval.

## 8. ID Convention

Use:

```text
<TYPE>-<DOMAIN>-<NNN>
```

Examples:

- `FR-AUTH-001`
- `NFR-PERF-001`
- `UC-PAY-001`
- `BR-ORDER-001`
- `CR-GEN-001`

The domain should be stable. If a requirement starts as `FR-AUTH-001`, do not later rename it to `FR-LOGIN-001` unless a change decision explicitly changes the convention.

## 9. Traceability

Every requirement should answer:

- Where did it come from?
- Which feature, goal, or use case does it satisfy?
- How will it be verified?
- What other requirements depend on it?

Use Section 16 of the SRS or `Project/Traceability-Matrix.md` to maintain these links.

## 10. Handling Gaps And Conflicts

Use markers:

- `[TBD]` when required information is missing.
- `[ASSUMPTION]` when a defensible inference is made.
- `[CONFLICT]` when sources disagree.
- `[REVIEW]` when human attention is required.

Do not hide uncertainty. Visible uncertainty is safer than invented certainty.

## 11. Change Requests

For changes after drafting:

1. Log the change request.
2. Analyze impact.
3. Ask for human decision when approved content, scope, conflicts, or risk are affected.
4. Patch only affected sections.
5. Validate the patch.
6. Submit changed content for review.

Authorization to patch is not the same as final requirement approval.

## 12. Review Checklist

Before baselining an SRS, check that:

- Required sections are present for the project tier.
- Requirement IDs are unique and stable.
- Status labels use the canonical four-status model.
- Requirements are atomic and verifiable.
- Acceptance criteria exist for functional requirements.
- NFRs are measurable.
- Terms match the glossary.
- All `[TBD]`, `[ASSUMPTION]`, and `[CONFLICT]` markers are tracked.
- Traceability links are complete.
- The revision history is updated.

## 13. Where To Put Output

Generated SRS content, validation reports, traceability matrices, change request logs, and refactor logs should be written to `Project/`.

The `Agent/` and `Context/` directories are operating material. They should be changed only when maintaining the kit itself.
