---
title: "<Project Name> - Software Requirements Specification"
aliases:
  - "<Project Name> SRS"
document_type: srs
srs_schema_version: "1.0"
project: "<Project Name>"
version: "0.1"
status: Draft
authors:
  - "<Author>"
reviewers: []
approvers: []
created: YYYY-MM-DD
last_updated: YYYY-MM-DD
tags:
  - srs
  - requirements
---

# Software Requirements Specification

> [!important] Template usage
> - Thay toàn bộ nội dung trong dấu `<...>`.
> - Giữ nguyên ID sau khi đã được sử dụng hoặc tham chiếu.
> - Với mục không áp dụng, ghi `Not Applicable` và nêu lý do trước khi loại khỏi bản cuối.
> - Không điền thông tin chưa được xác nhận như một sự thật. Dùng `[TBD]` hoặc `[ASSUMPTION]` khi cần.
> - Hướng dẫn chi tiết cho từng phần được trình bày tại [SRS-Guide].
> - Kiến thức nền tảng được trình bày tại [SRS-About].

---

# 0. Document Control

## 0.1 Document Information

| Field | Value |
|---|---|
| Project Name | `<Project Name>` |
| Software/System Name | `<Software or System Name>` |
| Document Name | Software Requirements Specification |
| Document ID | `<Document ID>` |
| Version | `0.1` |
| Status | `Draft` |
| Author | `<Author>` |
| Reviewer | `<Reviewer or Review Group>` |
| Approver | `<Approver>` |
| Created Date | `YYYY-MM-DD` |
| Last Updated | `YYYY-MM-DD` |

---

## 0.2 Revision History

| Version | Date | Author | Changed Sections | Change Description | Status |
|---|---|---|---|---|---|
| 0.1 | `YYYY-MM-DD` | `<Author>` | Initial document | Initial draft | Draft |

---

## 0.3 Review and Approval

| Role | Name | Review Status | Review Date | Comments |
|---|---|---|---|---|
| Author | `<Name>` | Drafted | `YYYY-MM-DD` | |
| Reviewer | `<Name or Group>` | Pending | | |
| Approver | `<Name or Role>` | Pending | | |

---

# 1. Introduction

## 1.1 Purpose

`<Mô tả mục đích của tài liệu, phần mềm được đặc tả, phiên bản áp dụng và cách tài liệu được sử dụng.>`

---

## 1.2 Scope

`<Mô tả ngắn gọn hệ thống, mục tiêu tổng quát và ranh giới của phiên bản đang được đặc tả.>`

### 1.2.1 In Scope

- `<Capability, process, data scope or integration included in the project>`
- `<Item>`

### 1.2.2 Out of Scope

- `<Capability, process, data scope or integration excluded from the project>`
- `<Item>`

### 1.2.3 Future Scope

<!-- Chỉ giữ mục này khi cần phân biệt phạm vi hiện tại với định hướng tương lai. -->

- `<Potential future capability that is not part of the current commitment>`

---

## 1.3 Intended Audience

| Audience | Purpose of Reading | Relevant Sections |
|---|---|---|
| `<Audience or Role>` | `<How this audience uses the SRS>` | `<Sections>` |

---

## 1.4 Definitions, Acronyms and Abbreviations

| Term | Type | Definition | Source or Notes |
|---|---|---|---|
| `<Term>` | Term / Acronym / Abbreviation | `<Definition>` | `<Source or context>` |

---

## 1.5 References

| Reference ID | Document or Source | Version/Date | Owner | Location | Relevant Content |
|---|---|---|---|---|---|
| REF-001 | `<Reference Name>` | `<Version or Date>` | `<Owner>` | `<Link or Path>` | `<Relevant sections>` |

---

## 1.6 Document Overview

`<Tóm tắt cấu trúc và nội dung chính của tài liệu.>`

---

# 2. Overall Description

## 2.1 Product Perspective

`<Mô tả vị trí của hệ thống trong môi trường vận hành, ranh giới trách nhiệm và quan hệ với các hệ thống hoặc quy trình khác.>`

### 2.1.1 System Boundary

`<Mô tả phần nằm trong hệ thống và phần thuộc môi trường bên ngoài.>`

### 2.1.2 Context Diagram

---

## 2.2 Product Functions

| Function Group ID | Function Group | Description | Related Features |
|---|---|---|---|
| PF-001 | `<Function Group>` | `<High-level capability>` | `<Feature IDs>` |

---

## 2.3 User Classes and Characteristics

| User Class ID | User Class | Goals | Responsibilities | Technical Experience | Usage Frequency | Restrictions |
|---|---|---|---|---|---|---|
| USR-001 | `<User Class>` | `<Goals>` | `<Responsibilities>` | `<Experience>` | `<Frequency>` | `<Restrictions>` |

---

## 2.4 Operating Environment

| Category | Requirement or Environment |
|---|---|
| Application Type | `<Web, mobile, desktop, service or other>` |
| Client Environment | `<Supported client environment>` |
| Server Environment | `<Required server environment>` |
| Network Environment | `<Network and connectivity requirements>` |
| Runtime Environment | `<Required runtime environment>` |
| Data Platform | `<Required data platform if constrained>` |
| Other | `<Other environmental requirements>` |

---

## 2.5 Design and Implementation Constraints

| Constraint ID | Constraint | Source | Rationale | Scope | Verification Method | Status |
|---|---|---|---|---|---|---|
| CON-001 | `<Mandatory constraint>` | `<Source ID>` | `<Reason>` | `<Affected scope>` | Test / Analysis / Inspection / Demonstration | Proposed |

---

## 2.6 Assumptions and Dependencies

### 2.6.1 Assumptions

| Assumption ID | Assumption | Source | Impact if False | Owner | Status |
|---|---|---|---|---|---|
| ASM-001 | `<Assumption>` | `<Source ID>` | `<Impact>` | `<Owner>` | Open |

### 2.6.2 Dependencies

| Dependency ID | Dependency | Owner | Required Condition | Impact if Unavailable | Related Requirements | Status |
|---|---|---|---|---|---|---|
| DEP-001 | `<Dependency>` | `<Owner>` | `<Condition>` | `<Impact>` | `<Requirement IDs>` | Open |

---

# 3. Stakeholders, Actors and External Systems

## 3.1 Stakeholders

| Stakeholder ID | Stakeholder | Role | Interests | Decision Authority | Validation Responsibility | Status |
|---|---|---|---|---|---|---|
| STK-001 | `<Stakeholder>` | `<Role>` | `<Interests>` | `<Authority>` | `<Sections or requirements>` | Active |

---

## 3.2 Actors

| Actor ID | Actor | Actor Type | Goal | Main Interactions | Access Conditions | Related User Class |
|---|---|---|---|---|---|---|
| ACT-001 | `<Actor>` | Human / System / Device | `<Goal>` | `<Interactions>` | `<Conditions>` | `<User Class ID>` |

---

## 3.3 Actor Permission Overview

| Actor or Role | View | Create | Update | Delete | Approve | Configure | Data Scope |
|---|---:|---:|---:|---:|---:|---:|---|
| `<Actor or Role>` | Yes/No | Yes/No | Yes/No | Yes/No | Yes/No | Yes/No | `<Scope>` |

---

## 3.4 External Systems

| External System ID | System | Owner | Integration Purpose | Data Sent | Data Received | Interface | Availability Dependency |
|---|---|---|---|---|---|---|---|
| EXT-001 | `<External System>` | `<Owner>` | `<Purpose>` | `<Data>` | `<Data>` | `<Interface reference>` | `<Dependency>` |

---

# 4. Business Context

<!-- Có thể tham chiếu BRD hoặc tài liệu business context riêng thay vì lặp lại toàn bộ nội dung. -->

## 4.1 Problem Statement

`<Mô tả vấn đề hiện tại, đối tượng bị ảnh hưởng, bối cảnh và tác động. Không mô tả giải pháp kỹ thuật tại đây.>`

---

## 4.2 Business Goals

| Business Goal ID | Goal | Owner | Expected Outcome | Priority | Source | Status |
|---|---|---|---|---|---|---|
| BG-001 | `<Business Goal>` | `<Owner>` | `<Outcome>` | Must / Should / Could | `<Source ID>` | Proposed |

---

## 4.3 Success Criteria

| Success Criterion ID | Related Goal | Metric | Target | Measurement Method | Evaluation Time | Owner |
|---|---|---|---|---|---|---|
| SC-001 | `<Business Goal ID>` | `<Metric>` | `<Target>` | `<Method>` | `<Time>` | `<Owner>` |

---

## 4.4 Current Workflow

### 4.4.1 Workflow Summary

`<Mô tả quy trình hiện tại ở mức tổng quan.>`

### 4.4.2 Current Workflow Steps

| Step | Participant | Action | Input | Output | Issue or Limitation |
|---:|---|---|---|---|---|
| 1 | `<Participant>` | `<Action>` | `<Input>` | `<Output>` | `<Issue>` |

### 4.4.3 Current Workflow Diagram

---

## 4.5 Target Workflow

### 4.5.1 Workflow Summary

`<Mô tả quy trình mục tiêu ở mức tổng quan.>`

### 4.5.2 Target Workflow Steps

| Step | Actor/System | Action | Input | Business Rule | Output | Resulting State |
|---:|---|---|---|---|---|---|
| 1 | `<Actor or System>` | `<Action>` | `<Input>` | `<Business Rule ID>` | `<Output>` | `<State>` |

### 4.5.3 Target Workflow Diagram

---

# 5. Product Features

## 5.1 Feature List

| Feature ID | Feature Name | Description | Primary Actor | Related Goal | Priority | Release | Status |
|---|---|---|---|---|---|---|---|
| F-001 | `<Feature Name>` | `<Description>` | `<Actor ID>` | `<Business Goal ID>` | Must / Should / Could / Won't | `<Release>` | Proposed |

---

## 5.2 Feature Details

<!-- Sao chép khối dưới đây cho từng feature khi cần mô tả thêm. -->

### F-XXX — `<Feature Name>`

| Attribute | Value |
|---|---|
| Description | `<Description>` |
| Primary Actors | `<Actor IDs>` |
| Business Goals | `<Business Goal IDs>` |
| Use Cases | `<Use Case IDs>` |
| Functional Requirements | `<Requirement IDs>` |
| Priority | Must / Should / Could / Won't |
| Status | Proposed / Draft / Approved / Deferred |

---

# 6. Use Case Specifications

<!-- Phần này có thể được tách thành file riêng khi số lượng use case lớn. -->

## 6.1 Use Case Overview

| Use Case ID | Use Case Name | Primary Actor | Goal | Related Feature | Priority | Status |
|---|---|---|---|---|---|---|
| UC-001 | `<Use Case Name>` | `<Actor ID>` | `<Goal>` | `<Feature ID>` | `<Priority>` | Proposed |

---

## 6.2 Use Case Details

<!-- Sao chép khối dưới đây cho từng use case. -->

### UC-XXX — `<Use Case Name>`

| Attribute | Value |
|---|---|
| Goal | `<Actor goal>` |
| Primary Actor | `<Actor ID>` |
| Supporting Actors | `<Actor or External System IDs>` |
| Trigger | `<Trigger>` |
| Priority | `<Priority>` |
| Status | Proposed / Draft / Approved |

#### Preconditions

- `<Precondition>`

#### Main Flow

1. `<Actor or system action>`
2. `<Actor or system action>`

#### Alternative Flows

##### AF-01 — `<Alternative Flow Name>`

- **Starts at:** Step `<Number>`
- **Condition:** `<Condition>`

1. `<Alternative action>`
2. `<Alternative action>`

- **Returns to:** Step `<Number>` / Ends use case

#### Exception Flows

##### EF-01 — `<Exception Flow Name>`

- **Occurs at:** Step `<Number>`
- **Condition:** `<Failure condition>`

1. `<System response>`
2. `<Recovery or termination behavior>`

- **Resulting state:** `<State>`

#### Success Postconditions

- `<Postcondition>`

#### Failure Postconditions

- `<Minimum guarantee after failure>`

#### Related Business Rules

- `<Business Rule IDs>`

#### Related Requirements

- `<Requirement IDs>`

#### Open Questions

- `<Open Question IDs or None>`

---

# 7. Business Rules

## 7.1 Business Rule Catalogue

| Rule ID | Rule Name | Category | Rule Statement | Source | Scope | Priority | Status |
|---|---|---|---|---|---|---|---|
| BR-001 | `<Rule Name>` | `<Category>` | `<Rule Statement>` | `<Source ID>` | `<Scope>` | `<Priority>` | Proposed |

---

## 7.2 Business Rule Details

<!-- Sao chép khối dưới đây cho từng rule cần mô tả chi tiết. -->

### BR-XXX — `<Rule Name>`

| Attribute | Value |
|---|---|
| Category | Validation / Calculation / Eligibility / Authorization / Timing / State / Data / Policy / Compliance / Exception |
| Statement | `<Rule Statement>` |
| Rationale | `<Rationale>` |
| Source | `<Source ID>` |
| Scope | `<Scope>` |
| Conditions | `<Conditions>` |
| Exceptions | `<Exceptions or None>` |
| Effective Period | `<Period or Not Applicable>` |
| Related Use Cases | `<Use Case IDs>` |
| Related Requirements | `<Requirement IDs>` |
| Priority | `<Priority>` |
| Status | Proposed / Draft / Approved / Superseded |

---

# 8. Functional Requirements

## 8.1 Functional Requirement Catalogue

| Requirement ID | Name | Statement | Source | Priority | Verification | Status |
|---|---|---|---|---|---|---|
| FR-001 | `<Requirement Name>` | `The system shall <required behavior> when <condition>.` | `<Source ID>` | Must / Should / Could | Test / Analysis / Inspection / Demonstration | Proposed |

---

## 8.2 Functional Requirement Details

<!--
Mỗi requirement chỉ mô tả một nghĩa vụ chính.
Sao chép khối dưới đây cho từng functional requirement.
-->

### FR-XXX — `<Requirement Name>`

| Attribute | Value |
|---|---|
| Statement | `Hệ thống phải <hành vi bắt buộc> khi <điều kiện áp dụng>.` |
| Rationale | `<Why this requirement is necessary>` |
| Source | `<Source ID>` |
| Actors | `<Actor IDs>` |
| Preconditions | `<Preconditions or None>` |
| Trigger | `<Trigger>` |
| Inputs | `<Inputs>` |
| Processing Rules | `<Processing rules at requirement level>` |
| Outputs | `<Outputs>` |
| Error Conditions | `<Error conditions>` |
| Postconditions | `<Postconditions>` |
| Related Business Rules | `<Business Rule IDs>` |
| Related Requirements | `<Requirement IDs or None>` |
| Priority | Must / Should / Could |
| Verification Method | Test / Analysis / Inspection / Demonstration |
| Status | Proposed / Draft / Approved / Implemented / Verified / Deferred / Superseded |

#### Acceptance Criteria

- **AC-FR-XXX-01**
  - **Given:** `<Initial context or condition>`
  - **When:** `<Action or event>`
  - **Then:** `<Expected observable result>`

---

# 9. Data Requirements

## 9.1 Data Scope

`<Mô tả phạm vi dữ liệu hệ thống tiếp nhận, tạo, xử lý, lưu trữ, trao đổi và loại trừ.>`

---

## 9.2 Data Entity Overview

| Entity ID | Entity | Definition | Owner | Main Attributes | Related Entities | Lifecycle | Related Requirements |
|---|---|---|---|---|---|---|---|
| ENT-001 | `<Entity>` | `<Definition>` | `<Owner>` | `<Attributes>` | `<Entity IDs>` | `<Lifecycle summary>` | `<Requirement IDs>` |

---

## 9.3 Data Dictionary

| Data ID | Data Item | Entity | Definition | Logical Type | Required | Format/Range | Default | Validation Rule | Source | Sensitivity |
|---|---|---|---|---|---:|---|---|---|---|---|
| DATA-001 | `<Data Item>` | `<Entity ID>` | `<Definition>` | `<Logical type>` | Yes/No | `<Format or range>` | `<Default>` | `<Rule ID>` | `<Source ID>` | Public / Internal / Confidential / Restricted |

---

## 9.4 Data Validation Rules

| Validation ID | Data or Entity | Condition | Response When Invalid | Related Rule | Related Requirement |
|---|---|---|---|---|---|
| VAL-001 | `<Data or Entity ID>` | `<Validation condition>` | `<System response>` | `<Business Rule ID>` | `<Requirement ID>` |

---

## 9.5 Data Lifecycle

| Entity | Created When | Created By | Updated When | Locked/Finalized When | Archived When | Deleted When | Recovery Rule |
|---|---|---|---|---|---|---|---|
| `<Entity ID>` | `<Condition>` | `<Actor/System>` | `<Condition>` | `<Condition>` | `<Condition>` | `<Condition>` | `<Rule>` |

---

## 9.6 Data Retention and Deletion

| Data Category | Retention Period | Basis | Deletion Method | Archive Rule | Authorized Role | Verification |
|---|---|---|---|---|---|---|
| `<Data Category>` | `<Period or TBD>` | `<Business, legal or policy basis>` | `<Method>` | `<Rule>` | `<Role>` | `<Method>` |

---

## 9.7 Data Migration

<!-- Xóa hoặc ghi Not Applicable nếu dự án không có migration dữ liệu. -->

| Migration ID | Source | Target | Scope | Mapping Reference | Cleansing Rules | Validation | Rollback | Owner |
|---|---|---|---|---|---|---|---|---|
| MIG-001 | `<Source>` | `<Target>` | `<Scope>` | `<Reference>` | `<Rules>` | `<Validation>` | `<Rollback>` | `<Owner>` |

---

# 10. External Interface Requirements

## 10.1 User Interface Requirements

| UI Requirement ID | Interface or Screen Group | Requirement | Actors | Related Feature | Verification | Status |
|---|---|---|---|---|---|---|
| UI-001 | `<Interface Group>` | `<Requirement>` | `<Actor IDs>` | `<Feature ID>` | `<Method>` | Proposed |

---

## 10.2 Software Interface Requirements

| Interface ID | External System | Purpose | Data Sent | Data Received | Protocol/Format | Authentication | Timeout | Retry | Error Handling | Version |
|---|---|---|---|---|---|---|---|---|---|---|
| IF-SW-001 | `<External System ID>` | `<Purpose>` | `<Data>` | `<Data>` | `<Protocol and format>` | `<Authentication>` | `<Timeout>` | `<Retry policy>` | `<Error handling>` | `<Version>` |

---

## 10.3 Hardware Interface Requirements

<!-- Xóa hoặc ghi Not Applicable nếu hệ thống không giao tiếp phần cứng. -->

| Interface ID | Device | Purpose | Input | Output | Protocol | Failure Detection | Unavailable Behavior | Verification |
|---|---|---|---|---|---|---|---|---|
| IF-HW-001 | `<Device>` | `<Purpose>` | `<Input>` | `<Output>` | `<Protocol>` | `<Detection>` | `<Behavior>` | `<Method>` |

---

## 10.4 Communication Interface Requirements

| Interface ID | Communication Requirement | Protocol | Security | Message Format | Limits | Recovery | Verification |
|---|---|---|---|---|---|---|---|
| IF-COM-001 | `<Requirement>` | `<Protocol>` | `<Security>` | `<Format>` | `<Limits>` | `<Recovery>` | `<Method>` |

---

# 11. Non-functional Requirements

## 11.1 Non-functional Requirement Catalogue

| Requirement ID | Category | Statement | Source | Target/Measure | Verification | Priority | Status |
|---|---|---|---|---|---|---|---|
| NFR-001 | `<Category>` | `<Measurable requirement statement>` | `<Source ID>` | `<Target and unit>` | Test / Analysis / Inspection / Demonstration | `<Priority>` | Proposed |

---

## 11.2 Non-functional Requirement Details

<!-- Sao chép khối dưới đây cho từng NFR. -->

### NFR-XXX — `<Requirement Name>`

| Attribute | Value |
|---|---|
| Category | Performance / Availability / Reliability / Scalability / Security / Privacy / Usability / Maintainability / Compatibility / Portability / Accessibility / Logging / Recovery / Compliance |
| Statement | `<Measurable requirement statement>` |
| Scope | `<Affected function, component or system>` |
| Measurement Condition | `<Load, environment, data volume or other condition>` |
| Target | `<Target value and unit>` |
| Source | `<Source ID>` |
| Rationale | `<Rationale>` |
| Priority | Must / Should / Could |
| Verification Method | Test / Analysis / Inspection / Demonstration |
| Status | Proposed / Draft / Approved / Implemented / Verified / Deferred |

#### Acceptance Criteria

- **AC-NFR-XXX-01**
  - **Given:** `<Measurement environment and condition>`
  - **When:** `<Measurement action>`
  - **Then:** `<Expected measurable result>`

---

## 11.3 Performance

`<Requirement IDs or Not Applicable with rationale>`

## 11.4 Availability

`<Requirement IDs or Not Applicable with rationale>`

## 11.5 Reliability

`<Requirement IDs or Not Applicable with rationale>`

## 11.6 Scalability

`<Requirement IDs or Not Applicable with rationale>`

## 11.7 Security

`<Requirement IDs or Not Applicable with rationale>`

## 11.8 Privacy

`<Requirement IDs or Not Applicable with rationale>`

## 11.9 Usability

`<Requirement IDs or Not Applicable with rationale>`

## 11.10 Maintainability

`<Requirement IDs or Not Applicable with rationale>`

## 11.11 Compatibility and Portability

`<Requirement IDs or Not Applicable with rationale>`

## 11.12 Accessibility

`<Requirement IDs or Not Applicable with rationale>`

## 11.13 Logging and Auditing

`<Requirement IDs or Not Applicable with rationale>`

## 11.14 Backup and Recovery

`<Requirement IDs or Not Applicable with rationale>`

## 11.15 Compliance

`<Requirement IDs or Not Applicable with rationale>`

---

# 12. Access Control Requirements

## 12.1 Authentication Requirements

| Requirement ID | Statement | Source | Verification | Status |
|---|---|---|---|---|
| SEC-AUTHN-001 | `<Authentication requirement>` | `<Source ID>` | `<Method>` | Proposed |

---

## 12.2 Authorization Requirements

| Requirement ID | Statement | Source | Verification | Status |
|---|---|---|---|---|
| SEC-AUTHZ-001 | `<Authorization requirement>` | `<Source ID>` | `<Method>` | Proposed |

---

## 12.3 Access Control Matrix

| Role or Actor | Resource | View | Create | Update | Delete | Approve | Configure | Scope |
|---|---|---:|---:|---:|---:|---:|---:|---|
| `<Role or Actor>` | `<Resource>` | Yes/No | Yes/No | Yes/No | Yes/No | Yes/No | Yes/No | `<Data scope>` |

---

# 13. State Models

<!-- Chỉ giữ các state model có ảnh hưởng đến hành vi hoặc business rule. -->

## 13.1 State Definitions

| State ID | Entity | State | Meaning | Entry Condition | Allowed Actions | Prohibited Actions | Exit Condition | Terminal |
|---|---|---|---|---|---|---|---|---:|
| STATE-001 | `<Entity ID>` | `<State>` | `<Meaning>` | `<Condition>` | `<Actions>` | `<Actions>` | `<Condition>` | Yes/No |

---

## 13.2 State Transitions

| Transition ID | Entity | Current State | Event | Triggering Actor | Guard Condition | Action | Next State | Error Outcome | Related Rule |
|---|---|---|---|---|---|---|---|---|---|
| TR-001 | `<Entity ID>` | `<State>` | `<Event>` | `<Actor ID>` | `<Condition>` | `<Action>` | `<State>` | `<Outcome>` | `<Rule ID>` |

---

## 13.3 State Diagram

---

# 14. Error Handling and Edge Cases

## 14.1 Error Catalogue

| Error ID | Category | Condition | Detection | System Response | User Response | Data State | Retry/Rollback | Logging/Audit | Related Requirement |
|---|---|---|---|---|---|---|---|---|---|
| ERR-001 | `<Category>` | `<Condition>` | `<Detection>` | `<System response>` | `<Message or action>` | `<Resulting data state>` | `<Rule>` | `<Requirement>` | `<Requirement ID>` |

---

## 14.2 Edge Cases

| Edge Case ID | Scenario | Expected Behavior | Related Rule | Related Requirement | Verification |
|---|---|---|---|---|---|
| EDGE-001 | `<Boundary or unusual condition>` | `<Expected behavior>` | `<Rule ID>` | `<Requirement ID>` | `<Method>` |

---

# 15. Acceptance Criteria and Verification

## 15.1 Acceptance Criteria Catalogue

| Acceptance Criterion ID | Requirement ID | Preconditions | Action/Event | Expected Result | Data Condition | Priority | Verification Method |
|---|---|---|---|---|---|---|---|
| AC-001 | `<Requirement ID>` | `<Preconditions>` | `<Action or event>` | `<Expected result>` | `<Data condition>` | `<Priority>` | Test / Analysis / Inspection / Demonstration |

---

## 15.2 Verification Methods

| Verification Method | Definition | Applicable Requirements | Evidence Location |
|---|---|---|---|
| Test | `<Project-specific definition>` | `<Requirement IDs>` | `<Link or path>` |
| Analysis | `<Project-specific definition>` | `<Requirement IDs>` | `<Link or path>` |
| Inspection | `<Project-specific definition>` | `<Requirement IDs>` | `<Link or path>` |
| Demonstration | `<Project-specific definition>` | `<Requirement IDs>` | `<Link or path>` |

---

# 16. Requirements Traceability

## 16.1 Requirements Traceability Matrix

| Requirement ID | Source | Business Goal | Feature | Use Case | Business Rule | Data/Interface | Verification | Test/Evidence | Release | Status |
|---|---|---|---|---|---|---|---|---|---|---|
| `<Requirement ID>` | `<Source ID>` | `<Goal ID>` | `<Feature ID>` | `<Use Case ID>` | `<Rule IDs>` | `<Related IDs>` | `<Method>` | `<Reference>` | `<Release>` | `<Status>` |

---

## 16.2 Requirement Dependencies

| Source Requirement | Relationship | Target Requirement | Rationale | Change Impact |
|---|---|---|---|---|
| `<Requirement ID>` | Depends On / Requires / Conflicts With / Refines / Replaces / Derived From / Related To | `<Requirement ID>` | `<Rationale>` | `<Impact>` |

---

# 17. Open Questions, Decisions and Risks

## 17.1 Open Questions

| Question ID | Question | Context | Affected Sections | Owner | Due Date | Priority | Status | Resolution |
|---|---|---|---|---|---|---|---|---|
| OQ-001 | `<Question>` | `<Context>` | `<Sections or IDs>` | `<Owner>` | `YYYY-MM-DD` | `<Priority>` | Open | |

---

## 17.2 Decisions

| Decision ID | Decision | Date | Decision Owner | Rationale | Alternatives Considered | Affected Requirements | Effective Date | Status |
|---|---|---|---|---|---|---|---|---|
| DEC-001 | `<Decision>` | `YYYY-MM-DD` | `<Owner>` | `<Rationale>` | `<Alternatives>` | `<Requirement IDs>` | `YYYY-MM-DD` | Approved |

---

## 17.3 Requirement-related Risks

<!-- Có thể tham chiếu Risk Register riêng thay vì ghi chi tiết tại đây. -->

| Risk ID | Risk | Cause | Impact | Probability | Severity | Related Requirements | Mitigation | Owner | Status |
|---|---|---|---|---|---|---|---|---|---|
| RISK-001 | `<Risk>` | `<Cause>` | `<Impact>` | `<Probability>` | `<Severity>` | `<Requirement IDs>` | `<Mitigation>` | `<Owner>` | Open |

---

# 18. Appendices

## 18.1 Glossary

---

## 18.2 Diagrams

| Diagram ID | Diagram | Purpose | Version | Last Updated | Related Requirements | Location |
|---|---|---|---|---|---|---|
| DIA-001 | `<Diagram Name>` | `<Purpose>` | `<Version>` | `YYYY-MM-DD` | `<Requirement IDs>` | `<Link or Path>` |

---

## 18.3 Supporting Documents

| Document | Purpose | Version | Location |
|---|---|---|---|
| `<Document>` | `<Purpose>` | `<Version>` | `<Link or Path>` |

---

# 19. Requirement Identification Convention

| Prefix | Item Type |
|---|---|
| `REF` | Reference |
| `STK` | Stakeholder |
| `ACT` | Actor |
| `EXT` | External System |
| `BG` | Business Goal |
| `SC` | Success Criterion |
| `F` | Feature |
| `UC` | Use Case |
| `BR` | Business Rule |
| `FR` | Functional Requirement |
| `NFR` | Non-functional Requirement |
| `CON` | Constraint |
| `ASM` | Assumption |
| `DEP` | Dependency |
| `ENT` | Data Entity |
| `DATA` | Data Item |
| `VAL` | Data Validation |
| `IF` | Interface |
| `SEC` | Security or Access Control Requirement |
| `STATE` | State |
| `TR` | State Transition |
| `ERR` | Error |
| `EDGE` | Edge Case |
| `AC` | Acceptance Criterion |
| `OQ` | Open Question |
| `DEC` | Decision |
| `RISK` | Risk |
| `DIA` | Diagram |

ID format used by this project:

```text
<PREFIX>-<DOMAIN>-<SEQUENCE>
```

`<Document the project-specific ID convention here.>`

---

# 20. Requirement Status Convention

| Status | Meaning |
|---|---|
| Proposed | Requirement has been identified but not yet reviewed |
| Draft | Requirement is being refined |
| Under Review | Requirement is being reviewed |
| Approved | Requirement has been accepted as a baseline |
| Implemented | Requirement has been implemented but not fully verified |
| Verified | Evidence confirms the requirement is satisfied |
| Deferred | Requirement has been postponed |
| Rejected | Requirement has been rejected |
| Superseded | Requirement has been replaced |
| Deprecated | Requirement is retained for history but is no longer active |

---

# 21. SRS Review Checklist

## 21.1 Scope and Context

- [ ] Purpose and Scope are clear.
- [ ] In Scope and Out of Scope are defined.
- [ ] System boundary is clear.
- [ ] Stakeholders, users, actors and external systems are identified.
- [ ] Assumptions, dependencies and constraints are documented.

## 21.2 Requirements

- [ ] Each requirement has a unique ID.
- [ ] Each requirement has a source.
- [ ] Each requirement contains one main obligation.
- [ ] Each requirement is clear and unambiguous.
- [ ] Each requirement is feasible.
- [ ] Each requirement is verifiable.
- [ ] Each requirement avoids unnecessary implementation details.
- [ ] Requirements do not conflict or duplicate each other.
- [ ] Business rules are referenced rather than duplicated.

## 21.3 Coverage

- [ ] Functional requirements are covered.
- [ ] Data requirements are covered.
- [ ] Interface requirements are covered.
- [ ] Non-functional requirements are measurable.
- [ ] Security and access control are covered.
- [ ] States and transitions are covered where applicable.
- [ ] Error conditions and edge cases are covered.
- [ ] Acceptance criteria are present.

## 21.4 Traceability and Completion

- [ ] Requirements are traceable to their sources.
- [ ] Requirements are linked to verification evidence.
- [ ] Requirement dependencies are documented.
- [ ] Open questions are resolved or explicitly tracked.
- [ ] All `[TBD]` and `[ASSUMPTION]` markers have been reviewed.
- [ ] Diagrams and textual requirements are consistent.
- [ ] Revision History has been updated.
- [ ] Required stakeholders have reviewed the SRS.
- [ ] Document status and version are correct.

---

# 22. Approval

| Role | Name | Decision | Date | Comments |
|---|---|---|---|---|
| Reviewer | `<Name>` | Approved / Rejected / Changes Requested | `YYYY-MM-DD` | |
| Approver | `<Name>` | Approved / Rejected | `YYYY-MM-DD` | |
