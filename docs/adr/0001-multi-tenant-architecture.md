# ADR 0001 - Multi-Tenant Architecture

## Status
Accepted

## Context
Agua Nativa is being designed as a SaaS platform for rural water associations.
The system must support multiple associations with strict data isolation between tenants from day one.
Initially, the platform will serve two associations, but it must be able to scale to many more without architectural rework.

## Options Considered
1. Single-tenant per deployment
2. Shared database with separate schema per tenant
3. Shared database with shared schema and tenant_id isolation

## Decision
We will adopt a shared database, shared schema, multi-tenant architecture with mandatory tenant_id isolation across domain entities.
Tenant isolation must be enforced in the backend, authorization rules, queries, auditing, and service boundaries.

## Consequences
- Lower infrastructure cost in the initial phase
- Faster SaaS expansion for new associations
- Strong need for disciplined tenant-aware backend design
- Mandatory auditability and authorization by tenant
- All domain modeling must consider tenant isolation from the start
