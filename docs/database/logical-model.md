# Logical Database Model

## Tenants
Primary entity representing each water association using the platform.

Main attributes:
- id
- name
- status
- created_at

---

## Users
Users belonging to a tenant.

Attributes:
- id
- tenant_id
- name
- email
- role
- status
- created_at

Relationship:
users.tenant_id -> tenants.id

---

## Customers
Represents the person responsible for water consumption.

Attributes:
- id
- tenant_id
- name
- document
- phone
- email
- created_at

Relationship:
customers.tenant_id -> tenants.id

---

## Units
Represents a property connected to the water network.

Attributes:
- id
- tenant_id
- customer_id
- address
- status
- created_at

Relationships:
units.tenant_id -> tenants.id
units.customer_id -> customers.id

---

## Meters
Represents a physical water meter device.

Attributes:
- id
- tenant_id
- serial_number
- model
- installation_date
- status

Relationship:
meters.tenant_id -> tenants.id

---

## Meter Installations
Tracks meter replacement history.

Attributes:
- id
- tenant_id
- unit_id
- meter_id
- installed_at
- removed_at

Relationships:
meter_installations.unit_id -> units.id
meter_installations.meter_id -> meters.id

---

## Readings
Stores water consumption measurements.

Attributes:
- id
- tenant_id
- meter_id
- reading_value
- reading_date
- reader_id

Relationships:
readings.meter_id -> meters.id
readings.reader_id -> users.id

---

## Tariffs
Defines pricing rules.

Attributes:
- id
- tenant_id
- name
- base_fee
- minimum_consumption
- created_at

Relationship:
tariffs.tenant_id -> tenants.id

---

## Invoices
Billing documents generated for units.

Attributes:
- id
- tenant_id
- unit_id
- reference_month
- total_amount
- status
- created_at

Relationships:
invoices.tenant_id -> tenants.id
invoices.unit_id -> units.id

---

## Invoice Items
Individual billing components inside invoices.

Attributes:
- id
- tenant_id
- invoice_id
- description
- amount

Relationship:
invoice_items.invoice_id -> invoices.id

---

## Payments
Records invoice payments.

Attributes:
- id
- tenant_id
- invoice_id
- payment_method
- amount
- paid_at

Relationship:
payments.invoice_id -> invoices.id

---

## Multi-Tenant Rule
Every entity that belongs to business data must include tenant_id.

## Integrity Rule
All relationships must enforce tenant boundary validation.
