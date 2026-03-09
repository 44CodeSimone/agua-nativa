# Database Conceptual Model

## Core Platform Entities
- tenants
- associations
- platform_users
- tenant_users
- roles
- permissions
- audit_logs

## Operational Entities
- customers
- customer_contacts
- units
- meters
- meter_installations
- readings
- reading_occurrences
- reading_routes

## Financial Entities
- tariffs
- tariff_rules
- extra_charges
- invoices
- invoice_items
- payments
- payment_methods
- payment_reconciliation

## Communication Entities
- notifications
- notification_deliveries
- announcements
- attachments

## Supporting Entities
- addresses
- tenant_settings
- billing_cycles

## Multi-Tenant Rule
All operational domain entities must include tenant_id to ensure strict data isolation between associations.

## Audit Rule
All critical operations must generate audit logs containing actor, tenant_id, action, target resource, and timestamp.
