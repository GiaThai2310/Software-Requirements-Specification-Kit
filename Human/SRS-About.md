---
title: About SRS
aliases:
  - SRS Overview
  - Software Requirements Specification Overview
tags:
  - srs
  - requirements-engineering
  - software-documentation
status: completed
---

# About SRS

> Trang này cung cấp kiến thức nền tảng về Software Requirements Specification.
>
> Hướng dẫn viết chi tiết được trình bày tại [[SRS-Guide]].  
> Mẫu tài liệu dùng trực tiếp được trình bày tại [[SRS-Template]].

---

# 1. SRS là gì?

**SRS**, viết tắt của **Software Requirements Specification**, là tài liệu hoặc tập hợp nội dung đặc tả những gì phần mềm phải thực hiện và các điều kiện mà phần mềm phải đáp ứng.

SRS trả lời các câu hỏi chính:

- Phần mềm được xây dựng để hỗ trợ mục tiêu nào?
- Phạm vi của phần mềm là gì?
- Ai hoặc hệ thống nào tương tác với phần mềm?
- Phần mềm phải cung cấp những chức năng nào?
- Phần mềm phải tuân theo những quy tắc nào?
- Phần mềm phải quản lý và trao đổi dữ liệu nào?
- Phần mềm phải đạt các đặc tính chất lượng nào?
- Làm thế nào để xác minh rằng requirement đã được đáp ứng?

SRS tập trung vào:

> Phần mềm phải làm gì và phải đáp ứng điều kiện nào?

SRS không nên tập trung vào cách lập trình hoặc cách tổ chức source code, trừ khi một công nghệ, kiến trúc hoặc phương pháp triển khai là ràng buộc bắt buộc đã được phê duyệt.

---

# 2. SRS dùng để làm gì?

## 2.1 Thống nhất yêu cầu

SRS tạo ra một nguồn thông tin chung để các bên cùng hiểu:

- Mục tiêu của phần mềm.
- Phạm vi thực hiện.
- Các chức năng cần có.
- Các quy tắc phải tuân theo.
- Các giới hạn và giả định.
- Các điều kiện dùng để đánh giá kết quả.

---

## 2.2 Kiểm soát phạm vi

SRS giúp phân biệt:

- Nội dung thuộc phạm vi.
- Nội dung nằm ngoài phạm vi.
- Nội dung được hoãn sang phiên bản khác.
- Nội dung chưa được xác nhận.
- Nội dung phụ thuộc vào quyết định hoặc hệ thống bên ngoài.

---

## 2.3 Làm đầu vào cho thiết kế và phát triển

SRS giúp nhóm kỹ thuật xác định:

- Các capability cần triển khai.
- Các hành vi phần mềm phải cung cấp.
- Dữ liệu cần xử lý.
- Interface cần hỗ trợ.
- Business rule cần thực thi.
- Constraint cần tuân thủ.

SRS không thay thế tài liệu thiết kế. Nó cung cấp căn cứ để thiết kế được tạo ra.

---

## 2.4 Làm đầu vào cho kiểm thử và xác minh

Requirement trong SRS phải đủ rõ để xác định:

- Điều kiện kiểm thử.
- Dữ liệu đầu vào.
- Kết quả mong đợi.
- Trường hợp lỗi.
- Giá trị biên.
- Phương pháp xác minh.
- Bằng chứng nghiệm thu.

---

## 2.5 Hỗ trợ nghiệm thu

SRS là căn cứ để đánh giá:

- Chức năng đã được triển khai chưa.
- Business rule đã được thực thi đúng chưa.
- Non-functional requirement đã đạt chưa.
- Điều kiện nghiệm thu đã được đáp ứng chưa.

---

## 2.6 Hỗ trợ bảo trì và thay đổi

SRS giúp người tham gia sau này hiểu:

- Vì sao requirement tồn tại.
- Requirement đến từ nguồn nào.
- Thành phần nào chịu ảnh hưởng khi requirement thay đổi.
- Requirement nào đã được thay thế hoặc loại bỏ.
- Phiên bản nào đang có hiệu lực.

---

# 3. SRS thường chứa những gì?

Một SRS thường xem xét các nhóm nội dung sau:

1. Document Control.
2. Introduction.
3. Scope.
4. Overall Description.
5. Users, Actors và External Systems.
6. Functional Requirements.
7. Required States and Modes.
8. Data Requirements.
9. Interface Requirements.
10. Performance and Timing Requirements.
11. Security and Privacy Requirements.
12. Software Quality Requirements.
13. Design and Implementation Constraints.
14. Verification và Acceptance Criteria.
15. Requirements Traceability.
16. Supporting Diagrams và Glossary.

Các nội dung sau có thể được đặt trong SRS hoặc tách thành tài liệu hỗ trợ:

- Business Context.
- Business Goals.
- Use Case Specifications.
- Business Rule Catalogue.
- Open Questions.
- Decision Log.
- Risk Register.
- Detailed Data Dictionary.
- Access Control Matrix.

Không phải dự án nào cũng cần mọi phần. Cấu trúc SRS phải được điều chỉnh theo:

- Quy mô.
- Mức độ rủi ro.
- Loại sản phẩm.
- Môi trường vận hành.
- Quy định của tổ chức.
- Yêu cầu pháp lý.
- Mục đích sử dụng tài liệu.

---

# 4. Functional Requirement là gì?

**Functional Requirement** mô tả hành vi hoặc chức năng mà phần mềm bắt buộc phải cung cấp.

Một Functional Requirement tốt cần xác định khi phù hợp:

- Chủ thể chịu nghĩa vụ.
- Hành vi bắt buộc.
- Điều kiện áp dụng.
- Trigger.
- Input.
- Output.
- Validation.
- Trạng thái bị thay đổi.
- Phản hồi khi thất bại.
- Business Rule liên quan.
- Phương pháp xác minh.

Một cấu trúc câu thường dùng:

> Hệ thống phải `<hành vi bắt buộc>` khi `<điều kiện áp dụng>`.

Mỗi Functional Requirement nên chỉ chứa một nghĩa vụ chính.

---

# 5. Use Case là gì?

**Use Case** mô tả một mục tiêu hoàn chỉnh mà actor đạt được thông qua tương tác với hệ thống.

Một Use Case thường có:

- Use Case ID.
- Goal.
- Primary Actor.
- Supporting Actors.
- Trigger.
- Preconditions.
- Main Flow.
- Alternative Flows.
- Exception Flows.
- Postconditions.
- Related Business Rules.
- Related Requirements.

Use Case và Functional Requirement không giống nhau:

- Use Case mô tả luồng tương tác để đạt một mục tiêu.
- Functional Requirement mô tả một nghĩa vụ cụ thể của phần mềm.
- Một Use Case có thể liên quan đến nhiều Functional Requirement.
- Một Functional Requirement có thể được sử dụng trong nhiều Use Case.

---

# 6. Non-functional Requirement là gì?

**Non-functional Requirement** mô tả đặc tính chất lượng, giới hạn hoặc điều kiện vận hành mà phần mềm phải đáp ứng.

Các nhóm thường được xem xét:

- Performance.
- Availability.
- Reliability.
- Security.
- Privacy.
- Usability.
- Accessibility.
- Maintainability.
- Compatibility.
- Portability.
- Scalability.
- Logging and Auditing.
- Backup and Recovery.
- Compliance.

Non-functional Requirement phải có tiêu chí đo hoặc điều kiện xác minh rõ ràng.

Không nên chỉ dùng các từ định tính như:

- Nhanh.
- Ổn định.
- An toàn.
- Dễ sử dụng.
- Linh hoạt.
- Có khả năng mở rộng tốt.

---

# 7. Business Rule là gì?

**Business Rule** là quy tắc nghiệp vụ mà hệ thống hoặc quy trình phải tuân theo.

Business Rule có thể:

- Áp dụng cho nhiều Use Case.
- Chi phối nhiều Functional Requirement.
- Xác định điều kiện hợp lệ.
- Xác định cách tính toán.
- Xác định quyền hoặc điều kiện đủ.
- Xác định giới hạn thời gian.
- Xác định quy tắc chuyển trạng thái.
- Xác định ngoại lệ.

Business Rule nên có ID riêng và được requirement tham chiếu thay vì lặp lại toàn bộ nội dung ở nhiều nơi.

---

# 8. Requirement khác Business Rule như thế nào?

| Thành phần | Câu hỏi chính |
|---|---|
| Requirement | Phần mềm phải cung cấp hành vi hoặc đặc tính gì? |
| Business Rule | Quy tắc nào chi phối hành vi hoặc quyết định nghiệp vụ? |
| Use Case | Actor đạt mục tiêu thông qua luồng tương tác nào? |
| Acceptance Criteria | Điều kiện nào chứng minh requirement đã đạt? |
| Verification Method | Requirement sẽ được xác minh bằng cách nào? |

---

# 9. Đặc điểm của một Requirement tốt

## 9.1 Necessary

Requirement thực sự cần thiết để đáp ứng need, policy, constraint hoặc higher-level requirement.

## 9.2 Correct

Requirement phản ánh đúng nguồn và nhu cầu đã được xác nhận.

## 9.3 Appropriate

Mức độ chi tiết phù hợp với cấp phần mềm đang được đặc tả.

## 9.4 Singular

Requirement chỉ chứa một nghĩa vụ chính.

## 9.5 Clear

Câu văn rõ ràng, thuật ngữ nhất quán và chủ thể được xác định.

## 9.6 Unambiguous

Requirement chỉ cho phép một cách diễn giải hợp lý.

## 9.7 Complete

Có đủ hành vi, điều kiện, kết quả và constraint cần thiết.

## 9.8 Consistent

Không mâu thuẫn với requirement, rule, diagram hoặc dữ liệu khác.

## 9.9 Feasible

Có thể triển khai trong giới hạn kỹ thuật, thời gian, chi phí và quy định áp dụng.

## 9.10 Verifiable

Có thể xác định khách quan rằng requirement đã được đáp ứng.

## 9.11 Traceable

Có thể truy vết tới nguồn và tới bằng chứng xác minh.

## 9.12 Prioritized

Có mức độ ưu tiên hoặc criticality rõ ràng khi dự án cần quản lý phạm vi.

---

# 10. Cách viết Requirement

Một requirement nên có các thuộc tính cơ bản:

```text
ID
Name
Statement
Type
Source
Rationale
Priority
Verification Method
Status
Dependencies
Traceability
```

Các thuộc tính bổ sung có thể bao gồm:

```text
Actors
Preconditions
Trigger
Inputs
Outputs
Error Conditions
Postconditions
Related Business Rules
Acceptance Criteria
```

Không phải mọi thuộc tính đều cần xuất hiện trong mỗi câu requirement. Chúng có thể được quản lý bằng bảng hoặc công cụ Requirements Management.

---

# 11. Verification và Acceptance Criteria

## 11.1 Verification Method

Các phương pháp thường dùng:

- **Test:** thực thi phần mềm trong điều kiện xác định.
- **Analysis:** sử dụng tính toán, mô hình hoặc phân tích.
- **Inspection:** kiểm tra tài liệu, cấu hình, code hoặc artifact.
- **Demonstration:** quan sát phần mềm thực hiện hành vi.

## 11.2 Acceptance Criteria

Acceptance Criteria mô tả điều kiện để requirement được chấp nhận.

Có thể tổ chức theo:

- Given.
- When.
- Then.

Acceptance Criteria không thay thế Requirement Statement.

---

# 12. Traceability là gì?

Traceability là khả năng theo dõi requirement theo hai hướng.

## 12.1 Backward Traceability

Giúp xác định:

- Requirement đến từ đâu.
- Need, policy hoặc stakeholder nào tạo ra requirement.
- Higher-level requirement nào được phân bổ xuống.

## 12.2 Forward Traceability

Giúp xác định:

- Requirement được thiết kế ở đâu.
- Requirement được triển khai ở đâu.
- Requirement được xác minh bằng artifact nào.
- Requirement thuộc release nào.

---

# 13. SRS khác các tài liệu khác như thế nào?

| Document | Câu hỏi chính |
|---|---|
| Business Requirements Document | Tại sao dự án cần được thực hiện? |
| Software Requirements Specification | Phần mềm phải làm gì và đáp ứng điều kiện nào? |
| Software Architecture Document | Hệ thống được tổ chức ở mức kiến trúc như thế nào? |
| Software Design Document | Phần mềm sẽ được thiết kế chi tiết như thế nào? |
| API Specification | Các hệ thống giao tiếp qua interface nào và theo contract nào? |
| Database Design Document | Dữ liệu được tổ chức vật lý như thế nào? |
| Test Plan | Hoạt động kiểm thử được tổ chức như thế nào? |
| Test Specification | Requirement được kiểm thử bằng test case nào? |
| Deployment Guide | Phần mềm được cài đặt và triển khai như thế nào? |
| User Manual | Người dùng sử dụng phần mềm như thế nào? |

---

# 14. SRS không phải là gì?

SRS không phải là:

- Tài liệu thiết kế kiến trúc chi tiết.
- Tài liệu thiết kế database vật lý.
- Danh sách endpoint hoàn chỉnh.
- Source code documentation.
- Test case document.
- Product roadmap.
- Sprint backlog.
- Deployment guide.
- User manual.

SRS có thể tham chiếu các tài liệu trên nhưng không nên thay thế toàn bộ chúng.

---

# 15. Những lỗi thường gặp

## 15.1 Trộn requirement với implementation

Requirement mô tả hành vi hoặc constraint bắt buộc, không mô tả solution không cần thiết.

## 15.2 Viết requirement không đo được

Các mục tiêu định tính phải được chuyển thành điều kiện hoặc tiêu chí xác minh.

## 15.3 Gộp nhiều nghĩa vụ vào một requirement

Requirement không atomic gây khó khăn cho truy vết, triển khai và kiểm thử.

## 15.4 Chỉ mô tả happy path

Cần xem xét invalid input, failure, conflict, timeout, dependency unavailable và partial processing.

## 15.5 Lặp Business Rule

Lặp rule ở nhiều nơi làm tăng nguy cơ không đồng bộ.

## 15.6 Không ghi nguồn

Requirement không có nguồn khó được xác nhận và quản lý thay đổi.

## 15.7 Không quản lý phiên bản

Thay đổi không có lịch sử khiến các bên sử dụng nhầm requirement cũ.

## 15.8 Mô tả thiết kế dữ liệu quá sớm

SRS nên tập trung vào Data Requirement ở mức conceptual hoặc logical.

## 15.9 Không có Verification Method

Requirement không có cách xác minh rõ ràng chưa đủ chất lượng.

## 15.10 Không duy trì Traceability

Thiếu traceability làm khó đánh giá impact khi thay đổi.

---

# 16. Checklist kiểm tra nhanh

## Scope

- [ ] Purpose và Scope đã rõ.
- [ ] In Scope và Out of Scope đã được xác định.
- [ ] System boundary đã rõ.
- [ ] Users, Actors và External Systems đã được nhận diện.

## Requirements

- [ ] Mỗi requirement có ID.
- [ ] Mỗi requirement chỉ chứa một nghĩa vụ chính.
- [ ] Requirement có source.
- [ ] Requirement rõ ràng và đơn nghĩa.
- [ ] Requirement khả thi.
- [ ] Requirement có thể xác minh.
- [ ] Requirement không chứa implementation không cần thiết.

## Coverage

- [ ] Functional Requirements đã được xem xét.
- [ ] States and Modes đã được xem xét.
- [ ] Data Requirements đã được xem xét.
- [ ] Interface Requirements đã được xem xét.
- [ ] Non-functional Requirements đã được xem xét.
- [ ] Security và Privacy đã được xem xét.
- [ ] Error Conditions đã được xem xét.

## Traceability

- [ ] Requirement truy vết được về source.
- [ ] Requirement liên kết với Verification Method.
- [ ] Business Rule được tham chiếu nhất quán.
- [ ] Diagram và nội dung chữ không mâu thuẫn.

## Completion

- [ ] Không còn placeholder chưa xử lý trong bản phê duyệt.
- [ ] Assumption và Open Question đã được xử lý hoặc theo dõi.
- [ ] Revision History đã được cập nhật.
- [ ] Stakeholder liên quan đã review.
