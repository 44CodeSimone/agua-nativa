# Water Association Domain Model

## Customer
Represents a person or entity responsible for a water consumption unit.

A customer may own or be responsible for one or more units.

## Unit
Represents a physical property connected to the water network.

Each unit belongs to exactly one tenant and is associated with one customer.

A unit may have one active meter installed.

## Meter
Represents the physical water meter device installed at a unit.

Meters store identification data such as serial number and installation history.

## Meter Installation
Represents the installation event of a meter in a unit.

This allows the system to track meter replacements over time.

## Reading
Represents a measurement of water consumption collected from a meter.

Each reading records:
- previous value
- current value
- consumption calculation
- reading date
- reading agent

## Tariff
Defines how water consumption is priced.

Tariffs may include:
- fixed base fee
- consumption tiers
- minimum consumption

## Invoice
Represents the billing document generated for a unit.

An invoice may contain:
- consumption charge
- extra charges
- adjustments

## Extra Charges
Represents additional charges applied to a customer or unit.

Examples:
- meter replacement
- maintenance
- penalties

Extra charges may be applied to the next billing cycle.

## Payment
Represents the settlement of an invoice.

Payments may be performed via:
- Pix
- bank slip
- other supported methods.

## Multi-Tenant Rule
All domain entities must contain tenant_id to guarantee data isolation between associations.
