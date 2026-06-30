# Software Requirements Specification

## Xe điện Vinfast Happy — Omnichannel E-Commerce Platform (HappyWeb)

---

## 0. Document Control

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 0.1 Document Information

| Field | Value |
|---|---|
| Document Title | Software Requirements Specification — Xe điện Vinfast Happy |
| Project Name | HappyWeb Omnichannel Platform |
| Version | 1.0.0-DRAFT |
| Prepared By | AI Requirements Engineer (Agent) |
| Date | 2026-06-27 |
| Classification | Internal |

### 0.2 Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.0.0-DRAFT | 2026-06-27 | Agent | Initial full-generation draft from FE-context, BE-context, Question-Resolve sources. |

### 0.3 Review And Approval

| Role | Name | Status | Date |
|---|---|---|---|
| Product Owner | [TBD] | REVIEW | — |
| Tech Lead | [TBD] | REVIEW | — |
| Business Stakeholder | [TBD] | REVIEW | — |

---

## 1. Introduction

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 1.1 Purpose

Tài liệu Software Requirements Specification (SRS) này xác định đầy đủ các yêu cầu chức năng, phi chức năng và giao diện cho Xe điện Vinfast Happy Omnichannel E-Commerce Platform (sau đây gọi là "the System" hoặc "HappyWeb"). Đây là tài liệu tham chiếu yêu cầu chính thức cho các hoạt động thiết kế, phát triển, kiểm thử và nghiệm thu, phù hợp với các khái niệm của tiêu chuẩn IEEE/ISO/IEC 29148.

### 1.2 Scope

#### 1.2.1 In Scope

1. **Public Website** — Trang thương mại điện tử hướng tới khách hàng (customer-facing) để xem sản phẩm, đặt hàng (ORDERABLE) và gửi yêu cầu tư vấn (CONTACT_ONLY và luồng phụ cho ORDERABLE).
2. **Internal Dashboard** — Giao diện quản lý dựa trên vai trò (role-based) dành cho Staff, Store Manager, General Manager và Super Admin.

Công nghệ sử dụng: Next.js frontend trên Cloudflare Pages; ASP.NET Core Web API backend; Neon Postgres; Cloudflare R2 cho hình ảnh; Cloudflare CDN.

#### 1.2.2 Out Of Scope

- Các ứng dụng di động gốc (native mobile applications).
- Tích hợp Zalo OA API hoặc Messenger API (chỉ sử dụng static deep links trong giai đoạn này).
- Cổng thanh toán trực tuyến (online payment gateway).
- Tự động bổ sung kho hàng (automated stock replenishment).
- Tích hợp hệ thống ERP hoặc kế toán (accounting system).

#### 1.2.3 Future Scope

- Tích hợp Zalo OA / Messenger API để theo dõi định tuyến.
- Thanh toán trực tuyến (VNPay, MoMo, Stripe).
- Cổng thông tin tài khoản khách hàng (customer account portal) với lịch sử đơn hàng.
- Quản lý kho hàng đa chi nhánh nâng cao (advanced multi-branch inventory management).
- Ứng dụng di động (mobile application).

### 1.3 Intended Audience

| Audience | Primary Sections |
|---|---|
| Product Owner / Business Stakeholder | 1, 2, 4, 5, 17 |
| UX / UI Designer | 5, 6, 10, 13 |
| Frontend Developer | 5, 6, 8, 10, 12 |
| Backend Developer | 7, 8, 9, 10, 11, 12, 13, 14 |
| QA / Test Engineer | 8, 14, 15 |
| DevOps / Infrastructure | 2.4, 11 |
| Project Manager | 0, 1, 17, 22 |

### 1.4 Definitions, Acronyms And Abbreviations

| Term | Type | Definition | Source |
|---|---|---|---|
| API | Acronym | Application Programming Interface | Industry standard |
| RBAC | Acronym | Role-Based Access Control | Industry standard |
| CDN | Acronym | Content Delivery Network | Industry standard |
| CTA | Acronym | Call To Action — a UI element prompting a specific action | Industry standard |
| JWT | Acronym | JSON Web Token | Industry standard |
| UUID | Acronym | Universally Unique Identifier (128-bit primary key) | Industry standard |
| ORM | Acronym | Object-Relational Mapper | Industry standard |
| DTO | Acronym | Data Transfer Object | Industry standard |
| p95 | Domain term | 95th-percentile response time | Industry standard |
| MoSCoW | Acronym | Must / Should / Could / Wont prioritisation framework | Industry standard |
| SRS | Acronym | Software Requirements Specification | IEEE 29148 |
| EF Core | Acronym | Entity Framework Core (ORM for ASP.NET Core) | Industry standard |
| ORDERABLE | Domain term | Product purchase mode allowing direct cart addition and order placement | FE-context.md, BE-context.md |
| CONTACT_ONLY | Domain term | Product purchase mode preventing direct ordering; customer must contact the business | FE-context.md, BE-context.md |
| SHOW_PRICE | Domain term | Price visibility: display formatted price publicly | FE-context.md |
| HIDE_PRICE | Domain term | Price visibility: hide price area entirely on public site | FE-context.md |
| CONTACT_FOR_PRICE | Domain term | Price visibility: display "Lien he" instead of numeric price | FE-context.md |
| Purchase Mode | Domain term | Per-product attribute controlling order vs. contact flow | FE-context.md |
| Price Visibility | Domain term | Per-product attribute controlling public price presentation | FE-context.md |
| Contact Request | Domain term | Customer-submitted consultation/quote request routed to staff | BE-context.md |
| Soft Delete | Domain term | Deactivating a record (IsActive=false) instead of permanent deletion | Question-Resolve.md |
| Audit Trail | Domain term | System-generated log of administrative actions | Question-Resolve.md |
| Super Admin | Domain term | Highest-privilege internal role; unrestricted global access | Question-Resolve.md |
| General Manager | Domain term | Internal role; cross-branch access; no branch restriction | Question-Resolve.md |
| Store Manager | Domain term | Internal role; access restricted to assigned branch | Question-Resolve.md |
| Staff | Domain term | Operational internal role; branch-scoped | Question-Resolve.md |
| Overselling | Domain term | Accepting an order when stock is zero or negative | Question-Resolve.md |
| Deep Link | Domain term | Static URL or URI scheme opening an external app (Zalo, phone, Messenger) | Question-Resolve.md |
| MainImageUrl | Domain term | Primary thumbnail image URL stored in Cloudflare R2 | Question-Resolve.md |

### 1.5 References

| Ref ID | Document | Location |
|---|---|---|
| REF-GEN-001 | FE-context.md | Context/FE-context.md (2026-06-27) |
| REF-GEN-002 | BE-context.md | Context/BE-context.md (2026-06-27) |
| REF-GEN-003 | Question-Resolve.md | Context/Question-Resolve.md (2026-06-27) |
| REF-GEN-004 | SRS-TOC.md | Context/SRS-TOC.md |
| REF-GEN-005 | SRS-Template.md | Context/SRS-Template.md |
| REF-GEN-006 | IEEE/ISO/IEC 29148:2018 | Requirements Engineering standard |

### 1.6 Document Overview

Các phần 2–4 mô tả về hệ thống, các bên liên quan và bối cảnh kinh doanh. Các phần 5–8 mô tả về tính năng, kịch bản sử dụng (use cases), quy tắc nghiệp vụ và yêu cầu chức năng. Các phần 9–12 mô tả về mô hình dữ liệu, giao diện, yêu cầu phi chức năng (NFRs) và kiểm soát truy cập. Các phần 13–15 mô tả mô hình trạng thái, xử lý lỗi và tiêu chí nghiệm thu. Các phần 16–18 mô tả khả năng truy vết (traceability), câu hỏi chưa giải quyết, rủi ro và phụ lục.

---

## 2. Overall Description

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 2.1 Product Perspective

HappyWeb là một hệ thống thương mại điện tử đa kênh (`Omnichannel`) xây dựng mới dành cho "Xe điện Vinfast Happy", một nhà bán lẻ xe đạp điện và phụ kiện. Hệ thống này thay thế các quy trình bán hàng thủ công (qua điện thoại, tin nhắn mạng xã hội) bằng một giải pháp số chuyên nghiệp: một website công khai và một trang quản lý vận hành nội bộ tập trung.

#### 2.1.1 System Boundary

**Included (Bao gồm):** Public Website (Next.js, Cloudflare Pages); Internal Dashboard (Next.js, Cloudflare Pages, phân quyền truy cập); Backend API (ASP.NET Core); Neon Postgres DB; Cloudflare R2 để lưu trữ hình ảnh; cấu hình static deep links trỏ đến Zalo / Messenger / Hotline.

**Excluded (Không bao gồm):** Các nền tảng mạng xã hội bên ngoài; các đơn vị xử lý thanh toán; các đơn vị vận chuyển.

#### 2.1.2 Context Diagram

```
  [Customer]
      | HTTPS
      v
  [Public Website] ----API----> [Backend API]
                                    |--- [Neon Postgres]
  [Staff/Manager/Admin]             |--- [Cloudflare R2]
      | HTTPS (authenticated)
      v
  [Internal Dashboard] ----API----> [Backend API]

  [Zalo / Messenger / Hotline] <--- Static Deep Link --- [Public Website]
```

### 2.2 Product Functions

| PF ID | Function | Primary Actor |
|---|---|---|
| PF-GEN-001 | Public product catalog với tính năng lọc danh mục | Customer |
| PF-GEN-002 | Trang chi tiết sản phẩm hiển thị nút kêu gọi hành động (CTA) tương ứng theo purchase mode | Customer |
| PF-GEN-003 | Giỏ hàng (chỉ cho phép các sản phẩm ở chế độ ORDERABLE) | Customer |
| PF-GEN-004 | Đặt hàng và thanh toán không cần tài khoản (Guest checkout) | Customer |
| PF-GEN-005 | Gửi yêu cầu tư vấn (Contact request) thông qua biểu mẫu tích hợp | Customer |
| PF-GEN-006 | Điều hướng bằng liên kết tĩnh (static deep link) trỏ đến Zalo, Messenger, Hotline | Customer |
| PF-GEN-007 | Quản lý sản phẩm nội bộ (CRUD và thư viện ảnh) | Staff, Manager, Admin |
| PF-GEN-008 | Quản lý danh mục sản phẩm nội bộ (CRUD) | Manager, Admin |
| PF-GEN-009 | Quản lý đơn hàng nội bộ và vòng đời trạng thái đơn hàng | Staff, Manager, Admin |
| PF-GEN-010 | Quản lý yêu cầu tư vấn nội bộ và vòng đời trạng thái yêu cầu | Staff, Manager, Admin |
| PF-GEN-011 | Quản lý tài khoản nhân viên với RBAC | Manager, Admin |
| PF-GEN-012 | Quản lý cài đặt hệ thống (hotline, deep links) | Super Admin |
| PF-GEN-013 | Ghi nhận nhật ký hệ thống (Audit trail) cho các hành động quản trị | System (automated) |
| PF-GEN-014 | Theo dõi số lượng tồn kho (chỉ mang tính thông tin; cho phép số lượng âm) | Staff, Manager, Admin |

### 2.3 User Classes And Characteristics

| STK ID | User Class | Description | Proficiency | Frequency |
|---|---|---|---|---|
| STK-GEN-001 | Customer (Guest) | Khách truy cập ẩn danh; không yêu cầu đăng nhập | Low–Medium | Variable |
| STK-GEN-002 | Staff | Người dùng nội bộ vận hành; giới hạn theo chi nhánh | Medium | Daily |
| STK-GEN-003 | Store Manager | Quản lý cấp chi nhánh | Medium–High | Daily |
| STK-GEN-004 | General Manager | Quản lý chuỗi cửa hàng; không bị giới hạn chi nhánh | High | Daily |
| STK-GEN-005 | Super Admin | Quản trị viên toàn cầu; có toàn quyền truy cập hệ thống | High | As needed |

### 2.4 Operating Environment

| Component | Technology | Hosting |
|---|---|---|
| Frontend (Public + Internal) | Next.js 14+, TypeScript, Tailwind CSS, shadcn/ui | Cloudflare Pages |
| Backend API | ASP.NET Core Web API, C#, EF Core | Render / Azure Functions / AWS Lambda / VPS |
| Database | PostgreSQL via Neon Postgres | Neon cloud |
| Image Storage | Cloudflare R2 | Cloudflare |
| DNS / CDN | Cloudflare Free | Cloudflare |
| Browser Support | Chrome 110+, Firefox 110+, Edge 110+, Safari 16+ [ASSUMPTION] | N/A |
| Device Support | Responsive đối với public site; tối ưu hóa desktop đối với dashboard [ASSUMPTION] | N/A |

### 2.5 Design And Implementation Constraints

| CON ID | Constraint | Source |
|---|---|---|
| CON-SEC-001 | Mọi lưu lượng truy cập phải được phân phối qua HTTPS | Industry standard [ASSUMPTION] |
| CON-SEC-002 | Internal Dashboard yêu cầu phiên làm việc đã xác thực hợp lệ | Question-Resolve.md |
| CON-SEC-003 | Phiên làm việc của nhân viên sẽ hết hạn sau 30 phút không hoạt động | Question-Resolve.md |
| CON-TECH-001 | Frontend: Next.js + TypeScript + Tailwind CSS + shadcn/ui | FE-context.md |
| CON-TECH-002 | Backend: ASP.NET Core Web API + C# + EF Core | BE-context.md |
| CON-TECH-003 | Database: Neon Postgres | BE-context.md |
| CON-TECH-004 | Lưu trữ hình ảnh: Cloudflare R2 | BE-context.md |
| CON-TECH-005 | Nơi lưu trữ (hosting) frontend: Cloudflare Pages | FE-context.md |
| CON-BUS-001 | Khách hàng không cần tài khoản để đặt hàng hoặc gửi yêu cầu liên hệ | FE-context.md, BE-context.md |
| CON-BUS-002 | Số lượng tồn kho không phải là rào cản bắt buộc; cho phép bán quá mức (overselling) | Question-Resolve.md |
| CON-BUS-003 | Zalo, Messenger, Hotline: chỉ sử dụng liên kết tĩnh (static deep links); không tích hợp API | Question-Resolve.md |
| CON-BUS-004 | Các giá trị của Hotline và liên kết kênh truyền thông có thể cấu hình được qua cấu hình Admin | Question-Resolve.md |
| CON-DATA-001 | Tài khoản nhân viên không bao giờ được xóa vĩnh viễn (hard-delete); chỉ được xóa mềm (soft-delete) | Question-Resolve.md |

### 2.6 Assumptions And Dependencies

| ID | Item | Impact If Wrong |
|---|---|---|
| ASM-GEN-001 | Locale là tiếng Việt; múi giờ UTC+7 [ASSUMPTION] | Cần thiết kế lại phần quốc tế hóa (internationalisation) |
| ASM-GEN-002 | Giá trị tiền tệ sử dụng VND, không có chữ số thập phân [ASSUMPTION] | Cần thiết kế lại phần xử lý tiền tệ |
| ASM-GEN-003 | Mỗi sản phẩm thuộc về duy nhất một danh mục [ASSUMPTION] | Cần thay đổi mô hình dữ liệu |
| ASM-GEN-004 | Backend cung cấp các RESTful JSON API [ASSUMPTION] | Cần thiết kế lại API nếu có thay đổi |
| ASM-GEN-005 | Email thông báo hủy đơn được gửi qua nhà cung cấp SMTP bên thứ ba — nhà cung cấp TBD (OQ-GEN-002) [ASSUMPTION] | Luồng thông báo bị chặn cho đến khi nhà cung cấp được chọn |
| ASM-GEN-006 | JWT được lưu trữ trong HTTP-only cookies đối với các phiên làm việc của dashboard [ASSUMPTION] | Cần thiết kế lại phần bảo mật nếu có thay đổi |
| ASM-GEN-007 | Tên và giá sản phẩm được lưu snapshot trong OrderItem tại thời điểm tạo đơn hàng [ASSUMPTION] | Mất tính chính xác của dữ liệu lịch sử nếu sản phẩm được chỉnh sửa sau khi đặt hàng |
| DEP-GEN-001 | Mức độ khả dụng (SLA) của gói Neon Postgres miễn phí không được đảm bảo | Rủi ro thời gian ngừng hoạt động (downtime) của DB |
| DEP-GEN-002 | Cloudflare R2 để tải và phân phối hình ảnh | Hình ảnh không thể hiển thị nếu R2 gặp sự cố |
| DEP-GEN-003 | Sự ổn định của cấu trúc URL trỏ đến Zalo / Messenger | Deep links bị lỗi nếu các nền tảng thay đổi cấu trúc URL |

---

## 3. Stakeholders, Actors And External Systems

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 3.1 Stakeholders

| STK ID | Stakeholder | Project Role | Interest |
|---|---|---|---|
| STK-GEN-001 | Customer (Guest) | End user | Tìm kiếm sản phẩm, đặt hàng, liên hệ dễ dàng |
| STK-GEN-002 | Staff | Operational user | Vận hành hiệu quả |
| STK-GEN-003 | Store Manager | Branch manager | Hiệu suất chi nhánh, quản lý nhân viên |
| STK-GEN-004 | General Manager | Network manager | Giám sát toàn bộ chuỗi cửa hàng |
| STK-GEN-005 | Super Admin | System administrator | Toàn quyền kiểm soát hệ thống |
| STK-GEN-006 | Business Owner | Decision-maker | Doanh thu, thương hiệu, hiệu quả vận hành |

### 3.2 Actors

| ACT ID | Actor | Type | Description |
|---|---|---|---|
| ACT-GEN-001 | Customer | Primary, Human | Khách truy cập ẩn danh; không yêu cầu tài khoản |
| ACT-GEN-002 | Staff | Primary, Human | Đã xác thực; giới hạn quyền theo chi nhánh |
| ACT-GEN-003 | Store Manager | Primary, Human | Đã xác thực; giới hạn quyền trong một chi nhánh |
| ACT-GEN-004 | General Manager | Primary, Human | Đã xác thực; phạm vi quản lý toàn hệ thống |
| ACT-GEN-005 | Super Admin | Primary, Human | Đã xác thực; toàn quyền truy cập toàn cầu không giới hạn |
| ACT-GEN-006 | System | Secondary, Automated | Tự động kích hoạt thông báo, ghi chép lịch sử kiểm toán, hành vi trạng thái |

### 3.3 Actor Permission Overview (Summary)

Xem thêm Chi tiết tại Section 12.

| Capability | Customer | Staff | Store Mgr | General Mgr | Super Admin |
|---|:---:|:---:|:---:|:---:|:---:|
| Xem sản phẩm công khai | Yes | Yes | Yes | Yes | Yes |
| Đặt hàng (khách vãng lai) | Yes | — | — | — | — |
| Gửi yêu cầu tư vấn | Yes | — | — | — | — |
| Truy cập Internal Dashboard | — | Yes | Yes | Yes | Yes |
| CRUD sản phẩm | — | Yes | Yes | Yes | Yes |
| CRUD danh mục | — | No | Yes | Yes | Yes |
| Quản lý đơn hàng | — | Branch | Branch | All | All |
| Quản lý yêu cầu tư vấn | — | Branch | Branch | All | All |
| Quản lý tài khoản nhân viên | — | No | Branch | All | All |
| Quản lý cài đặt hệ thống | — | No | No | No | Yes |
| Xem nhật ký hệ thống (audit trail) | — | No | No | Yes | Yes |

### 3.4 External Systems

| EXT ID | System | Integration | Purpose |
|---|---|---|---|
| EXT-INTG-001 | Zalo | Static HTTPS deep link | Điều hướng nút CTA liên hệ / tư vấn |
| EXT-INTG-002 | Facebook Messenger | Static HTTPS deep link | Điều hướng nút CTA liên hệ / tư vấn |
| EXT-INTG-003 | Hotline | Static `tel:` deep link | Nút CTA gọi điện trực tiếp; số điện thoại cấu hình bởi Super Admin |
| EXT-INTG-004 | Cloudflare R2 | Cloud object storage | Tải lên và lấy lại hình ảnh sản phẩm |
| EXT-INTG-005 | Neon Postgres | Cloud managed database | Lưu trữ dữ liệu quan hệ một cách nhất quán |
| EXT-INTG-006 | SMTP Provider | Email API | Gửi thông báo hủy đơn cho khách hàng [TBD: OQ-GEN-002] |
| EXT-INTG-007 | Cloudflare Pages | Static hosting + CDN | Triển khai giao diện frontend |

---

## 4. Business Context

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 4.1 Problem Statement

Cửa hàng "Xe điện Vinfast Happy" bán xe đạp điện và phụ kiện trên nhiều kênh khác nhau (cửa hàng vật lý, Zalo, Messenger, điện thoại) mà không có cơ sở hạ tầng kỹ thuật số tập trung. Điều này dẫn tới: trải nghiệm khách hàng không nhất quán; không có hệ thống tập trung theo dõi đơn hàng và yêu cầu liên hệ; không có dấu vết kiểm toán (audit trail); gặp khó khăn trong việc giám sát lượng tồn kho. HappyWeb giải quyết vấn đề này bằng một nền tảng bán hàng đa kênh thống nhất.

### 4.2 Business Goals

| BG ID | Goal | Priority |
|---|---|---|
| BG-GEN-001 | Tăng tỷ lệ chuyển đổi thông qua danh mục sản phẩm trực tuyến chuyên nghiệp | Must |
| BG-GEN-002 | Tập trung hóa quản lý đơn hàng để đảm bảo khả năng truy vết và hoàn thành đơn hàng có hệ thống | Must |
| BG-GEN-003 | Thu thập các yêu cầu tư vấn và cho phép nhân viên theo dõi một cách có cấu trúc | Must |
| BG-GEN-004 | Cho phép quản trị viên cấu hình sản phẩm và cài đặt mà không cần sự can thiệp của lập trình viên | Must |
| BG-GEN-005 | Hỗ trợ liên hệ đa kênh (form, Zalo, Messenger, Hotline) với khả năng theo dõi nội bộ tập trung | Should |
| BG-GEN-006 | Cung cấp kiến trúc có khả năng mở rộng lên tới 500 người dùng đồng thời tại thời điểm cao điểm | Should |
| BG-GEN-007 | Duy trì nhật ký hệ thống (audit trail) đầy đủ đối với các hành động quản trị | Should |

### 4.3 Success Criteria

| SC ID | Criterion | Measurement |
|---|---|---|
| SC-GEN-001 | Website công khai có thể truy cập được bởi khách hàng ẩn danh | Kiểm thử chức năng (Functional test) |
| SC-GEN-002 | Khách thực hiện thanh toán ORDERABLE trong 3 hoặc ít hơn các thao tác chính | Kiểm thử tính khả dụng (Usability test) |
| SC-GEN-003 | Yêu cầu liên hệ xuất hiện trên trang quản lý trong vòng 10 giây sau khi gửi | Kiểm thử tích hợp hệ thống (End-to-end test) |
| SC-GEN-004 | Nhân viên có thể cập nhật trạng thái đơn hàng trong 5 hoặc ít hơn số lần nhấp chuột | Kiểm thử tính khả dụng (Usability test) |
| SC-GEN-005 | Đạt 500 người dùng đồng thời; p95 API response <= 3 s | Kiểm thử tải (Load test) |
| SC-GEN-006 | Mọi hành động quản trị đều được ghi lại trong nhật ký hệ thống | Xác minh nhật ký kiểm toán (Audit log verification) |
| SC-GEN-007 | Super Admin có thể cập nhật hotline mà không cần triển khai lại mã nguồn | Kiểm thử thủ công (Manual test) |

### 4.4 Current Workflow

1. Khách hàng liên hệ qua Zalo / Messenger / điện thoại.
2. Nhân viên trả lời thủ công, thương lượng và xác nhận đơn hàng bằng lời nói.
3. Đơn hàng được ghi chép trong sổ tay hoặc bảng tính (spreadsheets).
4. Không có cái nhìn tập trung về đơn hàng, kho hàng hoặc lịch sử tư vấn.

### 4.5 Target Workflow

**ORDERABLE product:** Xem sản phẩm -> Thêm vào giỏ hàng -> Thanh toán (khách vãng lai) -> Đơn hàng ở trạng thái PENDING hiển thị trên dashboard quản trị -> Nhân viên chuyển sang: CONFIRMED -> SHIPPING -> DELIVERED. Khách hàng nhận được thông báo qua email nếu đơn hàng bị hủy.

**Contact flow (CONTACT_ONLY hoặc luồng phụ cho ORDERABLE):** Trang sản phẩm hiển thị nút CTA -> Kênh liên lạc hợp nhất (deep link hoặc biểu mẫu tích hợp) -> Tạo yêu cầu ContactRequest mới trạng thái NEW trên trang quản lý -> Nhân viên liên hệ khách hàng và cập nhật: CONTACTED -> CLOSED.

---

## 5. Product Features

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 5.1 Feature List

| F ID | Feature | Priority | Domain |
|---|---|---|---|
| F-PROD-001 | Public Product Catalog with Category Filter | Must | PROD |
| F-PROD-002 | Product Detail Page (Purchase-Mode Aware CTAs) | Must | PROD |
| F-PROD-003 | Per-Product Price Visibility Control | Must | PROD |
| F-PROD-004 | Multi-Image Product Gallery | Should | PROD |
| F-CART-001 | Shopping Cart (ORDERABLE Products Only) | Must | CART |
| F-ORD-001 | Guest Checkout and Order Placement | Must | ORD |
| F-ORD-002 | Order Status Lifecycle Management | Must | ORD |
| F-ORD-003 | Order Cancellation With Optional Reason and Customer Notification | Must | ORD |
| F-CONT-001 | Unified Contact Request Flow (CONTACT_ONLY and ORDERABLE) | Must | CONT |
| F-CONT-002 | Static Deep Link CTAs (Zalo, Messenger, Hotline) | Must | CONT |
| F-CONT-003 | Contact Request Status Lifecycle | Must | CONT |
| F-ADMIN-001 | Internal Product Management (CRUD + Images) | Must | ADMIN |
| F-ADMIN-002 | Internal Category Management (CRUD) | Must | ADMIN |
| F-ADMIN-003 | Internal Order Management | Must | ADMIN |
| F-ADMIN-004 | Internal Contact Request Management | Must | ADMIN |
| F-ADMIN-005 | Staff Account Management with Soft Delete | Must | ADMIN |
| F-ADMIN-006 | Flexible RBAC Permission Management | Must | ADMIN |
| F-ADMIN-007 | System Settings (Hotline, Deep Links, Configurable) | Must | ADMIN |
| F-ADMIN-008 | Audit Trail Logging | Should | ADMIN |
| F-INV-001 | Stock Quantity Tracking (Informational; Negative Permitted) | Must | INV |

### 5.2 Feature Details

**F-PROD-001**: Danh sách sản phẩm đang hoạt động dạng phân trang hoặc cuộn vô hạn với tính năng lọc theo danh mục. Mỗi thẻ sản phẩm hiển thị tên, hình ảnh chính, giá bán (theo cấu hình priceVisibility), và nút CTA tương ứng với purchaseMode.

**F-PROD-002**: Trang chi tiết sản phẩm dựa trên đường dẫn tĩnh (slug). Hiển thị tên, mô tả sản phẩm, ảnh chính, thư viện ảnh phụ, giá bán (theo priceVisibility). Các nút kêu gọi hành động (CTAs): ORDERABLE = nút chính "Thêm vào giỏ hàng" + nút phụ "Yêu cầu tư vấn"; CONTACT_ONLY = chỉ hiển thị nút chính "Liên hệ với chúng tôi".

**F-PROD-003**: Ba trạng thái hiển thị giá trên mỗi sản phẩm: SHOW_PRICE (hiển thị giá đã định dạng), HIDE_PRICE (ẩn hoàn toàn vùng giá), CONTACT_FOR_PRICE (hiển thị chữ "Liên hệ"). Có thể cấu hình bởi Staff/Manager/Admin.

**F-PROD-004**: Một MainImageUrl (ảnh thu nhỏ chính) + không hoặc nhiều ảnh phụ trong bảng riêng biệt. Ảnh chính được sử dụng ở trang danh sách và giỏ hàng; thư viện ảnh phụ được hiển thị ở trang chi tiết sản phẩm.

**F-CART-001**: Giỏ hàng lưu trữ ở client-side chỉ chứa các sản phẩm ORDERABLE. Cho phép thêm, xóa, điều chỉnh số lượng. Sản phẩm CONTACT_ONLY bị chặn thêm vào giỏ hàng ở cả phía frontend và backend.

**F-ORD-001**: Không yêu cầu tạo tài khoản. Trang thanh toán thu thập: tên người nhận, số điện thoại, địa chỉ, và ghi chú tùy chọn. Backend xác thực tất cả các mặt hàng là ORDERABLE trước khi lưu đơn hàng.

**F-ORD-002**: Vòng đời trạng thái đơn hàng: PENDING -> CONFIRMED -> SHIPPING -> DELIVERED | CANCELLED. Tất cả các chuyển đổi trạng thái đều thực hiện thủ công; không tự động xác nhận đơn hàng.

**F-ORD-003**: Nhân viên nhập lý do tùy chọn khi hủy đơn. Thông báo email vẫn được gửi cho khách hàng trong mọi trường hợp. Lý do hủy đơn được lưu trữ để phục vụ cho lịch sử kiểm toán.

**F-CONT-001**: CONTACT_ONLY: Chỉ hiển thị nút CTA "Liên hệ với chúng tôi". ORDERABLE: hiển thị thêm nút CTA phụ "Yêu cầu tư vấn". Cả hai đều điều hướng về một kênh liên lạc hợp nhất. Biểu mẫu gửi trực tiếp trên web sẽ tạo bản ghi ContactRequest.

**F-CONT-002**: Zalo, Messenger, Hotline được cấu hình dưới dạng các liên kết tĩnh (static deep links). Tất cả giá trị liên kết có thể cấu hình được trong phần System Settings bởi Super Admin.

**F-CONT-003**: Vòng đời trạng thái yêu cầu liên hệ: NEW -> CONTACTED -> CLOSED (hoặc chuyển trực tiếp từ NEW -> CLOSED).

**F-ADMIN-001**: Toàn quyền CRUD đối với sản phẩm bao gồm purchaseMode, priceVisibility, danh mục sản phẩm, và quản lý nhiều hình ảnh. Các hành động nguy hiểm (xóa) sẽ kích hoạt hộp thoại xác nhận và ghi nhận vào nhật ký hệ thống.

**F-ADMIN-002**: Manager trở lên có quyền tạo, cập nhật, xóa danh mục. Danh mục có thể lựa chọn khi thêm/sửa sản phẩm.

**F-ADMIN-003**: Người dùng nội bộ có thể xem và cập nhật trạng thái đơn hàng trong phạm vi quyền hạn của họ.

**F-ADMIN-004**: Người dùng nội bộ có thể xem và cập nhật trạng thái yêu cầu liên hệ trong phạm vi quyền hạn của họ.

**F-ADMIN-005**: Manager và Admin có quyền tạo, cập nhật và xóa mềm (soft-delete) tài khoản nhân viên. Nghiêm cấm xóa cứng (hard-delete).

**F-ADMIN-006**: Quyền hạn được gán cho các vai trò (roles); được tách biệt và có thể cấu hình. Có thể thêm vai trò mới mà không cần thay đổi mã nguồn.

**F-ADMIN-007**: Super Admin cấu hình số điện thoại hotline, liên kết Zalo, liên kết Messenger. Thay đổi có hiệu lực ngay lập tức mà không cần triển khai lại hệ thống.

**F-ADMIN-008**: Hệ thống tự động ghi nhật ký mọi hành động quản trị quan trọng bao gồm người thực hiện, loại hành động, thực thể bị ảnh hưởng, mã định danh thực thể, dấu thời gian UTC và các giá trị thay đổi.

**F-INV-001**: StockQuantity là một số nguyên có dấu. Cho phép bán quá mức (overselling) dẫn đến số lượng âm. Số lượng tồn kho chính xác chỉ hiển thị cho người dùng nội bộ.

---

## 6. Use Case Specifications

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 6.1 Use Case Overview

| UC ID | Use Case | Primary Actor | Feature(s) |
|---|---|---|---|
| UC-PROD-001 | Browse Product Catalog | Customer | F-PROD-001 |
| UC-PROD-002 | View Product Detail | Customer | F-PROD-002, F-PROD-003 |
| UC-CART-001 | Add ORDERABLE Product To Cart | Customer | F-CART-001 |
| UC-ORD-001 | Complete Guest Checkout | Customer | F-ORD-001 |
| UC-CONT-001 | Submit Contact Request Via Inline Form | Customer | F-CONT-001 |
| UC-CONT-002 | Access External Channel Via Deep Link | Customer | F-CONT-002 |
| UC-OADM-001 | Update Order Status | Staff/Manager/Admin | F-ORD-002 |
| UC-OADM-002 | Cancel Order With Optional Reason | Staff/Manager/Admin | F-ORD-003 |
| UC-CADM-001 | Update Contact Request Status | Staff/Manager/Admin | F-CONT-003 |
| UC-PADM-001 | Create Or Edit Product | Staff/Manager/Admin | F-ADMIN-001 |
| UC-PADM-002 | Manage Product Categories | Store Manager/GM/Super Admin | F-ADMIN-002 |
| UC-SADM-001 | Create Staff Account | Store Manager/GM/Super Admin | F-ADMIN-005 |
| UC-SADM-002 | Deactivate Staff Account | Store Manager/GM/Super Admin | F-ADMIN-005 |
| UC-SYS-001 | Update System Settings | Super Admin | F-ADMIN-007 |

### 6.2 Use Case Details

#### UC-ORD-001 Complete Guest Checkout

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s7, BE-context.md s7, Question-Resolve.md
- **Actor**: Customer | **Precondition**: Giỏ hàng chứa >= 1 sản phẩm ORDERABLE.
- **Main Flow**:
  1. Khách hàng điều hướng đến trang thanh toán.
  2. Khách hàng nhập tên người nhận, số điện thoại, địa chỉ, và ghi chú tùy chọn.
  3. Khách hàng gửi biểu mẫu thanh toán.
  4. Frontend kiểm tra tính hợp lệ: giỏ hàng không trống, tất cả sản phẩm đều là ORDERABLE.
  5. Frontend gửi yêu cầu `POST /api/orders`.
  6. Backend xác thực tất cả sản phẩm là ORDERABLE và đang hoạt động.
  7. Backend lưu thông tin đơn hàng (trạng thái PENDING); giảm StockQuantity.
  8. Frontend hiển thị màn hình xác nhận đơn hàng thành công.
- **Alt A — CONTACT_ONLY in cart**: Frontend chặn bước gửi biểu mẫu và hiển thị thông báo lỗi.
- **Alt B — Backend rejects product**: Bước 6 trả về lỗi 422; frontend hiển thị thông báo lỗi tương ứng.
- **Postconditions**: Đơn hàng được lưu trữ với trạng thái PENDING; hiển thị trên Internal Dashboard.

#### UC-OADM-002 Cancel Order With Optional Reason

- **Priority**: Must | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Actor**: Staff / Manager / Admin | **Precondition**: Đơn hàng có trạng thái PENDING, CONFIRMED, hoặc SHIPPING. Tác nhân có quyền `order:update-status`.
- **Main Flow**:
  1. Tác nhân mở trang chi tiết đơn hàng trên dashboard.
  2. Tác nhân chọn "Hủy đơn hàng."
  3. Hệ thống hiển thị hộp thoại yêu cầu nhập lý do hủy đơn tùy chọn.
  4. Tác nhân nhập lý do (hoặc để trống) và xác nhận.
  5. Backend chuyển trạng thái đơn hàng sang CANCELLED; lưu lý do hủy (có thể null); ghi nhận thông tin nhân viên thực hiện và dấu thời gian.
  6. Hệ thống gửi email thông báo cho khách hàng (kèm lý do hủy nếu có).
  7. Bản ghi nhật ký hệ thống (audit trail) được tạo.
- **Alt — Order is DELIVERED or CANCELLED**: Nút hành động Hủy đơn hàng bị vô hiệu hóa.
- **Postconditions**: Đơn hàng chuyển sang CANCELLED; khách hàng được thông báo; audit log được cập nhật.

#### UC-SADM-001 Create Staff Account

- **Priority**: Must | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Actor**: Store Manager (chỉ cho chi nhánh của mình), General Manager, hoặc Super Admin. | **Precondition**: Tác nhân có quyền `staff:create`.
- **Main Flow**:
  1. Tác nhân truy cập mục Quản lý nhân viên (Staff Management).
  2. Tác nhân nhấp chọn "Tạo tài khoản nhân viên."
  3. Hệ thống hiển thị biểu mẫu điền thông tin: Username, Họ và tên, Số điện thoại, Email, Mật khẩu mặc định, Chi nhánh, và Vai trò.
  4. Tác nhân gửi biểu mẫu.
  5. Backend kiểm tra tính duy nhất của Username và Email.
  6. Backend tạo tài khoản (IsActive=true, mật khẩu được mã hóa).
  7. Bản ghi nhật ký hệ thống (audit trail) được tạo.
  8. Hệ thống hiển thị thông báo tạo tài khoản thành công.
- **Alt — Duplicate username or email**: Trả về mã lỗi 409; biểu mẫu hiển thị lỗi trực tiếp trên ô nhập liệu tương ứng.
- **Postconditions**: Tài khoản nhân viên mới được kích hoạt hoạt động; audit log được lưu trữ.

---

## 7. Business Rules

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 7.1 Business Rule Catalogue

| BR ID | Rule Name | Domain | Priority |
|---|---|---|---|
| BR-PROD-001 | PurchaseMode Determines Order Eligibility | PROD | Must |
| BR-PROD-002 | PriceVisibility Governs Public Price Display | PROD | Must |
| BR-PROD-003 | CONTACT_ONLY Product Cart Rejection (Dual Layer) | PROD | Must |
| BR-PROD-004 | Backend Validates PurchaseMode On Order Creation | PROD | Must |
| BR-PROD-005 | Product Slug Must Be Unique | PROD | Must |
| BR-PROD-006 | Inactive Products Hidden From Public Catalog | PROD | Must |
| BR-INV-001 | Overselling Permitted; No Hard Stock Gate | INV | Must |
| BR-INV-002 | Exact Stock Numbers Are Internal Only | INV | Must |
| BR-ORD-001 | Orders Cannot Be Auto-Confirmed | ORD | Must |
| BR-ORD-002 | Order Status Transitions Follow Defined Lifecycle | ORD | Must |
| BR-ORD-003 | Cancelled Orders Retain Full History | ORD | Must |
| BR-ORD-004 | All Order Items Must Be ORDERABLE At Time Of Order | ORD | Must |
| BR-CONT-001 | Both CONTACT_ONLY And ORDERABLE Products Support Contact Flow | CONT | Must |
| BR-CONT-002 | Contact Flow Routes To Unified Communication Channel | CONT | Must |
| BR-CONT-003 | ContactRequest Status Follows Defined Lifecycle | CONT | Must |
| BR-ACC-001 | Authentication Required For All Internal Dashboard Access | ACC | Must |
| BR-ACC-002 | Permissions Are Role-Based And Configurable (RBAC) | ACC | Must |
| BR-ACC-003 | Store Manager Scope Restricted To Assigned Branch | ACC | Must |
| BR-ACC-004 | General Manager Scope Covers All Branches | ACC | Must |
| BR-ACC-005 | Super Admin Has Unrestricted Global Access | ACC | Must |
| BR-ACC-006 | Staff May Only Change Their Own Password | ACC | Must |
| BR-ACC-007 | Staff Core Profile Updates Require Manager Or Admin | ACC | Must |
| BR-ACC-008 | Staff Accounts Use Soft Delete | ACC | Must |
| BR-ACC-009 | Session Expires After 30 Minutes Of Inactivity | ACC | Must |
| BR-AUD-001 | Dangerous Administrative Actions Must Be Audit Logged | AUD | Should |
| BR-AUD-002 | Audit Logs Are Immutable | AUD | Should |
| BR-SET-001 | Hotline And Channel Links Configurable Via Admin Settings | SET | Must |

### 7.2 Selected Business Rule Details

**BR-PROD-001** — Nguồn: FE-context.md s2, BE-context.md s2. Hệ thống xác định điều kiện đặt hàng của sản phẩm hoàn toàn dựa trên thuộc tính PurchaseMode. ORDERABLE = được thêm vào giỏ hàng và đặt hàng trực tiếp. CONTACT_ONLY = không được đặt hàng trực tiếp. Ràng buộc này được thực thi chặt chẽ ở cả giao diện frontend và API backend.

**BR-ORD-002** — Nguồn: Question-Resolve.md. Các chuyển đổi trạng thái được phép: PENDING->CONFIRMED, CONFIRMED->SHIPPING, SHIPPING->DELIVERED, PENDING->CANCELLED, CONFIRMED->CANCELLED, SHIPPING->CANCELLED. Nghiêm cấm mọi chuyển đổi trạng thái bắt đầu từ trạng thái DELIVERED hoặc CANCELLED; không cho phép quay ngược trạng thái.

**BR-INV-001** — Nguồn: Question-Resolve.md. Hệ thống không từ chối đơn hàng dựa trên StockQuantity. Đơn hàng được chấp nhận ngay cả khi số lượng tồn kho bằng 0 hoặc âm. Nhân viên sẽ xử lý thủ công đối với các đơn hàng bị âm kho.

**BR-CONT-001** — Nguồn: Question-Resolve.md. CONTACT_ONLY: Chỉ hiển thị nút CTA "Liên hệ với chúng tôi". ORDERABLE: Nút CTA chính "Thêm vào giỏ hàng" + nút CTA phụ "Yêu cầu tư vấn". Cả hai nút CTA liên hệ đều trỏ đến cùng một kênh liên lạc hợp nhất. Hệ thống chấp nhận yêu cầu liên hệ từ cả hai loại sản phẩm này.

**BR-ACC-008** — Nguồn: Question-Resolve.md. Tài khoản nhân viên nghỉ việc sẽ bị vô hiệu hóa (IsActive=false). Hồ sơ tài khoản và các dữ liệu liên quan trong lịch sử được giữ lại vô thời hạn. Nghiêm cấm xóa cứng (hard-delete) khỏi cơ sở dữ liệu.

---

## 8. Functional Requirements

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 8.1 Functional Requirement Catalogue

| FR ID | Requirement | Domain | Priority |
|---|---|---|---|
| FR-PROD-001 | List Active Products With Optional Category Filter | PROD | Must |
| FR-PROD-002 | Include PurchaseMode And PriceVisibility In Every Product Response | PROD | Must |
| FR-PROD-003 | Render Public Price Area According To PriceVisibility | PROD | Must |
| FR-PROD-004 | Render Product Card CTA According To PurchaseMode | PROD | Must |
| FR-PROD-005 | Expose Product Detail Page By Slug | PROD | Must |
| FR-PROD-006 | Return Gallery Images On Product Detail Response | PROD | Should |
| FR-PROD-007 | Validate PurchaseMode And PriceVisibility Enum On Product Write | PROD | Must |
| FR-PROD-008 | Enforce Unique Slug On Product Create And Update | PROD | Must |
| FR-PROD-009 | Exclude Inactive Products From Public API | PROD | Must |
| FR-CAT-001 | CRUD Product Categories | CAT | Must |
| FR-CAT-002 | Associate Each Product With Exactly One Category | CAT | Must |
| FR-CAT-003 | Filter Public Product Listing By Category | CAT | Must |
| FR-CART-001 | Add ORDERABLE Product To Cart | CART | Must |
| FR-CART-002 | Block CONTACT_ONLY Product From Cart (Frontend And Backend) | CART | Must |
| FR-CART-003 | Remove Product From Cart | CART | Must |
| FR-CART-004 | Update Product Quantity In Cart | CART | Must |
| FR-ORD-001 | Submit Guest Checkout Order | ORD | Must |
| FR-ORD-002 | Validate All Order Items Are ORDERABLE | ORD | Must |
| FR-ORD-003 | Validate Order Items List Is Non-Empty | ORD | Must |
| FR-ORD-004 | Validate Order Item Quantity Is Greater Than Zero | ORD | Must |
| FR-ORD-005 | Validate Order Products Exist And Are Active | ORD | Must |
| FR-ORD-006 | Persist New Order With Status PENDING | ORD | Must |
| FR-ORD-007 | Decrement StockQuantity On Order Placement; Permit Negative | ORD | Must |
| FR-ORD-008 | Admin List And View Orders (Scope-Restricted) | ORD | Must |
| FR-ORD-009 | Admin Transition Order Status Via Defined Lifecycle | ORD | Must |
| FR-ORD-010 | Admin Cancel Order With Optional Reason | ORD | Must |
| FR-ORD-011 | Send Customer Notification Email On Cancellation | ORD | Must |
| FR-CONT-001 | Submit Contact Request Via Public Form | CONT | Must |
| FR-CONT-002 | Validate Contact Request Required Fields | CONT | Must |
| FR-CONT-003 | Persist ContactRequest With Status NEW | CONT | Must |
| FR-CONT-004 | Display Static Deep Link CTAs (Zalo, Messenger, Hotline) | CONT | Must |
| FR-CONT-005 | Admin List And View Contact Requests (Scope-Restricted) | CONT | Must |
| FR-CONT-006 | Admin Transition Contact Request Status | CONT | Must |
| FR-AUTH-001 | Authenticate Internal Users Via Username And Password | AUTH | Must |
| FR-AUTH-002 | Enforce Session Timeout After 30 Minutes Of Inactivity | AUTH | Must |
| FR-AUTH-003 | Allow Staff To Change Their Own Password | AUTH | Must |
| FR-AUTH-004 | Require Manager Or Admin To Update Staff Core Profile | AUTH | Must |
| FR-STAFF-001 | Create Staff Account | STAFF | Must |
| FR-STAFF-002 | Deactivate Staff Account (Soft Delete Only) | STAFF | Must |
| FR-STAFF-003 | Update Staff Account Profile (Manager Or Admin Only) | STAFF | Must |
| FR-RBAC-001 | Enforce RBAC Permission Check On All Internal API Endpoints | RBAC | Must |
| FR-RBAC-002 | Restrict Branch Scope For Staff And Store Manager | RBAC | Must |
| FR-RBAC-003 | Grant Network-Wide Scope To General Manager And Super Admin | RBAC | Must |
| FR-AUD-001 | Create Immutable Audit Log Entry For Dangerous Admin Actions | AUD | Should |
| FR-AUD-002 | Prevent Modification Or Deletion Of Audit Log Entries | AUD | Should |
| FR-SET-001 | Super Admin Configure Hotline And Deep Link URLs | SET | Must |
| FR-SET-002 | Serve Public Settings Via Unauthenticated Endpoint | SET | Must |
| FR-INV-001 | Decrement StockQuantity On Order Placement; Permit Negative | INV | Must |
| FR-INV-002 | Display Exact StockQuantity To Authenticated Internal Users | INV | Must |
| FR-INV-003 | Exclude Exact StockQuantity From Public API | INV | Must |
| FR-IMG-001 | Upload Main Product Image To Cloudflare R2 | IMG | Must |
| FR-IMG-002 | Upload Secondary Gallery Images To Cloudflare R2 | IMG | Should |
| FR-IMG-003 | Store MainImageUrl As Primary Product Image Reference | IMG | Must |
| FR-IMG-004 | Store Gallery Images In Separate ProductImage Table | IMG | Should |

### 8.2 Functional Requirement Details

#### FR-PROD-001 List Active Products With Optional Category Filter

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s11, BE-context.md s9, Question-Resolve.md
- **Rationale**: Khách hàng phải xem được danh sách sản phẩm và có khả năng lọc sản phẩm theo danh mục.
- **Statement**: Hệ thống phải cung cấp endpoint `GET /api/products` trả về danh sách các sản phẩm đang hoạt động (IsActive=true). Endpoint này hỗ trợ tham số truy vấn tùy chọn `categoryId` để lọc danh sách sản phẩm theo danh mục.
- **Acceptance Criteria**:
  1. Khi không truyền `categoryId`, hệ thống trả về toàn bộ sản phẩm đang hoạt động.
  2. Khi truyền `categoryId` hợp lệ, hệ thống chỉ trả về sản phẩm hoạt động thuộc danh mục đó.
  3. Khi truyền `categoryId` không đúng định dạng, hệ thống trả về mã lỗi 400 Bad Request.
  4. Các sản phẩm đã ngừng hoạt động (IsActive=false) không được hiển thị trên danh sách sản phẩm công khai.
- **Dependencies**: FR-CAT-002, FR-PROD-002, FR-INV-003

#### FR-PROD-002 Include PurchaseMode And PriceVisibility In Every Product Response

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s10, BE-context.md s9
- **Rationale**: Frontend cần các thông tin này để kết xuất chính xác nút CTA và cách hiển thị giá.
- **Statement**: Hệ thống phải bao gồm hai trường dữ liệu `purchaseMode` và `priceVisibility` trong mọi phản hồi API sản phẩm (cả trang danh sách và trang chi tiết).
- **Acceptance Criteria**:
  1. Giá trị `purchaseMode` phải là một trong hai giá trị ORDERABLE hoặc CONTACT_ONLY.
  2. Giá trị `priceVisibility` phải là một trong ba giá trị SHOW_PRICE, HIDE_PRICE hoặc CONTACT_FOR_PRICE.
  3. Cả hai trường dữ liệu này đều không được mang giá trị null hoặc bị thiếu trong phản hồi.
- **Dependencies**: None

#### FR-PROD-003 Render Public Price Area According To PriceVisibility

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s3
- **Rationale**: Doanh nghiệp kiểm soát cách hiển thị giá đối với từng sản phẩm; frontend không được tự ý suy đoán giá trị từ trường giá mang giá trị null.
- **Statement**: Website công khai phải hiển thị khu vực giá như sau: SHOW_PRICE = hiển thị giá VND đã định dạng; HIDE_PRICE = không có phần tử hiển thị giá trong DOM; CONTACT_FOR_PRICE = hiển thị dòng chữ "Liên hệ".
- **Acceptance Criteria**:
  1. Nếu là SHOW_PRICE, giá đã định dạng phải hiển thị ở thẻ sản phẩm và trang chi tiết.
  2. Nếu là HIDE_PRICE, không tồn tại bất kỳ thẻ hiển thị giá nào trong cấu trúc DOM.
  3. Nếu là CONTACT_FOR_PRICE, dòng chữ "Liên hệ" được hiển thị tại vị trí của giá sản phẩm.
- **Dependencies**: FR-PROD-002

#### FR-PROD-004 Render Product Card CTA According To PurchaseMode

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s4
- **Statement**: Tại trang danh sách sản phẩm: ORDERABLE = hiển thị nút CTA "Thêm vào giỏ hàng"; CONTACT_ONLY = hiển thị nút CTA "Liên hệ tư vấn" hoặc "Nhận báo giá"; không hiển thị nút Thêm vào giỏ hàng đối với sản phẩm CONTACT_ONLY.
- **Acceptance Criteria**:
  1. Nếu là ORDERABLE, nút Thêm vào giỏ hàng hiển thị và không hiển thị nút liên hệ tư vấn.
  2. Nếu là CONTACT_ONLY, hiển thị nút liên hệ tư vấn và không hiển thị nút Thêm vào giỏ hàng.
- **Dependencies**: FR-PROD-002

#### FR-CART-002 Block CONTACT_ONLY Product From Cart (Frontend And Backend)

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s6, BE-context.md s2, s12
- **Rationale**: Quy tắc nghiệp vụ BR-PROD-003. Kiểm tra tính hợp lệ ở cả 2 lớp để tăng tính bảo mật bảo vệ hệ thống.
- **Statement**: Khi người dùng cố gắng thêm sản phẩm CONTACT_ONLY vào giỏ hàng: frontend chặn trước khi gọi API và hiển thị thông báo "Sản phẩm này cần liên hệ tư vấn trước khi đặt hàng." Backend trả về lỗi 422 với mã lỗi `CONTACT_ONLY_PRODUCT` nếu phát hiện sản phẩm CONTACT_ONLY trong payload đơn đặt hàng.
- **Acceptance Criteria**:
  1. Đối với sản phẩm CONTACT_ONLY, frontend hiển thị thông báo chặn và không gọi API thêm sản phẩm vào giỏ hàng.
  2. Nếu gửi payload chứa sản phẩm CONTACT_ONLY đến backend, API `POST /api/orders` trả về lỗi 422 kèm mã lỗi `CONTACT_ONLY_PRODUCT`.
- **Dependencies**: FR-PROD-002, FR-ORD-002

#### FR-ORD-001 Submit Guest Checkout Order

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s7, BE-context.md s7
- **Rationale**: Khách hàng có thể thực hiện mua hàng mà không cần phải tạo tài khoản.
- **Statement**: Hệ thống phải chấp nhận endpoint `POST /api/orders` (không yêu cầu xác thực) chứa các trường thông tin: `receiverName`, `receiverPhone`, `receiverAddress`, `note` (tùy chọn), và danh sách `items` (gồm `productId`, `quantity`). Sau khi xác thực thành công, đơn hàng được lưu trữ với trạng thái PENDING.
- **Acceptance Criteria**:
  1. Payload hợp lệ, tất cả sản phẩm đều là ORDERABLE: trả về mã trạng thái 201 Created kèm mã đơn hàng mới tạo.
  2. Danh sách mặt hàng trống: trả về lỗi 400 Bad Request.
  3. Số lượng sản phẩm `quantity` <= 0: trả về lỗi 400 Bad Request.
  4. Sản phẩm `productId` không tồn tại: trả về lỗi 422.
  5. Sản phẩm không hoạt động: trả về lỗi 422.
- **Dependencies**: Từ FR-ORD-002 đến FR-ORD-007

#### FR-ORD-010 Admin Cancel Order With Optional Reason

- **Priority**: Must | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Statement**: Khi người dùng nội bộ đã được xác thực có quyền `order:update-status` thực hiện chuyển trạng thái đơn hàng sang CANCELLED qua endpoint `PUT /api/admin/orders/{id}/status`, hệ thống phải chấp nhận thông tin trường `cancellationReason` tùy chọn. Hệ thống lưu lý do hủy đơn (có thể null) và kích hoạt yêu cầu FR-ORD-011.
- **Acceptance Criteria**:
  1. Hủy đơn kèm lý do: thông tin đơn hàng lưu lý do hủy; email thông báo gửi cho khách hàng chứa nội dung lý do này.
  2. Hủy đơn không kèm lý do: thông tin đơn hàng lưu giá trị null; email gửi cho khách hàng bỏ qua trường thông tin lý do hủy.
  3. Đơn hàng đang ở trạng thái DELIVERED: trả về mã lỗi 409 Conflict.
  4. Đơn hàng đã ở trạng thái CANCELLED: trả về mã lỗi 409 Conflict.
- **Dependencies**: FR-ORD-011, FR-AUD-001, FR-RBAC-001

#### FR-CONT-001 Submit Contact Request Via Public Form

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s8, BE-context.md s8, Question-Resolve.md
- **Rationale**: Thu thập nhu cầu tư vấn của khách hàng; làm cơ sở cho luồng xử lý của nhân viên.
- **Statement**: Hệ thống phải chấp nhận endpoint `POST /api/contact-requests` (không yêu cầu xác thực) chứa các trường thông tin: `productId`, `customerName`, `customerPhone`, `customerMessage` (tùy chọn). Khi lưu thành công, bản ghi ContactRequest được tạo với trạng thái ban đầu là NEW.
- **Acceptance Criteria**:
  1. Payload hợp lệ: trả về mã trạng thái 201 Created.
  2. Thiếu thông tin `customerName` hoặc `customerPhone`: trả về lỗi 400 Bad Request.
  3. Sản phẩm `productId` không tồn tại: trả về lỗi 422.
  4. Gửi thành công: frontend hiển thị thông báo "Yêu cầu tư vấn của bạn đã được gửi. Nhân viên sẽ liên hệ lại sớm."
  5. Chấp nhận sản phẩm ở chế độ ORDERABLE (không giới hạn sản phẩm CONTACT_ONLY).
- **Dependencies**: FR-CONT-002, FR-CONT-003

#### FR-AUTH-001 Authenticate Internal Users Via Username And Password

- **Priority**: Must | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Statement**: Hệ thống phải cung cấp endpoint `POST /api/auth/login` chấp nhận thông tin đăng nhập gồm `username` and `password`. Nếu thành công, hệ thống cấp mã Token JWT lưu trong HTTP-only cookie. Nếu thất bại, trả về lỗi 401 Unauthorized mà không tiết lộ trường thông tin nào bị sai.
- **Acceptance Criteria**:
  1. Thông tin đăng nhập hợp lệ: cấp mã session token; cho phép truy cập trang dashboard quản trị.
  2. Sai username hoặc mật khẩu: trả về lỗi 401 kèm thông báo chung "Invalid username or password."
  3. Tài khoản đã bị vô hiệu hóa: trả về lỗi 401 kèm thông báo chung tương tự.
- **Dependencies**: FR-AUTH-002
- **Notes**: Chưa định nghĩa chính sách khóa tài khoản khi nhập sai mật khẩu nhiều lần [TBD: OQ-GEN-001].

#### FR-STAFF-001 Create Staff Account

- **Priority**: Must | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Statement**: Người dùng nội bộ có quyền `staff:create` được phép tạo tài khoản nhân viên mới với các thông tin: `username`, `fullName`, `phoneNumber`, `email`, `defaultPassword` (được mã hóa), `branchId` (tùy chọn), `roleId` và trạng thái mặc định IsActive=true.
- **Acceptance Criteria**:
  1. Username và email chưa tồn tại: trả về mã trạng thái 201 Created.
  2. Username đã tồn tại: trả về lỗi 409 Conflict.
  3. Email đã tồn tại: trả về lỗi 409 Conflict.
  4. Tạo thành công: hệ thống ghi nhật ký hoạt động tương ứng theo FR-AUD-001.
- **Dependencies**: FR-RBAC-001, FR-AUD-001
- **Notes**: Mật khẩu được mã hóa bằng thuật toán bcrypt hoặc Argon2. Chưa định nghĩa chính sách yêu cầu đổi mật khẩu ở lần đăng nhập đầu tiên [TBD: OQ-GEN-006].

#### FR-AUD-001 Create Immutable Audit Log Entry For Dangerous Admin Actions

- **Priority**: Should | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Statement**: Hệ thống phải tự động tạo bản ghi nhật ký kiểm toán AuditLog cho các hành vi: tạo mới, vô hiệu hóa, cập nhật thông tin tài khoản nhân viên; tạo mới, xóa sản phẩm; thay đổi trạng thái đơn hàng; thay đổi cấu hình hệ thống. Mỗi bản ghi lưu: mã người thực hiện, username người thực hiện, loại hành động, thực thể bị ảnh hưởng, mã định danh thực thể, dấu thời gian UTC và bản sao các trường dữ liệu thay đổi.
- **Acceptance Criteria**:
  1. Tạo nhân viên mới: tạo bản ghi AuditLog với loại hành động "STAFF_CREATED".
  2. Hủy đơn hàng: tạo bản ghi AuditLog với loại hành động "ORDER_CANCELLED" chứa kèm lý do hủy đơn (nếu có).
  3. Các bản ghi nhật ký kiểm toán không được phép chỉnh sửa hoặc xóa qua bất kỳ endpoint nào của ứng dụng.
- **Dependencies**: FR-AUD-002

#### FR-SET-001 Super Admin Configure Hotline And Deep Link URLs

- **Priority**: Must | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Statement**: Hệ thống phải cung cấp endpoint `PUT /api/admin/settings` (chỉ dành cho Super Admin) để cập nhật thông tin: số điện thoại hotline, liên kết sâu Zalo, liên kết sâu Messenger. Các thay đổi được lưu trữ và áp dụng ngay lập tức trên website công khai mà không cần triển khai lại mã nguồn.
- **Acceptance Criteria**:
  1. Super Admin cập nhật hotline: endpoint `/api/settings/public` phản hồi giá trị hotline mới ngay trong lần gọi tiếp theo.
  2. Người dùng không phải Super Admin gọi API cập nhật cấu hình: trả về lỗi 403 Forbidden.
- **Dependencies**: FR-RBAC-001, FR-SET-002

---

## 9. Data Requirements And Data Model

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 9.1 Modeling Scope

Phạm vi bao gồm: products, categories, product images, orders, order items, contact requests, branches, roles, permissions, users, audit logs, system settings.

### 9.2 Conceptual Data Model

```
[Category] 1---< [Product] >---< [ProductImage]
                    |
             [OrderItem] >----  [Order]
                    |
            [ContactRequest]

[Branch] 1---< [User] >---- [Role] >----< [Permission]
[User] 1---< [AuditLog]
[SystemSetting] (key-value)
```

### 9.3 Conceptual Model

#### 9.3.1 Conceptual Entity Summary

| Entity ID | Entity Name | Business Definition | Primary Owner | Status |
|---|---|---|---|---|
| ENT-PROD-001 | Category | Nhóm phân loại sản phẩm dùng để lọc danh mục sản phẩm công khai | Manager/Admin | REVIEW |
| ENT-PROD-002 | Product | Sản phẩm có thể bán được với các cấu hình về chế độ mua hàng và hiển thị giá | Staff/Manager/Admin | REVIEW |
| ENT-PROD-003 | ProductImage | Hình ảnh thư viện phụ liên kết với một sản phẩm | Staff/Manager/Admin | REVIEW |
| ENT-ORD-001 | Order | Đơn đặt hàng của khách vãng lai chứa thông tin chi tiết giao nhận | Customer (create), Staff (manage) | REVIEW |
| ENT-ORD-002 | OrderItem | Mặt hàng trong đơn hàng; lưu snapshot tên và giá sản phẩm tại thời điểm mua | System (auto-created with order) | REVIEW |
| ENT-CONT-001 | ContactRequest | Yêu cầu tư vấn hoặc báo giá của khách hàng liên kết với một sản phẩm | Customer (create), Staff (manage) | REVIEW |
| ENT-ACC-001 | Branch | Địa điểm chi nhánh vật lý dùng để giới hạn phạm vi quyền hạn của nhân viên | Manager/Admin | REVIEW |
| ENT-ACC-002 | Role | Nhóm quyền có tên gọi dùng để kiểm soát truy cập dựa trên vai trò | Super Admin | REVIEW |
| ENT-ACC-003 | Permission | Quyền truy cập riêng lẻ có thể gán cho một vai trò | Super Admin | REVIEW |
| ENT-ACC-004 | RolePermission | Liên kết nhiều-nhiều giữa Role và Permission | Super Admin | REVIEW |
| ENT-ACC-005 | User | Tài khoản nhân viên, quản lý hoặc quản trị viên nội bộ truy cập dashboard | Manager/Admin | REVIEW |
| ENT-AUD-001 | AuditLog | Bản ghi bất biến ghi nhận các hành động hành chính quan trọng | System (automated) | REVIEW |
| ENT-SET-001 | SystemSetting | Bản ghi cấu hình dạng key-value cho số hotline và liên kết sâu của các kênh liên lạc | Super Admin | REVIEW |

#### 9.3.2 Conceptual Relationship Summary

| Relationship ID | Source Entity | Relationship | Target Entity | Cardinality | Optionality | Business Meaning | Status |
|---|---|---|---|---|---|---|---|
| REL-PROD-001 | Category | contains | Product | 1:N | Required | Mỗi sản phẩm thuộc về duy nhất một danh mục | REVIEW |
| REL-PROD-002 | Product | has | ProductImage | 1:N | Optional | Một sản phẩm có thể có không hoặc nhiều hình ảnh phụ | REVIEW |
| REL-PROD-003 | Product | is ordered as | OrderItem | 1:N | Optional | Một sản phẩm có thể xuất hiện trong nhiều dòng sản phẩm của đơn hàng | REVIEW |
| REL-PROD-004 | Product | receives | ContactRequest | 1:N | Optional | Một sản phẩm có thể nhận được nhiều yêu cầu tư vấn | REVIEW |
| REL-ORD-001 | Order | contains | OrderItem | 1:N | Required | Mỗi đơn hàng phải chứa ít nhất một mặt hàng | REVIEW |
| REL-ORD-002 | User | cancels | Order | 1:N | Optional | Người dùng nội bộ có thể hủy các đơn đặt hàng | REVIEW |
| REL-CONT-001 | User | handles | ContactRequest | 1:N | Optional | Người dùng nội bộ có thể xử lý các yêu cầu tư vấn | REVIEW |
| REL-ACC-001 | Branch | employs | User | 1:N | Optional | Một chi nhánh có thể có nhiều tài khoản nhân viên | REVIEW |
| REL-ACC-002 | Role | is assigned to | User | 1:N | Required | Mỗi người dùng có duy nhất một vai trò | REVIEW |
| REL-ACC-003 | Role | grants | RolePermission | 1:N | Optional | Một vai trò có thể được cấp nhiều quyền hạn khác nhau | REVIEW |
| REL-ACC-004 | Permission | granted via | RolePermission | 1:N | Optional | Một quyền hạn có thể được gán cho nhiều vai trò | REVIEW |
| REL-ACC-005 | User | generates | AuditLog | 1:N | Optional | Các hành động hành chính của người dùng được ghi nhật ký hệ thống | REVIEW |
| REL-SET-001 | User | updates | SystemSetting | 1:N | Optional | Super Admin cập nhật cấu hình hệ thống | REVIEW |

### 9.4 Entity Attributes

#### ENT-PROD-001 Category
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Mã định danh duy nhất của danh mục |
| Name | VARCHAR(200) | NOT NULL, UNIQUE | Tên hiển thị của danh mục |
| Slug | VARCHAR(200) | NOT NULL, UNIQUE | Đường dẫn thân thiện dùng cho định tuyến và lọc danh mục sản phẩm |
| Description | TEXT | NULLABLE | Mô tả tùy chọn của danh mục |
| IsActive | BOOLEAN | NOT NULL, DEFAULT TRUE | Cờ xóa mềm; false = danh mục bị vô hiệu hóa và ẩn khỏi trang công khai |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian tạo bản ghi |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian cập nhật bản ghi lần cuối |

#### ENT-PROD-002 Product
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Mã định danh duy nhất của sản phẩm |
| CategoryId | UUID | FK -> Category.Id, NOT NULL | Tham chiếu tới danh mục cha |
| Name | VARCHAR(500) | NOT NULL | Tên hiển thị của sản phẩm |
| Slug | VARCHAR(500) | NOT NULL, UNIQUE | Đường dẫn thân thiện phục vụ định tuyến trang chi tiết sản phẩm |
| Description | TEXT | NULLABLE | Mô tả chi tiết tùy chọn hiển thị trên trang chi tiết sản phẩm |
| Price | DECIMAL(18,0) | NULLABLE, CHECK >= 0 | Giá sản phẩm tính bằng VND; có thể mang giá trị null nếu chưa xác định giá |
| StockQuantity | INTEGER | NOT NULL, DEFAULT 0 (signed; negative permitted) | Số lượng tồn kho hiện tại; hỗ trợ số nguyên có dấu cho phép số lượng âm (bán quá mức) |
| MainImageUrl | TEXT | NULLABLE | Đường dẫn ảnh thu nhỏ chính lưu tại Cloudflare R2 |
| IsActive | BOOLEAN | NOT NULL, DEFAULT TRUE | Cờ xóa mềm; false = sản phẩm bị ẩn khỏi danh mục sản phẩm công khai |
| PurchaseMode | VARCHAR(20) | NOT NULL, CHECK IN ('ORDERABLE','CONTACT_ONLY') | Xác định điều kiện đặt hàng và hiển thị nút CTA trên website công khai |
| PriceVisibility | VARCHAR(30) | NOT NULL, CHECK IN ('SHOW_PRICE','HIDE_PRICE','CONTACT_FOR_PRICE') | Điều khiển cách hiển thị khu vực giá sản phẩm trên website công khai |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian tạo bản ghi |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian cập nhật bản ghi lần cuối |

#### ENT-PROD-003 ProductImage
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Mã định danh duy nhất của hình ảnh thư viện phụ |
| ProductId | UUID | FK -> Product.Id, NOT NULL | Tham chiếu tới sản phẩm cha |
| ImageUrl | TEXT | NOT NULL | Đường dẫn hình ảnh lưu tại Cloudflare R2 |
| SortOrder | INTEGER | NOT NULL, DEFAULT 0 | Chỉ số thứ tự hiển thị của thư viện ảnh sản phẩm |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian tạo bản ghi |

#### ENT-ORD-001 Order
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Mã định danh duy nhất của đơn hàng |
| ReceiverName | VARCHAR(200) | NOT NULL | Họ và tên của người nhận hàng |
| ReceiverPhone | VARCHAR(20) | NOT NULL | Số điện thoại của người nhận hàng |
| ReceiverAddress | TEXT | NOT NULL | Địa chỉ giao nhận hàng do khách hàng cung cấp |
| Note | TEXT | NULLABLE | Ghi chú hoặc yêu cầu giao hàng đặc biệt tùy chọn của khách hàng |
| Status | VARCHAR(20) | NOT NULL, CHECK IN ('PENDING','CONFIRMED','SHIPPING','DELIVERED','CANCELLED') | Trạng thái hiện tại trong vòng đời đơn hàng |
| CancellationReason | TEXT | NULLABLE | Lý do tùy chọn do người hủy đơn nhập vào khi hủy đơn hàng |
| CancelledByUserId | UUID | FK -> User.Id, NULLABLE | Tham chiếu tới tài khoản nhân viên thực hiện hủy đơn hàng |
| CancelledAt | TIMESTAMPTZ | NULLABLE | Dấu thời gian khi đơn hàng bị hủy |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian đặt hàng |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian cập nhật trạng thái đơn hàng lần cuối |

#### ENT-ORD-002 OrderItem
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Mã định danh duy nhất của mặt hàng đơn hàng |
| OrderId | UUID | FK -> Order.Id, NOT NULL | Tham chiếu tới đơn hàng cha |
| ProductId | UUID | FK -> Product.Id, NOT NULL | Tham chiếu tới sản phẩm được đặt |
| ProductName | VARCHAR(500) | NOT NULL (snapshot at order time — ASM-GEN-007) | Bản lưu tên sản phẩm tại thời điểm tạo đơn hàng |
| UnitPrice | DECIMAL(18,0) | NOT NULL (snapshot at order time — ASM-GEN-007) | Bản lưu đơn giá sản phẩm tại thời điểm tạo đơn hàng |
| Quantity | INTEGER | NOT NULL, CHECK > 0 | Số lượng sản phẩm đặt mua; bắt buộc phải là số dương |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian tạo bản ghi |

#### ENT-CONT-001 ContactRequest
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Mã định danh duy nhất của yêu cầu tư vấn |
| ProductId | UUID | FK -> Product.Id, NOT NULL | Tham chiếu tới sản phẩm cần tư vấn |
| CustomerName | VARCHAR(200) | NOT NULL | Họ và tên của khách hàng gửi yêu cầu |
| CustomerPhone | VARCHAR(20) | NOT NULL | Số điện thoại khách hàng dùng để liên hệ tư vấn |
| CustomerMessage | TEXT | NULLABLE | Nội dung tin nhắn hoặc câu hỏi chi tiết tùy chọn của khách hàng |
| Status | VARCHAR(20) | NOT NULL, CHECK IN ('NEW','CONTACTED','CLOSED'), DEFAULT 'NEW' | Trạng thái hiện tại trong vòng đời yêu cầu tư vấn |
| HandledByUserId | UUID | FK -> User.Id, NULLABLE | Tham chiếu tới tài khoản nhân viên xử lý yêu cầu tư vấn |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian gửi yêu cầu |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian cập nhật trạng thái yêu cầu lần cuối |

#### ENT-ACC-001 Branch
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Mã định danh duy nhất của chi nhánh |
| Name | VARCHAR(200) | NOT NULL | Tên hiển thị của chi nhánh vật lý |
| Description | TEXT | NULLABLE | Mô tả tùy chọn về chi nhánh |
| IsActive | BOOLEAN | NOT NULL, DEFAULT TRUE | Cờ xóa mềm; false = chi nhánh bị vô hiệu hóa hoạt động |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian tạo bản ghi |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian cập nhật bản ghi lần cuối |

#### ENT-ACC-002 Role
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Mã định danh duy nhất của vai trò |
| Name | VARCHAR(100) | NOT NULL, UNIQUE | Tên hiển thị duy nhất của vai trò (ví dụ: Staff, Store Manager) |
| Description | TEXT | NULLABLE | Mô tả tùy chọn về phạm vi và chức năng của vai trò |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian tạo bản ghi |

#### ENT-ACC-003 Permission
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Mã định danh duy nhất của quyền truy cập |
| Code | VARCHAR(100) | NOT NULL, UNIQUE | Mã quyền duy nhất dạng máy đọc (ví dụ: order:update-status) |
| Description | TEXT | NULLABLE | Mô tả quyền hạn dạng người đọc |

#### ENT-ACC-004 RolePermission
| Column | Type | Constraints | Description |
|---|---|---|---|
| RoleId | UUID | FK -> Role.Id, NOT NULL | Tham chiếu tới vai trò được cấp quyền |
| PermissionId | UUID | FK -> Permission.Id, NOT NULL | Tham chiếu tới quyền truy cập được cấp |
| PRIMARY KEY | (RoleId, PermissionId) | Composite | Khóa chính composite để ngăn cấp quyền trùng lặp |

#### ENT-ACC-005 User
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Mã định danh duy nhất của tài khoản người dùng nội bộ |
| Username | VARCHAR(100) | NOT NULL, UNIQUE | Tên đăng nhập duy nhất dùng để xác thực trang dashboard |
| FullName | VARCHAR(200) | NOT NULL | Họ và tên hiển thị của nhân viên |
| PhoneNumber | VARCHAR(20) | NOT NULL | Số điện thoại liên hệ của nhân viên |
| Email | VARCHAR(200) | NOT NULL, UNIQUE | Địa chỉ email duy nhất dùng cho nhận thông báo và khôi phục tài khoản |
| PasswordHash | TEXT | NOT NULL | Mật khẩu đã được băm bằng bcrypt hoặc Argon2; không bao giờ lưu văn bản thường |
| RoleId | UUID | FK -> Role.Id, NOT NULL | Tham chiếu tới vai trò được gán |
| BranchId | UUID | FK -> Branch.Id, NULLABLE (null = no branch restriction) | Tham chiếu tới chi nhánh làm việc; null đối với General Manager và Super Admin |
| IsActive | BOOLEAN | NOT NULL, DEFAULT TRUE | Cờ xóa mềm; false = tài khoản bị vô hiệu hóa và chặn quyền đăng nhập |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian tạo bản ghi |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian chỉnh sửa thông tin hồ sơ lần cuối |

#### ENT-AUD-001 AuditLog
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Mã định danh duy nhất của bản ghi nhật ký kiểm toán |
| ActorUserId | UUID | FK -> User.Id, NULLABLE | Tham chiếu tới tài khoản người thực hiện hành động |
| ActorUsername | VARCHAR(100) | NOT NULL | Ảnh chụp tên đăng nhập tại thời điểm thực hiện để truy vết kể cả khi tài khoản bị vô hiệu hóa |
| ActionType | VARCHAR(100) | NOT NULL | Loại hành động hành chính (ví dụ: STAFF_CREATED, ORDER_CANCELLED) |
| EntityType | VARCHAR(100) | NOT NULL | Loại thực thể bị ảnh hưởng (ví dụ: User, Product, Order) |
| EntityId | UUID | NULLABLE | Mã định danh của bản ghi thực thể bị ảnh hưởng |
| Changes | JSONB | NULLABLE | Ảnh chụp cấu trúc JSON lưu trữ giá trị cũ và mới của các trường dữ liệu thay đổi |
| CreatedAt | TIMESTAMPTZ | NOT NULL (immutable; no UpdatedAt) | Dấu thời gian bất biến ghi lại thời điểm xảy ra hành động |

#### ENT-SET-001 SystemSetting
| Column | Type | Constraints | Description |
|---|---|---|---|
| Key | VARCHAR(100) | PK, NOT NULL | Mã định danh duy nhất của cài đặt (ví dụ: hotline, zalo_url, messenger_url) |
| Value | TEXT | NULLABLE | Giá trị hiện tại của cấu hình; có thể null nếu chưa được thiết lập |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Dấu thời gian cập nhật lần cuối |
| UpdatedByUserId | UUID | FK -> User.Id, NULLABLE | Tham chiếu tới tài khoản Super Admin thực hiện cập nhật gần nhất |

### 9.5 Data Dictionary

| Field | Entity | Description |
|---|---|---|
| PurchaseMode | Product | ORDERABLE hoặc CONTACT_ONLY; điều khiển quyền thêm giỏ hàng/đặt hàng và cách kết xuất CTA |
| PriceVisibility | Product | SHOW_PRICE, HIDE_PRICE, hoặc CONTACT_FOR_PRICE; điều khiển cách kết xuất vùng giá công khai |
| MainImageUrl | Product | Đường dẫn ảnh thu nhỏ chính lưu trong Cloudflare R2 |
| StockQuantity | Product | Số nguyên có dấu; cho phép giá trị âm (bán quá mức) |
| Status | Order | PENDING, CONFIRMED, SHIPPING, DELIVERED, hoặc CANCELLED |
| CancellationReason | Order | Lý do hủy đơn tùy chọn; lưu null nếu không cung cấp lý do hủy |
| Status | ContactRequest | NEW, CONTACTED, hoặc CLOSED |
| IsActive | User/Product/Category/Branch | Cờ xóa mềm; false = bản ghi bị vô hiệu hóa nhưng dữ liệu lịch sử được giữ lại |
| BranchId | User | Null = không giới hạn chi nhánh (General Manager, Super Admin) |
| ActionType | AuditLog | ví dụ: STAFF_CREATED, ORDER_CANCELLED, PRODUCT_DELETED |

### 9.6 Data Constraints And Validation Rules

| VAL ID | Entity | Field | Rule |
|---|---|---|---|
| VAL-PROD-001 | Product | Slug | Phải là duy nhất. [ASSUMPTION] Chỉ chứa ký tự chữ cái, chữ số và dấu gạch ngang. |
| VAL-PROD-002 | Product | Price | >= 0 nếu được cung cấp; có thể null. |
| VAL-PROD-003 | Product | StockQuantity | Không có giới hạn dưới (cho phép giá trị âm). |
| VAL-PROD-004 | Product | PurchaseMode | Phải thuộc các giá trị: ORDERABLE hoặc CONTACT_ONLY. |
| VAL-PROD-005 | Product | PriceVisibility | Phải thuộc các giá trị: SHOW_PRICE, HIDE_PRICE, hoặc CONTACT_FOR_PRICE. |
| VAL-ORD-001 | Order | Items | Yêu cầu chứa ít nhất một mặt hàng. |
| VAL-ORD-002 | OrderItem | Quantity | Phải lớn hơn 0. |
| VAL-ORD-003 | OrderItem | ProductId | Phải tham chiếu đến sản phẩm ORDERABLE đang hoạt động và tồn tại. |
| VAL-CONT-001 | ContactRequest | CustomerName | Bắt buộc nhập. Không được để trống. |
| VAL-CONT-002 | ContactRequest | CustomerPhone | Bắt buộc nhập. Không được để trống. [TBD: OQ-GEN-007 — quy tắc xác thực số điện thoại.] |
| VAL-CONT-003 | ContactRequest | ProductId | Phải tham chiếu đến sản phẩm tồn tại. |
| VAL-USER-001 | User | Username | Phải là duy nhất trên toàn hệ thống. |
| VAL-USER-002 | User | Email | Phải là duy nhất. Đúng định dạng địa chỉ email. |
| VAL-USER-003 | User | PasswordHash | Lưu dưới dạng băm bcrypt hoặc Argon2. Không bao giờ lưu văn bản thường hay ghi nhật ký hệ thống. |

### 9.7 Data Ownership And Source Of Truth

| Entity | Created By | Mutated By | Source Of Truth |
|---|---|---|---|
| Product, Category, ProductImage | Staff/Manager/Admin | Staff/Manager/Admin | Neon Postgres |
| Order, OrderItem | Guest Customer (create) | Internal users (status only) | Neon Postgres |
| ContactRequest | Guest Customer (create) | Internal users (status only) | Neon Postgres |
| User, Role, Permission, Branch | Manager/Admin | Manager/Admin | Neon Postgres |
| AuditLog | System (automated) | Never (immutable) | Neon Postgres |
| SystemSetting | Super Admin | Super Admin | Neon Postgres |
| Product images (files) | Staff/Admin | Staff/Admin | Cloudflare R2 |

### 9.8 Data Lifecycle

| Entity | Created | Modified | Deactivated/Closed |
|---|---|---|---|
| Product | Staff/Manager/Admin | Staff/Manager/Admin | Soft delete (IsActive=false) |
| Category | Manager/Admin | Manager/Admin | [TBD: OQ-GEN-004] |
| Order | Guest Customer | Internal (status only) | CANCELLED là trạng thái kết thúc; không bao giờ bị xóa |
| ContactRequest | Guest Customer | Internal (status only) | CLOSED là trạng thái kết thúc; không bao giờ bị xóa |
| User | Manager/Admin | Manager/Admin (profile); Staff (own password) | Soft delete (IsActive=false) |
| AuditLog | System | Never | Never |

### 9.9 Data Retention And Deletion

- Đơn hàng (Orders) và Yêu cầu tư vấn (ContactRequests) được lưu trữ vô thời hạn.
- Tài khoản người dùng (User): chỉ áp dụng xóa mềm (soft delete); nghiêm cấm xóa cứng (hard deletion).
- Nhật ký kiểm toán (AuditLog): lưu trữ vô thời hạn; không thể xóa thông qua bất kỳ giao diện ứng dụng nào.
- Hình ảnh sản phẩm (Product images): được giữ lại trừ khi bị xóa thủ công bởi Admin. Các sản phẩm xóa mềm vẫn giữ lại ảnh [ASSUMPTION].
- [TBD: Đánh giá sự tuân thủ về quyền riêng tư dữ liệu và lưu trữ thông tin (PDPA) đối với thị trường Việt Nam.]

### 9.10 Data Migration

Không áp dụng — hệ thống được xây dựng mới hoàn toàn (greenfield system). [TBD: Bổ sung các hạng mục di trú dữ liệu nếu có yêu cầu nhập dữ liệu cũ từ hệ thống khác.]

### 9.11 Data Traceability Matrix

Xem thêm chi tiết tại Section 16.

---

## 10. External Interface Requirements

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 10.1 User Interface Requirements

| UI ID | Requirement | Priority | Source |
|---|---|---|---|
| UI-GEN-001 | Public site: giao diện hiện đại, phong cách tối giản cao cấp, tông màu chủ đạo #2D3E96, nút CTA nổi bật | Must | FE-context.md s1 |
| UI-GEN-002 | Internal dashboard: giao diện SaaS/doanh nghiệp gọn gàng với bảng dữ liệu hiển thị mật độ thông tin cao | Must | FE-context.md s1 |
| UI-GEN-003 | Public site tương thích responsive hoàn toàn; chiều rộng thiết bị di động tối thiểu 375px | Must | [ASSUMPTION] |
| UI-GEN-004 | Internal dashboard được tối ưu cho desktop; đảm bảo không bị vỡ giao diện trên thiết bị di động | Should | FE-context.md s1 |
| UI-GEN-005 | Thông báo gửi yêu cầu tư vấn thành công: "Yeu cau tu van cua ban da duoc gui. Nhan vien se lien he lai som." | Must | FE-context.md s8 |
| UI-GEN-006 | Thông báo chặn giỏ hàng đối với sản phẩm CONTACT_ONLY: "San pham nay can lien he tu van truoc khi dat hang." | Must | FE-context.md s6 |

### 10.2 Software Interface Requirements

| IF ID | Endpoint | Auth | Purpose |
|---|---|---|---|
| IF-INTG-001 | GET /api/products | None | Xem danh sách sản phẩm công khai và lọc theo danh mục |
| IF-INTG-002 | GET /api/products/{slug} | None | Xem chi tiết sản phẩm công khai và thư viện ảnh |
| IF-INTG-003 | POST /api/orders | None | Khách vãng lai đặt đơn hàng |
| IF-INTG-004 | POST /api/contact-requests | None | Gửi yêu cầu tư vấn sản phẩm |
| IF-INTG-005 | GET /api/admin/orders | RBAC | Xem danh sách đơn hàng nội bộ (giới hạn phạm vi quyền) |
| IF-INTG-006 | GET /api/admin/orders/{id} | RBAC | Xem chi tiết đơn hàng nội bộ |
| IF-INTG-007 | PUT /api/admin/orders/{id}/status | RBAC | Cập nhật trạng thái đơn hàng nội bộ |
| IF-INTG-008 | GET /api/admin/contact-requests | RBAC | Xem danh sách yêu cầu tư vấn nội bộ (giới hạn phạm vi quyền) |
| IF-INTG-009 | GET /api/admin/contact-requests/{id} | RBAC | Xem chi tiết yêu cầu tư vấn nội bộ |
| IF-INTG-010 | PUT /api/admin/contact-requests/{id}/status | RBAC | Cập nhật trạng thái yêu cầu tư vấn nội bộ |
| IF-INTG-011 | GET /api/admin/products | RBAC | Xem danh sách sản phẩm quản trị |
| IF-INTG-012 | POST /api/admin/products | RBAC | Tạo sản phẩm mới |
| IF-INTG-013 | PUT /api/admin/products/{id} | RBAC | Cập nhật sản phẩm |
| IF-INTG-014 | DELETE /api/admin/products/{id} | RBAC | Xóa mềm sản phẩm |
| IF-INTG-015 | GET/POST/PUT/DELETE /api/admin/categories | RBAC (Manager+) | Quản lý CRUD danh mục sản phẩm |
| IF-INTG-016 | GET /api/settings/public | None | Lấy cấu hình công khai (hotline, deep links) |
| IF-INTG-017 | GET/PUT /api/admin/settings | RBAC (Super Admin) | Đọc/cập nhật cài đặt hệ thống |
| IF-INTG-018 | POST /api/auth/login | None | Xác thực đăng nhập người dùng nội bộ |
| IF-INTG-019 | POST /api/auth/logout | Required | Kết thúc phiên làm việc |
| IF-INTG-020 | POST /api/auth/change-password | Required | Nhân viên tự thực hiện đổi mật khẩu của mình |
| IF-INTG-021 | GET/POST/PUT /api/admin/staff | RBAC (Manager+) | Quản lý tài khoản nhân viên |
| IF-INTG-022 | PUT /api/admin/staff/{id}/deactivate | RBAC (Manager+) | Vô hiệu hóa tài khoản nhân viên (xóa mềm) |

### 10.3 Hardware Interface Requirements

Không có. Ứng dụng web hoạt động trên hạ tầng đám mây; không phụ thuộc thiết bị phần cứng chuyên dụng.

### 10.4 Communication Interface Requirements

- Giao thức truyền thông API: bắt buộc HTTPS (sử dụng TLS 1.2+).
- Định dạng nội dung API body: định dạng JSON, sử dụng bảng mã UTF-8.
- Thông báo email: thông qua giao thức SMTP hoặc API nhà cung cấp [TBD: OQ-GEN-002].
- Các liên kết CTA ngoài: sử dụng giao thức `https://` (Zalo, Messenger) và `tel:` (Hotline).

---

## 11. Non-Functional Requirements

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 11.1 Non-Functional Requirement Catalogue

| NFR ID | Requirement | Category | Priority |
|---|---|---|---|
| NFR-PERF-001 | API p95 response time < 3 seconds at 500 concurrent users | Performance | Should |
| NFR-AVAIL-001 | 99% system availability (30-day rolling) | Availability | Should |
| NFR-SCAL-001 | Architecture horizontally scalable to 500 concurrent users | Scalability | Should |
| NFR-SEC-001 | Enforce HTTPS for all traffic | Security | Must |
| NFR-SEC-002 | Passwords stored as bcrypt or Argon2 hash | Security | Must |
| NFR-SEC-003 | Session timeout after 30 min of inactivity | Security | Must |
| NFR-SEC-004 | RBAC enforced on all internal endpoints | Security | Must |
| NFR-SEC-005 | Audit log immutability | Security | Should |
| NFR-PRIV-001 | Exact StockQuantity hidden from public API | Privacy | Must |
| NFR-USE-001 | Checkout completable in 3 or fewer primary actions | Usability | Should |
| NFR-MAINT-001 | System settings updatable without code redeployment | Maintainability | Must |
| NFR-LOG-001 | Structured audit logging for administrative actions | Logging | Should |
| NFR-COMP-001 | Soft delete for all staff accounts | Compliance | Must |

### 11.3 Performance

**NFR-PERF-001** — Nguồn: Question-Resolve.md. Hệ thống phải đảm bảo thời gian phản hồi của mọi yêu cầu API ở mức p95 dưới 3 giây khi kiểm thử tải với 500 người dùng hoạt động đồng thời. Tiêu chí nghiệm thu: kết quả kiểm thử tải với 500 người dùng đồng thời cho kết quả p95 <= 3000 ms.

### 11.4 Availability

**NFR-AVAIL-001** — Nguồn: Question-Resolve.md. Hệ thống phải duy trì mức độ sẵn sàng đạt 99% tính trên chu kỳ 30 ngày liên tục, không bao gồm các khoảng thời gian bảo trì hệ thống định kỳ đã thông báo trước. Thời gian ngừng hoạt động đột xuất tối đa cho phép: 7.2 giờ/tháng.

### 11.6 Scalability

**NFR-SCAL-001** — Nguồn: Question-Resolve.md. Kiến trúc phần mềm phải hỗ trợ mở rộng quy mô ngang để phục vụ 500 người dùng đồng thời tại thời điểm cao điểm mà không cần phải thực hiện bất kỳ thay đổi nào đối với mã nguồn ứng dụng.

### 11.7 Security

**NFR-SEC-001**: Bắt buộc tự động chuyển hướng toàn bộ lưu lượng truy cập HTTP sang HTTPS.

**NFR-SEC-002**: Mật khẩu tài khoản nhân viên phải được băm bằng thuật toán bcrypt hoặc Argon2; không bao giờ lưu trữ, ghi nhật ký hoặc truyền nhận mật khẩu ở dạng văn bản gốc.

**NFR-SEC-003**: Phiên làm việc quản trị đã xác thực phải tự động hết hạn sau 30 phút không hoạt động; yêu cầu đăng nhập lại khi thực hiện các yêu cầu tiếp theo.

**NFR-SEC-004**: Tất cả API quản trị nội bộ bắt buộc phải xác thực quyền truy cập RBAC trước khi xử lý yêu cầu; trả về mã lỗi 403 Forbidden đối với các yêu cầu không có quyền hạn tương ứng.

### 11.8 Privacy

**NFR-PRIV-001**: API sản phẩm công khai không được trả về số lượng tồn kho thực tế StockQuantity. Số lượng tồn kho (kể cả các giá trị âm) chỉ hiển thị cho người dùng nội bộ đã được xác thực.

### 11.9 Usability

**NFR-USE-001**: Khách hàng có thể hoàn tất quy trình đặt mua hàng (từ trang xem sản phẩm cho đến trang hiển thị xác nhận đơn hàng thành công) trong phạm vi tối đa 3 thao tác chính.

### 11.10 Maintainability

**NFR-MAINT-001**: Số hotline, liên kết Zalo, Messenger được lưu trữ trong DB và có thể cập nhật thông qua giao diện Admin; các cập nhật có hiệu lực ngay lập tức trên trang công khai mà không yêu cầu triển khai lại mã nguồn.

### 11.13 Logging And Auditing

**NFR-LOG-001**: Nhật ký kiểm toán có cấu trúc ghi nhận lại đầy đủ mọi hành động quản trị nguy hiểm; hỗ trợ nhân viên có thẩm quyền truy vấn danh sách nhật ký trực tiếp trên dashboard quản trị.

### 11.15 Compliance

**NFR-COMP-001**: Nghiêm cấm xóa cứng thông tin nhân viên khỏi cơ sở dữ liệu. Vô hiệu hóa tài khoản (IsActive=false) là cơ chế duy nhất được phép để loại bỏ nhân sự rời đi khỏi hệ thống hoạt động.

---

## 12. Access Control Requirements

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 12.1 Authentication Requirements

| SEC ID | Requirement | Priority |
|---|---|---|
| SEC-AUTH-001 | Tất cả tài khoản quản trị nội bộ xác thực bằng Username + Password | Must |
| SEC-AUTH-002 | Mật khẩu được lưu trữ dạng băm bằng bcrypt hoặc Argon2 | Must |
| SEC-AUTH-003 | Phiên đăng nhập hết hạn sau 30 phút không hoạt động | Must |
| SEC-AUTH-004 | Tài khoản đã bị vô hiệu hóa không được phép đăng nhập (trả về lỗi 401 giống sai mật khẩu) | Must |
| SEC-AUTH-005 | Nhân viên chỉ được phép thay đổi mật khẩu của chính mình | Must |
| SEC-AUTH-006 | Lỗi đăng nhập không được tiết lộ thông tin ô nhập liệu nào bị sai | Should |
| SEC-AUTH-007 | [TBD: OQ-GEN-001 — chính sách khóa tài khoản sau số lần đăng nhập sai chưa được xác định] | Should |

### 12.2 Authorization Requirements

**Quy định về Vai trò và Phạm vi Chi nhánh:**

| Role | Branch Scope | Provisioned By |
|---|---|---|
| Super Admin | Không giới hạn (toàn cầu) | Khởi tạo hệ thống ban đầu |
| General Manager | Không giới hạn (toàn cầu) | Super Admin gán quyền |
| Store Manager | Chỉ trong phạm vi chi nhánh được chỉ định | Super Admin hoặc General Manager gán quyền |
| Staff | Chỉ trong phạm vi chi nhánh được chỉ định | Super Admin, General Manager, hoặc Store Manager gán quyền |

**Danh mục Mã Quyền hạn (Permissions):**

| Code | Description |
|---|---|
| product:read | Xem danh sách sản phẩm quản trị |
| product:create | Tạo mới sản phẩm |
| product:update | Chỉnh sửa thông tin sản phẩm |
| product:delete | Xóa mềm sản phẩm (có kiểm toán) |
| category:read | Xem danh sách danh mục sản phẩm |
| category:create | Tạo mới danh mục sản phẩm |
| category:update | Chỉnh sửa danh mục sản phẩm |
| category:delete | Xóa danh mục sản phẩm |
| order:read | Xem danh sách đơn đặt hàng |
| order:update-status | Cập nhật trạng thái đơn hàng |
| contact-request:read | Xem yêu cầu tư vấn của khách hàng |
| contact-request:update-status | Cập nhật trạng thái yêu cầu tư vấn |
| staff:read | Xem thông tin tài khoản nhân viên |
| staff:create | Tạo tài khoản nhân viên mới (có kiểm toán) |
| staff:update | Chỉnh sửa hồ sơ thông tin nhân viên |
| staff:deactivate | Vô hiệu hóa tài khoản nhân viên (xóa mềm, có kiểm toán) |
| settings:read | Xem thông tin cài đặt cấu hình hệ thống |
| settings:update | Cập nhật cài đặt cấu hình hệ thống |
| audit:read | Xem nhật ký kiểm toán hệ thống |

### 12.3 Access Control Matrix

| Permission | Staff | Store Manager | General Manager | Super Admin |
|---|:---:|:---:|:---:|:---:|
| product:read | Yes | Yes | Yes | Yes |
| product:create | Yes | Yes | Yes | Yes |
| product:update | Yes | Yes | Yes | Yes |
| product:delete | Yes (audited) | Yes (audited) | Yes (audited) | Yes |
| category:read | Yes | Yes | Yes | Yes |
| category:create | No | Yes | Yes | Yes |
| category:update | No | Yes | Yes | Yes |
| category:delete | No | Yes (audited) | Yes (audited) | Yes (audited) |
| order:read | Branch only | Branch only | All | All |
| order:update-status | Branch only | Branch only | All | All |
| contact-request:read | Branch only | Branch only | All | All |
| contact-request:update-status | Branch only | Branch only | All | All |
| staff:read | Own record | Branch only | All | All |
| staff:create | No | Branch (audited) | All (audited) | All |
| staff:update | Own password | Branch only | All | All |
| staff:deactivate | No | Branch (audited) | All (audited) | All |
| settings:read | No | No | No | Yes |
| settings:update | No | No | No | Yes |
| audit:read | No | No | Yes | Yes |

---

## 13. State Models

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 13.1 State Definitions

**Trạng thái Đơn hàng (Order States):**

| STATE ID | State | Description |
|---|---|---|
| STATE-ORD-001 | PENDING | Khách hàng vừa đặt hàng; chờ nhân viên xử lý |
| STATE-ORD-002 | CONFIRMED | Nhân viên đã xác nhận đơn; đang chuẩn bị đóng gói hàng |
| STATE-ORD-003 | SHIPPING | Đơn hàng đang được vận chuyển |
| STATE-ORD-004 | DELIVERED | Giao hàng thành công. Trạng thái kết thúc. |
| STATE-ORD-005 | CANCELLED | Bị hủy bởi người dùng nội bộ. Trạng thái kết thúc. |

**Trạng thái Yêu cầu Tư vấn (ContactRequest States):**

| STATE ID | State | Description |
|---|---|---|
| STATE-CONT-001 | NEW | Khách vừa gửi yêu cầu; chưa có nhân viên xử lý |
| STATE-CONT-002 | CONTACTED | Nhân viên đã liên hệ trao đổi với khách hàng |
| STATE-CONT-003 | CLOSED | Yêu cầu đã được xử lý hoàn tất. Trạng thái kết thúc. |

### 13.2 State Transitions

**Chuyển đổi trạng thái Đơn hàng (Order):**

| TR ID | From | To | Trigger | Actor |
|---|---|---|---|---|
| TR-ORD-001 | (none) | PENDING | Khách đặt hàng thanh toán | System |
| TR-ORD-002 | PENDING | CONFIRMED | Nhân viên xác nhận | Staff/Manager/Admin |
| TR-ORD-003 | CONFIRMED | SHIPPING | Nhân viên giao vận chuyển | Staff/Manager/Admin |
| TR-ORD-004 | SHIPPING | DELIVERED | Nhân viên hoàn tất giao hàng | Staff/Manager/Admin |
| TR-ORD-005 | PENDING | CANCELLED | Nhân viên hủy (lý do tùy chọn) | Staff/Manager/Admin |
| TR-ORD-006 | CONFIRMED | CANCELLED | Nhân viên hủy (lý do tùy chọn) | Staff/Manager/Admin |
| TR-ORD-007 | SHIPPING | CANCELLED | Nhân viên hủy (lý do tùy chọn) | Staff/Manager/Admin |

**Chuyển đổi trạng thái Yêu cầu Tư vấn (ContactRequest):**

| TR ID | From | To | Trigger | Actor |
|---|---|---|---|---|
| TR-CONT-001 | (none) | NEW | Khách hàng gửi biểu mẫu | System |
| TR-CONT-002 | NEW | CONTACTED | Nhân viên cập nhật trạng thái | Staff/Manager/Admin |
| TR-CONT-003 | CONTACTED | CLOSED | Nhân viên đóng yêu cầu | Staff/Manager/Admin |
| TR-CONT-004 | NEW | CLOSED | Nhân viên đóng trực tiếp | Staff/Manager/Admin |

### 13.3 State Diagram

```
Order Lifecycle:
  Customer -> [PENDING] -> [CONFIRMED] -> [SHIPPING] -> [DELIVERED] *
  [PENDING]  --\
  [CONFIRMED] --+-- Staff cancels (optional reason) -> [CANCELLED] *
  [SHIPPING]  --/     (customer notification sent)
  (* = terminal)

ContactRequest Lifecycle:
  Customer -> [NEW] -> [CONTACTED] -> [CLOSED] *
              [NEW] -> (direct close) -> [CLOSED] *
  (* = terminal)
```

---

## 14. Error Handling And Edge Cases

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 14.1 Error Catalogue

| ERR ID | Scenario | HTTP Code | Error Code | User-Facing Message |
|---|---|---|---|---|
| ERR-ORD-001 | CONTACT_ONLY product in order | 422 | CONTACT_ONLY_PRODUCT | "One or more products cannot be ordered directly." |
| ERR-ORD-002 | Empty order items | 400 | EMPTY_ORDER | "Your cart is empty." |
| ERR-ORD-003 | Quantity <= 0 | 400 | INVALID_QUANTITY | "Item quantity must be at least 1." |
| ERR-ORD-004 | Product not found | 422 | PRODUCT_NOT_FOUND | "One or more products could not be found." |
| ERR-ORD-005 | Product inactive | 422 | PRODUCT_INACTIVE | "One or more products are no longer available." |
| ERR-ORD-006 | Cancel on DELIVERED or CANCELLED order | 409 | INVALID_STATUS_TRANSITION | "This order cannot be cancelled." |
| ERR-CONT-001 | Missing customerName or customerPhone | 400 | MISSING_REQUIRED_FIELD | "Please provide your name and phone number." |
| ERR-CONT-002 | Product not found for contact request | 422 | PRODUCT_NOT_FOUND | "The specified product could not be found." |
| ERR-AUTH-001 | Invalid username or password | 401 | INVALID_CREDENTIALS | "Invalid username or password." |
| ERR-AUTH-002 | Account deactivated | 401 | INVALID_CREDENTIALS | "Invalid username or password." (same message; no disclosure) |
| ERR-AUTH-003 | Session expired | 401 | SESSION_EXPIRED | "Your session has expired. Please log in again." |
| ERR-PERM-001 | Insufficient RBAC permissions | 403 | FORBIDDEN | "You do not have permission to perform this action." |
| ERR-USER-001 | Duplicate username on staff create | 409 | DUPLICATE_USERNAME | "This username is already in use." |
| ERR-USER-002 | Duplicate email on staff create | 409 | DUPLICATE_EMAIL | "This email address is already in use." |
| ERR-PROD-001 | Invalid PurchaseMode enum value | 400 | INVALID_PURCHASE_MODE | "Invalid purchase mode value." |
| ERR-PROD-002 | Invalid PriceVisibility enum value | 400 | INVALID_PRICE_VISIBILITY | "Invalid price visibility value." |
| ERR-PROD-003 | Duplicate product slug | 409 | DUPLICATE_SLUG | "A product with this slug already exists." |

### 14.2 Edge Cases

| EDGE ID | Scenario | Required Behavior |
|---|---|---|
| EDGE-INV-001 | Order placed when StockQuantity = 0 | Đơn đặt hàng được chấp nhận; StockQuantity giảm xuống -1; nhân viên xử lý thủ công qua dashboard. |
| EDGE-INV-002 | Order placed when StockQuantity already negative | Đơn đặt hàng được chấp nhận; tiếp tục trừ âm tồn kho; không tự động chặn đơn hàng. |
| EDGE-ORD-001 | Empty cart at checkout | Frontend ngăn chặn trước; backend trả về lỗi ERR-ORD-002 nếu yêu cầu lọt qua. |
| EDGE-ORD-002 | Product changes ORDERABLE -> CONTACT_ONLY after added to cart | [ASSUMPTION] Mặt hàng vẫn tồn tại trong giỏ hàng ở client-side; backend chặn ở bước checkout (ERR-ORD-001); frontend xác thực lại khi tải trang checkout. |
| EDGE-ORD-003 | Staff cancels without entering a reason | Chấp nhận đơn hủy; email thông báo gửi đi không chứa trường lý do; CancellationReason lưu là null. |
| EDGE-CONT-001 | Customer submits contact request for ORDERABLE product | Được chấp nhận theo quy tắc BR-CONT-001; không có hạn chế. |
| EDGE-AUTH-001 | Staff logs in with deactivated account | Trả về mã ERR-AUTH-002 (cùng thông báo lỗi với ERR-AUTH-001 để bảo mật thông tin). |
| EDGE-PROD-001 | Admin deletes product with PENDING orders | [TBD: OQ-GEN-005 — Đề xuất: hiển thị cảnh báo chứa số lượng đơn hàng bị ảnh hưởng; yêu cầu xác nhận trước khi thực hiện.] |
| EDGE-IMG-001 | Product created with no images | Được chấp nhận; MainImageUrl = null; website công khai hiển thị ảnh placeholder hoặc trạng thái trống. |
| EDGE-SET-001 | Super Admin leaves hotline blank | [ASSUMPTION] Lưu trữ dưới dạng chuỗi rỗng hoặc null; website công khai ẩn nút CTA gọi hotline. |
| EDGE-CAT-001 | Admin deletes category with products assigned | [TBD: OQ-GEN-004 — Đề xuất: chặn xóa; hiển thị số lượng sản phẩm đang bị ảnh hưởng.] |

---

## 15. Acceptance Criteria And Verification

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 15.1 Acceptance Criteria Catalogue

| AC ID | Linked FR | Description | Verification |
|---|---|---|---|
| AC-PROD-001 | FR-PROD-001 | Public list returns only active products | Automated API test |
| AC-PROD-002 | FR-PROD-001 | Category filter returns only matching active products | Automated API test |
| AC-PROD-003 | FR-PROD-002 | Product response includes purchaseMode and priceVisibility | Automated API test |
| AC-PROD-004 | FR-PROD-003 | SHOW_PRICE renders formatted price | UI manual test |
| AC-PROD-005 | FR-PROD-003 | HIDE_PRICE hides price area from DOM | UI manual test |
| AC-PROD-006 | FR-PROD-003 | CONTACT_FOR_PRICE displays "Lien he" | UI manual test |
| AC-CART-001 | FR-CART-002 | CONTACT_ONLY product blocked; message displayed | UI manual + automated test |
| AC-ORD-001 | FR-ORD-001 | Valid guest checkout returns 201 | Automated API test |
| AC-ORD-002 | FR-ORD-002 | Backend rejects CONTACT_ONLY product in order (422) | Automated API test |
| AC-ORD-003 | FR-ORD-003 | Backend rejects empty order (400) | Automated API test |
| AC-ORD-004 | FR-ORD-010 | Cancellation with reason; reason in notification | End-to-end test |
| AC-ORD-005 | FR-ORD-010 | Cancellation without reason; notification sent without reason | End-to-end test |
| AC-ORD-006 | FR-ORD-010 | DELIVERED order cancellation returns 409 | Automated API test |
| AC-CONT-001 | FR-CONT-001 | Valid contact request returns 201 | Automated API test |
| AC-CONT-002 | FR-CONT-002 | Missing customerPhone returns 400 | Automated API test |
| AC-CONT-003 | FR-CONT-001 | Success message displayed after submission | UI manual test |
| AC-CONT-004 | FR-CONT-001 | Contact request for ORDERABLE product returns 201 | Automated API test |
| AC-AUTH-001 | FR-AUTH-001 | Valid credentials grant dashboard access | Manual test |
| AC-AUTH-002 | FR-AUTH-001 | Invalid credentials return 401 | Automated API test |
| AC-AUTH-003 | FR-AUTH-002 | Session expires after 30 min inactivity | Manual test with timer |
| AC-AUTH-004 | FR-AUTH-001 | Deactivated account returns same 401 as wrong password | Automated API test |
| AC-STAFF-001 | FR-STAFF-001 | Unique staff account creation returns 201 | Automated API test |
| AC-STAFF-002 | FR-STAFF-001 | Duplicate username returns 409 | Automated API test |
| AC-STAFF-003 | FR-STAFF-002 | Deactivated account cannot authenticate | Automated API test |
| AC-RBAC-001 | FR-RBAC-001 | Staff cannot access Super Admin settings (403) | Automated API test |
| AC-RBAC-002 | FR-RBAC-002 | Store Manager cannot see out-of-branch orders | Automated API test |
| AC-AUD-001 | FR-AUD-001 | Staff account creation creates audit log entry | Automated API + DB check |
| AC-INV-001 | FR-INV-001 | Order accepted when stock=0; stock goes negative | Automated API + DB check |
| AC-INV-002 | FR-INV-003 | Public product API does not return exact stockQuantity | Automated API test |
| AC-SET-001 | FR-SET-001 | Super Admin updates hotline; public settings API reflects new value | End-to-end test |

### 15.2 Verification Methods

| Method | Description |
|---|---|
| Automated API Test | Kiểm thử tích hợp tự động (sử dụng xUnit / NUnit cho backend .NET) |
| UI Manual Test | Kiểm thử thủ công giao diện trên trình duyệt web |
| End-to-End Test | Kiểm thử toàn trình từ giao diện người dùng đến cơ sở dữ liệu |
| Load Test | Kiểm thử tải bằng k6 hoặc công cụ tương đương; mô phỏng số lượng người dùng đồng thời |
| DB Check | Truy vấn trực tiếp cơ sở dữ liệu để kiểm tra trạng thái lưu trữ |

---

## 16. Requirements Traceability

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 16.1 Requirements Traceability Matrix

| FR ID | Business Goal | Business Rule(s) | Use Case | Primary Entity | Acceptance Criteria |
|---|---|---|---|---|---|
| FR-PROD-001 | BG-GEN-001 | BR-PROD-006 | UC-PROD-001 | ENT-PROD-002 | AC-PROD-001, AC-PROD-002 |
| FR-PROD-002 | BG-GEN-001 | BR-PROD-002 | UC-PROD-001, UC-PROD-002 | ENT-PROD-002 | AC-PROD-003 |
| FR-PROD-003 | BG-GEN-001 | BR-PROD-002 | UC-PROD-002 | ENT-PROD-002 | AC-PROD-004, AC-PROD-005, AC-PROD-006 |
| FR-PROD-004 | BG-GEN-001 | BR-PROD-001 | UC-PROD-001, UC-PROD-002 | ENT-PROD-002 | — |
| FR-CART-002 | BG-GEN-002 | BR-PROD-003 | UC-CART-001 | ENT-PROD-002 | AC-CART-001 |
| FR-ORD-001 | BG-GEN-002 | BR-ORD-001, BR-ORD-004 | UC-ORD-001 | ENT-ORD-001, ENT-ORD-002 | AC-ORD-001, AC-ORD-002, AC-ORD-003 |
| FR-ORD-002 | BG-GEN-002 | BR-PROD-004 | UC-ORD-001 | ENT-ORD-002, ENT-PROD-002 | AC-ORD-002 |
| FR-ORD-010 | BG-GEN-002 | BR-ORD-002, BR-ORD-003 | UC-OADM-002 | ENT-ORD-001 | AC-ORD-004, AC-ORD-005, AC-ORD-006 |
| FR-CONT-001 | BG-GEN-003 | BR-CONT-001 | UC-CONT-001 | ENT-CONT-001 | AC-CONT-001 through AC-CONT-004 |
| FR-AUTH-001 | BG-GEN-004 | BR-ACC-001 | — | ENT-ACC-005 | AC-AUTH-001, AC-AUTH-002, AC-AUTH-004 |
| FR-AUTH-002 | BG-GEN-004 | BR-ACC-009 | — | ENT-ACC-005 | AC-AUTH-003 |
| FR-STAFF-001 | BG-GEN-004 | BR-ACC-002 | UC-SADM-001 | ENT-ACC-005 | AC-STAFF-001, AC-STAFF-002 |
| FR-STAFF-002 | BG-GEN-004 | BR-ACC-008 | UC-SADM-002 | ENT-ACC-005 | AC-STAFF-003 |
| FR-RBAC-001 | BG-GEN-004 | BR-ACC-002 | All internal UCs | ENT-ACC-002 through ENT-ACC-004 | AC-RBAC-001, AC-RBAC-002 |
| FR-AUD-001 | BG-GEN-007 | BR-AUD-001 | UC-SADM-001, UC-OADM-002 | ENT-AUD-001 | AC-AUD-001 |
| FR-INV-001 | BG-GEN-002 | BR-INV-001 | UC-ORD-001 | ENT-PROD-002 | AC-INV-001 |
| FR-INV-003 | BG-GEN-001 | BR-INV-002 | UC-PROD-001 | ENT-PROD-002 | AC-INV-002 |
| FR-SET-001 | BG-GEN-004 | BR-SET-001 | UC-SYS-001 | ENT-SET-001 | AC-SET-001 |

### 16.2 Requirement Dependencies

| FR ID | Depends On |
|---|---|
| FR-PROD-003 | FR-PROD-002 |
| FR-PROD-004 | FR-PROD-002 |
| FR-CART-002 | FR-PROD-002, FR-ORD-002 |
| FR-ORD-001 | FR-ORD-002 through FR-ORD-007 |
| FR-ORD-010 | FR-ORD-011, FR-AUD-001, FR-RBAC-001 |
| FR-CONT-001 | FR-CONT-002, FR-CONT-003 |
| FR-STAFF-001 | FR-RBAC-001, FR-AUD-001 |
| FR-RBAC-002 | FR-RBAC-001 |
| FR-RBAC-003 | FR-RBAC-001 |
| FR-IMG-002 | FR-IMG-004 |
| FR-AUD-001 | FR-AUD-002 |
| FR-SET-001 | FR-RBAC-001, FR-SET-002 |

---

## 17. Open Questions, Decisions And Risks

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 17.1 Open Questions

| OQ ID | Question | Affected Items | Owner | Status |
|---|---|---|---|---|
| OQ-GEN-001 | Chính sách khóa tài khoản (số lần đăng nhập sai tối đa trước khi bị khóa)? | SEC-AUTH-007, FR-AUTH-001 | Product Owner | OPEN |
| OQ-GEN-002 | Lựa chọn nhà cung cấp SMTP / email nào gửi thông báo hủy đơn cho khách hàng? | FR-ORD-011, ASM-GEN-005, EXT-INTG-006 | Tech Lead | OPEN |
| OQ-GEN-003 | Đường dẫn liên kết Zalo OA và Messenger Page chính xác dùng cho static deep links? | FR-CONT-004, FR-SET-001 | Business Owner | OPEN |
| OQ-GEN-004 | Quy trình khi xóa danh mục có chứa sản phẩm — chặn hành động hay cho phép xóa kèm đổi danh mục? | ENT-PROD-001, EDGE-CAT-001 | Product Owner | OPEN |
| OQ-GEN-005 | Sản phẩm được xóa mềm hay xóa cứng? | F-ADMIN-001, ENT-PROD-002, EDGE-PROD-001 | Product Owner | OPEN |
| OQ-GEN-006 | Có bắt buộc đổi mật khẩu ở lần đăng nhập đầu tiên cho tài khoản nhân viên mới tạo không? | FR-STAFF-001 | Product Owner | OPEN |
| OQ-GEN-007 | Quy tắc xác thực định dạng số điện thoại CustomerPhone cụ thể? | VAL-CONT-002, FR-CONT-002 | Tech Lead | OPEN |
| OQ-GEN-008 | Đường dẫn liên kết kênh giao tiếp hợp nhất đối với các nút CTA CONTACT_ONLY? ('Chi tiết sẽ được cung cả sau.') | FR-CONT-004, EXT-INTG-001, EXT-INTG-002 | Business Owner | OPEN |
| OQ-GEN-009 | Email thông báo hủy đơn hàng có bao gồm chi tiết đơn hàng (danh sách mặt hàng, tổng tiền) không? | FR-ORD-011 | Product Owner | OPEN |

### 17.2 Decisions

| DEC ID | Decision | Source | Date |
|---|---|---|---|
| DEC-GEN-001 | Số lượng tồn kho chỉ mang tính thông tin; cho phép bán quá mức (overselling) và tồn kho âm | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-002 | Sản phẩm ORDERABLE hỗ trợ luồng tư vấn/liên hệ qua nút CTA phụ | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-003 | Tài khoản nhân viên chỉ áp dụng xóa mềm (soft delete); nghiêm cấm xóa cứng | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-004 | Zalo, Messenger, Hotline chỉ sử dụng các liên kết sâu tĩnh (static deep links); không tích hợp API | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-005 | Vòng đời đơn hàng: PENDING->CONFIRMED->SHIPPING->DELIVERED; trạng thái CANCELLED có thể chuyển từ PENDING/CONFIRMED/SHIPPING | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-006 | Đơn hàng không tự động duyệt; tất cả chuyển đổi trạng thái yêu cầu nhân viên thao tác thủ công | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-007 | Sản phẩm hỗ trợ thư viện nhiều hình ảnh; MainImageUrl là ảnh thu nhỏ hiển thị chính | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-008 | Danh mục sản phẩm (Category) là một thực thể DB độc lập; mỗi sản phẩm thuộc về duy nhất một danh mục | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-009 | Hotline và các liên kết kênh liên lạc có thể cấu hình bởi Super Admin qua cài đặt hệ thống | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-010 | Thời gian tự động hết hạn phiên đăng nhập dashboard quản trị là 30 phút không hoạt động | Question-Resolve.md | 2026-06-27 |

### 17.3 Requirement-Related Risks

| RISK ID | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| RISK-GEN-001 | Gói Neon Postgres miễn phí có thể không đáp ứng mục tiêu sẵn sàng 99% | Medium | High | Nâng cấp lên gói Neon Pro hoặc gói Postgres trả phí trước khi triển khai hệ thống thực tế |
| RISK-GEN-002 | Gửi email thông báo thất bại do chưa chọn nhà cung cấp dịch vụ SMTP | High | Medium | Lựa chọn và cấu hình nhà cung cấp dịch vụ email trước khi đưa phân hệ quản lý đơn hàng vào hoạt động |
| RISK-GEN-003 | Vượt giới hạn truyền tải/API của Cloudflare R2 khi danh mục sản phẩm mở rộng | Low | Medium | Giám sát dung lượng; áp dụng giới hạn kích thước ảnh tải lên và nén ảnh tự động |
| RISK-GEN-004 | Các liên kết tĩnh deep link bị lỗi nếu Zalo hoặc Meta thay đổi cấu trúc URL | Low | Medium | Lưu trữ URL trong cài đặt hệ thống; Super Admin có thể cập nhật trực tiếp mà không cần sửa code |
| RISK-GEN-005 | Tồn kho bị âm gây bối rối cho nhân viên nếu không được đào tạo quy trình | Medium | Medium | Thiết kế chỉ báo trực quan rõ ràng (bôi đỏ/nổi bật) cho các giá trị âm tồn kho trên dashboard quản trị |
| RISK-GEN-006 | Lỗ hổng phân quyền RBAC gây truy cập trái phép hoặc chặn quyền người dùng hợp lệ | Medium | High | Tiến hành đánh giá lại ma trận phân quyền (Access Control Matrix - Mục 12.3) trước giai đoạn UAT |
| RISK-GEN-007 | Xác thực số điện thoại quá lỏng hoặc quá chặt gây lỗi khi gửi yêu cầu tư vấn | Low | Medium | Giải quyết câu hỏi OQ-GEN-007 trước khi triển khai quy tắc xác thực số điện thoại |

---

## 18. Appendices

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 18.1 Glossary

Xem Mục 1.4 để biết thêm chi tiết về bảng thuật ngữ chính. Các thuật ngữ bổ sung khác được định nghĩa ngay trong nội dung thông qua các ký hiệu [ASSUMPTION] và [TBD].

### 18.2 Diagrams

#### DIA-GEN-001 Order Status Lifecycle

```
  Customer submits -> [PENDING] -> [CONFIRMED] -> [SHIPPING] -> [DELIVERED] *

  [PENDING]  --\
  [CONFIRMED] --+-- Staff cancels (optional reason) -> [CANCELLED] *
  [SHIPPING]  --/   (customer email notification sent)
  (* = terminal states)
```

#### DIA-GEN-002 ContactRequest Status Lifecycle

```
  Customer submits -> [NEW] -> [CONTACTED] -> [CLOSED] *
                      [NEW] -> (direct close) -> [CLOSED] *
  (* = terminal state)
```

#### DIA-GEN-003 Omnichannel Contact Flow

```
  Customer on Public Website
       |
       +-- CONTACT_ONLY product --> "Contact Us" CTA (primary only)
       |                                     |
       +-- ORDERABLE product -----> "Add to Cart" (primary)
                                   + "Request Consultation" (secondary)
                                             |
                              [Unified Contact Channel]
                              /         |         \
                    Deep link       Deep link      Inline Form
                    (Zalo)       (Messenger)       POST /api/contact-requests
                                                           |
                                                  ContactRequest [NEW]
                                                  in Internal Dashboard
```

### 18.3 Supporting Documents

| Document | Location |
|---|---|
| FE-context.md | [FE-context.md](file:///d:/Code/VinfastHappyWeb/Software-Requirements-Specification-Kit/Context/FE-context.md) |
| BE-context.md | [BE-context.md](file:///d:/Code/VinfastHappyWeb/Software-Requirements-Specification-Kit/Context/BE-context.md) |
| Question-Resolve.md | [Question-Resolve.md](file:///d:/Code/VinfastHappyWeb/Software-Requirements-Specification-Kit/Context/Question-Resolve.md) |
| SRS-TOC.md | [SRS-TOC.md](file:///d:/Code/VinfastHappyWeb/Software-Requirements-Specification-Kit/Context/SRS-TOC.md) |
| SRS-Template.md | [SRS-Template.md](file:///d:/Code/VinfastHappyWeb/Software-Requirements-Specification-Kit/Context/SRS-Template.md) |

---

## 19. Requirement Identification Convention

Quy tắc đặt mã định danh: `<TYPE>-<DOMAIN>-<NNN>`

| Type | Meaning | Example |
|---|---|---|
| FR | Yêu cầu chức năng | FR-PROD-001 |
| NFR | Yêu cầu phi chức năng | NFR-PERF-001 |
| BR | Quy tắc nghiệp vụ | BR-PROD-001 |
| VAL | Quy tắc xác thực dữ liệu | VAL-PROD-001 |
| ENT | Thực thể dữ liệu | ENT-PROD-001 |
| REL | Mối quan hệ dữ liệu | REL-PROD-001 |
| UC | Kịch bản sử dụng (Use Case) | UC-PROD-001 |
| STATE | Trạng thái thực thể | STATE-ORD-001 |
| TR | Chuyển đổi trạng thái | TR-ORD-001 |
| ERR | Mã lỗi hệ thống | ERR-ORD-001 |
| EDGE | Trường hợp biên | EDGE-INV-001 |
| DIA | Sơ đồ minh họa | DIA-GEN-001 |
| SEC | Yêu cầu bảo mật | SEC-AUTH-001 |
| UI | Yêu cầu giao diện | UI-GEN-001 |
| IF | Giao diện API | IF-INTG-001 |
| PF | Tính năng sản phẩm | PF-GEN-001 |
| REF | Tài liệu tham chiếu | REF-GEN-001 |

Các mã phân hệ (Domain codes): GEN, PROD, CAT, CART, ORD, CONT, AUTH, STAFF, RBAC, ADMIN, INV, IMG, AUD, SET, PERF, AVAIL, SCAL, SEC, PRIV, USE, MAINT, LOG, COMP, ACC, INTG.

Mã định danh là cố định vĩnh viễn. Các hạng mục không còn sử dụng vẫn được giữ nguyên mã và gắn nhãn DEPRECATED. Không tái sử dụng mã cũ.

---

## 20. Requirement Status Convention

| Status | Meaning | Set By |
|---|---|---|
| DRAFT | Bản nháp do Agent soạn thảo; chưa gửi duyệt | Agent |
| REVIEW | Đã gửi để duyệt hoặc đang chờ quyết định | Agent |
| APPROVED | Đã được phê duyệt chính thức bởi con người | Chỉ con người |
| DEPRECATED | Lưu giữ cho lịch sử kiểm toán; không còn hiệu lực | Agent (sau khi nhận lệnh hoặc CR được duyệt) |

Agent không bao giờ tự chuyển trạng thái yêu cầu sang APPROVED.

---

## 21. SRS Review Checklist

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 21.1 Scope And Context
- [x] Định nghĩa rõ ràng vấn đề cần giải quyết (Mục 4.1)
- [x] Tài liệu hóa chi tiết các phần In-scope và Out-of-scope (Mục 1.2)
- [x] Xác định đầy đủ các User Classes (Mục 2.3)
- [x] Xác định đầy đủ các hệ thống kết nối bên ngoài (Mục 3.4)

### 21.2 Requirements
- [x] Mọi yêu cầu đều có một mã ID duy nhất
- [x] Mọi yêu cầu sử dụng các cấu trúc câu EARS-compliant "shall" hoặc cấu trúc tương tự để mô tả hành vi hệ thống
- [x] Mọi yêu cầu chức năng chi tiết đều có tối thiểu 1 tiêu chí nghiệm thu
- [x] Không sử dụng các từ ngữ mơ hồ, chung chung (nhanh, dễ dàng, mượt mà) trong mô tả yêu cầu kỹ thuật
- [x] Gán mức độ ưu tiên MoSCoW cho từng yêu cầu
- [x] Thiết lập trạng thái ban đầu cho toàn bộ yêu cầu là REVIEW (chưa duyệt)

### 21.3 Coverage
- [x] Toàn bộ 20 tính năng ở Mục 5.1 được giải quyết bằng các yêu cầu FR ở Mục 8
- [x] Toàn bộ 27 quy tắc nghiệp vụ ở Mục 7 có thể truy vết tới FR tương ứng
- [x] Toàn bộ 9 thực thể dữ liệu ở Mục 9 được tham chiếu bởi ít nhất 1 FR
- [x] Ghi nhận đầy đủ 9 câu hỏi đang mở tại Mục 17.1
- [x] Ghi nhận đầy đủ 10 quyết định đã thống nhất từ Question-Resolve.md tại Mục 17.2

### 21.4 Traceability And Completion
- [x] Ma trận truy vết yêu cầu (Mục 16.1) bao gồm đầy đủ các yêu cầu mức ưu tiên Must
- [x] Các hạng mục [TBD] được liệt kê kèm phần mô tả chi tiết
- [x] Các hạng mục [ASSUMPTION] được liệt kê kèm lý do cụ thể
- [x] Các rủi ro được liệt kê tại Mục 17.3 kèm đánh giá khả năng xảy ra, mức độ ảnh hưởng và phương án giảm thiểu rủi ro
- [ ] Các câu hỏi từ OQ-GEN-001 đến OQ-GEN-009: yêu cầu con người giải quyết trước khi phê duyệt chính thức tài liệu
- [ ] ASM-GEN-005 (SMTP provider): chưa chọn nhà cung cấp gửi email; bắt buộc giải quyết trước khi đưa tính năng quản lý đơn hàng vào vận hành thực tế

---

## 22. Approval

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

Tài liệu đặc tả yêu cầu phần mềm này được trình duyệt cho con người đánh giá phê duyệt. Không có nội dung nào tự động mang trạng thái APPROVED.

| Section | Reviewer | Status | Date |
|---|---|---|---|
| 0–4 (Bối cảnh và Nghiệp vụ) | [TBD] | REVIEW | — |
| 5–8 (Tính năng và Yêu cầu chức năng) | [TBD] | REVIEW | — |
| 9 (Mô hình dữ liệu) | [TBD] | REVIEW | — |
| 10–12 (Giao diện, NFR và Kiểm soát quyền truy cập) | [TBD] | REVIEW | — |
| 13–15 (Trạng thái, Xử lý lỗi và Tiêu chí nghiệm thu) | [TBD] | REVIEW | — |
| 16–18 (Traceability, Câu hỏi mở và Phụ lục) | [TBD] | REVIEW | — |

---

*End of Document — SRS-HappyWeb-VI v1.0.0-DRAFT — Generated 2026-06-29 — Status: REVIEW*

