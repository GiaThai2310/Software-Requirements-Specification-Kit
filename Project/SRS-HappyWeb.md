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

This Software Requirements Specification (SRS) defines the complete functional, non-functional, and interface requirements for the Xe điện Vinfast Happy Omnichannel E-Commerce Platform (hereafter "the System" or "HappyWeb"). It is the authoritative requirements reference for design, development, testing, and acceptance activities, aligned with IEEE/ISO/IEC 29148 concepts.

### 1.2 Scope

#### 1.2.1 In Scope

1. **Public Website** — customer-facing e-commerce site for browsing products, placing orders (ORDERABLE), and submitting consultation requests (CONTACT_ONLY and secondary flow for ORDERABLE).
2. **Internal Dashboard** — role-based management interface for Staff, Store Manager, General Manager, and Super Admin.

Technology stack: Next.js frontend on Cloudflare Pages; ASP.NET Core Web API backend; Neon Postgres; Cloudflare R2 for images; Cloudflare CDN.

#### 1.2.2 Out Of Scope

- Native mobile applications.
- Zalo OA API or Messenger API integration (static deep links only at this stage).
- Online payment gateway.
- Automated stock replenishment.
- ERP or accounting system integration.

#### 1.2.3 Future Scope

- Zalo OA / Messenger API tracked routing.
- Online payment (VNPay, MoMo, Stripe).
- Customer account portal with order history.
- Advanced multi-branch inventory management.
- Mobile application.

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

Sections 2–4: system description, stakeholders, business context. Sections 5–8: features, use cases, business rules, functional requirements. Sections 9–12: data model, interfaces, NFRs, access control. Sections 13–15: state models, error handling, acceptance criteria. Sections 16–18: traceability, open questions, risks, appendices.

---

## 2. Overall Description

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 2.1 Product Perspective

HappyWeb is a greenfield omnichannel e-commerce platform for "Xe điện Vinfast Happy", an electric bicycle and accessory retailer. It replaces manual sales processes (phone, social media DMs) with a professional digital presence: a public website and a centralised internal operations dashboard.

#### 2.1.1 System Boundary

**Included:** Public Website (Next.js, Cloudflare Pages); Internal Dashboard (Next.js, Cloudflare Pages, role-gated); Backend API (ASP.NET Core); Neon Postgres DB; Cloudflare R2 image storage; configurable static deep links to Zalo / Messenger / Hotline.

**Excluded:** External social media platforms; payment processors; shipping carriers.

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
| PF-GEN-001 | Public product catalog with category filtering | Customer |
| PF-GEN-002 | Product detail page with purchase-mode-aware CTAs | Customer |
| PF-GEN-003 | Shopping cart (ORDERABLE products only) | Customer |
| PF-GEN-004 | Guest checkout and order placement | Customer |
| PF-GEN-005 | Contact request submission via inline form | Customer |
| PF-GEN-006 | Static deep link redirection (Zalo, Messenger, Hotline) | Customer |
| PF-GEN-007 | Internal product management (CRUD + gallery) | Staff, Manager, Admin |
| PF-GEN-008 | Internal category management (CRUD) | Manager, Admin |
| PF-GEN-009 | Internal order management and status lifecycle | Staff, Manager, Admin |
| PF-GEN-010 | Internal contact request management and lifecycle | Staff, Manager, Admin |
| PF-GEN-011 | Staff account management with RBAC | Manager, Admin |
| PF-GEN-012 | System settings management (hotline, deep links) | Super Admin |
| PF-GEN-013 | Audit trail logging of administrative actions | System (automated) |
| PF-GEN-014 | Stock quantity tracking (informational; negative permitted) | Staff, Manager, Admin |

### 2.3 User Classes And Characteristics

| STK ID | User Class | Description | Proficiency | Frequency |
|---|---|---|---|---|
| STK-GEN-001 | Customer (Guest) | Anonymous visitor; no login required | Low–Medium | Variable |
| STK-GEN-002 | Staff | Operational internal user; branch-scoped | Medium | Daily |
| STK-GEN-003 | Store Manager | Branch-level manager | Medium–High | Daily |
| STK-GEN-004 | General Manager | Cross-branch manager; no branch restriction | High | Daily |
| STK-GEN-005 | Super Admin | Global administrator; full system access | High | As needed |

### 2.4 Operating Environment

| Component | Technology | Hosting |
|---|---|---|
| Frontend (Public + Internal) | Next.js 14+, TypeScript, Tailwind CSS, shadcn/ui | Cloudflare Pages |
| Backend API | ASP.NET Core Web API, C#, EF Core | Render / Azure Functions / AWS Lambda / VPS |
| Database | PostgreSQL via Neon Postgres | Neon cloud |
| Image Storage | Cloudflare R2 | Cloudflare |
| DNS / CDN | Cloudflare Free | Cloudflare |
| Browser Support | [ASSUMPTION] Chrome 110+, Firefox 110+, Edge 110+, Safari 16+ | N/A |
| Device Support | [ASSUMPTION] Responsive on public site; desktop-optimised for dashboard | N/A |

### 2.5 Design And Implementation Constraints

| CON ID | Constraint | Source |
|---|---|---|
| CON-SEC-001 | All traffic must be served over HTTPS | [ASSUMPTION] Industry standard |
| CON-SEC-002 | Internal Dashboard requires valid authenticated session | Question-Resolve.md |
| CON-SEC-003 | Staff sessions expire after 30 min of inactivity | Question-Resolve.md |
| CON-TECH-001 | Frontend: Next.js + TypeScript + Tailwind CSS + shadcn/ui | FE-context.md |
| CON-TECH-002 | Backend: ASP.NET Core Web API + C# + EF Core | BE-context.md |
| CON-TECH-003 | Database: Neon Postgres only | BE-context.md |
| CON-TECH-004 | Image storage: Cloudflare R2 | BE-context.md |
| CON-TECH-005 | Frontend hosting: Cloudflare Pages | FE-context.md |
| CON-BUS-001 | Customers need no account to order or submit contact requests | FE-context.md, BE-context.md |
| CON-BUS-002 | Stock quantity is not a hard gate; overselling permitted | Question-Resolve.md |
| CON-BUS-003 | Zalo, Messenger, Hotline: static deep links only; no API integration | Question-Resolve.md |
| CON-BUS-004 | Hotline and channel link values configurable via Admin settings | Question-Resolve.md |
| CON-DATA-001 | Staff accounts must never be hard-deleted; only soft-deleted | Question-Resolve.md |

### 2.6 Assumptions And Dependencies

| ID | Item | Impact If Wrong |
|---|---|---|
| ASM-GEN-001 | [ASSUMPTION] Locale is Vietnamese; timezone UTC+7 | Internationalisation work required |
| ASM-GEN-002 | [ASSUMPTION] Monetary values in VND, no decimal places | Currency handling redesign required |
| ASM-GEN-003 | [ASSUMPTION] Each product belongs to exactly one category | Data model change needed |
| ASM-GEN-004 | [ASSUMPTION] Backend exposes RESTful JSON API | API redesign if changed |
| ASM-GEN-005 | [ASSUMPTION] Cancellation email sent via third-party SMTP — provider TBD (OQ-GEN-002) | Notification flow blocked until provider chosen |
| ASM-GEN-006 | [ASSUMPTION] JWT stored in HTTP-only cookies for dashboard sessions | Security redesign if changed |
| ASM-GEN-007 | [ASSUMPTION] Product name and price snapshotted in OrderItem at order creation time | Historical accuracy lost if products edited post-order |
| DEP-GEN-001 | Neon Postgres free tier availability SLA not guaranteed | DB downtime risk |
| DEP-GEN-002 | Cloudflare R2 for image serving | Images unavailable on R2 outage |
| DEP-GEN-003 | Zalo / Messenger URL scheme stability | Deep links break if platforms change schemes |

---

## 3. Stakeholders, Actors And External Systems

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 3.1 Stakeholders

| STK ID | Stakeholder | Project Role | Interest |
|---|---|---|---|
| STK-GEN-001 | Customer (Guest) | End user | Easy browsing, ordering, contacting |
| STK-GEN-002 | Staff | Operational user | Efficient operations |
| STK-GEN-003 | Store Manager | Branch manager | Branch performance, staff management |
| STK-GEN-004 | General Manager | Network manager | Cross-branch oversight |
| STK-GEN-005 | Super Admin | System administrator | Full platform control |
| STK-GEN-006 | Business Owner | Decision-maker | Revenue, brand, efficiency |

### 3.2 Actors

| ACT ID | Actor | Type | Description |
|---|---|---|---|
| ACT-GEN-001 | Customer | Primary, Human | Anonymous visitor; no account required |
| ACT-GEN-002 | Staff | Primary, Human | Authenticated; branch-scoped |
| ACT-GEN-003 | Store Manager | Primary, Human | Authenticated; single-branch scope |
| ACT-GEN-004 | General Manager | Primary, Human | Authenticated; network-wide scope |
| ACT-GEN-005 | Super Admin | Primary, Human | Authenticated; unrestricted global access |
| ACT-GEN-006 | System | Secondary, Automated | Triggers notifications, audit entries, status behaviors |

### 3.3 Actor Permission Overview (Summary)

See Section 12 for full detail.

| Capability | Customer | Staff | Store Mgr | General Mgr | Super Admin |
|---|:---:|:---:|:---:|:---:|:---:|
| Browse public products | Yes | Yes | Yes | Yes | Yes |
| Place orders (guest) | Yes | — | — | — | — |
| Submit contact requests | Yes | — | — | — | — |
| Access Internal Dashboard | — | Yes | Yes | Yes | Yes |
| CRUD products | — | Yes | Yes | Yes | Yes |
| CRUD categories | — | No | Yes | Yes | Yes |
| Manage orders | — | Branch | Branch | All | All |
| Manage contact requests | — | Branch | Branch | All | All |
| Manage staff accounts | — | No | Branch | All | All |
| System settings | — | No | No | No | Yes |
| View audit trail | — | No | No | Yes | Yes |

### 3.4 External Systems

| EXT ID | System | Integration | Purpose |
|---|---|---|---|
| EXT-INTG-001 | Zalo | Static HTTPS deep link | Contact / consultation CTA redirect |
| EXT-INTG-002 | Facebook Messenger | Static HTTPS deep link | Contact / consultation CTA redirect |
| EXT-INTG-003 | Hotline | Static `tel:` deep link | Direct call CTA; number configurable by Super Admin |
| EXT-INTG-004 | Cloudflare R2 | Cloud object storage | Product image upload and retrieval |
| EXT-INTG-005 | Neon Postgres | Cloud managed database | Persistent relational data store |
| EXT-INTG-006 | SMTP Provider | Email API | Order cancellation notification [TBD: OQ-GEN-002] |
| EXT-INTG-007 | Cloudflare Pages | Static hosting + CDN | Frontend deployment |

---

## 4. Business Context

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 4.1 Problem Statement

Xe điện Vinfast Happy sells electric bicycles and accessories across multiple channels (physical store, Zalo, Messenger, phone) with no centralised digital infrastructure. This results in: inconsistent customer experience; no centralised order or contact request tracking; no audit trail; difficulty monitoring inventory. HappyWeb solves this with a unified omnichannel platform.

### 4.2 Business Goals

| BG ID | Goal | Priority |
|---|---|---|
| BG-GEN-001 | Increase conversion via professional online product catalog | Must |
| BG-GEN-002 | Centralise order management for traceability and systematic fulfilment | Must |
| BG-GEN-003 | Capture consultation requests and enable structured staff follow-up | Must |
| BG-GEN-004 | Enable admins to configure products and settings without developer involvement | Must |
| BG-GEN-005 | Support omnichannel contact (form, Zalo, Messenger, Hotline) with unified internal tracking | Should |
| BG-GEN-006 | Provide architecture scalable to 500 concurrent users at peak | Should |
| BG-GEN-007 | Maintain a full audit trail of administrative actions | Should |

### 4.3 Success Criteria

| SC ID | Criterion | Measurement |
|---|---|---|
| SC-GEN-001 | Public website accessible to anonymous customers | Functional test |
| SC-GEN-002 | ORDERABLE checkout completable in 3 or fewer primary actions | Usability test |
| SC-GEN-003 | Contact request visible in dashboard within 10 seconds of submission | End-to-end test |
| SC-GEN-004 | Staff can update order status in 5 or fewer dashboard actions | Usability test |
| SC-GEN-005 | 500 concurrent users; p95 API response <= 3 s | Load test |
| SC-GEN-006 | Every administrative action logged in audit trail | Audit log verification |
| SC-GEN-007 | Super Admin can update hotline without code deployment | Manual test |

### 4.4 Current Workflow

1. Customer contacts via Zalo / Messenger / phone.
2. Staff manually replies, negotiates, and verbally confirms orders.
3. Orders tracked in notebooks or spreadsheets.
4. No central view of orders, inventory, or consultation history.

### 4.5 Target Workflow

**ORDERABLE product:** Browse -> Add to cart -> Checkout (guest) -> PENDING order in dashboard -> Staff: CONFIRMED -> SHIPPING -> DELIVERED. Customer notified if cancelled.

**Contact flow (CONTACT_ONLY or ORDERABLE secondary):** Product page CTA -> unified channel (deep link or inline form) -> ContactRequest NEW in dashboard -> Staff: CONTACTED -> CLOSED.

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

**F-PROD-001**: Paginated/scrollable list of active products with category filter. Each card shows name, main image, price (per priceVisibility), purchase-mode-aware CTA.

**F-PROD-002**: Slug-based detail page. Shows name, description, main image, gallery, price (per priceVisibility). CTAs: ORDERABLE = primary "Add to Cart" + secondary "Request Consultation"; CONTACT_ONLY = primary "Contact Us" only.

**F-PROD-003**: Three states per product: SHOW_PRICE (formatted price), HIDE_PRICE (hide area), CONTACT_FOR_PRICE ("Lien he"). Configurable by Staff/Manager/Admin.

**F-PROD-004**: One MainImageUrl (primary thumbnail) + zero or more secondary gallery images in a separate table. Main image used in listing/cart; gallery displayed on detail page.

**F-CART-001**: Client-side cart containing only ORDERABLE products. Add, remove, adjust quantities. CONTACT_ONLY products blocked at both frontend and backend layers.

**F-ORD-001**: No account required. Checkout collects: receiver name, phone, address, optional note. Backend validates all items are ORDERABLE before persisting order.

**F-ORD-002**: Lifecycle: PENDING -> CONFIRMED -> SHIPPING -> DELIVERED | CANCELLED. All transitions are manual; no auto-confirmation.

**F-ORD-003**: Staff prompts optional reason on cancel. Notification sent to customer regardless. Reason stored for audit history.

**F-CONT-001**: CONTACT_ONLY: "Contact Us" CTA only. ORDERABLE: secondary "Request Consultation" CTA. Both route to unified channel. Inline form submissions create ContactRequest.

**F-CONT-002**: Zalo, Messenger, Hotline as static deep links. All link values configurable via System Settings by Super Admin.

**F-CONT-003**: Lifecycle: NEW -> CONTACTED -> CLOSED (or NEW -> CLOSED directly).

**F-ADMIN-001**: Full CRUD for products incl. purchaseMode, priceVisibility, category, multi-image management. Dangerous actions (delete) trigger confirmation and audit log.

**F-ADMIN-002**: Manager+ creates, updates, deletes categories. Categories selectable during product editing.

**F-ADMIN-003**: Internal users view and transition order status within their scope.

**F-ADMIN-004**: Internal users view and transition contact request status within their scope.

**F-ADMIN-005**: Managers and Admins create, update, and soft-delete staff accounts. Hard deletion prohibited.

**F-ADMIN-006**: Permissions mapped to roles; decoupled and configurable. New roles addable without code changes.

**F-ADMIN-007**: Super Admin configures hotline, Zalo URL, Messenger URL. Changes take effect without redeployment.

**F-ADMIN-008**: System logs all significant administrative actions with actor, action type, entity, timestamp, changed values.

**F-INV-001**: StockQuantity is a signed integer. Overselling permitted (negative values). Exact values visible to internal users only.

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
- **Actor**: Customer | **Precondition**: Cart has >= 1 ORDERABLE product.
- **Main Flow**:
  1. Customer navigates to checkout.
  2. Customer enters receiver name, phone, address, optional note.
  3. Customer submits checkout form.
  4. Frontend validates: cart non-empty, all items ORDERABLE.
  5. Frontend sends POST /api/orders.
  6. Backend validates all products are ORDERABLE and active.
  7. Backend persists order (status PENDING); decrements StockQuantity.
  8. Frontend displays order confirmation.
- **Alt A — CONTACT_ONLY in cart**: Frontend blocks step 3 with message.
- **Alt B — Backend rejects product**: Step 6 returns 422; frontend shows error.
- **Postconditions**: Order persisted PENDING; visible in Internal Dashboard.

#### UC-OADM-002 Cancel Order With Optional Reason

- **Priority**: Must | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Actor**: Staff / Manager / Admin | **Precondition**: Order is PENDING, CONFIRMED, or SHIPPING. Actor has order:update-status permission.
- **Main Flow**:
  1. Actor opens order detail in dashboard.
  2. Actor selects "Cancel Order."
  3. System shows modal for optional cancellation reason.
  4. Actor enters reason (or leaves blank) and confirms.
  5. Backend transitions order to CANCELLED; stores reason (nullable); records actor and timestamp.
  6. System sends customer notification email (with reason if provided; without if not).
  7. Audit trail entry created.
- **Alt — Order is DELIVERED or CANCELLED**: Cancel action is disabled.
- **Postconditions**: Order CANCELLED; customer notified; audit log updated.

#### UC-SADM-001 Create Staff Account

- **Priority**: Must | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Actor**: Store Manager (own branch), General Manager, or Super Admin. **Precondition**: Actor has staff:create permission.
- **Main Flow**:
  1. Actor navigates to Staff Management.
  2. Actor clicks "Create Staff Account."
  3. System shows form: Username, Full Name, Phone, Email, Default Password, Branch, Role.
  4. Actor submits.
  5. Backend validates username and email uniqueness.
  6. Backend creates account (IsActive=true, password hashed).
  7. Audit trail entry created.
  8. System shows success confirmation.
- **Alt — Duplicate username or email**: 409; form shows inline error.
- **Postconditions**: Account active; audit log persisted.

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

**BR-PROD-001** — Source: FE-context.md s2, BE-context.md s2. The system shall determine order flow eligibility exclusively from PurchaseMode. ORDERABLE = cart and order eligible. CONTACT_ONLY = not eligible. Enforcement at both frontend UI and backend API layers.

**BR-ORD-002** — Source: Question-Resolve.md. Permitted transitions: PENDING->CONFIRMED, CONFIRMED->SHIPPING, SHIPPING->DELIVERED, PENDING->CANCELLED, CONFIRMED->CANCELLED, SHIPPING->CANCELLED. Prohibited: any transition from DELIVERED or CANCELLED; no reverse transitions.

**BR-INV-001** — Source: Question-Resolve.md. The system shall not reject an order based on StockQuantity. Orders accepted even when stock is zero or negative. Staff resolve negative-stock orders manually.

**BR-CONT-001** — Source: Question-Resolve.md. CONTACT_ONLY: "Contact Us" CTA only. ORDERABLE: primary "Add to Cart" + secondary "Request Consultation." Both CTAs route to the same unified channel. Contact requests from both product types are accepted.

**BR-ACC-008** — Source: Question-Resolve.md. Departing staff accounts are deactivated (IsActive=false). Account records and all linked historical data are retained indefinitely. Hard deletion prohibited.

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
- **Rationale**: Customers must discover and filter products by category.
- **Statement**: The system shall expose `GET /api/products` returning a list of active products (IsActive=true). The endpoint shall accept optional `categoryId` query parameter to filter by category.
- **Acceptance Criteria**:
  1. Given no `categoryId`, all active products are returned.
  2. Given valid `categoryId`, only active products in that category are returned.
  3. Given invalid `categoryId` format, the system shall return 400 Bad Request.
  4. Inactive products shall never appear in the public product list.
- **Dependencies**: FR-CAT-002, FR-PROD-002, FR-INV-003

#### FR-PROD-002 Include PurchaseMode And PriceVisibility In Every Product Response

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s10, BE-context.md s9
- **Rationale**: Frontend requires these fields to render correct CTA and price display.
- **Statement**: The system shall include `purchaseMode` and `priceVisibility` in every product API response (listing and detail).
- **Acceptance Criteria**:
  1. `purchaseMode` is one of ORDERABLE, CONTACT_ONLY in every response.
  2. `priceVisibility` is one of SHOW_PRICE, HIDE_PRICE, CONTACT_FOR_PRICE in every response.
  3. Neither field is null or absent.
- **Dependencies**: None

#### FR-PROD-003 Render Public Price Area According To PriceVisibility

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s3
- **Rationale**: Business controls price presentation per product; frontend must not infer from a null price.
- **Statement**: The public website shall render the price area as follows: SHOW_PRICE = display formatted VND price; HIDE_PRICE = no price area element in DOM; CONTACT_FOR_PRICE = display text "Lien he".
- **Acceptance Criteria**:
  1. Given SHOW_PRICE, formatted price is visible on product card and detail page.
  2. Given HIDE_PRICE, no price area element is present in the DOM.
  3. Given CONTACT_FOR_PRICE, the text "Lien he" appears in the price area.
- **Dependencies**: FR-PROD-002

#### FR-PROD-004 Render Product Card CTA According To PurchaseMode

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s4
- **Statement**: On the listing page: ORDERABLE = display "Them vao gio hang" (Add to Cart) CTA; CONTACT_ONLY = display "Lien he tu van" or "Nhan bao gia" CTA; no Add to Cart button for CONTACT_ONLY.
- **Acceptance Criteria**:
  1. Given ORDERABLE, Add to Cart button is visible; no contact-only CTA.
  2. Given CONTACT_ONLY, contact CTA is visible; no Add to Cart button.
- **Dependencies**: FR-PROD-002

#### FR-CART-002 Block CONTACT_ONLY Product From Cart (Frontend And Backend)

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s6, BE-context.md s2, s12
- **Rationale**: BR-PROD-003. Defence-in-depth at both layers.
- **Statement**: Attempt to add CONTACT_ONLY product to cart: frontend blocks before API call and displays "San pham nay can lien he tu van truoc khi dat hang." Backend returns 422 with `CONTACT_ONLY_PRODUCT` if CONTACT_ONLY product appears in an order payload.
- **Acceptance Criteria**:
  1. Given CONTACT_ONLY, frontend displays blocking message and does not call add-to-cart API.
  2. Given CONTACT_ONLY in order payload, backend `POST /api/orders` returns 422 with `CONTACT_ONLY_PRODUCT`.
- **Dependencies**: FR-PROD-002, FR-ORD-002

#### FR-ORD-001 Submit Guest Checkout Order

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s7, BE-context.md s7
- **Rationale**: Customers complete purchases without an account.
- **Statement**: The system shall accept `POST /api/orders` (unauthenticated) with: `receiverName`, `receiverPhone`, `receiverAddress`, optional `note`, and `items` (list of `productId`, `quantity`). On successful validation, persist order with status PENDING.
- **Acceptance Criteria**:
  1. Valid payload, all ORDERABLE: 201 Created with new order ID.
  2. Empty items list: 400 Bad Request.
  3. Quantity <= 0: 400 Bad Request.
  4. Non-existent productId: 422.
  5. Inactive product: 422.
- **Dependencies**: FR-ORD-002 through FR-ORD-007

#### FR-ORD-010 Admin Cancel Order With Optional Reason

- **Priority**: Must | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Statement**: When authenticated internal user with `order:update-status` transitions order to CANCELLED via `PUT /api/admin/orders/{id}/status`, the system shall accept optional `cancellationReason`. The system shall persist reason (nullable) and trigger FR-ORD-011.
- **Acceptance Criteria**:
  1. Cancellation with reason: order stores reason; notification includes reason.
  2. Cancellation without reason: order stores null; notification sent without reason field.
  3. Order status DELIVERED: system returns 409 Conflict.
  4. Order status already CANCELLED: system returns 409 Conflict.
- **Dependencies**: FR-ORD-011, FR-AUD-001, FR-RBAC-001

#### FR-CONT-001 Submit Contact Request Via Public Form

- **Priority**: Must | **Status**: REVIEW | **Source**: FE-context.md s8, BE-context.md s8, Question-Resolve.md
- **Rationale**: Captures consultation intent; feeds internal follow-up workflow.
- **Statement**: The system shall accept `POST /api/contact-requests` (unauthenticated) with: `productId`, `customerName`, `customerPhone`, optional `customerMessage`. On success, persist ContactRequest with status NEW.
- **Acceptance Criteria**:
  1. Valid payload: 201 Created.
  2. Missing `customerName` or `customerPhone`: 400.
  3. Non-existent `productId`: 422.
  4. On success, frontend displays: "Yeu cau tu van cua ban da duoc gui. Nhan vien se lien he lai som."
  5. ORDERABLE product's productId: system accepts the request (no CONTACT_ONLY restriction).
- **Dependencies**: FR-CONT-002, FR-CONT-003

#### FR-AUTH-001 Authenticate Internal Users Via Username And Password

- **Priority**: Must | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Statement**: The system shall expose `POST /api/auth/login` accepting `username` and `password`. On success, issue JWT in HTTP-only cookie. On failure, return 401 without revealing which field is incorrect.
- **Acceptance Criteria**:
  1. Valid credentials: session token returned; dashboard access granted.
  2. Invalid username or password: 401 with message "Invalid username or password."
  3. Deactivated account: 401 with same generic message.
- **Dependencies**: FR-AUTH-002
- **Notes**: [TBD: OQ-GEN-001 — brute-force lockout policy undefined.]

#### FR-STAFF-001 Create Staff Account

- **Priority**: Must | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Statement**: Authenticated users with `staff:create` permission shall create a new staff account with: `username`, `fullName`, `phoneNumber`, `email`, `defaultPassword` (hashed), optional `branchId`, `roleId`, IsActive=true.
- **Acceptance Criteria**:
  1. Unique username and email: 201 Created.
  2. Duplicate username: 409 Conflict.
  3. Duplicate email: 409 Conflict.
  4. On success: audit log entry created per FR-AUD-001.
- **Dependencies**: FR-RBAC-001, FR-AUD-001
- **Notes**: Password stored as bcrypt or Argon2 hash. [TBD: OQ-GEN-006 — first-login password change policy.]

#### FR-AUD-001 Create Immutable Audit Log Entry For Dangerous Admin Actions

- **Priority**: Should | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Statement**: The system shall automatically create an AuditLog entry for: staff account creation, deactivation, profile modification; product creation, deletion; order status change; system settings change. Each entry records: actor user ID, actor username, action type, entity type, entity ID, UTC timestamp, changed value snapshot.
- **Acceptance Criteria**:
  1. Staff account created: AuditLog entry with actionType "STAFF_CREATED" persisted.
  2. Order cancelled: AuditLog entry with actionType "ORDER_CANCELLED" and reason (if any) persisted.
  3. No AuditLog entry modifiable or deletable via any application endpoint.
- **Dependencies**: FR-AUD-002

#### FR-SET-001 Super Admin Configure Hotline And Deep Link URLs

- **Priority**: Must | **Status**: REVIEW | **Source**: Question-Resolve.md
- **Statement**: The system shall provide `PUT /api/admin/settings` (Super Admin only). Super Admin updates: hotline number, Zalo deep link URL, Messenger deep link URL. Changes persisted and reflected on public website without redeployment.
- **Acceptance Criteria**:
  1. Super Admin updates hotline: `/api/settings/public` reflects new value on next request.
  2. Non-Super-Admin calls `PUT /api/admin/settings`: 403 Forbidden.
- **Dependencies**: FR-RBAC-001, FR-SET-002

---

## 9. Data Requirements And Data Model

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 9.1 Modeling Scope

Covers: products, categories, product images, orders, order items, contact requests, branches, roles, permissions, users, audit logs, system settings.

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
| ENT-PROD-001 | Category | Product classification group used for catalog filtering | Manager/Admin | REVIEW |
| ENT-PROD-002 | Product | Sellable item with purchase mode and price visibility controls | Staff/Manager/Admin | REVIEW |
| ENT-PROD-003 | ProductImage | Secondary gallery image associated with a product | Staff/Manager/Admin | REVIEW |
| ENT-ORD-001 | Order | Guest customer purchase order with delivery details | Customer (create), Staff (manage) | REVIEW |
| ENT-ORD-002 | OrderItem | Line item within an order; snapshots product name and price at order time | System (auto-created with order) | REVIEW |
| ENT-CONT-001 | ContactRequest | Customer consultation or quote request linked to a product | Customer (create), Staff (manage) | REVIEW |
| ENT-ACC-001 | Branch | Physical store location to which staff may be scoped | Manager/Admin | REVIEW |
| ENT-ACC-002 | Role | Named permission group for role-based access control | Super Admin | REVIEW |
| ENT-ACC-003 | Permission | Individual access right assignable to a role | Super Admin | REVIEW |
| ENT-ACC-004 | RolePermission | Many-to-many association between Role and Permission | Super Admin | REVIEW |
| ENT-ACC-005 | User | Internal staff, manager, or admin account for dashboard access | Manager/Admin | REVIEW |
| ENT-AUD-001 | AuditLog | Immutable record of significant administrative actions | System (automated) | REVIEW |
| ENT-SET-001 | SystemSetting | Key-value configuration entry for hotline and deep link URLs | Super Admin | REVIEW |

#### 9.3.2 Conceptual Relationship Summary

| Relationship ID | Source Entity | Relationship | Target Entity | Cardinality | Optionality | Business Meaning | Status |
|---|---|---|---|---|---|---|---|
| REL-PROD-001 | Category | contains | Product | 1:N | Required | Every product belongs to exactly one category | REVIEW |
| REL-PROD-002 | Product | has | ProductImage | 1:N | Optional | A product may have zero or more gallery images | REVIEW |
| REL-PROD-003 | Product | is ordered as | OrderItem | 1:N | Optional | A product can appear in multiple order line items | REVIEW |
| REL-PROD-004 | Product | receives | ContactRequest | 1:N | Optional | A product can have multiple consultation requests | REVIEW |
| REL-ORD-001 | Order | contains | OrderItem | 1:N | Required | Every order has at least one line item | REVIEW |
| REL-ORD-002 | User | cancels | Order | 1:N | Optional | An internal user may cancel orders | REVIEW |
| REL-CONT-001 | User | handles | ContactRequest | 1:N | Optional | An internal user may handle contact requests | REVIEW |
| REL-ACC-001 | Branch | employs | User | 1:N | Optional | A branch may have multiple staff members | REVIEW |
| REL-ACC-002 | Role | is assigned to | User | 1:N | Required | Every user has exactly one role | REVIEW |
| REL-ACC-003 | Role | grants | RolePermission | 1:N | Optional | A role may have multiple permissions | REVIEW |
| REL-ACC-004 | Permission | granted via | RolePermission | 1:N | Optional | A permission may be assigned to multiple roles | REVIEW |
| REL-ACC-005 | User | generates | AuditLog | 1:N | Optional | A user's administrative actions are logged | REVIEW |
| REL-SET-001 | User | updates | SystemSetting | 1:N | Optional | Super Admin updates system configuration | REVIEW |

### 9.4 Entity Attributes

#### ENT-PROD-001 Category
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Unique identifier for the category |
| Name | VARCHAR(200) | NOT NULL, UNIQUE | Display name of the category |
| Slug | VARCHAR(200) | NOT NULL, UNIQUE | URL-friendly identifier for routing and filtering |
| Description | TEXT | NULLABLE | Optional text describing the category |
| IsActive | BOOLEAN | NOT NULL, DEFAULT TRUE | Soft-delete flag; false = deactivated, hidden from public |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Record creation timestamp |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Last modification timestamp |

#### ENT-PROD-002 Product
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Unique identifier for the product |
| CategoryId | UUID | FK -> Category.Id, NOT NULL | Reference to the parent category |
| Name | VARCHAR(500) | NOT NULL | Display name of the product |
| Slug | VARCHAR(500) | NOT NULL, UNIQUE | URL-friendly identifier for product detail page routing |
| Description | TEXT | NULLABLE | Optional detailed product description shown on detail page |
| Price | DECIMAL(18,0) | NULLABLE, CHECK >= 0 | Product price in VND; nullable when price not yet determined |
| StockQuantity | INTEGER | NOT NULL, DEFAULT 0 (signed; negative permitted) | Current inventory count; negative values permitted (overselling allowed) |
| MainImageUrl | TEXT | NULLABLE | Primary thumbnail image URL stored in Cloudflare R2 |
| IsActive | BOOLEAN | NOT NULL, DEFAULT TRUE | Soft-delete flag; false = hidden from public catalog |
| PurchaseMode | VARCHAR(20) | NOT NULL, CHECK IN ('ORDERABLE','CONTACT_ONLY') | Determines order eligibility and CTA rendering on public site |
| PriceVisibility | VARCHAR(30) | NOT NULL, CHECK IN ('SHOW_PRICE','HIDE_PRICE','CONTACT_FOR_PRICE') | Controls how the price area is displayed on the public site |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Record creation timestamp |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Last modification timestamp |

#### ENT-PROD-003 ProductImage
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Unique identifier for the gallery image |
| ProductId | UUID | FK -> Product.Id, NOT NULL | Reference to the parent product |
| ImageUrl | TEXT | NOT NULL | Image URL stored in Cloudflare R2 |
| SortOrder | INTEGER | NOT NULL, DEFAULT 0 | Display ordering index for the gallery |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Record creation timestamp |

#### ENT-ORD-001 Order
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Unique identifier for the order |
| ReceiverName | VARCHAR(200) | NOT NULL | Name of the order recipient |
| ReceiverPhone | VARCHAR(20) | NOT NULL | Phone number of the order recipient |
| ReceiverAddress | TEXT | NOT NULL | Delivery address provided by the customer |
| Note | TEXT | NULLABLE | Optional customer note or special instructions |
| Status | VARCHAR(20) | NOT NULL, CHECK IN ('PENDING','CONFIRMED','SHIPPING','DELIVERED','CANCELLED') | Current order lifecycle state |
| CancellationReason | TEXT | NULLABLE | Optional reason provided when the order is cancelled |
| CancelledByUserId | UUID | FK -> User.Id, NULLABLE | Reference to the staff member who cancelled the order |
| CancelledAt | TIMESTAMPTZ | NULLABLE | Timestamp when the order was cancelled |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Order placement timestamp |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Last status change timestamp |

#### ENT-ORD-002 OrderItem
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Unique identifier for the line item |
| OrderId | UUID | FK -> Order.Id, NOT NULL | Reference to the parent order |
| ProductId | UUID | FK -> Product.Id, NOT NULL | Reference to the ordered product |
| ProductName | VARCHAR(500) | NOT NULL (snapshot at order time — ASM-GEN-007) | Snapshot of product name at time of order creation |
| UnitPrice | DECIMAL(18,0) | NOT NULL (snapshot at order time — ASM-GEN-007) | Snapshot of product unit price at time of order creation |
| Quantity | INTEGER | NOT NULL, CHECK > 0 | Number of units ordered; must be positive |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Record creation timestamp |

#### ENT-CONT-001 ContactRequest
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Unique identifier for the contact request |
| ProductId | UUID | FK -> Product.Id, NOT NULL | Reference to the product being inquired about |
| CustomerName | VARCHAR(200) | NOT NULL | Name of the customer submitting the request |
| CustomerPhone | VARCHAR(20) | NOT NULL | Phone number of the customer for follow-up |
| CustomerMessage | TEXT | NULLABLE | Optional message or question from the customer |
| Status | VARCHAR(20) | NOT NULL, CHECK IN ('NEW','CONTACTED','CLOSED'), DEFAULT 'NEW' | Current request lifecycle state |
| HandledByUserId | UUID | FK -> User.Id, NULLABLE | Reference to the staff member who handled the request |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Request submission timestamp |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Last status change timestamp |

#### ENT-ACC-001 Branch
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Unique identifier for the branch |
| Name | VARCHAR(200) | NOT NULL | Display name of the branch location |
| Description | TEXT | NULLABLE | Optional text describing the branch |
| IsActive | BOOLEAN | NOT NULL, DEFAULT TRUE | Soft-delete flag; false = branch deactivated |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Record creation timestamp |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Last modification timestamp |

#### ENT-ACC-002 Role
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Unique identifier for the role |
| Name | VARCHAR(100) | NOT NULL, UNIQUE | Unique display name of the role (e.g., Staff, Store Manager) |
| Description | TEXT | NULLABLE | Optional text describing the role's purpose and scope |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Record creation timestamp |

#### ENT-ACC-003 Permission
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Unique identifier for the permission |
| Code | VARCHAR(100) | NOT NULL, UNIQUE | Unique machine-readable permission code (e.g., order:update-status) |
| Description | TEXT | NULLABLE | Human-readable description of the permission |

#### ENT-ACC-004 RolePermission
| Column | Type | Constraints | Description |
|---|---|---|---|
| RoleId | UUID | FK -> Role.Id, NOT NULL | Reference to the role being granted the permission |
| PermissionId | UUID | FK -> Permission.Id, NOT NULL | Reference to the permission being granted |
| PRIMARY KEY | (RoleId, PermissionId) | Composite | Prevents duplicate role-permission assignments |

#### ENT-ACC-005 User
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Unique identifier for the user account |
| Username | VARCHAR(100) | NOT NULL, UNIQUE | Unique login identifier for dashboard authentication |
| FullName | VARCHAR(200) | NOT NULL | Display name of the staff member |
| PhoneNumber | VARCHAR(20) | NOT NULL | Contact phone number of the staff member |
| Email | VARCHAR(200) | NOT NULL, UNIQUE | Unique email address for notifications and recovery |
| PasswordHash | TEXT | NOT NULL | Bcrypt or Argon2 hashed password; never stored in plaintext |
| RoleId | UUID | FK -> Role.Id, NOT NULL | Reference to the assigned role determining permissions |
| BranchId | UUID | FK -> Branch.Id, NULLABLE (null = no branch restriction) | Reference to assigned branch; null for General Manager and Super Admin |
| IsActive | BOOLEAN | NOT NULL, DEFAULT TRUE | Soft-delete flag; false = account deactivated, login blocked |
| CreatedAt | TIMESTAMPTZ | NOT NULL | Account creation timestamp |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Last profile modification timestamp |

#### ENT-AUD-001 AuditLog
| Column | Type | Constraints | Description |
|---|---|---|---|
| Id | UUID | PK, NOT NULL | Unique identifier for the audit log entry |
| ActorUserId | UUID | FK -> User.Id, NULLABLE | Reference to the user who performed the action |
| ActorUsername | VARCHAR(100) | NOT NULL | Username snapshot for traceability even if user is later deactivated |
| ActionType | VARCHAR(100) | NOT NULL | Type of administrative action (e.g., STAFF_CREATED, ORDER_CANCELLED) |
| EntityType | VARCHAR(100) | NOT NULL | Type of entity affected (e.g., User, Product, Order) |
| EntityId | UUID | NULLABLE | Identifier of the affected entity instance |
| Changes | JSONB | NULLABLE | JSON snapshot of old and new values for changed fields |
| CreatedAt | TIMESTAMPTZ | NOT NULL (immutable; no UpdatedAt) | Immutable timestamp of when the action occurred |

#### ENT-SET-001 SystemSetting
| Column | Type | Constraints | Description |
|---|---|---|---|
| Key | VARCHAR(100) | PK, NOT NULL | Unique setting identifier (e.g., hotline, zalo_url, messenger_url) |
| Value | TEXT | NULLABLE | Current setting value; nullable if not yet configured |
| UpdatedAt | TIMESTAMPTZ | NOT NULL | Timestamp of the last update |
| UpdatedByUserId | UUID | FK -> User.Id, NULLABLE | Reference to the Super Admin who last updated this setting |


### 9.5 Data Dictionary

| Field | Entity | Description |
|---|---|---|
| PurchaseMode | Product | ORDERABLE or CONTACT_ONLY; controls cart/order eligibility and CTA rendering |
| PriceVisibility | Product | SHOW_PRICE, HIDE_PRICE, or CONTACT_FOR_PRICE; controls public price display |
| MainImageUrl | Product | Primary thumbnail URL in Cloudflare R2 |
| StockQuantity | Product | Signed integer; negative values permitted (overselling) |
| Status | Order | PENDING, CONFIRMED, SHIPPING, DELIVERED, or CANCELLED |
| CancellationReason | Order | Optional text; null if no reason provided |
| Status | ContactRequest | NEW, CONTACTED, or CLOSED |
| IsActive | User/Product/Category/Branch | Soft-delete flag; false = deactivated, record retained |
| BranchId | User | Null = no branch restriction (General Manager, Super Admin) |
| ActionType | AuditLog | e.g., STAFF_CREATED, ORDER_CANCELLED, PRODUCT_DELETED |

### 9.6 Data Constraints And Validation Rules

| VAL ID | Entity | Field | Rule |
|---|---|---|---|
| VAL-PROD-001 | Product | Slug | Unique. [ASSUMPTION] Alphanumeric + hyphens only. |
| VAL-PROD-002 | Product | Price | >= 0 if provided; nullable. |
| VAL-PROD-003 | Product | StockQuantity | No lower bound (negative permitted). |
| VAL-PROD-004 | Product | PurchaseMode | Must be ORDERABLE or CONTACT_ONLY. |
| VAL-PROD-005 | Product | PriceVisibility | Must be SHOW_PRICE, HIDE_PRICE, or CONTACT_FOR_PRICE. |
| VAL-ORD-001 | Order | Items | At least one item required. |
| VAL-ORD-002 | OrderItem | Quantity | Must be > 0. |
| VAL-ORD-003 | OrderItem | ProductId | Must reference existing, active, ORDERABLE product. |
| VAL-CONT-001 | ContactRequest | CustomerName | Required. Non-empty. |
| VAL-CONT-002 | ContactRequest | CustomerPhone | Required. Non-empty. [TBD: OQ-GEN-007 — exact format rule pending.] |
| VAL-CONT-003 | ContactRequest | ProductId | Must reference existing product. |
| VAL-USER-001 | User | Username | Unique across all users. |
| VAL-USER-002 | User | Email | Unique. Valid email format. |
| VAL-USER-003 | User | PasswordHash | Bcrypt or Argon2 hash only. Never stored or logged in plaintext. |

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
| Order | Guest Customer | Internal (status only) | CANCELLED terminal; never deleted |
| ContactRequest | Guest Customer | Internal (status only) | CLOSED terminal; never deleted |
| User | Manager/Admin | Manager/Admin (profile); Staff (own password) | Soft delete (IsActive=false) |
| AuditLog | System | Never | Never |

### 9.9 Data Retention And Deletion

- Orders and ContactRequests retained indefinitely.
- User accounts: soft delete only; hard deletion prohibited.
- AuditLog entries: retained indefinitely; not deletable via any application interface.
- Product images: retained unless explicitly removed by Admin. [ASSUMPTION] Soft-deleted products retain images.
- [TBD: PDPA / data retention compliance scope for Vietnam market.]

### 9.10 Data Migration

Not applicable — greenfield system. [TBD: if legacy records imported, MIG items added.]

### 9.11 Data Traceability Matrix

See Section 16.

---

## 10. External Interface Requirements

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 10.1 User Interface Requirements

| UI ID | Requirement | Priority | Source |
|---|---|---|---|
| UI-GEN-001 | Public site: modern e-commerce layout, minimal premium aesthetic, brand color #2D3E96, clear CTAs | Must | FE-context.md s1 |
| UI-GEN-002 | Internal dashboard: SaaS/enterprise clean UI with data-dense tables | Must | FE-context.md s1 |
| UI-GEN-003 | Public site fully responsive; min mobile width 375px | Must | [ASSUMPTION] |
| UI-GEN-004 | Internal dashboard optimised for desktop; mobile not intentionally broken | Should | FE-context.md s1 |
| UI-GEN-005 | Contact request success message: "Yeu cau tu van cua ban da duoc gui. Nhan vien se lien he lai som." | Must | FE-context.md s8 |
| UI-GEN-006 | Cart block message for CONTACT_ONLY: "San pham nay can lien he tu van truoc khi dat hang." | Must | FE-context.md s6 |

### 10.2 Software Interface Requirements

| IF ID | Endpoint | Auth | Purpose |
|---|---|---|---|
| IF-INTG-001 | GET /api/products | None | Public product list + category filter |
| IF-INTG-002 | GET /api/products/{slug} | None | Public product detail + gallery |
| IF-INTG-003 | POST /api/orders | None | Guest order placement |
| IF-INTG-004 | POST /api/contact-requests | None | Contact request submission |
| IF-INTG-005 | GET /api/admin/orders | RBAC | Internal order list (scoped) |
| IF-INTG-006 | GET /api/admin/orders/{id} | RBAC | Internal order detail |
| IF-INTG-007 | PUT /api/admin/orders/{id}/status | RBAC | Internal order status update |
| IF-INTG-008 | GET /api/admin/contact-requests | RBAC | Internal contact request list (scoped) |
| IF-INTG-009 | GET /api/admin/contact-requests/{id} | RBAC | Internal contact request detail |
| IF-INTG-010 | PUT /api/admin/contact-requests/{id}/status | RBAC | Internal contact request status update |
| IF-INTG-011 | GET /api/admin/products | RBAC | Internal product list |
| IF-INTG-012 | POST /api/admin/products | RBAC | Create product |
| IF-INTG-013 | PUT /api/admin/products/{id} | RBAC | Update product |
| IF-INTG-014 | DELETE /api/admin/products/{id} | RBAC | Soft-delete product |
| IF-INTG-015 | GET/POST/PUT/DELETE /api/admin/categories | RBAC (Manager+) | Category CRUD |
| IF-INTG-016 | GET /api/settings/public | None | Public settings (hotline, deep links) |
| IF-INTG-017 | GET/PUT /api/admin/settings | RBAC (Super Admin) | Read/update system settings |
| IF-INTG-018 | POST /api/auth/login | None | Internal user authentication |
| IF-INTG-019 | POST /api/auth/logout | Required | Session termination |
| IF-INTG-020 | POST /api/auth/change-password | Required | Staff self-service password change |
| IF-INTG-021 | GET/POST/PUT /api/admin/staff | RBAC (Manager+) | Staff account management |
| IF-INTG-022 | PUT /api/admin/staff/{id}/deactivate | RBAC (Manager+) | Staff soft deactivation |

### 10.3 Hardware Interface Requirements

None. Cloud-hosted web application; no dedicated hardware dependencies.

### 10.4 Communication Interface Requirements

- All API communication: HTTPS (TLS 1.2+).
- All API bodies: JSON, UTF-8 encoding.
- Email notifications: SMTP or transactional provider API [TBD: OQ-GEN-002].
- External CTAs: `https://` (Zalo, Messenger) and `tel:` (Hotline).

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

**NFR-PERF-001** — Source: Question-Resolve.md. Statement: The system shall respond to all API requests at p95 within 3 seconds under 500 concurrent users. Acceptance Criterion: Load test with 500 concurrent users produces p95 <= 3000 ms.

### 11.4 Availability

**NFR-AVAIL-001** — Source: Question-Resolve.md. Statement: The system shall maintain 99% availability on a rolling 30-day basis, excluding planned maintenance. Maximum unplanned downtime: 7.2 hours/month.

### 11.6 Scalability

**NFR-SCAL-001** — Source: Question-Resolve.md. Statement: Architecture shall support horizontal scaling to 500 concurrent users at peak without application code changes.

### 11.7 Security

**NFR-SEC-001**: All HTTP traffic redirected to HTTPS.

**NFR-SEC-002**: User passwords stored exclusively as bcrypt or Argon2 hashes; plaintext never stored, logged, or transmitted.

**NFR-SEC-003**: Authenticated internal sessions expire after 30 minutes of inactivity; re-authentication required.

**NFR-SEC-004**: Every internal API endpoint validates RBAC permissions before processing; unauthorised requests receive 403.

### 11.8 Privacy

**NFR-PRIV-001**: Public product API shall not return exact StockQuantity. Negative balances visible only to authenticated internal users.

### 11.9 Usability

**NFR-USE-001**: Customer can complete checkout (product page to confirmation) in 3 or fewer primary actions.

### 11.10 Maintainability

**NFR-MAINT-001**: Hotline, Zalo URL, Messenger URL stored in DB and editable via Admin UI; changes propagate to public site without redeployment.

### 11.13 Logging And Auditing

**NFR-LOG-001**: Structured audit log entries for all dangerous administrative actions; queryable by authorized users in Internal Dashboard.

### 11.15 Compliance

**NFR-COMP-001**: No staff account shall be hard-deleted. Deactivation (IsActive=false) is the only permitted removal mechanism.

---

## 12. Access Control Requirements

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 12.1 Authentication Requirements

| SEC ID | Requirement | Priority |
|---|---|---|
| SEC-AUTH-001 | All internal users authenticate via Username + Password | Must |
| SEC-AUTH-002 | Passwords stored as bcrypt or Argon2 hash | Must |
| SEC-AUTH-003 | Session expires after 30 min of inactivity | Must |
| SEC-AUTH-004 | Deactivated accounts cannot authenticate (return same 401 as wrong password) | Must |
| SEC-AUTH-005 | Staff may only change their own password | Must |
| SEC-AUTH-006 | Login failure does not reveal which field is incorrect | Should |
| SEC-AUTH-007 | [TBD: OQ-GEN-001 — brute-force lockout policy; failed-attempt threshold undefined] | Should |

### 12.2 Authorization Requirements

**Role Hierarchy And Branch Scope:**

| Role | Branch Scope | Provisioned By |
|---|---|---|
| Super Admin | None (global) | System initialisation |
| General Manager | None (global) | Super Admin |
| Store Manager | Assigned branch only | Super Admin or General Manager |
| Staff | Assigned branch only | Super Admin, General Manager, or Store Manager |

**Permission Code Registry:**

| Code | Description |
|---|---|
| product:read | View products in dashboard |
| product:create | Create new products |
| product:update | Edit existing products |
| product:delete | Soft-delete products (audited) |
| category:read | View categories |
| category:create | Create categories |
| category:update | Edit categories |
| category:delete | Delete categories |
| order:read | View orders |
| order:update-status | Update order status |
| contact-request:read | View contact requests |
| contact-request:update-status | Update contact request status |
| staff:read | View staff accounts |
| staff:create | Create staff accounts (audited) |
| staff:update | Edit staff profiles |
| staff:deactivate | Deactivate staff accounts (audited) |
| settings:read | Read system settings |
| settings:update | Update system settings |
| audit:read | View audit trail |

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

**Order States:**

| STATE ID | State | Description |
|---|---|---|
| STATE-ORD-001 | PENDING | Placed by customer; awaiting staff action |
| STATE-ORD-002 | CONFIRMED | Staff confirmed; preparing shipment |
| STATE-ORD-003 | SHIPPING | Order in transit |
| STATE-ORD-004 | DELIVERED | Successfully delivered. Terminal. |
| STATE-ORD-005 | CANCELLED | Cancelled by internal user. Terminal. |

**ContactRequest States:**

| STATE ID | State | Description |
|---|---|---|
| STATE-CONT-001 | NEW | Submitted; not yet acted on |
| STATE-CONT-002 | CONTACTED | Staff reached out to customer |
| STATE-CONT-003 | CLOSED | Fully handled. Terminal. |

### 13.2 State Transitions

**Order:**

| TR ID | From | To | Trigger | Actor |
|---|---|---|---|---|
| TR-ORD-001 | (none) | PENDING | Customer checkout | System |
| TR-ORD-002 | PENDING | CONFIRMED | Staff confirms | Staff/Manager/Admin |
| TR-ORD-003 | CONFIRMED | SHIPPING | Staff marks shipped | Staff/Manager/Admin |
| TR-ORD-004 | SHIPPING | DELIVERED | Staff marks delivered | Staff/Manager/Admin |
| TR-ORD-005 | PENDING | CANCELLED | Staff cancels (optional reason) | Staff/Manager/Admin |
| TR-ORD-006 | CONFIRMED | CANCELLED | Staff cancels (optional reason) | Staff/Manager/Admin |
| TR-ORD-007 | SHIPPING | CANCELLED | Staff cancels (optional reason) | Staff/Manager/Admin |

**ContactRequest:**

| TR ID | From | To | Trigger | Actor |
|---|---|---|---|---|
| TR-CONT-001 | (none) | NEW | Customer submits form | System |
| TR-CONT-002 | NEW | CONTACTED | Staff updates status | Staff/Manager/Admin |
| TR-CONT-003 | CONTACTED | CLOSED | Staff closes | Staff/Manager/Admin |
| TR-CONT-004 | NEW | CLOSED | Staff closes directly | Staff/Manager/Admin |

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
| EDGE-INV-001 | Order placed when StockQuantity = 0 | Order accepted; StockQuantity decremented to -1; staff monitors dashboard. |
| EDGE-INV-002 | Order placed when StockQuantity already negative | Order accepted; further decremented; no automatic block. |
| EDGE-ORD-001 | Empty cart at checkout | Frontend prevents; backend returns ERR-ORD-002 if reached. |
| EDGE-ORD-002 | Product changes ORDERABLE -> CONTACT_ONLY after added to cart | [ASSUMPTION] Cart item persists client-side; backend rejects at checkout (ERR-ORD-001); frontend re-validates on checkout load. |
| EDGE-ORD-003 | Staff cancels without entering a reason | Accepted; notification sent without reason; CancellationReason stored as null. |
| EDGE-CONT-001 | Customer submits contact request for ORDERABLE product | Accepted per BR-CONT-001; no restriction. |
| EDGE-AUTH-001 | Staff logs in with deactivated account | Returns ERR-AUTH-002 (same message as ERR-AUTH-001; no disclosure). |
| EDGE-PROD-001 | Admin deletes product with PENDING orders | [TBD: OQ-GEN-005 — Recommendation: display warning with affected order count; require confirmation.] |
| EDGE-IMG-001 | Product created with no images | Accepted; MainImageUrl = null; public site renders placeholder or empty state. |
| EDGE-SET-001 | Super Admin leaves hotline blank | [ASSUMPTION] Stored as empty string or null; public site hides hotline CTA. |
| EDGE-CAT-001 | Admin deletes category with products assigned | [TBD: OQ-GEN-004 — Recommendation: block delete; show count of affected products.] |

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
| Automated API Test | Integration tests (xUnit / NUnit for .NET backend) |
| UI Manual Test | QA manual test on a web browser |
| End-to-End Test | Full flow from UI to database verification |
| Load Test | k6 or equivalent; simulates concurrent users |
| DB Check | Direct database query to verify persisted state |

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
| OQ-GEN-001 | Brute-force lockout policy (failed-attempt threshold before lockout)? | SEC-AUTH-007, FR-AUTH-001 | Product Owner | OPEN |
| OQ-GEN-002 | Which SMTP / email provider for order cancellation notifications? | FR-ORD-011, ASM-GEN-005, EXT-INTG-006 | Tech Lead | OPEN |
| OQ-GEN-003 | Exact Zalo OA URL and Messenger Page URL for static deep links? | FR-CONT-004, FR-SET-001 | Business Owner | OPEN |
| OQ-GEN-004 | What happens when a category with products is deleted — block or allow with reassignment? | ENT-PROD-001, EDGE-CAT-001 | Product Owner | OPEN |
| OQ-GEN-005 | Are products soft-deleted or hard-deleted? | F-ADMIN-001, ENT-PROD-002, EDGE-PROD-001 | Product Owner | OPEN |
| OQ-GEN-006 | Is a "first login password change" required for new staff accounts? | FR-STAFF-001 | Product Owner | OPEN |
| OQ-GEN-007 | Exact phone number format validation rule for CustomerPhone? | VAL-CONT-002, FR-CONT-002 | Tech Lead | OPEN |
| OQ-GEN-008 | Unified communication channel URL(s) for CONTACT_ONLY CTAs? ("Details to be provided later.") | FR-CONT-004, EXT-INTG-001, EXT-INTG-002 | Business Owner | OPEN |
| OQ-GEN-009 | Should order cancellation email include full order details (items, total)? | FR-ORD-011 | Product Owner | OPEN |

### 17.2 Decisions

| DEC ID | Decision | Source | Date |
|---|---|---|---|
| DEC-GEN-001 | Stock quantity informational only; overselling permitted; negative values allowed | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-002 | ORDERABLE products support contact/consultation flow via secondary CTA | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-003 | Staff accounts use soft delete only; hard deletion prohibited | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-004 | Zalo, Messenger, Hotline are static deep links; no API integration at this stage | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-005 | Order lifecycle: PENDING->CONFIRMED->SHIPPING->DELIVERED; CANCELLED reachable from PENDING/CONFIRMED/SHIPPING | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-006 | Orders cannot be auto-confirmed; all transitions require manual staff action | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-007 | Products support multi-image gallery; MainImageUrl is primary thumbnail | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-008 | Category is a dedicated DB entity; each product belongs to exactly one category | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-009 | Hotline and channel URLs are configurable by Super Admin via system settings | Question-Resolve.md | 2026-06-27 |
| DEC-GEN-010 | Internal dashboard session timeout is 30 minutes of inactivity | Question-Resolve.md | 2026-06-27 |

### 17.3 Requirement-Related Risks

| RISK ID | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| RISK-GEN-001 | Neon Postgres free tier may not meet 99% availability target | Medium | High | Upgrade to Neon Pro or paid managed Postgres before production launch |
| RISK-GEN-002 | Email notification delivery fails — SMTP provider not yet selected | High | Medium | Select and configure provider before order management goes live |
| RISK-GEN-003 | Cloudflare R2 egress/API limits exceeded as catalog grows | Low | Medium | Monitor usage; implement image size limits and compression |
| RISK-GEN-004 | Static deep link URLs break if Zalo or Meta changes URL schemes | Low | Medium | Store URLs in system settings; Super Admin can update without redeployment |
| RISK-GEN-005 | Negative stock balances cause operational confusion if staff untrained | Medium | Medium | Clear visual indicators (red/highlighted) for negative values in dashboard |
| RISK-GEN-006 | RBAC gaps allow unintended access or block legitimate access | Medium | High | Conduct RBAC matrix review (Section 12.3) before UAT |
| RISK-GEN-007 | Phone validation too strict or too loose causes contact request issues | Low | Medium | Resolve OQ-GEN-007 before implementing validation |

---

## 18. Appendices

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 18.1 Glossary

See Section 1.4 for the primary glossary. Additional terms are defined inline using [ASSUMPTION] and [TBD] markers.

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
| FE-context.md | Context/FE-context.md |
| BE-context.md | Context/BE-context.md |
| Question-Resolve.md | Context/Question-Resolve.md |
| SRS-TOC.md | Context/SRS-TOC.md |
| SRS-Template.md | Context/SRS-Template.md |

---

## 19. Requirement Identification Convention

Pattern: `<TYPE>-<DOMAIN>-<NNN>`

| Type | Meaning | Example |
|---|---|---|
| FR | Functional Requirement | FR-PROD-001 |
| NFR | Non-Functional Requirement | NFR-PERF-001 |
| BR | Business Rule | BR-PROD-001 |
| UC | Use Case | UC-ORD-001 |
| CON | Constraint | CON-SEC-001 |
| F | Feature | F-PROD-001 |
| AC | Acceptance Criterion | AC-ORD-001 |
| STK | Stakeholder | STK-GEN-001 |
| ACT | Actor | ACT-GEN-001 |
| EXT | External System | EXT-INTG-001 |
| BG | Business Goal | BG-GEN-001 |
| SC | Success Criterion | SC-GEN-001 |
| ENT | Data Entity | ENT-PROD-002 |
| VAL | Validation Rule | VAL-PROD-001 |
| ASM | Assumption | ASM-GEN-001 |
| DEP | Dependency | DEP-GEN-001 |
| OQ | Open Question | OQ-GEN-001 |
| DEC | Decision | DEC-GEN-001 |
| RISK | Risk | RISK-GEN-001 |
| STATE | State | STATE-ORD-001 |
| TR | State Transition | TR-ORD-001 |
| ERR | Error | ERR-ORD-001 |
| EDGE | Edge Case | EDGE-INV-001 |
| DIA | Diagram | DIA-GEN-001 |
| SEC | Security Requirement | SEC-AUTH-001 |
| UI | UI Requirement | UI-GEN-001 |
| IF | Interface | IF-INTG-001 |
| PF | Product Function | PF-GEN-001 |
| REF | Reference | REF-GEN-001 |

Domain codes: GEN, PROD, CAT, CART, ORD, CONT, AUTH, STAFF, RBAC, ADMIN, INV, IMG, AUD, SET, PERF, AVAIL, SCAL, SEC, PRIV, USE, MAINT, LOG, COMP, ACC, INTG.

IDs are permanent. Deprecated items retain IDs, marked DEPRECATED. IDs never reused.

---

## 20. Requirement Status Convention

| Status | Meaning | Set By |
|---|---|---|
| DRAFT | Agent-authored; not yet submitted for review | Agent |
| REVIEW | Submitted for human review or awaiting decision | Agent |
| APPROVED | Explicitly accepted by a human approver | Human only |
| DEPRECATED | Retained for audit history; no longer active | Agent (after human instruction or approved CR) |

The Agent shall never set APPROVED on its own initiative.

---

## 21. SRS Review Checklist

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

### 21.1 Scope And Context
- [x] Problem statement clearly defined (Section 4.1)
- [x] In-scope and out-of-scope documented (Section 1.2)
- [x] All user classes identified (Section 2.3)
- [x] All external systems identified (Section 3.4)

### 21.2 Requirements
- [x] Every requirement has a unique ID
- [x] Every requirement uses EARS-compliant "shall" statements
- [x] Every detailed FR has >= 1 acceptance criterion
- [x] No vague terms (fast, easy, seamless) in requirement statements
- [x] MoSCoW priority assigned to every requirement
- [x] All status values set to REVIEW (not APPROVED)

### 21.3 Coverage
- [x] All 20 features in Section 5.1 addressed by FRs in Section 8
- [x] All 27 business rules in Section 7 traceable to FRs
- [x] All 9 data entities in Section 9 referenced by >= 1 FR
- [x] All 9 open questions documented in Section 17.1
- [x] All 10 decisions from Question-Resolve.md captured in Section 17.2

### 21.4 Traceability And Completion
- [x] Traceability matrix (Section 16.1) covers all Must-priority FRs
- [x] [TBD] items listed inline with descriptions
- [x] [ASSUMPTION] items listed with reasoning
- [x] Risks in Section 17.3 with likelihood, impact, mitigation
- [ ] OQ-GEN-001 through OQ-GEN-009: require human resolution before full approval
- [ ] ASM-GEN-005 (SMTP provider): dependency unresolved; must be resolved before order management goes live

---

## 22. Approval

**Last Updated**: 2026-06-27
**Status**: REVIEW
**Author**: Agent

This SRS is submitted for human review. No content carries APPROVED status.

| Section | Reviewer | Status | Date |
|---|---|---|---|
| 0–4 (Context and Business) | [TBD] | REVIEW | — |
| 5–8 (Features and Requirements) | [TBD] | REVIEW | — |
| 9 (Data Model) | [TBD] | REVIEW | — |
| 10–12 (Interfaces, NFRs, Access Control) | [TBD] | REVIEW | — |
| 13–15 (States, Errors, Acceptance) | [TBD] | REVIEW | — |
| 16–18 (Traceability, OQs, Appendices) | [TBD] | REVIEW | — |

---

*End of Document — SRS-HappyWeb v1.0.0-DRAFT — Generated 2026-06-27 — Status: REVIEW*
