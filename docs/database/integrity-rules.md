# Multi-Tenant Integrity Rules

## Tenant Boundary Rule
Every business table must contain tenant_id.

## Cross-Tenant Protection Rule
No foreign key or business relationship may allow linking records from different tenants.

## Historical Integrity Rule
Critical historical records such as readings, invoices, invoice items, payments, and audit logs must not be physically deleted in normal operation.

## Soft Delete Rule
When removal is needed for business entities, prefer logical deletion strategies where appropriate.

## Auditability Rule
Critical actions must generate audit records with:
- tenant_id
- actor_id
- action
- target_type
- target_id
- timestamp

## Referential Integrity Rule
Foreign keys must be explicitly defined for all critical relationships.

## Billing Integrity Rule
Invoices must preserve billing history even if customer or unit data changes later.

## Meter Traceability Rule
Meter replacement history must be preserved through meter_installations.

## Payment Integrity Rule
Payments must always be linked to the invoice they settle.

## Default Safety Rule
Database design must fail closed by default for tenant isolation and critical integrity constraints.
