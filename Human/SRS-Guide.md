---
title: SRS Guide
aliases:
  - Software Requirements Specification Guide
tags:
  - srs
  - requirements-engineering
  - software-documentation
status: completed
template: "[SRS-Template]"
overview: "[SRS-About]"
---

# Software Requirements Specification Guide

> Tài liệu này hướng dẫn cách xây dựng một SRS rõ ràng, nhất quán, có thể xác minh và truy vết.
>
> Kiến thức nền tảng được trình bày tại [SRS-About].  
> Mẫu dùng trực tiếp được trình bày tại [SRS-Template].

> [!important] Tailoring
> Đây là guide mở rộng dành cho người viết SRS.
>
> Các phần được đánh dấu **Core** nên được xem xét trong hầu hết dự án.  
> Các phần được đánh dấu **Conditional** chỉ giữ khi phù hợp.  
> Các phần được đánh dấu **Supporting** có thể đặt trong SRS hoặc tách thành artifact riêng.

---

# 0. Cơ sở tham chiếu

Guide được tổ chức dựa trên các nguyên tắc phổ biến của Requirements Engineering, đặc biệt từ:

- ISO/IEC/IEEE 29148:2018.
- NASA Software Engineering Handbook về Software Requirements Specification.
- INCOSE Guide to Writing Requirements.
- Các mô hình chất lượng phần mềm liên quan.

Guide không phải bản sao nguyên văn của một tiêu chuẩn và không quy định rằng mọi dự án phải sử dụng toàn bộ các phần.

---

# 1. Document Control — Core

## 1.1 Document Information

> Xác định tài liệu, phiên bản và trạng thái đang được sử dụng.

Nên gồm:

- Project Name.
- Software/System Name.
- Document Name.
- Document ID.
- Version.
- Status.
- Author.
- Reviewer.
- Approver nếu có.
- Created Date.
- Last Updated.

Các trạng thái có thể dùng:

- Draft.
- Under Review.
- Approved.
- Superseded.
- Archived.

---

## 1.2 Revision History

> Ghi lại các thay đổi quan trọng của tài liệu.

Nên gồm:

- Version.
- Date.
- Author.
- Changed Sections.
- Change Description.
- Review Status.

---

## 1.3 Review and Approval

> Xác định trách nhiệm review và phê duyệt.

Có thể gồm:

- Reviewer.
- Approver.
- Review Date.
- Review Status.
- Comments.
- Conditions of Approval.

Với dự án nhỏ, có thể rút gọn phần này.

---

# 2. Introduction — Core

## 2.1 Purpose

> Mô tả mục đích của tài liệu và phần mềm được đặc tả.

Nên làm rõ:

- Phần mềm hoặc thành phần được mô tả.
- Phiên bản hoặc release áp dụng.
- Mục đích sử dụng SRS.
- Nhóm người đọc chính.
- Quan hệ với các tài liệu khác.

Không nên:

- Mô tả chi tiết requirement.
- Trình bày solution.
- Lặp lại toàn bộ Scope.

---

## 2.2 Scope

> Xác định ranh giới của phần mềm và phiên bản đang được đặc tả.

Nên gồm:

### In Scope

- Capability được triển khai.
- Quy trình được hỗ trợ.
- Dữ liệu được quản lý.
- Integration được thực hiện.

### Out of Scope

- Capability chưa được phê duyệt.
- Quy trình nằm ngoài trách nhiệm phần mềm.
- Integration chưa triển khai.
- Nội dung được hoãn.

### Future Scope — Conditional

Chỉ ghi định hướng tương lai để tránh nhầm với cam kết hiện tại.

Scope phải nhất quán với:

- Features.
- Use Cases.
- Requirements.
- Interfaces.
- Acceptance Criteria.

---

## 2.3 Intended Audience

> Xác định nhóm người đọc và cách họ sử dụng tài liệu.

Có thể gồm:

- Stakeholder.
- Product Owner.
- Business Analyst.
- System Analyst.
- Architect.
- Developer.
- Tester.
- Security Reviewer.
- Operations.
- Maintenance.

---

## 2.4 Definitions, Acronyms and Abbreviations

> Định nghĩa thuật ngữ, từ viết tắt, đơn vị và trạng thái được dùng trong SRS.

Nguyên tắc:

- Một khái niệm có một tên chính.
- Không dùng từ viết tắt trước khi định nghĩa.
- Thuật ngữ phải thống nhất với requirement, diagram và model.
- Thuật ngữ quan trọng có thể được quản lý trong Glossary riêng.

---

## 2.5 References

> Liệt kê nguồn được sử dụng để xây dựng requirement.

Có thể gồm:

- Stakeholder Needs.
- Business Requirements.
- Policies.
- Regulations.
- Standards.
- Existing System Documentation.
- Interface Specifications.
- Data Definitions.
- Architecture Constraints.
- Contractual Documents.

Mỗi reference nên có:

- Reference ID.
- Name.
- Version hoặc Date.
- Owner.
- Location.
- Relevant Content.

---

## 2.6 Document Overview — Conditional

> Tóm tắt cấu trúc tài liệu khi SRS dài hoặc có nhiều artifact liên kết.

---

# 3. Overall Description — Core

## 3.1 Product Perspective

> Mô tả vị trí của phần mềm trong bối cảnh tổng thể.

Nên làm rõ:

- Phần mềm độc lập hay là thành phần của hệ thống lớn hơn.
- System boundary.
- External systems.
- Dữ liệu chính đi vào và đi ra.
- Quan hệ với sản phẩm hoặc quy trình hiện có.
- Trách nhiệm thuộc hệ thống và trách nhiệm thuộc môi trường ngoài.

Có thể tham chiếu System Context Diagram.

Không nên mô tả:

- Source code structure.
- Class hoặc module nội bộ.
- Database schema vật lý.
- Chi tiết triển khai hạ tầng không bắt buộc.

---

## 3.2 Product Functions

> Tóm tắt các capability hoặc nhóm chức năng chính.

Nên:

- Nhóm các chức năng liên quan.
- Giữ mức độ tổng quan.
- Tham chiếu tới feature hoặc requirement chi tiết.

Không nên:

- Mô tả toàn bộ processing flow.
- Liệt kê mọi validation.
- Thay thế Functional Requirements.

---

## 3.3 User Classes and Characteristics

> Mô tả các nhóm người dùng và đặc điểm ảnh hưởng đến việc sử dụng phần mềm.

Có thể gồm:

- Goals.
- Responsibilities.
- Usage Frequency.
- Technical Experience.
- Devices.
- Access Restrictions.
- Support Needs.

Cần phân biệt:

- User Class.
- Actor.
- Organizational Role.
- Authorization Role.

---

## 3.4 Operating Environment

> Mô tả môi trường phần mềm phải hoạt động.

Có thể gồm:

- Application Type.
- Client Environment.
- Server Environment.
- Operating System.
- Browser.
- Network.
- Runtime.
- Data Platform.
- Device.
- Deployment Environment.

Chỉ ghi công nghệ cụ thể khi đó là requirement hoặc constraint.

---

## 3.5 Design and Implementation Constraints

> Ghi lại các ràng buộc kỹ thuật hoặc tổ chức bắt buộc.

Có thể gồm:

- Required Technology.
- Required Platform.
- Compatibility.
- Data Standard.
- Communication Standard.
- Security Standard.
- Legal Constraint.
- Hardware Limit.
- Existing Component.
- Required Programming Language.
- Organizational Policy.

Mỗi constraint nên có:

- ID.
- Source.
- Rationale.
- Scope.
- Verification Method.
- Status.

---

## 3.6 Assumptions and Dependencies

### Assumptions

Mỗi assumption nên có:

- ID.
- Statement.
- Source.
- Impact if False.
- Owner.
- Status.

### Dependencies

Mỗi dependency nên có:

- ID.
- Owner.
- Required Condition.
- Impact if Unavailable.
- Related Requirements.
- Status.

Assumption và dependency không được trình bày như requirement đã được xác nhận.

---

# 4. Stakeholders, Actors and External Systems — Core

## 4.1 Stakeholders

> Xác định cá nhân, nhóm hoặc tổ chức có lợi ích, trách nhiệm hoặc quyền quyết định.

Có thể ghi:

- Stakeholder ID.
- Role.
- Interests.
- Decision Authority.
- Validation Responsibility.
- Status.

---

## 4.2 Actors

> Xác định người, hệ thống hoặc thiết bị trực tiếp tương tác với phần mềm.

Có thể ghi:

- Actor ID.
- Actor Type.
- Goal.
- Main Interactions.
- Access Conditions.
- Related User Class.

Actor không nên được định nghĩa hoàn toàn theo:

- Job title.
- Database role.
- Account name.
- Implementation structure.

---

## 4.3 Actor Permission Overview — Conditional

> Mô tả quyền tổng quan của actor hoặc role.

Có thể phân biệt:

- View.
- Create.
- Update.
- Delete.
- Approve.
- Configure.
- Export.
- Data Scope.

Permission chi tiết có thể được quản lý bằng Access Control Matrix.

---

## 4.4 External Systems

> Mô tả hệ thống ngoài tương tác với phần mềm.

Nên ghi:

- External System ID.
- Owner.
- Integration Purpose.
- Data Sent.
- Data Received.
- Interface.
- Availability Dependency.

---

# 5. Business Context — Supporting

Phần này có thể được giữ trong SRS hoặc tham chiếu BRD, Product Brief hoặc tài liệu nghiệp vụ khác.

## 5.1 Problem Statement

> Mô tả vấn đề, đối tượng bị ảnh hưởng, bối cảnh và tác động.

Không đưa solution kỹ thuật vào phần này.

---

## 5.2 Business Goals

Mỗi goal nên có:

- ID.
- Owner.
- Expected Outcome.
- Priority.
- Source.
- Status.

---

## 5.3 Success Criteria

Mỗi criterion nên:

- Liên kết với Business Goal.
- Có metric.
- Có target.
- Có Measurement Method.
- Có Evaluation Time.
- Có owner.

Cần phân biệt:

- Success Criteria của sản phẩm hoặc dự án.
- Acceptance Criteria của requirement.
- KPI vận hành.

---

## 5.4 Current Workflow

Nên xác định:

- Participants.
- Steps.
- Inputs.
- Outputs.
- Decision Points.
- Manual Activities.
- Problems.
- Exceptions.

---

## 5.5 Target Workflow

Nên xác định:

- Actors.
- System Actions.
- Business Rules.
- Inputs.
- Outputs.
- Resulting States.
- Main Alternatives.
- Important Failures.

Target Workflow không thay thế Use Case hoặc Functional Requirement.

---

# 6. Product Features — Supporting

## 6.1 Feature List

Mỗi feature có thể gồm:

- Feature ID.
- Name.
- Description.
- Primary Actor.
- Related Goal.
- Priority.
- Release.
- Status.

Feature giúp nhóm requirement và quản lý scope.

---

## 6.2 Feature Prioritization — Conditional

Có thể sử dụng:

- Must.
- Should.
- Could.
- Won't for now.

Hoặc quy ước khác đã được định nghĩa.

Không nên gán mọi feature ở mức ưu tiên cao nhất.

---

# 7. Use Case Specifications — Supporting

Use Case không bắt buộc trong mọi SRS nhưng hữu ích khi hệ thống có nhiều luồng tương tác.

## 7.1 Use Case Overview

Mỗi Use Case nên có:

- Use Case ID.
- Name.
- Primary Actor.
- Goal.
- Related Feature.
- Priority.
- Status.

---

## 7.2 Use Case Structure

### Goal

Kết quả actor muốn đạt.

### Primary Actor

Actor khởi tạo và nhận giá trị chính.

### Supporting Actors

Actor hoặc external system hỗ trợ.

### Trigger

Sự kiện làm Use Case bắt đầu.

### Preconditions

Điều kiện phải đúng trước khi Use Case được thực hiện.

### Main Flow

Luồng thành công tiêu chuẩn.

Mỗi bước nên:

- Có thứ tự.
- Xác định actor hoặc system action.
- Mô tả một hành động chính.
- Tránh chi tiết UI không cần thiết.
- Tham chiếu Business Rule khi phù hợp.

### Alternative Flows

Luồng hợp lệ khác với Main Flow nhưng vẫn đạt mục tiêu.

### Exception Flows

Luồng không thể hoàn thành như dự kiến.

Nên xác định:

- Failure Condition.
- System Response.
- Data State.
- Recovery.
- Notification.
- Logging hoặc Audit nếu cần.

### Postconditions

Nên phân biệt:

- Success Postconditions.
- Failure Postconditions.
- Minimal Guarantee.

### Related Business Rules

Danh sách Rule ID.

### Related Requirements

Danh sách Requirement ID.

---

## 7.3 Use Case Writing Rules

- Tập trung vào mục tiêu actor.
- Mô tả hành vi bên ngoài.
- Không mô tả class, method hoặc table.
- Không gộp nhiều mục tiêu độc lập.
- Không bỏ qua exception quan trọng.
- Không lặp nguyên văn Business Rule.
- Dùng thuật ngữ trong Glossary.
- Bảo đảm precondition và postcondition nhất quán.

---

# 8. Business Rules — Core hoặc Supporting

Business Rule phải được ghi lại, nhưng có thể nằm trong SRS hoặc Business Rule Catalogue riêng.

## 8.1 Business Rule Structure

Mỗi rule nên có:

- Rule ID.
- Rule Name.
- Category.
- Statement.
- Rationale.
- Source.
- Scope.
- Conditions.
- Exceptions.
- Effective Period.
- Related Use Cases.
- Related Requirements.
- Priority.
- Status.

---

## 8.2 Business Rule Categories

Có thể gồm:

- Validation.
- Calculation.
- Eligibility.
- Authorization.
- Timing.
- State Transition.
- Data Integrity.
- Policy.
- Compliance.
- Exception.

---

## 8.3 Business Rule Management

- Mỗi rule có một nguồn chính.
- Không lặp toàn bộ rule trong nhiều requirement.
- Requirement tham chiếu Rule ID.
- Khi rule thay đổi, phải review mọi phần tham chiếu.
- Rule chưa xác nhận phải có trạng thái.
- Rule có thời gian hiệu lực phải được quản lý phiên bản.
- Exception phải được ghi rõ.

---

# 9. Functional Requirements — Core

## 9.1 Purpose

Functional Requirement mô tả hành vi mà phần mềm bắt buộc phải cung cấp.

Mỗi requirement nên:

- Có ID duy nhất.
- Chứa một nghĩa vụ chính.
- Có source.
- Có condition khi cần.
- Có kết quả quan sát được.
- Có Verification Method.
- Có status.
- Không phụ thuộc không cần thiết vào implementation.

---

## 9.2 Functional Requirement Structure

### Requirement ID

Mã duy nhất và ổn định.

### Name

Tên ngắn gọn.

### Statement

Cấu trúc thường dùng:

> Hệ thống phải `<hành vi bắt buộc>` khi `<điều kiện áp dụng>`.

### Rationale

Lý do requirement tồn tại.

### Source

Nguồn phát sinh requirement.

### Actors

Actor liên quan.

### Preconditions

Điều kiện cần trước khi hành vi xảy ra.

### Trigger

Sự kiện kích hoạt.

### Inputs

Dữ liệu đầu vào.

### Processing Rules

Quy tắc xử lý ở mức requirement.

Không mô tả:

- Class.
- Method.
- Query.
- Framework.
- Layer.
- Thuật toán không bắt buộc.

### Outputs

Kết quả đầu ra.

### Error Conditions

Trường hợp phải từ chối, cảnh báo hoặc xử lý khác.

### Postconditions

Trạng thái sau khi hoàn thành.

### Related Business Rules

Rule ID được áp dụng.

### Related Requirements

Dependency hoặc quan hệ khác.

### Priority

Mức độ ưu tiên.

### Verification Method

- Test.
- Analysis.
- Inspection.
- Demonstration.

### Status

Trạng thái quản lý requirement.

---

## 9.3 Atomicity

Mỗi requirement chỉ chứa một nghĩa vụ chính.

Không gộp:

- Nhiều hành vi độc lập.
- Hành vi nghiệp vụ và hiệu năng.
- Hành vi chính và reporting không liên quan.
- Nhiều actor không liên quan.

Một requirement có thể chứa nhiều condition nếu chúng cùng chi phối một hành vi duy nhất.

---

## 9.4 Requirement Dependencies

Có thể dùng:

- Depends On.
- Requires.
- Conflicts With.
- Refines.
- Replaces.
- Derived From.
- Related To.

Cần ghi:

- Source Requirement.
- Target Requirement.
- Relationship.
- Rationale.
- Change Impact.

---

# 10. Data Requirements — Core

## 10.1 Data Scope

> Xác định dữ liệu phần mềm nhận, tạo, xử lý, lưu trữ, trao đổi hoặc loại trừ.

---

## 10.2 Data Entities

Mỗi entity nên có:

- Entity ID.
- Definition.
- Owner.
- Main Attributes.
- Relationships.
- States.
- Lifecycle.
- Related Requirements.

SRS tập trung vào conceptual hoặc logical data requirement.

Không nên đi sâu vào:

- Physical table.
- Index.
- Migration.
- ORM configuration.
- Database-specific type.
- SQL.

---

## 10.3 Data Dictionary

Mỗi data item quan trọng nên có:

- Data ID.
- Name.
- Entity.
- Definition.
- Logical Type.
- Required.
- Format.
- Range.
- Unit.
- Allowed Values.
- Default.
- Validation.
- Source.
- Sensitivity.
- Retention.

---

## 10.4 Data Validation Rules

Có thể gồm:

- Required.
- Format.
- Range.
- Length.
- Uniqueness.
- Cross-field.
- Cross-entity.
- State-dependent.
- Temporal.
- Referential Integrity.
- Duplicate Detection.
- Business Rule Validation.

---

## 10.5 Data Lifecycle

Nên xác định:

- Creation.
- Update.
- Finalization hoặc Locking.
- Expiration.
- Archive.
- Anonymization.
- Deletion.
- Recovery.

---

## 10.6 Data Retention and Deletion — Conditional

Giữ khi có yêu cầu nghiệp vụ, pháp lý, bảo mật hoặc vận hành.

---

## 10.7 Data Migration — Conditional

Giữ khi phần mềm tiếp nhận dữ liệu từ hệ thống cũ hoặc nguồn khác.

---

# 11. Interface Requirements — Core

## 11.1 User Interface Requirements

Mô tả yêu cầu ở mức phần mềm:

- Screen Groups.
- Navigation.
- Inputs.
- Outputs.
- Validation Feedback.
- Error Feedback.
- Accessibility.
- Localization.
- Data Format.
- Role-based Visibility.

Không thay thế UI Design hoặc Prototype.

---

## 11.2 Software Interface Requirements

Mỗi interface nên xác định:

- Interface ID.
- External System.
- Purpose.
- Data Sent.
- Data Received.
- Protocol.
- Format.
- Authentication.
- Authorization.
- Timeout.
- Retry.
- Error Handling.
- Versioning.
- Availability Dependency.

Chi tiết endpoint có thể nằm trong API Specification.

---

## 11.3 Hardware Interface Requirements — Conditional

Giữ khi phần mềm tương tác với phần cứng.

Nên xác định:

- Device.
- Input.
- Output.
- Protocol.
- Connection.
- Failure Detection.
- Unavailable Behavior.
- Simulation Requirement nếu có.

---

## 11.4 Communication Interface Requirements — Conditional

Giữ khi có requirement riêng về:

- Network.
- Protocol.
- Encryption.
- Certificate.
- Message Format.
- Size Limit.
- Rate Limit.
- Connection Recovery.
- Clock Synchronization.

---

## 11.5 Internal Interface Requirements — Conditional

Chỉ ghi khi internal interface:

- Là contract bắt buộc.
- Được phân bổ từ requirement cấp cao.
- Ảnh hưởng trực tiếp tới verification.
- Phải duy trì compatibility.
- Bị ràng buộc bởi standard.

Chi tiết thiết kế khác nên nằm trong Software Design Document.

---

# 12. Non-functional Requirements — Core

## 12.1 General Rules

Mỗi NFR nên:

- Có ID.
- Có scope.
- Có Measurement Condition.
- Có Target và Unit.
- Có source.
- Có priority.
- Có Verification Method.
- Có status.

---

## 12.2 Performance and Timing

Có thể xác định:

- Response Time.
- Throughput.
- Concurrent Users.
- Transaction Volume.
- Batch Processing Time.
- Background Processing Time.
- Startup Time.
- Peak Load.
- Data Volume.
- Resource Utilization.
- Interface Latency.
- Processing Deadline.

Không dùng các từ không đo được như:

- Nhanh.
- Hiệu quả.
- Tối ưu.
- Gần như tức thời.
- Thời gian hợp lý.

---

## 12.3 Availability

Có thể xác định:

- Service Hours.
- Availability Target.
- Planned Downtime.
- Unplanned Downtime.
- Maintenance Window.
- Monitoring.
- Alerting.
- Failover.
- Dependency Availability.

---

## 12.4 Reliability

Có thể xác định:

- Processing Accuracy.
- Transaction Integrity.
- Duplicate Prevention.
- Error Recovery.
- Data Loss Tolerance.
- Consistency After Failure.
- Failure Rate.

---

## 12.5 Scalability

Có thể xác định:

- User Growth.
- Transaction Growth.
- Data Growth.
- Geographic Growth.
- Tenant Growth.
- Scale Threshold.
- Scale Without Service Interruption.

---

## 12.6 Security

Có thể xác định:

- Authentication.
- Authorization.
- Session Management.
- Credential Management.
- Encryption.
- Input Validation.
- Secrets Management.
- Security Logging.
- Privileged Operations.
- Vulnerability Management.
- Incident Response.
- Integrity Protection.

---

## 12.7 Privacy — Conditional

Giữ khi xử lý dữ liệu cá nhân hoặc dữ liệu chịu quy định.

Có thể xác định:

- Collection.
- Purpose.
- Consent.
- Data Minimization.
- Access.
- Correction.
- Export.
- Retention.
- Deletion.
- Anonymization.
- Disclosure.
- Data Residency.

---

## 12.8 Usability

Có thể xác định:

- Learnability.
- Number of Steps.
- Feedback.
- Error Prevention.
- Recovery from User Error.
- Help Content.
- Supported Language.

---

## 12.9 Accessibility — Conditional

Có thể xác định:

- Keyboard Operation.
- Screen Reader.
- Contrast.
- Text Scaling.
- Focus.
- Alternative Text.
- Form Labeling.
- Error Identification.
- Applicable Standard.

---

## 12.10 Maintainability

Có thể xác định:

- Configurability.
- Modularity.
- Testability.
- Documentation.
- Upgradeability.
- Dependency Management.
- Backward Compatibility.

Không mô tả architecture chi tiết nếu không phải constraint.

---

## 12.11 Compatibility and Portability

Có thể xác định:

- Browser.
- Operating System.
- Device.
- API Version.
- Data Format.
- Deployment Environment.
- Container.
- Cloud.
- Installation.
- Environment Migration.

---

## 12.12 Logging and Auditing

Có thể xác định:

- Events.
- Log Level.
- Correlation ID.
- Actor.
- Time.
- Before/After Values.
- Retention.
- Access.
- Integrity.
- Sensitive Data Exclusion.
- Monitoring Integration.

---

## 12.13 Backup and Recovery — Conditional

Có thể xác định:

- Backup Scope.
- Frequency.
- Retention.
- Recovery Point Objective.
- Recovery Time Objective.
- Restore Testing.
- Encryption.
- Access Control.
- Disaster Recovery.

---

## 12.14 Compliance — Conditional

Giữ khi có:

- Legal Requirement.
- Industry Standard.
- Internal Policy.
- Audit Requirement.
- Reporting Requirement.
- Evidence Retention.
- Regional Data Requirement.

---

## 12.15 Safety — Conditional

Giữ khi lỗi phần mềm có thể gây nguy hiểm đến người, tài sản, môi trường hoặc nhiệm vụ quan trọng.

---

# 13. Access Control Requirements — Conditional

Có thể nằm trong Security Requirements hoặc được tách riêng khi hệ thống có phân quyền phức tạp.

## 13.1 Authentication

Có thể xác định:

- Login Method.
- Account Condition.
- Password Policy.
- Multi-factor Authentication.
- Lockout.
- Session.
- Logout.
- Reset.
- Identity Provider.

---

## 13.2 Authorization

Có thể xác định:

- Role.
- Permission.
- Resource.
- Action.
- Scope.
- Ownership.
- Data-level Restriction.
- Privileged Operation.
- Default Deny.
- Separation of Duties.

---

## 13.3 Access Control Matrix

Nên phân biệt:

- View.
- Create.
- Update.
- Delete.
- Approve.
- Configure.
- Export.
- Override.
- Data Scope.

---

# 14. Required States and Modes — Core khi áp dụng

Giữ phần này khi hành vi phụ thuộc vào trạng thái.

## 14.1 State Definition

Mỗi state nên có:

- State ID.
- Entity.
- State Name.
- Meaning.
- Entry Condition.
- Allowed Actions.
- Prohibited Actions.
- Exit Condition.
- Terminal Flag.

---

## 14.2 State Transition

Mỗi transition nên có:

- Transition ID.
- Entity.
- Current State.
- Event.
- Triggering Actor.
- Guard Condition.
- Action.
- Next State.
- Error Outcome.
- Related Business Rule.

---

## 14.3 State Consistency

Cần xác định:

- Valid Transition.
- Invalid Transition.
- Automatic Transition.
- Manual Transition.
- Time-based Transition.
- External Event Transition.
- Concurrent Transition.
- Duplicate Action.
- Failure State.
- Rollback if applicable.

---

# 15. Error Handling and Edge Cases — Core

## 15.1 Error Categories

Có thể gồm:

- Validation Error.
- Authentication Error.
- Authorization Error.
- Business Rule Violation.
- Not Found.
- Conflict.
- Duplicate Request.
- Concurrency Error.
- Integration Error.
- Timeout.
- Infrastructure Error.
- Data Integrity Error.
- Unexpected Error.

---

## 15.2 Error Requirement

Mỗi lỗi quan trọng nên xác định:

- Condition.
- Detection.
- System Response.
- User Response.
- Data State.
- Retry.
- Rollback.
- Logging.
- Audit.
- Recovery.

---

## 15.3 Edge Case Review

Cần xem xét:

- Missing Data.
- Invalid Format.
- Boundary Value.
- Duplicate Data.
- Repeated Action.
- Concurrent Action.
- Lost Connection.
- External System Unavailable.
- Partial Failure.
- Timeout.
- Expired Session.
- Permission Changed During Operation.
- State Changed During Operation.
- Stale Data.
- Restart Recovery.

---

# 16. Acceptance Criteria and Verification — Core

## 16.1 Acceptance Criteria

Acceptance Criteria nên:

- Liên kết với Requirement ID.
- Có precondition.
- Có action hoặc event.
- Có expected result.
- Có data condition khi cần.
- Có Verification Method.
- Bao phủ success và failure quan trọng.

Có thể dùng:

- Given.
- When.
- Then.

Acceptance Criteria không thay thế Requirement Statement.

---

## 16.2 Verification Methods

- **Test:** thực thi phần mềm trong điều kiện xác định.
- **Analysis:** sử dụng tính toán, mô hình hoặc phân tích.
- **Inspection:** kiểm tra tài liệu, cấu hình, code hoặc artifact.
- **Demonstration:** quan sát phần mềm thực hiện hành vi.

Mỗi requirement nên có:

- Verification Method.
- Verification Condition.
- Expected Result.
- Pass/Fail Criteria.
- Evidence Location.

---

# 17. Requirements Traceability — Core

## 17.1 Backward Traceability

Xác định:

- Requirement đến từ source nào.
- Need hoặc policy nào tạo ra requirement.
- Higher-level requirement nào được phân bổ.

---

## 17.2 Forward Traceability

Xác định:

- Requirement liên quan tới design element nào.
- Requirement được triển khai ở đâu khi cần.
- Requirement được xác minh bằng artifact nào.
- Requirement thuộc release nào.

---

## 17.3 Requirements Traceability Matrix

RTM có thể liên kết:

- Source.
- Business Goal.
- Feature.
- Use Case.
- Business Rule.
- Requirement.
- Data hoặc Interface.
- Verification Method.
- Test hoặc Evidence.
- Release.
- Status.

Không phải dự án nào cũng cần mọi cột.

---

## 17.4 Change Impact Analysis

Khi requirement thay đổi, cần rà soát:

- Source.
- Business Rule.
- Use Case.
- Dependent Requirements.
- Data Requirement.
- Interface Requirement.
- State Model.
- Acceptance Criteria.
- Test.
- Diagram.
- Release Scope.
- Related Documentation.

---

# 18. Open Questions, Decisions and Risks — Supporting

Các nội dung này có thể nằm trong SRS draft hoặc artifact riêng.

## 18.1 Open Questions

Mỗi question nên có:

- ID.
- Context.
- Affected Sections.
- Owner.
- Due Date.
- Priority.
- Status.
- Resolution.

Bản SRS Approved không nên còn Open Question quan trọng không có kế hoạch xử lý.

---

## 18.2 Decisions

Mỗi decision nên có:

- ID.
- Decision.
- Date.
- Owner.
- Rationale.
- Alternatives.
- Affected Requirements.
- Effective Date.
- Status.

---

## 18.3 Risks

SRS không thay thế Risk Register.

Chỉ giữ risk ảnh hưởng trực tiếp đến requirement hoặc tham chiếu tài liệu quản lý risk.

---

# 19. Appendices — Supporting

Có thể gồm:

- Glossary.
- Data Dictionary.
- System Context Diagram.
- Use Case Diagram.
- Workflow Diagram.
- State Machine Diagram.
- Conceptual Data Model.
- Interface Catalogue.
- Supporting Documents.

Mỗi diagram nên có:

- ID.
- Name.
- Purpose.
- Version.
- Last Updated.
- Related Requirements.
- Location.

---

# 20. Requirement Identification Convention — Core

Có thể sử dụng:

- `REF` — Reference.
- `STK` — Stakeholder.
- `ACT` — Actor.
- `EXT` — External System.
- `BG` — Business Goal.
- `F` — Feature.
- `UC` — Use Case.
- `BR` — Business Rule.
- `FR` — Functional Requirement.
- `NFR` — Non-functional Requirement.
- `CON` — Constraint.
- `ASM` — Assumption.
- `DEP` — Dependency.
- `ENT` — Data Entity.
- `DATA` — Data Item.
- `VAL` — Validation.
- `IF` — Interface.
- `SEC` — Security Requirement.
- `STATE` — State.
- `TR` — Transition.
- `ERR` — Error.
- `EDGE` — Edge Case.
- `AC` — Acceptance Criterion.
- `OQ` — Open Question.
- `DEC` — Decision.
- `RISK` — Risk.
- `DIA` — Diagram.

ID nên:

- Duy nhất.
- Ổn định.
- Không tái sử dụng.
- Không phụ thuộc hoàn toàn vào heading.
- Dễ tìm kiếm.
- Không chứa thông tin dễ thay đổi.

Requirement bị loại bỏ phải được giữ trong lịch sử với status phù hợp.

---

# 21. Requirement Status Convention — Core

Có thể dùng:

- Proposed.
- Draft.
- Under Review.
- Approved.
- Implemented.
- Verified.
- Deferred.
- Rejected.
- Superseded.
- Deprecated.

Mỗi status nên có định nghĩa về:

- Người có quyền chuyển.
- Điều kiện chuyển.
- Bằng chứng cần có.
- Trạng thái tiếp theo hợp lệ.

---

# 22. Writing Conventions — Core

## 22.1 Mandatory Language

Nên thống nhất:

- “Phải” cho nghĩa vụ bắt buộc.
- “Không được” cho hành vi bị cấm.
- “Nên” cho khuyến nghị.
- “Có thể” cho quyền hoặc khả năng được phép.

---

## 22.2 Sentence Structure

Requirement nên:

- Có chủ thể rõ.
- Dùng thể chủ động.
- Dùng động từ chỉ hành vi.
- Có condition khi cần.
- Có kết quả quan sát được.
- Có một nghĩa vụ chính.
- Tránh câu dài và nhiều mệnh đề không liên quan.

---

## 22.3 Terminology

- Dùng thuật ngữ trong Glossary.
- Không đổi tên actor giữa các phần.
- Không dùng nhiều tên cho cùng entity.
- Không dịch cùng thuật ngữ theo nhiều cách.
- Dùng capitalization và số nhiều nhất quán.

---

## 22.4 Ambiguous Terms

Hạn chế khi chưa được định nghĩa:

- Nhanh.
- Hợp lý.
- Linh hoạt.
- Gần như.
- Thông thường.
- Tối ưu.
- Đầy đủ.
- Thân thiện.
- Hiệu quả.
- Phù hợp.
- Khi cần.
- Và các cụm tương tự.

---

## 22.5 Absolute Terms

Không dùng:

- Luôn luôn.
- Không bao giờ.
- Hoàn toàn.
- Một trăm phần trăm.

Trừ khi có thể chứng minh và xác minh ở mức tuyệt đối.

---

## 22.6 Cross-reference

- Ưu tiên dùng ID.
- Kiểm tra ID tồn tại.
- Cập nhật tham chiếu khi requirement thay đổi.
- Không chỉ dựa vào số chương.

---

# 23. Quality Review Checklist — Core

## 23.1 Document Control

- [ ] Version và Status đã đúng.
- [ ] Revision History đã cập nhật.
- [ ] Reviewer và Approver đã được xác định khi cần.

## 23.2 Scope and Context

- [ ] Purpose đã rõ.
- [ ] In Scope và Out of Scope đã rõ.
- [ ] System Boundary đã rõ.
- [ ] Users, Actors và External Systems đã được xác định.
- [ ] Assumptions, Dependencies và Constraints đã được ghi.

## 23.3 Functional Requirements

- [ ] Mỗi requirement có ID.
- [ ] Mỗi requirement có source.
- [ ] Mỗi requirement chứa một nghĩa vụ chính.
- [ ] Condition và expected result đã rõ.
- [ ] Requirement có thể xác minh.
- [ ] Không có implementation detail không cần thiết.
- [ ] Không có requirement trùng hoặc mâu thuẫn.

## 23.4 Business Rules

- [ ] Mỗi rule có ID.
- [ ] Rule có source.
- [ ] Requirement tham chiếu Rule ID.
- [ ] Rule không bị lặp không kiểm soát.
- [ ] Exception và effective period đã được ghi khi cần.

## 23.5 Data and Interfaces

- [ ] Data entities và data items quan trọng đã được xác định.
- [ ] Validation quan trọng đã được ghi.
- [ ] Data lifecycle đã được xem xét.
- [ ] External interfaces đã được xác định.
- [ ] Timeout, retry và failure behavior đã được xem xét.
- [ ] SRS không chứa quá nhiều physical design.

## 23.6 Non-functional Requirements

- [ ] Mỗi NFR có scope.
- [ ] Có Measurement Condition.
- [ ] Có Target và Unit.
- [ ] Có Verification Method.
- [ ] Performance đã được xem xét.
- [ ] Security đã được xem xét.
- [ ] Privacy và Compliance đã được xem xét khi áp dụng.
- [ ] Reliability, Usability và Maintainability đã được xem xét.

## 23.7 States and Errors

- [ ] Entity có state đã được nhận diện.
- [ ] Valid và invalid transition đã được xem xét.
- [ ] Failure State đã được xác định.
- [ ] Concurrency và duplicate action đã được xem xét.
- [ ] Error response và data state sau lỗi đã rõ.

## 23.8 Verification and Traceability

- [ ] Mỗi requirement có Verification Method.
- [ ] Acceptance Criteria quan trọng đã được ghi.
- [ ] Requirement truy vết được về source.
- [ ] Requirement truy vết được tới evidence.
- [ ] Dependency đã được xác định.
- [ ] RTM đã được cập nhật.

## 23.9 Consistency

- [ ] Thuật ngữ nhất quán.
- [ ] Actor và entity nhất quán.
- [ ] State nhất quán.
- [ ] Diagram và văn bản không mâu thuẫn.
- [ ] ID tham chiếu tồn tại.
- [ ] Không còn placeholder chưa xử lý trong bản Approved.

---

# 24. Completion Criteria

SRS có thể sẵn sàng cho review hoặc approval khi:

- Scope đã được xác nhận.
- Users, Actors và External Systems đã được xác định.
- Functional Requirements quan trọng đã đầy đủ.
- Business Rules đã được quản lý nhất quán.
- Data và Interface Requirements đã được xác định.
- Non-functional Requirements có tiêu chí đo.
- States, errors và edge cases quan trọng đã được xem xét.
- Verification Method đã được gán.
- Traceability đã được thiết lập.
- Open Question quan trọng đã được giải quyết hoặc có kế hoạch xử lý.
- Không còn mâu thuẫn nghiêm trọng.
- Review Checklist đã được thực hiện.
- Version và Status đã được cập nhật.

---

# 25. Supporting Artifacts

SRS có thể tham chiếu:

- Business Requirements Document.
- Product Brief.
- Business Rule Catalogue.
- Use Case Catalogue.
- Data Dictionary.
- Conceptual Data Model.
- Interface Specification.
- Access Control Matrix.
- Requirements Traceability Matrix.
- Test Specification.
- Architecture Document.
- Software Design Document.
- API Specification.
- UI/UX Design.
- Risk Register.
- Decision Log.

Việc tách artifact không làm giảm chất lượng SRS nếu:

- Reference rõ ràng.
- Traceability được duy trì.
- Các tài liệu không mâu thuẫn.
- Source of Truth được xác định.

---

# 26. Quan hệ giữa ba tài liệu Human

- [SRS-About] giải thích SRS và các khái niệm nền tảng.
- [SRS-Guide] hướng dẫn cách phân tích và viết từng phần.
- [SRS-Template] là mẫu sạch để nhân bản và điền cho một dự án cụ thể.

Ba tài liệu phải dùng cùng:

- Thuật ngữ.
- ID convention.
- Requirement structure.
- Verification method.
- Status convention.
