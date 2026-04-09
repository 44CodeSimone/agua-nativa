# Backend Module Map

## Objective

This document defines the backend module map of Água Nativa.

Its purpose is to clearly establish:

* which modules exist in the backend
* which modules are core
* which modules are supporting
* how modules relate to each other
* how to organize the NestJS backend without mixing responsibilities

This document complements:

* docs/architecture/service-architecture.md
* docs/architecture/system-overview.md
* docs/architecture/multi-tenant-strategy.md
* docs/database/*.md

---

## General Direction

The Água Nativa backend will be structured as a **modular monolith using NestJS**.

This means:

* a single backend application initially
* well-defined internal modules
* separated responsibilities
* controlled growth
* ability to evolve without structural rework

---

## Mandatory Module Rules

All modules must follow these rules:

* each module must have a clear responsibility
* no module should become a generic logic container
* business modules must not depend on HTTP details
* all modules must respect tenant boundaries
* sensitive modules must generate audit logs
* financial modules require strict validation
* module communication must be controlled

---

## Module Classification

Modules are divided into three groups:

1. foundation modules
2. core business modules
3. support and platform modules

---

## 1. Foundation Modules

These modules provide the structural base of the system.

### auth

Responsibilities:

* authentication
* authenticated context
* user identity
* access validation
* login integration

---

### tenants

Responsibilities:

* tenant context
* tenant identification
* logical isolation
* structural segregation rules

---

### users

Responsibilities:

* internal users
* roles and profiles
* tenant and association linkage
* activation and deactivation

---

### associations

Responsibilities:

* association data
* institutional configuration
* operational parameters

---

### audit

Responsibilities:

* audit trail
* traceability
* critical action logging
* user and tenant context

---

## 2. Core Business Modules

These modules represent the core system functionality.

### customers

Responsibilities:

* consumer registration
* customer status
* contact data
* linkage to units

---

### units

Responsibilities:

* consumer units
* location
* operational organization
* linkage to customers

---

### meters

Responsibilities:

* meters
* installation
* replacement
* status
* technical history

---

### readings

Responsibilities:

* meter readings
* validation
* anomaly detection
* consumption history
* field operation support

---

### tariffs

Responsibilities:

* tariff rules
* pricing tiers
* validity
* billing parameters

---

### extra-charges

Responsibilities:

* extra charges
* additional fees
* future billing entries
* traceability

---

### invoices

Responsibilities:

* invoice generation
* charge composition
* due dates
* status
* billing history

---

### payments

Responsibilities:

* payment processing
* settlement
* invoice linkage
* financial status
* reconciliation

---

## 3. Support and Platform Modules

These modules support operations and platform management.

### notifications

Responsibilities:

* notifications
* templates
* channels
* delivery history

---

### reports

Responsibilities:

* reporting
* data aggregation
* metrics
* exports
* management insights

---

### storage

Responsibilities:

* file storage
* attachments
* documents
* storage abstraction

---

### admin

Responsibilities:

* platform supervision
* controlled global view
* internal support actions

---

## Relationship Between Groups

### Foundation → Core Business

Foundation modules support core business modules.

Examples:

* auth controls access
* tenants ensure isolation
* users define operators
* audit logs critical actions

---

### Core Business → Support

Core modules feed support modules.

Examples:

* invoices trigger notifications
* payments feed reports
* readings generate audit events
* storage serves invoice documents

---

## Critical Modules

The most critical modules are:

* auth
* tenants
* readings
* invoices
* payments
* audit

These modules directly impact:

* security
* tenant isolation
* operational integrity
* financial consistency
* traceability

---

## Expected Dependencies

### auth

depends on:

* users
* tenants

---

### users

depends on:

* tenants
* associations

---

### customers

depends on:

* tenants
* associations

---

### units

depends on:

* customers
* tenants

---

### meters

depends on:

* units
* tenants

---

### readings

depends on:

* meters
* units
* customers
* tenants

---

### tariffs

depends on:

* tenants
* associations

---

### extra-charges

depends on:

* customers
* units
* invoices
* tenants

---

### invoices

depends on:

* customers
* units
* meters
* readings
* tariffs
* extra-charges
* tenants

---

### payments

depends on:

* invoices
* tenants

---

### notifications

depends on:

* customers
* invoices
* payments
* tenants

---

### reports

depends on:

* readings
* invoices
* payments
* customers
* tenants

---

### audit

receives events from:

* auth
* users
* readings
* tariffs
* extra-charges
* invoices
* payments
* admin

---

### storage

serves:

* invoices
* notifications
* admin
* future document needs

---

## Suggested NestJS Structure

The backend should evolve into a structure like:

src/
modules/
auth/
tenants/
users/
associations/
customers/
units/
meters/
readings/
tariffs/
extra-charges/
invoices/
payments/
notifications/
reports/
audit/
storage/
admin/

Each module should internally follow:

* controllers
* application
* domain
* infrastructure
* dto
* repositories
* events
* policies

---

## Implementation Strategy

When implementing the backend:

* do not create all modules at once
* start with structural foundation
* then core business modules
* then support modules

Suggested order:

1. auth
2. tenants
3. users
4. associations
5. customers
6. units
7. meters
8. readings
9. tariffs
10. extra-charges
11. invoices
12. payments
13. notifications
14. reports
15. audit
16. storage
17. admin

---

## Final Note

Água Nativa backend will not be a collection of loose endpoints.

It will be a **modular backend with clear boundaries, explicit responsibilities, and a controlled growth structure**.

This document exists to prevent:

* responsibility mixing
* unnecessary coupling
* structural confusion
* future rework

It must serve as a direct reference for the next phase of backend implementation.
