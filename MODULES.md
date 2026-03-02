# Modules — Odxis ERP

Detailed breakdown of all 17 operational modules in the Odxis ERP platform.

---

## 🏭 Inventory (`inventory`)

**Router size:** 19.4KB · **Key models:** Product, ProductVariant, ProductAttribute, BomItem, Warehouse, StockMovement

Full product lifecycle management with variant support, bill of materials for composite products, multi-warehouse stock tracking, and weighted average costing.

### Capabilities

- **Product management**: CRUD with SKU, barcode, tax configuration, images
- **Variants**: Multi-attribute variants (size × color × material) with independent pricing
- **Bill of Materials (BOM)**: Recipe/scandallo system for composite products (e.g., 1 Burger = 1 Bun + 150g Beef + 50g Cheese)
- **Warehouses**: Multi-warehouse stock with default warehouse per location
- **Stock movements**: IN, OUT, TRANSFER, ADJUSTMENT with full audit trail
- **Inventory costing**: Weighted average cost calculation + Kardex reports
- **Alerts**: Configurable minimum stock levels with automated notifications

---

## 🛒 POS — Point of Sale (`pos`)

**Router size:** 16.5KB · **Key models:** Order, OrderItem, CashRegister, Table

Complete point-of-sale system with table management, cash register lifecycle, and automatic accounting integration.

### Capabilities

- **Order management**: Create, modify, complete, cancel orders
- **Table service**: Table assignment, capacity tracking, status management (Available → Occupied → Reserved)
- **Cash register**: Open/close with base amount, expected vs actual reconciliation
- **Payment methods**: Cash, card, transfer, Nequi, Daviplata
- **Discounts**: Per-item and per-order discounts with permission control
- **Kitchen integration**: Automatic KDS ticket generation
- **Accounting**: Automatic journal entry creation on order completion

---

## 📺 KDS — Kitchen Display System (`kds`)

**Router size:** 4.2KB · **Key models:** KitchenOrder

Real-time kitchen order management with priority levels and timestamp tracking.

### Capabilities

- **Order queue**: PENDIENTE → EN_PREPARACION → LISTA → ENTREGADA
- **Priority levels**: NORMAL, URGENTE, VIP
- **Time tracking**: Sent, started, completed, delivered timestamps
- **Chef interface**: Designed for touch-screen kitchen displays

---

## 👥 CRM — Customer Relationship Management (`crm`)

**Router size:** 6.4KB · **Key models:** Customer, Supplier

Customer lifecycle management with supplier directory.

### Capabilities

- **Customer pipeline**: LEAD → PROSPECT → CLIENT status progression
- **Contact management**: Email, phone, company, tax ID (NIT/cédula)
- **Supplier directory**: Supplier catalog with product associations
- **Cross-module**: Customers linked to Orders, Invoices, Reservations

---

## 📒 Accounting (`accounting`)

**Router size:** 38.7KB · **Key models:** Account, JournalEntry, JournalLine, TaxConfig, BankAccount, FiscalPeriod

Full double-entry accounting system following Colombian PUC (Plan Único de Cuentas).

### Capabilities

- **Chart of Accounts**: 5-level PUC hierarchy (Class → Group → Account → Sub-account → Auxiliary)
- **Journal entries**: Manual and automatic (from POS, payroll, inventory)
- **Fiscal periods**: Open/close with validation
- **Tax configuration**: IVA 19%, IVA 5%, INC 8%, exempt, excluded
- **Bank accounts**: Multi-bank with transaction tracking and reconciliation
- **Withholding tax**: Automatic RENTA, IVA, ICA calculation with rules engine
- **Cost centers**: Per-line cost center allocation

---

## 🧾 Invoicing (`invoicing`)

**Router size:** 26.1KB · **Key models:** Invoice, DianInvoice, DianResolution, CreditNote, PurchaseInvoice, WithholdingTax

DIAN-compliant electronic invoicing with Dataico API integration.

### Capabilities

- **Electronic invoicing**: UBL 2.1 XML generation
- **CUFE generation**: Unique electronic invoice code
- **Resolution management**: Prefix, numbering range, expiry validation
- **Credit/debit notes**: Electronic adjustment documents
- **Purchase invoices**: Supplier invoice management with retention
- **Withholding tax**: Automatic calculation on taxable thresholds
- **Dataico integration**: Official DIAN submission API

---

## 📈 Reporting (`reporting`)

**Router size:** 10.5KB

Financial reporting module generating standard Colombian financial statements.

### Reports

- **Income Statement (P&L)**: Revenue, COGS, operating expenses, net income
- **Balance Sheet**: Assets, liabilities, equity at a point in time
- **Cash Flow Statement**: Operating, investing, financing activities
- **Custom reports**: Configurable date ranges and filters

---

## 👔 HR / Payroll (`hr`)

**Router size:** 44.9KB · **Key models:** Employee, Department, Shift, ShiftAssignment, PayrollPeriod, PayrollItem, LeaveRequest, PayrollNovelty, Dotacion

The largest module — full Colombian payroll system compliant with CST 2024.

### Capabilities

- **Employee management**: Full profile with personal, labor, contract, banking, uniform data
- **Departments**: Organizational structure with managers
- **Shifts**: Schedule management with night surcharge detection
- **Overtime**: Diurna (125%), nocturna (175%), dominical (200%), nocturna dominical (250%)
- **Payroll calculation**: Complete CST 2024 compliance
  - Social security: EPS 4%, AFP 4%, ARL (risk-based)
  - Parafiscales: SENA 2%, ICBF 3%, Caja de Compensación 4%
  - Prestaciones: Cesantías, intereses sobre cesantías, prima, vacaciones
  - Transport allowance (≤2 SMLMV)
  - Solidarity fund (>4 SMLMV)
- **Leave management**: Vacaciones, incapacidad, maternidad, paternidad, bereavement, unpaid
- **Novelties**: Commissions, bonuses, loans, garnishments per period
- **Uniform tracking**: Dotación delivery per quadrimester
- **Document management**: Digital employee file (ID, contracts, certificates)

---

## 🏨 PMS — Property Management System (`pms`)

**Router size:** 40.4KB · **Key models:** Room, Reservation, RoomCharge, Housekeeping, GuestHistory, RentalAsset

Complete hotel operations management.

### Capabilities

- **Room management**: Types, rates, amenities, status tracking
- **Reservations**: PENDIENTE → CONFIRMADA → CHECK_IN → CHECK_OUT → CANCELADA
- **Room charges**: Charge products/services to room folio during stay
- **Housekeeping**: Task assignment and status tracking (LIMPIA → SUCIA → EN_LIMPIEZA → FUERA_DE_SERVICIO)
- **Guest history**: Cross-stay guest profiles and preferences
- **Rental assets**: Equipment and asset tracking for property
- **POS integration**: Room charges link to POS orders
- **Accounting integration**: Automatic journal entries for room revenue

---

## 🎓 Academy LMS (`academy`)

**Router size:** 29.2KB · **Key models:** Course, Lesson, CourseEnrollment, LessonProgress

Learning management system for internal training.

### Capabilities

- **Course management**: Create courses with metadata, descriptions, ordering
- **Lessons**: Content items within courses with sequential ordering
- **Enrollments**: User enrollment tracking with completion status
- **Progress**: Per-lesson progress tracking (started, completed timestamps)
- **Knowledge base**: Integrated with support module

---

## 🎫 Support (`support`)

**Router size:** 13.9KB · **Key models:** SupportTicket, TicketCategory

Customer and internal support ticket system.

### Capabilities

- **Ticket lifecycle**: ABIERTO → EN_PROGRESO → PENDIENTE_CLIENTE → RESUELTO → CERRADO
- **Categories**: Configurable ticket categories
- **SLA tracking**: Priority-based response time tracking
- **Agent assignment**: Ticket routing to support agents
- **Knowledge base**: Self-service articles for common issues

---

## 💼 Services (`services`)

**Router size:** 17.1KB · **Key models:** ServiceCatalog, Professional, Appointment

Services and appointment booking system.

### Capabilities

- **Service catalog**: Service definitions with pricing and duration
- **Professionals**: Staff profiles with specializations and availability
- **Appointments**: Booking system with time slot management
- **CRM integration**: Appointments linked to customer profiles

---

## 🔐 Auth (`auth`)

**Router size:** 8.7KB · **Key models:** User

Authentication and authorization module.

### Capabilities

- **Registration**: bcrypt password hashing, organization creation
- **Login**: Email/password with optional 2FA
- **RBAC**: 35 permissions × 10 roles, customizable per user
- **2FA**: TOTP (authenticator app), SMS, email verification
- **Backup codes**: Recovery codes for 2FA lockouts
- **Session management**: Auth.js v5 with JWT + database sessions

---

## 📝 Blog (`blog`)

**Router size:** 7.5KB · **Key models:** BlogPost, BlogCategory

Content management for public-facing blog.

### Capabilities

- **Post management**: CRUD with rich text, images, SEO metadata
- **Categories**: Hierarchical categorization
- **SEO**: Title, description, slug, OpenGraph metadata
- **Authorship**: Posts linked to user profiles

---

## 💳 Subscriptions (`subscription`)

**Router size:** 8.1KB · **Key models:** Subscription

SaaS billing and plan management.

### Plans

| Plan | Target | Modules |
|------|--------|---------|
| **EMPRENDEDOR** | Small businesses | Inventory, POS, CRM, basic reporting |
| **CRECIMIENTO** | Growing businesses | + Invoicing, accounting, HR |
| **EMPRESA** | Enterprise | All 17 modules + priority support |

---

## 📊 Sales (`sales`)

**Router size:** 2.6KB

Sales pipeline management for B2B operations.

---

## 🤝 Partners (`partners`)

**Router size:** 1.2KB

Channel partner and reseller management program.

---

## 🏢 Organization (`organization`)

**Router size:** 1.5KB · **Key models:** Organization

Tenant configuration and settings management.

### Capabilities

- **Active modules**: Toggle which modules are available per organization
- **Settings**: Custom configuration per tenant (currency, locale, tax defaults)
- **Billing**: Wompi customer integration for subscription payments
