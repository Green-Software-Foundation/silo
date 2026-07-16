```
Status: Draft specification — under review by the HSWG (Hardware Sustainability Working Group).
Feedback and contributions from data center, sustainability, and software domain experts are welcome.
```

# SILO — Standardized Interoperability Layer for Real-Time Sustainability Optimization

> A vendor-neutral semantic and interoperability specification for real-time sustainability optimization in data centers.

## Overview

SILO defines a standardized interoperability layer between data center infrastructure and software platforms. It builds on the [Green Software Foundation](https://greensoftware.foundation/) Workload-Dynamic Power and Cooling (WDPC) standard, extending it with a common framework for collecting, normalizing, and exchanging operational metrics across:

- Compute
- Power
- Cooling
- Networking
- Storage
- Facility systems

By providing standardized data models, interfaces, and semantic definitions, SILO enables consistent, real-time visibility into both IT workloads and physical infrastructure — allowing data center operators, management platforms, and optimization engines to consume and share information through a common interface.

SILO does **not** replace existing management protocols or telemetry systems. It defines a semantic layer that complements the existing WDPC framework and provides a foundation for future cross-vendor interoperability.

## Why SILO

Data center sustainability optimization today is constrained by siloed domains — compute, power, cooling, and facility systems each expose data differently, with no shared vocabulary or common access pattern. SILO addresses this by establishing:

- **A common semantic layer** so metrics mean the same thing everywhere they're consumed
- **Standardized APIs** for discovery, querying, and streaming of operational data
- **A vendor-neutral translation framework** for heterogeneous, multi-vendor environments
- **Formal governance** to keep the specification stable and interoperable as it evolves

This unlocks coordinated, real-time decision-making across previously disconnected systems — the foundation for adaptive cooling, dynamic workload placement, energy efficiency optimization, predictive maintenance, heat reuse optimization, and automated sustainability reporting.

## Architecture

SILO plugs into the existing WDPC Data Bus as an internal interoperability layer, sitting between raw infrastructure telemetry and any external-facing interface (such as a grid-signal or ESG reporting layer):

```
 Grid Operator / External Signals
 (Renewable mix · Carbon intensity · Demand constraints)
                    ↕
 External Interface Specification
 (Grid signal ingestion · Power source awareness · ESG output)
                    ↕
 Internal Interoperability Layer  ← SILO (this specification)
 (Semantic normalization · Vendor-neutral translation · Data contracts)
                    ↕
 Existing WDPC Data Bus + Rack & Sensing + Facility Infrastructure
```

SILO is the internal layer: it normalizes cross-system data within the data center and provides the semantic model and vendor-neutral translation that any external interface depends on for reliable, grid-responsive decisions. An external interface without this internal layer only works reliably in homogeneous, single-vendor environments — the two are complementary, and neither is sufficient alone.

> **Future consideration:** ingestion of rack/sensing/facility infrastructure data for use in the Internal Interoperability Layer and higher levels of the architecture.

## Core Components

### 1. Semantic Models
A vendor-neutral data model defining the meaning, relationships, and context of operational metrics across IT and facility systems.
- Common taxonomies, metadata, and engineering units for consistent interpretation
- Enables downstream applications to understand not just a metric's value, but its source, dependencies, and operational context
- Includes canonical semantic models, cross-domain relationship definitions, normalization rules for vendor-specific telemetry, and metadata/schema governance mechanisms

### 2. APIs
Standardized interfaces for discovering, querying, and streaming operational data across heterogeneous infrastructure.
- Supports both real-time and historical data access via modern API frameworks
- Decouples data consumers from underlying hardware and vendor-specific implementations

### 3. Interoperability Framework
Normalizes and translates data from diverse protocols and vendor systems into a common semantic format.
- Validates incoming data for schema compliance, quality, and consistency
- Ensures reliable, interoperable data exchange across the data center ecosystem

### 4. Governance
Defines the process for maintaining semantic models, approving new metrics, and managing the specification's evolution.
- Versioning, compliance, and change-control mechanisms aligned with WDPC governance
- Canonical semantic models maintained by a **SILO Technical Steering Committee** (data center, sustainability, and software domain experts)
- New metric types introduced through formal review and approval
- Versioning kept aligned with WDPC releases for compatibility and coordinated ecosystem evolution

## Scope

| Internal Interoperability Layer (SILO) | External Interface (companion white paper) |
|---|---|
| Cross-system data normalization within the DC | DC ↔ Grid communication |
| Semantic model & vendor-neutral translation | Grid signal ingestion & ESG output |
| **Enables:** reliable external signals & responses | **Requires:** unified internal data |

## Sustainability Metrics

SILO supports standardized measurement and reporting of:

- Power Usage Effectiveness (PUE)
- Water Usage Effectiveness (WUE)
- Carbon Usage Effectiveness (CUE)
- Energy consumption
- Water consumption
- Associated carbon emissions

Success is evaluated by the **availability, consistency, and interoperability** of these metrics across participating systems — enabling organizations to quantify operational improvements and sustainability outcomes over time.

## Use Cases

- Adaptive cooling
- Dynamic workload placement
- Energy efficiency optimization
- Predictive maintenance
- Heat reuse optimization
- Automated sustainability reporting

## Related Documents

- **Bridging the Sustainability Gap** (white paper) — defines the external interface between the data center and the grid (grid signal ingestion, power source awareness, ESG output)
- **Companion Technical Note** — clarifies how this internal interoperability layer and the external interface form one complete, deployable architecture

