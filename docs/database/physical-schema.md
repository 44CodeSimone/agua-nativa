# Physical Database Schema

## tenants
Table for associations using the platform.

Columns:
- id UUID PRIMARY KEY
- name VARCHAR NOT NULL
- status VARCHAR NOT NULL
- created_at TIMESTAMP NOT NULL

## users
Table for tenant users.

Columns:
- id UUID PRIMARY KEY
- tenant_id UUID NOT NULL
- name VARCHAR NOT NULL
- email VARCHAR NOT NULL
- role VARCHAR NOT NULL
- status VARCHAR NOT NULL
- created_at TIMESTAMP NOT NULL

Foreign Keys:
- tenant_id REFERENCES tenants(id)

## customers
Table for people responsible for units.

Columns:
- id UUID PRIMARY KEY
- tenant_id UUID NOT NULL
- name VARCHAR NOT NULL
- document VARCHAR
- phone VARCHAR
- email VARCHAR
- created_at TIMESTAMP NOT NULL

Foreign Keys:
- tenant_id REFERENCES tenants(id)

## units
Table for physical properties.

Columns:
- id UUID PRIMARY KEY
- tenant_id UUID NOT NULL
- customer_id UUID NOT NULL
- address VARCHAR NOT NULL
- status VARCHAR NOT NULL
- created_at TIMESTAMP NOT NULL

Foreign Keys:
- tenant_id REFERENCES tenants(id)
- customer_id REFERENCES customers(id)

## meters
Table for water meter devices.

Columns:
- id UUID PRIMARY KEY
- tenant_id UUID NOT NULL
- serial_number VARCHAR NOT NULL
- model VARCHAR
- installation_date DATE
- status VARCHAR NOT NULL

Foreign Keys:
- tenant_id REFERENCES tenants(id)

## meter_installations
Table for meter installation history.

Columns:
- id UUID PRIMARY KEY
- tenant_id UUID NOT NULL
- unit_id UUID NOT NULL
- meter_id UUID NOT NULL
- installed_at TIMESTAMP NOT NULL
- removed_at TIMESTAMP

Foreign Keys:
- tenant_id REFERENCES tenants(id)
- unit_id REFERENCES units(id)
- meter_id REFERENCES meters(id)

## readings
Table for meter readings.

Columns:
- id UUID PRIMARY KEY
- tenant_id UUID NOT NULL
- meter_id UUID NOT NULL
- reading_value NUMERIC NOT NULL
- reading_date DATE NOT NULL
- reader_id UUID NOT NULL

Foreign Keys:
- tenant_id REFERENCES tenants(id)
- meter_id REFERENCES meters(id)
- reader_id REFERENCES users(id)

## tariffs
Table for pricing rules.

Columns:
- id UUID PRIMARY KEY
- tenant_id UUID NOT NULL
- name VARCHAR NOT NULL
- base_fee NUMERIC NOT NULL
- minimum_consumption NUMERIC NOT NULL
- created_at TIMESTAMP NOT NULL

Foreign Keys:
- tenant_id REFERENCES tenants(id)

## invoices
Table for billing records.

Columns:
- id UUID PRIMARY KEY
- tenant_id UUID NOT NULL
- unit_id UUID NOT NULL
- reference_month DATE NOT NULL
- total_amount NUMERIC NOT NULL
- status VARCHAR NOT NULL
- created_at TIMESTAMP NOT NULL

Foreign Keys:
- tenant_id REFERENCES tenants(id)
- unit_id REFERENCES units(id)

## invoice_items
Table for invoice line items.

Columns:
- id UUID PRIMARY KEY
- tenant_id UUID NOT NULL
- invoice_id UUID NOT NULL
- description VARCHAR NOT NULL
- amount NUMERIC NOT NULL

Foreign Keys:
- tenant_id REFERENCES tenants(id)
- invoice_id REFERENCES invoices(id)

## payments
Table for invoice payments.

Columns:
- id UUID PRIMARY KEY
- tenant_id UUID NOT NULL
- invoice_id UUID NOT NULL
- payment_method VARCHAR NOT NULL
- amount NUMERIC NOT NULL
- paid_at TIMESTAMP

Foreign Keys:
- tenant_id REFERENCES tenants(id)
- invoice_id REFERENCES invoices(id)
