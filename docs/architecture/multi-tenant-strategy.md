# Multi-Tenant Strategy

## Chosen Model
Shared database, shared schema, with logical isolation by tenant_id.

## Tenant Isolation Rules
- Every core domain entity must include tenant_id.
- No tenant can access data from another tenant.
- All reads and writes must be tenant-scoped.
- Tenant isolation must be validated in backend services and repositories.

## Authentication and Authorization
- Platform users and tenant users must be separated by role and scope.
- Tenant users can only operate inside their own tenant.
- Authorization decisions must consider both role and tenant context.

## Backend Enforcement
- Every request must carry authenticated tenant context.
- Backend use cases must validate tenant ownership before processing.
- Queries must always filter by tenant_id where applicable.
- Cross-tenant access must fail by default.

## Audit by Tenant
- Every critical action must record tenant_id, actor, action, target resource, and timestamp.
- Audit logs must support traceability by tenant.

## Scalability Considerations
- The architecture must support growth from 2 associations to many more without schema redesign.
- Indexing strategy must consider tenant-based filtering from the start.
