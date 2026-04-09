# Service Architecture

## Objective

This document defines the backend service architecture of Água Nativa.

Its purpose is to clearly establish:

* how the backend is structured into modules
* the responsibility of each module
* what each module can and cannot do
* how modules communicate with each other
* the structural foundation for the NestJS backend

This document complements the existing materials on system architecture, multi-tenant strategy, and data modeling.

---

## Architectural Direction

Água Nativa will start as a **modular monolith**.

This means:

* a single backend in the initial phase
* well-defined internal modules
* clear separation of responsibilities
* low coupling between components
* a structure prepared to evolve without architectural debt

This approach provides the best balance between:

* operational simplicity
* technical organization
* controlled development speed
* future scalability without overengineering

---

## Core Structural Rule

Even as a single backend, the system **must not become a mixed or unstructured codebase**.

It will be divided into business modules with clear boundaries.

Each module must have:

* its own responsibility
* its own business rules
* clearly defined input/output contracts
* strict separation between domain logic and infrastructure

---

## Mandatory Principles

The service architecture must follow these principles:

1. all processing must respect tenant boundaries
2. no module may access data from another tenant improperly
3. business rules must not be scattered
4. controllers must not contain business logic
5. infrastructure must not dictate business rules
6. modules must communicate clearly
7. critical actions must be auditable
8. security must exist from the beginning

---

## Multi-Tenant Context

The system is multi-tenant from day one.

Therefore, every backend module must:

* identify the tenant from the request
* validate user-tenant association
* restrict read/write operations to the correct tenant
* log relevant events with tenant context
* prevent data leakage between associations

The tenant is not a technical detail.
It is a core architectural element.

---

## Backend Domains

The backend will be organized into the following domains:

* authentication and access
* tenants
* associations
* users
* customers
* consumer units
* meters
* readings
* tariffs
* extra charges
* invoices
* payments
* notifications
* reports
* audit
* file storage
* platform administration

---

## Module: Authentication and Access

Responsibilities:

* user authentication
* identity management
* authenticated context
* permissions
* tenant linkage
* access control

This module defines **who the user is and what they can do**.

It must not handle:

* billing
* readings
* payments
* business reporting

---

## Module: Tenants

Responsibilities:

* tenant registration
* tenant lifecycle/status
* tenant metadata
* isolation configuration
* operational segregation foundation

---

## Module: Associations

Responsibilities:

* association data
* operational configuration
* local identity
* association-specific parameters

---

## Module: Users

Responsibilities:

* internal user management
* operational roles
* association linkage
* activation/deactivation

---

## Module: Customers

Responsibilities:

* consumer registration
* customer status
* contact data
* linkage to consumer units
* historical data

---

## Module: Consumer Units

Responsibilities:

* unit management
* location
* linkage to customers
* operational status

---

## Module: Meters

Responsibilities:

* meter registration
* installation
* replacement
* status tracking
* technical history

---

## Module: Readings

Responsibilities:

* meter reading registration
* validation
* anomaly detection
* consumption history

---

## Module: Tariffs

Responsibilities:

* tariff tables
* pricing tiers
* validity periods
* base calculation rules

---

## Module: Extra Charges

Responsibilities:

* non-recurring charges
* operational fees
* manual adjustments
* future billing entries

---

## Module: Invoices

Responsibilities:

* invoice generation
* item composition
* total calculation
* due dates
* invoice status

---

## Module: Payments

Responsibilities:

* payment registration
* invoice linkage
* payment status
* reconciliation

---

## Module: Notifications

Responsibilities:

* notification generation
* delivery management
* communication history

---

## Module: Reports

Responsibilities:

* aggregated queries
* operational metrics
* financial metrics

---

## Module: Audit

Responsibilities:

* audit trails
* tracking critical actions
* change history

---

## Module: Storage

Responsibilities:

* file storage
* documents
* attachments

---

## Module: Platform Administration

Responsibilities:

* platform-level control
* supervision
* administrative actions

---

## Module Communication

Communication priority:

1. direct internal calls
2. internal events
3. async processing

---

## Boundary Rules

* controllers do not contain business logic
* services handle business logic
* repositories handle data access
* tenant must always be validated

---

## Final Direction

Água Nativa backend will be built as a **multi-tenant modular monolith, secure and scalable**.
