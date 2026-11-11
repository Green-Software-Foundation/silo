# SILO Assembly Research Note

## What this Assembly is deciding

We are not redefining WDPC, and we are not writing the specification. We are agreeing the baseline requirements the SILO pre-draft specification must satisfy: who must conform and to what, where normalisation happens, the minimum metric set, and what makes SILO data auditable.

## The core question

What must SILO require so that operational data from any vendor is given a common, vendor-neutral meaning that every consumer can trust?

## What you need to know before deliberation

- WDPC moves the data; SILO gives it shared meaning [2][4].
- SILO is a standalone specification. It takes WDPC as a normative reference and does not revise it [2].
- SILO spans six domains [1]. The draft proposes starting with power and grid interaction [2], but this Assembly does not decide phasing.
- SILO is an internal interoperability layer. Grid signals and ESG reporting are handled by an external interface above it, which needs grid operator input. Without that, SILO still supports local optimisation within a facility [6].
- SILO enables measurement. It sets no targets, and conformance does not imply any sustainability outcome [2].
- SILO references existing schemas, such as DMTF Redfish, rather than redefining them [2].
- The Assembly works through four Topics, each closing open issues in the SILO repository. A fifth Topic is to be confirmed.

# Overview

A typical AI data centre runs servers, coolant distribution units, cooling systems, power distribution units, building management systems and energy management software from different vendors. Each exposes telemetry in a different format. That makes it hard to correlate data and automate optimisation across the whole system [5].

[Architecture Diagram](https://github.com/Green-Software-Foundation/silo/blob/assembly/assembly/resources/silo-conceptual-architecture.pdf)

The SILO conceptual architecture shows how SILO connects infrastructure data sources to the applications that use them. Data from compute, cooling, power, facility, network and storage systems arrives through protocol adapters. It is mapped and translated into the SILO semantic layer, then made available through SILO APIs to applications such as DCIM, workload orchestrators, digital twins, energy management and analytics. The diagram is a pre-draft for discussion, and the Assembly is one of the places it will evolve [10].

WDPC, an existing GSF standard, already provides a central data bus. Workloads, infrastructure, sensors and external systems publish and consume data through it in real time [3][4]. What is missing is a consistent way to interpret telemetry from many vendors and domains once it is on the bus [2].

SILO proposes that missing layer. It has four elements [2]:

- a vendor-neutral semantic model;
- APIs to discover, query and stream normalised data;
- an interoperability framework that translates and validates vendor telemetry;
- governance to maintain the model over time.

The Assembly’s task is to agree the baseline requirements the SILO pre-draft specification must satisfy. Its output, SILO Baseline Requirements, goes to the Hardware Standards Working Group as the input to that specification.

## What participants are not being asked to decide

- Changes to WDPC, or how telemetry is collected and transmitted onto the WDPC data bus.
- Sustainability targets, KPIs or reduction thresholds.
- A composite sustainability score for hardware or facilities.
- Optimisation, predictive maintenance or control logic that consumes SILO data.
- The final normative wording of the specification.
- Phasing, or which domains the specification covers first.
- Grid communication, grid signal ingestion and external ESG output, which belong to a separate external interface specification.
- Test suites, certification or badging schemes.
- Protocol-specific mapping tables, or API endpoint and method design.
- Optional or extended metrics, the full semantic model, or methods for calculating KPIs.
- Audit procedures, reporting templates, or transport and security mechanisms.

## What this Assembly will decide

The Assembly works through four Topics in order, each building on the last. Each closes one or more open issues in the SILO repository. A fifth Topic is to be confirmed.

| Topic | Question | Closes |
| --- | --- | --- |
| 1. Conformance boundary | What must a product, platform or facility system do to claim SILO conformance, and are protocol adapters part of SILO? | #5 |
| 2. How data flows and what the APIs serve | Where does translation to the SILO semantic model happen, and do the APIs serve only normalised data? | #3 |
| 3. Units, minimum metric set and resolution | Where are units declared and converted, and which metrics must every conformant source expose? | #19 |
| 4. Validation, provenance and lineage | Where is data validated, and what must a normalised value carry for a sustainability claim to be auditable? | #15, #18 |

The output is SILO Baseline Requirements, the agreed input to the SILO pre-draft specification.

---

# Suggested reading paths

## If you know facilities, hardware or energy but not the GSF specifications

Read: Overview → Track A → Track B recap.

## If you know software platforms or data but not data centre operations

Read: Overview → Track B → Track A recap.

# Glossary

| Term | Plain-English meaning |
| --- | --- |
| WDPC | Workload Dynamic Power and Cooling. GSF standard for real-time data exchange between workloads, data centres and grids. |
| Data bus | WDPC's shared exchange onto which facility, rack and component telemetry is published. |
| SILO | Standardized Interoperability Layer for Real-Time Sustainability Optimization. A proposed internal interoperability layer that gives operational data a common, vendor-neutral meaning. |
| Semantic layer | The layer that establishes common meaning, relationships and context for telemetry already on the bus. |
| Normalisation | Translating vendor- or protocol-specific telemetry into SILO's canonical model. |
| Protocol adapters | Components that bring data into SILO from the protocols equipment already uses, such as Redfish, BACnet and MQTT. |
| External Interface Specification | The proposed layer above SILO that handles grid signals and ESG output. |
| Grid signal | Grid data relevant to sustainability decisions: availability, carbon intensity, constraints. |
| Telemetry provider | An organisation supplying the instrumentation, schemas or data feeds that populate the bus. |
| Operator | The organisation running a data centre day to day, distinct from its electrical designer. |
| Device-class schema | An existing standard schema for a type of equipment, such as Redfish for accelerators. |
| PUE / WUE / CUE | Power, Water and Carbon Usage Effectiveness. These are standard facility efficiency metrics. |

The SILO Assembly Glossary is the single source of truth for full definitions.

---

# Track A: WDPC and SILO, for the infrastructure reader

Track A summarises the two GSF specifications for readers whose background is facilities, hardware or energy rather than GSF standards. Reference material, not a deliberation input.

## What WDPC is

WDPC starts from the scale of modern AI workloads. A single training run can cause power swings of over 200 MW in 40 ms. WDPC standardises communication between workloads and infrastructure so these swings don't destabilise power systems or waste renewable energy [3].

The WDPC specification defines [4]:

- **A central data bus.** All components connect to it directly, including workloads, servers, cooling, power distribution, sensors and external systems such as grid operators and municipal utilities.
- **Protocol Buffer data models** for high-performance exchange.
- **Hierarchical data models**, from facility level down to rack, node and component.
- **Frameworks** for energy markets, carbon optimisation and demand response.
- **Streaming and security requirements**, including sub-100 ms data publication.

WDPC supports Apache Kafka, Apache Pulsar and MQTT Sparkplug B, and bridges existing building management and SCADA systems onto the bus [4]. It standardises and distributes data. It does not prescribe control algorithms or central orchestration [4].

## What SILO adds

In the draft's terms, WDPC defines how telemetry is collected and exchanged. SILO begins where telemetry from multiple domains and vendors on the bus has to be interpreted consistently [2].

| Element | What the draft requires |
| --- | --- |
| Semantic model | Vendor-neutral taxonomies, metadata and engineering units. It references existing device-class schemas rather than redefining them. |
| APIs | Interfaces to discover, query (real-time and historical) and stream normalised telemetry, decoupling consumers from vendor implementations. |
| Interoperability framework | Translation of telemetry from diverse protocols and vendors into the model, with validation for schema compliance, quality and consistency. |
| Governance | A SILO Technical Steering Committee, a formal review process for new metric types, and versioning aligned to WDPC releases. |

## Where SILO sits

SILO is an internal interoperability layer. It sits between raw infrastructure telemetry and any external-facing interface, such as a grid-signal or ESG reporting layer [6].

| Layer | Role |
| --- | --- |
| Grid operator and external signals | Renewable mix, carbon intensity, demand constraints |
| External Interface Specification | Grid signal ingestion, power source awareness, ESG output |
| **SILO: internal interoperability layer** | **Semantic normalisation, vendor-neutral translation, data contracts** |
| WDPC data bus, rack and sensing, facility infrastructure | Existing data exchange, telemetry and equipment |

SILO connects with the WDPC data bus and also draws on existing standards such as Redfish and OpenTelemetry [2][10]. The conceptual architecture shows how data moves through SILO itself [10]:

1. **Protocol adapters** bring in data from the protocols equipment already uses, including Redfish, BACnet, Modbus, SNMP, MQTT and OpenTelemetry.
2. **Mapping and translation** converts that data into the SILO semantic layer.
3. **SILO APIs** make the normalised data available to applications such as DCIM, workload orchestrators, digital twins, energy management and analytics, and to external interfaces.

SILO does not dictate how vendors instrument equipment [2].

## Scope and phasing

SILO covers compute, power, cooling, networking, storage and facility systems [1]. The draft proposes delivering in phases [2]:

- **Starting with power and grid interaction**, including renewable and carbon-intensity signals and a two-way grid interface.
- **Following with cooling and thermal, environmental sensing, and network domains** in later phases.

That phasing is a proposal. This Assembly does not decide it.

### Grid interaction

SILO doesn't connect to the grid directly. It provides the consistent internal data that an external interface needs in order to respond to grid signals [6]. That interface requires input from grid operators. Without it, SILO still works as a tool for local optimisation within a single facility.

## What is fixed

- **WDPC is a normative reference.** SILO builds on it and does not revise it [2].
- **SILO sets no targets.** Target-setting is left to the regulatory and organisational frameworks that use SILO data [2].
- **Conformance is about data, not outcomes.** An implementation conforms if it:
    - exposes in-scope telemetry through the semantic model;
    - implements the APIs;
    - meets the interoperability requirements.
    
    Success is judged on the availability, consistency and interoperability of metrics, not on the values they report [2].
    

## Track A recap

For this Assembly, the important specification rules are:

- WDPC moves data; SILO interprets it.
- WDPC is a normative reference and is not being changed.
- SILO is an internal layer between infrastructure and external interfaces, and does not dictate instrumentation.
- SILO spans six domains. The draft proposes starting with power and grid, but this Assembly does not decide phasing.
- Grid interaction runs through an external interface above SILO and needs grid operator input. Without it, SILO supports local optimisation.
- SILO sets no targets and defines no composite score.
- Conformance is about data availability, consistency and interoperability.
- The draft lists four open issues of its own. This Assembly's four Topics are set out in the Overview.

---

# Track B: The data centre landscape, for the software reader

Track B summarises the operational and sustainability context for readers whose background is software platforms or data rather than data centre operations. Reference material, not a deliberation input.

## Why multi-vendor telemetry is hard

**What the sources say:** A single AI data centre typically combines servers, coolant distribution units, cooling systems, power distribution units, building management systems and energy management software from different vendors, each with its own telemetry format [5]. Software that wants to optimise across them has to build a custom integration for each vendor's format [1].

**Why the Assembly cares:** SILO's value depends on removing per-vendor integration work for consuming applications [2]. Every scoping decision should be tested against whether it achieves that.

## Efficiency is not sustainability

**What the sources say:** A facility can achieve its best-ever PUE and still be unsustainable. Sustainability depends on how power demand relates to the make-up of the supply: how much power drawn at a given moment is low-carbon rather than, for example, diesel backup [2].

**Why the Assembly cares:** This is why grid interaction matters to SILO, and why the draft proposes starting there. Coordinating workloads with grid conditions needs grid signals and facility telemetry in a common, interpretable form, and the draft states none currently exists across vendors and domains [2].

## Existing device schemas

**What the sources say:** Equipment telemetry already follows device-class schemas. The draft treats DMTF Redfish as the normative reference for GPU and accelerator telemetry, and points to the Open Compute Project's unified liquid cooling and CDU schema, still in development, for cooling [2]. The conceptual architecture also places SNIA Swordfish, OCP Hardware Management, OCP Cooling Environments and OpenTelemetry in SILO's standards ecosystem [10].

**Why the Assembly cares:** Reuse is the default. These schemas generally carry no sustainability-relevant metadata [2].

## The grid relationship

**What the sources say:** Grid signals are handled by an External Interface Specification that sits above SILO. It ingests grid signals, tracks power source composition and produces ESG output [6][7]. SILO supplies it with consistent internal data. WDPC also specifies grid operator integration at the data bus boundary [4].

**Why the Assembly cares:** SILO's value to the grid depends on the quality of the internal data it provides. Without an external interface and grid operator input, SILO still delivers value as a tool for local optimisation within a facility. Grid communication itself is out of scope for this Assembly, but the requirements it agrees determine what internal data an external interface can rely on.

## Regulatory drivers

**What the sources say:** The draft white paper sets out two main drivers [7]:

- **EU Energy Efficiency Directive (2023/1791).** Since September 2024, data centres with an IT power demand of 500 kW or more submit annual sustainability reports. Under Article 12(5), the European Commission must assess that data and, where appropriate, introduce minimum performance standards.
- **Corporate Sustainability Reporting Directive (2022/2464).** It requires credible Scope 2 disclosure and, increasingly, Scope 3 emissions attributable to IT infrastructure.

**Why the Assembly cares:** SILO supplies consistent, comparable data to these frameworks. It does not interpret or enforce them [2].

## Use cases

**What the sources say:** The draft lists use cases that become possible once the semantic layer exists. These are not requirements or conformance criteria [2]:

- Adaptive cooling
- Dynamic workload placement
- Energy efficiency optimisation
- Predictive maintenance (needs capability beyond SILO's scope)
- Heat reuse optimisation (may need control interfaces beyond SILO's scope)
- Automated sustainability reporting

**Why the Assembly cares:** Use cases explain why the model matters. They should inform scope without pulling control or analytics logic into the specification.

## Who has a stake

**What the sources say:** The draft identifies these groups as needed for further specification development [2]:

| Group | Role |
| --- | --- |
| Data centre operators | Primary implementers, balancing cost and sustainability targets |
| Hardware and component manufacturers | Chiller, UPS, GPU and accelerator, and CDU makers |
| Vendor software engineers | Management software for individual components |
| BMS engineers | Own much of the existing data stream SILO builds on |
| Grid operators and grid signal specialists | Grid-side signals and constraints |
| Facility operators | Day-to-day operation and maintenance |
| Electrical design engineers and EPC firms | Design of power distribution infrastructure |
| Telemetry providers | May need to extend schemas to support SILO |
| ESG policymakers and analysts | May classify SILO-derived data for regulatory purposes |
| Academic partners | Research input and validation |

**Why the Assembly cares:** A scoping decision that works for software consumers but not for telemetry providers or BMS engineers will struggle in implementation.

## Track B recap

For this Assembly, the important landscape points are:

- Multi-vendor telemetry forces per-vendor integration today.
- Efficiency and sustainability are different properties.
- Device schemas such as Redfish already exist and should be reused.
- Those schemas lack sustainability metadata.
- SILO feeds an external grid interface rather than talking to the grid itself. Without one, it supports local optimisation.
- SILO feeds regulatory reporting but does not interpret it.
- Use cases inform scope but are not requirements.

---

# Prior-art register

SILO does not start from nothing. Data already moves on a standard bus, device schemas exist, and cross-domain data modelling has a GSF precedent.

| Prior art | What it is | Why it matters here |
| --- | --- | --- |
| GSF WDPC | Central data bus and hierarchical data models for workload, power, thermal and grid data [3][4]. | SILO's foundation and normative reference. |
| DMTF Redfish | Management interface schema for servers and accelerators [2]. | Normative reference for GPU and accelerator telemetry. |
| OCP unified liquid cooling and CDU schema | Device schema in development [2]. | Intended reference for cooling telemetry. |
| SNIA Swordfish | Storage management standard extending DMTF Redfish [10]. | Part of SILO's standards ecosystem for storage. |
| OCP Hardware Management and Cooling Environments | Open Compute Project work on hardware management and cooling [10]. | Part of SILO's standards ecosystem. |
| External Interface Specification (draft white paper) | Proposed layer above SILO for grid signals and ESG output [6][7]. | Defines what SILO's internal data needs to support. |
| GSF SCI family | Software Carbon Intensity and extensions, including SCI for AI and SCI for Circularity [2]. | SILO data could feed future SCI-style calculations. SILO itself defines no score. |
| Supplier carbon labelling | Procurement-side embodied-carbon reporting efforts [2]. | Distinct from SILO's operational focus; candidate for liaison. |

Prior art is reference evidence only and confers no standing in the deliberation.

---

# References

1. Green Software Foundation. *SILO: Sustainability Interoperability Layer for Operations*. https://greensoftware.foundation/standards/silo/
2. GSF Hardware Standards Working Group. *SILO: Standardized Interoperability Layer for Real-Time Sustainability Optimization*, initial baseline specification (pre-standard working draft), GitHub. https://github.com/Green-Software-Foundation/silo/blob/initial-baseline/SPEC.md
3. Green Software Foundation. *WDPC: Workload Dynamic Power and Cooling*. https://greensoftware.foundation/standards/wdpc/
4. Green Software Foundation. *Workload Dynamic Power and Cooling (WDPC) Specification*, GitHub. https://github.com/Green-Software-Foundation/Workload-Dynamic-Power-and-Cooling/blob/dev/WDPC-Spec.md
5. Green Software Foundation. *SILO Project Q&A*, 3 August 2026. https://greensoftware.foundation/policy/research/silo-project-qa/
6. Green Software Foundation. *Companion Technical Note: Completing the Architecture, The Internal Interoperability Layer*, 22 July 2026. https://greensoftware.foundation/policy/research/silo-companion-technical-note/
7. GSF Hardware Standards Working Group. *Bridging the Sustainability Gap*, white paper (draft, not yet approved), GitHub. https://github.com/Green-Software-Foundation/sci-policy-and-legislation-alignment-white-paper-series/blob/main/whitepapers/Interoperability%20Layer%20for%20Real-Time%20Data%20Centre%20Sustainability%20Optimisation.md
8. Green Software Foundation. *Project Mycelium*. https://greensoftware.foundation/assemblies/project-mycelium
9. Green Software Foundation. *Assemblies*. https://greensoftware.foundation/assemblies/
10. GSF Hardware Standards Working Group. *SILO Conceptual Architecture* (pre-draft proposal), November 2026.
