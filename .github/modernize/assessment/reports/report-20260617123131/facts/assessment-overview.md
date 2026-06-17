# Assessment Overview

This directory contains supplementary analysis documents generated as part of the **newbee-mall** application assessment. Each document covers a specific aspect of the application's design, configuration, and behavior to support modernization planning.

## Supplementary Documents

| Document | Description |
|---|---|
| [Architecture Diagram](./architecture-diagram.md) | Two-layer architecture visualization: application architecture (technology stack, data storage, external services) and component relationship diagram (controllers, services, mappers, interceptors grouped by layer). |
| [Dependency Map](./dependency-map.md) | Visual map of all declared external dependencies grouped by functional category, with version and compatibility risk analysis and test dependency inventory. |
| [API & Service Communication Contracts](./api-service-contracts.md) | Full inventory of HTTP endpoints across the storefront and admin portals, DTO/contract definitions, communication patterns, security posture, and a sequence diagram of the primary request flow. |
| [Data Architecture & Persistence Layer](./data-architecture.md) | Database configuration, entity model with ER diagram, MyBatis mapper method inventory, caching strategy, data ownership boundaries, and data classification (PII/PHI/PCI) with control assessment. |
| [Configuration & Externalized Settings Inventory](./configuration-inventory.md) | All configuration sources, build and runtime profiles, property inventory (including hardcoded constants), startup dependency chain, secrets handling, feature flags, and framework/runtime versions. |
| [Core Business Workflows](./business-workflows.md) | Domain entity descriptions, primary workflows (registration, login, order placement, payment, cancellation, admin order management, cart management), order state machine, business rules, and a Mermaid sequence diagram of the order placement flow. |
