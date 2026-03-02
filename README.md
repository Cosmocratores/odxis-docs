<div align="center">

# ODXIS — Enterprise ERP SaaS

> A product of **[Cosmocratores SAS](https://cosmocratores.github.io)** · Support: help@odxis.com

### Multi-Tenant Resource Planning Platform for Colombian Businesses

[![Next.js](https://img.shields.io/badge/Next.js-15-black?logo=next.js)](https://nextjs.org)
[![tRPC](https://img.shields.io/badge/tRPC-11-blue?logo=trpc)](https://trpc.io)
[![Prisma](https://img.shields.io/badge/Prisma-6-2D3748?logo=prisma)](https://prisma.io)
[![Auth.js](https://img.shields.io/badge/Auth.js-v5-purple)](https://authjs.dev)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-316192?logo=postgresql)](https://postgresql.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6?logo=typescript)](https://typescriptlang.org)

</div>

---

## What is Odxis?

**Odxis** is a full-featured, multi-tenant ERP SaaS platform designed for Colombian commerce and hospitality businesses. It provides **17 fully integrated modules** within a single codebase — from inventory management and point-of-sale to hotel operations, payroll (CST 2024 compliant), electronic invoicing (DIAN), and a learning management system.

Every tenant's data is isolated at the row level via `organizationId`, enforced at the tRPC middleware layer. The RBAC system provides **35 granular permissions** across **10 predefined roles**, from Owner to Viewer.

> **Note:** This repository contains technical documentation and architecture research. The source code is maintained in a private repository.

---

## At a Glance

| Metric | Value |
|--------|-------|
| **Modules** | 17 operational + infrastructure |
| **Prisma Models** | 68 data models |
| **Enums** | 50 type definitions |
| **Schema Lines** | 2,172 |
| **Source Lines** | 30,887+ TypeScript/TSX |
| **tRPC Routers** | 18 (328KB) |
| **Enterprise Services** | 10 |
| **RBAC Permissions** | 35 atomic permissions |
| **Roles** | 10 predefined (Owner → Viewer) |
| **Compliance** | DIAN UBL 2.1, CST 2024 payroll |

---

## Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Framework** | Next.js 15 (App Router, Turbopack) | Full-stack React framework |
| **API** | tRPC 11 | End-to-end type-safe RPC |
| **ORM** | Prisma 6 | Database access + migrations |
| **Auth** | Auth.js v5 (NextAuth) | Authentication + session management |
| **UI** | Tailwind CSS v4 + shadcn/ui | Component library |
| **Animations** | Framer Motion 12 | UI transitions |
| **Database** | Azure PostgreSQL 16 (PgBouncer) | Managed relational database |
| **Hosting** | Vercel | Serverless deployment |
| **Rate Limiting** | Upstash Redis | API abuse prevention |
| **Payments** | Wompi | Colombian payment gateway |
| **Invoicing** | Dataico API | DIAN electronic invoicing |
| **Monitoring** | Sentry | Error tracking + performance |
| **Testing** | Vitest + Coverage v8 | Unit & integration tests |

---

## Modules

### Core Business

| Module | Router | Key Features |
|--------|--------|-------------|
| 🏭 **Inventory** | `inventory` | Products, variants, BOM/recipes, warehouses, stock movements, weighted average costing |
| 🛒 **POS** | `pos` | Point of sale, orders, payments, tables, cash register open/close, discounts |
| 📺 **KDS** | `kds` | Kitchen Display System — real-time order tracking for kitchen staff |
| 👥 **CRM** | `crm` | Customer lifecycle: Lead → Prospect → Client |
| 📊 **Sales** | `sales` | Sales pipeline management |
| 🤝 **Partners** | `partners` | Channel partner / reseller management |

### Finance & Compliance

| Module | Router | Key Features |
|--------|--------|-------------|
| 📒 **Accounting** | `accounting` | Chart of accounts (PUC), journal entries, fiscal periods, bank reconciliation |
| 🧾 **Invoicing** | `invoicing` | DIAN electronic invoicing (UBL 2.1 XML), CUFE, credit/debit notes, Dataico integration |
| 📈 **Reporting** | `reporting` | P&L, Balance Sheet, Cash Flow, custom financial reports |

### People & Operations

| Module | Router | Key Features |
|--------|--------|-------------|
| 👔 **HR / Payroll** | `hr` | Full Colombian payroll (CST 2024): social security, overtime, leave management, uniform tracking |
| 🏨 **PMS (Hotel)** | `pms` | Rooms, reservations, check-in/out, room charges, housekeeping, guest history |
| 🎓 **Academy LMS** | `academy` | Courses, lessons, enrollments, progress tracking |
| 🎫 **Support** | `support` | Ticket system, categories, SLA, knowledge base |
| 💼 **Services** | `services` | Service catalog, professionals, appointments |

### Platform

| Module | Router | Key Features |
|--------|--------|-------------|
| 🔐 **Auth** | `auth` | Registration, login, RBAC (35 permissions, 10 roles), 2FA (TOTP/SMS) |
| 📝 **Blog** | `blog` | Posts, categories, SEO metadata |
| 💳 **Subscriptions** | `subscription` | Plans: EMPRENDEDOR / CRECIMIENTO / EMPRESA, Wompi billing |
| 🏢 **Organization** | `organization` | Tenant configuration, active modules, settings |

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        VERCEL EDGE                          │
├─────────────────────────────────────────────────────────────┤
│  Next.js 15 App Router                                      │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────────────┐│
│  │  (public)/   │ │  (auth)/     │ │  (dashboard)/        ││
│  │  Landing     │ │  Login       │ │  Protected UI        ││
│  │  Blog (SSR)  │ │  Register    │ │  17 Module Views     ││
│  └──────────────┘ └──────────────┘ └──────────────────────┘│
├─────────────────────────────────────────────────────────────┤
│  tRPC 11 API Layer                                          │
│  ┌────────────────────────────────────────────────────────┐ │
│  │  Middleware Chain:                                      │ │
│  │  Auth → Rate Limit → Org Isolation → RBAC → Handler    │ │
│  │                                                         │ │
│  │  17 Sub-Routers  ·  10 Enterprise Services              │ │
│  └────────────────────────────────────────────────────────┘ │
├─────────────────────────────────────────────────────────────┤
│  Prisma 6 ORM                                               │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────────────┐│
│  │  68 Models   │ │  50 Enums    │ │  Row-Level Isolation  ││
│  │  2172 Lines  │ │  Type Safety │ │  via organizationId   ││
│  └──────────────┘ └──────────────┘ └──────────────────────┘│
├─────────────────────────────────────────────────────────────┤
│  Azure PostgreSQL 16 (PgBouncer) · Upstash Redis            │
└─────────────────────────────────────────────────────────────┘
```

See [ARCHITECTURE.md](ARCHITECTURE.md) for detailed diagrams and data flow.

---

## Enterprise Services

| Service | File | Description |
|---------|------|-------------|
| **DIAN Invoicing** | `dian.ts` | XML UBL 2.1 generation + Dataico API integration |
| **DIAN Resolution** | `dian-resolution.ts` | Validation of DIAN resolutions (range, expiry) |
| **RUT Validation** | `rut-validation.ts` | Online RUT validation + 48h cache |
| **Withholding Tax** | `withholding-auto.ts` | Automatic withholding calculation (RENTA/IVA/ICA) |
| **Accounting Helpers** | `accounting-helpers.ts` | Automatic journal entries (POS, payroll, costs) |
| **Payroll Calculator** | `payroll-calculator.ts` | Full CST 2024 Colombian payroll |
| **Inventory Costing** | `inventory-costing.ts` | Weighted average costing + Kardex |
| **Financial Reporting** | `financial-reporting.ts` | P&L, Balance Sheet, Cash Flow |
| **Two-Factor Auth** | `two-factor.ts` | TOTP/SMS 2FA + backup codes |
| **Audit Export** | `audit-export.ts` | Audit trail export (CSV/PDF/JSON) |

---

## Security Model

### RBAC — Role-Based Access Control

**35 atomic permissions** organized by module:

- **Dashboard**: `VIEW_DASHBOARD`
- **Inventory**: `VIEW_INVENTORY`, `MANAGE_INVENTORY`, `MANAGE_WAREHOUSES`, `MANAGE_BOM`, `MANAGE_TRANSFERS`
- **POS**: `VIEW_POS`, `MANAGE_POS`, `MANAGE_CASH_REGISTER`, `APPLY_DISCOUNTS`, `VOID_ORDERS`, `VIEW_POS_METRICS`
- **KDS**: `VIEW_KDS`, `MANAGE_KDS`
- **CRM**: `VIEW_CRM`, `MANAGE_CRM`
- **Accounting**: `VIEW_ACCOUNTING`, `MANAGE_ACCOUNTING`, `VIEW_REPORTS`
- **Invoicing**: `VIEW_INVOICES`, `MANAGE_INVOICES`, `EMIT_ELECTRONIC_INVOICE`
- **HR**: `VIEW_PAYROLL`, `MANAGE_PAYROLL`, `MANAGE_EMPLOYEES`, `MANAGE_SHIFTS`
- **Hotel**: `VIEW_ROOMS`, `MANAGE_ROOMS`, `MANAGE_RESERVATIONS`, `MANAGE_HOUSEKEEPING`, `CHARGE_TO_ROOM`
- **Academy/Support**: `VIEW_ACADEMY`, `MANAGE_ACADEMY`, `MANAGE_SUPPORT`
- **Admin**: `MANAGE_USERS`, `MANAGE_LOCATIONS`, `MANAGE_ORGANIZATION`, `VIEW_AUDIT_LOGS`, `MANAGE_BILLING`

### 10 Predefined Roles

| Role | Scope |
|------|-------|
| **OWNER** | All permissions |
| **ADMIN** | All except billing |
| **CONTADOR** | Accounting, invoicing, payroll, reports, audit |
| **CAJERO** | POS, cash register, inventory view, CRM view |
| **MESERO** | POS orders, KDS view |
| **RECEPCIONISTA** | Hotel reservations, CRM, POS, support |
| **RRHH** | Employees, shifts, payroll, reports |
| **CHEF** | KDS, BOM/recipes, inventory view |
| **MEMBER** | Dashboard, inventory/POS/CRM view |
| **VIEWER** | Dashboard only |

### Additional Security

- **2FA**: TOTP + SMS + backup codes
- **Rate Limiting**: Upstash Redis per-endpoint throttling
- **Audit Trail**: Immutable `AuditLog` with before/after snapshots
- **Multi-tenant isolation**: Row-level via `organizationId` enforced in tRPC middleware
- **Session management**: Auth.js v5 with JWT + database sessions

---

## Colombian Compliance

### DIAN Electronic Invoicing

- **UBL 2.1** XML generation via `dian.ts`
- **CUFE** (Código Único de Facturación Electrónica) generation
- **Resolution validation**: prefix, range, expiry dates
- **Credit/debit notes** with electronic signatures
- **Dataico API** integration for official DIAN submission

### Payroll — CST 2024

Full compliance with Colombian labor law (Código Sustantivo del Trabajo):

- Social security (EPS 4%, pension 4%, ARL 0.522-6.960%)
- Parafiscales (SENA 2%, ICBF 3%, Caja de Compensación 4%)
- Prestaciones sociales (cesantías, intereses, prima, vacaciones)
- Overtime types: diurna (125%), nocturna (175%), dominical (200%)
- Transport allowance for ≤2 SMLMV
- Solidarity fund for >4 SMLMV
- Leave management: vacaciones, incapacidad, maternidad/paternidad
- Withholding tax (retención en la fuente) calculation

### Tax System

- **IVA**: 19%, 5%, exempt, excluded
- **INC**: 8% consumption tax
- **Withholding**: Automatic RENTA, IVA, ICA calculation
- **RUT validation**: Online DIAN lookup with 48h cache

---

## Documentation

| Document | Description |
|----------|-------------|
| [README.md](README.md) | This file — project overview |
| [ARCHITECTURE.md](ARCHITECTURE.md) | System design with Mermaid diagrams |
| [MODULES.md](MODULES.md) | Detailed module breakdown |
| [SECURITY.md](SECURITY.md) | Security model & compliance |
| [TECH_STACK.md](TECH_STACK.md) | Technology choices & rationale |

---

## Competencies Demonstrated

This project demonstrates production-level expertise in:

- **Enterprise Architecture** — Multi-tenant SaaS with 17 modules in a single monolith
- **Type-Safe Full Stack** — End-to-end type safety from Prisma → tRPC → React
- **Domain Modeling** — 68 data models covering inventory, finance, HR, hospitality
- **Regulatory Compliance** — DIAN electronic invoicing, Colombian payroll law
- **Security Engineering** — RBAC, 2FA, audit trails, rate limiting
- **API Design** — 18 tRPC routers with middleware chains
- **Financial Systems** — Double-entry accounting, tax calculation, financial reporting

---

<div align="center">

**Private Repository:** [github.com/Cosmocratores/odxis](https://github.com/Cosmocratores/odxis)
·
**Live:** [odxis.vercel.app](https://odxis.vercel.app)

</div>
