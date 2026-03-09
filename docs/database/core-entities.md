# Database Core Entities

## Tenants
Represents an association using the system.

Fields:
- id
- name
- created_at
- status

## Users
Represents users belonging to a tenant.

Fields:
- id
- tenant_id
- name
- email
- role
- created_at

## Customers
Represents a person responsible for water consumption.

Fields:
- id
- tenant_id
- name
- document
- phone
- email
- created_at

## Units
Represents a physical property connected to water service.

Fields:
- id
- tenant_id
- customer_id
- address
- status
- created_at

## Meters
Represents a water meter device.

Fields:
- id
- tenant_id
- serial_number
- model
- installation_date
- status

## Meter Installations
Tracks meter changes for units.

Fields:
- id
- tenant_id
- unit_id
- meter_id
- installed_at
- removed_at

## Readings
Represents meter readings.

Fields:
- id
- tenant_id
- meter_id
- reading_value
- reading_date
- reader_id

## Tariffs
Defines pricing rules.

Fields:
- id
- tenant_id
- name
- base_fee
- minimum_consumption
- created_at

## Invoices
Represents billing documents.

Fields:
- id
- tenant_id
- unit_id
- reference_month
- total_amount
- status
- created_at

## Invoice Items
Represents line items inside invoices.

Fields:
- id
- tenant_id
- invoice_id
- description
- amount

## Payments
Represents invoice payments.

Fields:
- id
- tenant_id
- invoice_id
- payment_method
- amount
- paid_at
