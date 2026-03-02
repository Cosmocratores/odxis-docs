# Architecture — Odxis ERP

## System Overview

Odxis is a monolithic Next.js application following the **T3 Stack** pattern — tRPC for the API layer, Prisma for data access, and Auth.js for authentication. The multi-tenant architecture uses row-level data isolation via `organizationId` enforced in tRPC middleware.

## Request Lifecycle

```mermaid
sequenceDiagram
    participant C as Client (React)
    participant M as Middleware
    participant T as tRPC Router
    participant R as Rate Limiter
    participant A as Auth.js
    participant P as Prisma
    participant D as PostgreSQL

    C->>M: HTTP Request
    M->>M: Path-based routing
    M->>R: Check rate limit
    R->>R: Upstash Redis lookup
    M->>A: Verify session
    A->>A: JWT + DB session
    M->>T: Pass to tRPC handler
    T->>T: RBAC permission check
    T->>T: Inject organizationId
    T->>P: Query with org filter
    P->>D: SQL with WHERE org_id = ?
    D-->>P: Results
    P-->>T: Typed models
    T-->>C: Type-safe response
```

## Application Layers

```mermaid
graph TB
    subgraph "Client Layer"
        A[Next.js App Router] --> B[React Server Components]
        A --> C[Client Components]
        C --> D[tRPC React Query Client]
    end

    subgraph "API Layer"
        D --> E[tRPC HTTP Handler]
        E --> F[Middleware Chain]
        F --> G[Auth Middleware]
        F --> H[Rate Limit Middleware]
        F --> I[Org Isolation Middleware]
        F --> J[RBAC Middleware]
    end

    subgraph "Business Logic"
        J --> K[17 tRPC Routers]
        K --> L[10 Enterprise Services]
    end

    subgraph "Data Layer"
        L --> M[Prisma 6 ORM]
        M --> N[Azure PostgreSQL 16]
        H --> O[Upstash Redis]
    end

    subgraph "External Services"
        L --> P[Dataico API — DIAN]
        L --> Q[Wompi — Payments]
        A --> R[Sentry — Monitoring]
    end
```

## Multi-Tenant Data Isolation

Every data model includes an `organizationId` foreign key. The tRPC middleware automatically injects the organization context:

```
publicProcedure
  → authenticate (Auth.js session)
  → rateLimit (Upstash Redis)
  → injectOrganizationId (from session)
  → enforcePermission (RBAC check)
  → handler (business logic)
```

All queries are automatically scoped:

```
WHERE organizationId = ctx.session.user.organizationId
```

This ensures complete data isolation between tenants without database partitioning.

## Module Dependency Graph

```mermaid
graph LR
    subgraph "Core"
        ORG[Organization]
        AUTH[Auth/RBAC]
        AUDIT[Audit Log]
    end

    subgraph "Commerce"
        INV[Inventory]
        POS[POS]
        KDS[KDS]
        CRM[CRM]
    end

    subgraph "Finance"
        ACC[Accounting]
        INV_F[Invoicing]
        REP[Reporting]
    end

    subgraph "People"
        HR[HR/Payroll]
        PMS[PMS Hotel]
        SUP[Support]
        ACA[Academy]
        SVC[Services]
    end

    ORG --> AUTH
    AUTH --> POS
    AUTH --> INV
    INV --> POS
    POS --> KDS
    POS --> ACC
    POS --> INV_F
    ACC --> REP
    INV_F --> ACC
    CRM --> POS
    CRM --> PMS
    HR --> ACC
    PMS --> POS
    PMS --> ACC
    SUP --> AUTH
    ACA --> AUTH
    SVC --> CRM
    AUDIT --> AUTH
```

## Database Schema Overview

```mermaid
erDiagram
    Organization ||--o{ User : has
    Organization ||--o{ Location : has
    Organization ||--o{ Product : has
    Organization ||--o{ Order : has
    Organization ||--o{ Invoice : has
    Organization ||--o{ Employee : has
    Organization ||--o{ Room : has
    Organization ||--o{ Account : has

    User ||--o{ CashRegister : operates
    User ||--o{ SupportTicket : creates

    Product ||--o{ ProductVariant : has
    Product ||--o{ BomItem : "used in"
    Product ||--o{ StockMovement : tracks
    Product ||--o{ OrderItem : "sold via"

    Order ||--o{ OrderItem : contains
    Order ||--o{ KitchenOrder : "sent to"
    Order |o--|| Invoice : generates
    Order |o--|| JournalEntry : "creates entry"

    Invoice ||--o{ CreditNote : "adjusted by"
    Invoice ||--o{ WithholdingTax : "has retention"

    Account ||--o{ JournalLine : "has entries"
    JournalEntry ||--o{ JournalLine : contains

    Employee ||--o{ ShiftAssignment : works
    Employee ||--o{ PayrollItem : "paid via"
    Employee ||--o{ LeaveRequest : requests

    PayrollPeriod ||--o{ PayrollItem : contains

    Room ||--o{ Reservation : "booked for"
    Reservation ||--o{ RoomCharge : incurs
    Customer ||--o{ Reservation : makes
    Customer ||--o{ Order : places
```

## Deployment Architecture

```mermaid
graph TB
    subgraph "Vercel"
        EDGE[Edge Middleware]
        SSR[Server Functions]
        STATIC[Static Assets / CDN]
    end

    subgraph "Azure"
        PG[PostgreSQL 16 Flexible]
        PGB[PgBouncer :6432]
        PG --> PGB
    end

    subgraph "Upstash"
        REDIS[Redis — Rate Limiting]
    end

    subgraph "External"
        DIAN[Dataico — DIAN]
        WOMPI[Wompi — Payments]
        SENTRY[Sentry — Monitoring]
    end

    EDGE --> SSR
    SSR --> PGB
    SSR --> REDIS
    SSR --> DIAN
    SSR --> WOMPI
    SSR --> SENTRY
```

## Key Design Decisions

| Decision | Rationale |
|----------|-----------|
| **Monolith over Microservices** | Single team, shared data model, lower operational complexity |
| **tRPC over REST/GraphQL** | End-to-end type safety, zero code generation, smaller bundle |
| **Row-level isolation over schema-per-tenant** | Simpler migrations, lower cost, sufficient for target scale |
| **COP as integers** | Avoids floating-point rounding errors in financial calculations |
| **PUC chart of accounts** | Standard Colombian accounting classification |
| **Middleware-enforced RBAC** | Consistent security enforcement across all endpoints |
| **Automatic journal entries** | POS sales, payroll, and inventory automatically create accounting entries |
