# SILO Assembly Glossary

**Green Software Foundation | Hardware Standards Working Group**

This glossary is the single source of truth for terms used in the SILO Assembly Research Note and during deliberation. Terms are grouped by theme. Source numbers refer to the reference list at the end.

Where WDPC and SILO use the same word differently, both meanings are given.

## 1. Specifications, projects and bodies

| Term | Definition | Source |
|---|---|---|
| **SILO** | A proposed vendor-neutral semantic layer that sits above the WDPC data bus and gives telemetry from multiple vendors and domains a common, consistent meaning. The website expands the name as Sustainability Interoperability Layer for Operations. The draft specification expands it as Standardized Interoperability Layer for Real-Time Sustainability Optimization. | [1][2] |
| **WDPC** | Workload Dynamic Power and Cooling. An approved GSF standard that defines a central data bus and data models so workloads, data centres and power grids can exchange data in real time. | [3][4] |
| **External Grid Interface** | A proposed GSF specification for how a data centre receives and responds to real-time grid signals, set out in the draft white paper *Bridging the Sustainability Gap*. | [6][7] |
| **Project Mycelium** | A 2025 Hardware Standards Working Group Assembly that produced a data model for how hardware and software sustainability data relate. It led to WDPC. | [8][9] |
| **SCI** | Software Carbon Intensity. The GSF specification for measuring software carbon emissions per unit of useful work. The draft SILO specification notes that SILO data could feed SCI-style calculations, but SILO defines no score itself. | [2] |
| **Hardware Standards Working Group** | The GSF Working Group that oversees WDPC, SILO and other hardware sustainability standards. | [1][3] |
| **SILO Technical Steering Committee** | The proposed body of data centre, sustainability and software experts that would maintain SILO's canonical semantic models and approve new metric types. | [1][2] |
| **Assembly** | A time-boxed, question-driven GSF process that produces a defined output in weeks. A Working Group may then take that output through the full standards lifecycle. | [9] |

## 2. Architecture and data movement

| Term | Definition | Source |
|---|---|---|
| **Central data bus** | In WDPC, a shared data ring that all components connect to directly, allowing information to flow in both directions without hierarchical intermediaries. Often shortened to "data bus" or "WDPC data bus". | [4] |
| **Data bus** (SILO usage) | The shared telemetry exchange defined by WDPC, onto which facility, rack and component data is published. SILO consumes it but does not modify it. | [2] |
| **Message bus implementation** | The messaging software that carries the WDPC data bus. WDPC names Apache Kafka, Apache Pulsar or equivalents. | [4] |
| **Protobuf data model** | A message structure defined using Google Protocol Buffers. WDPC uses it for efficient serialisation, schema evolution and cross-platform compatibility. | [4] |
| **Schema evolution** | The ability to update a data model while staying backward and forward compatible, without disrupting services. | [4] |
| **Semantic layer** | The layer specified by SILO. It sits above the data bus and gives telemetry already on the bus common meaning, relationships and context. | [2] |
| **Normalisation** | Translating vendor- or protocol-specific telemetry into SILO's canonical semantic model. | [2] |
| **Interoperability framework** | The part of SILO that normalises telemetry from diverse protocols and vendors and validates it for schema compliance, quality and consistency. | [1][2] |
| **SILO APIs** | Standard interfaces to discover, query (real-time and historical) and stream normalised telemetry, so consuming applications don't depend on individual vendor implementations. | [1][2] |
| **Consuming application** | Software that uses normalised SILO data, such as optimisation engines, dashboards, reporting tools and grid-response systems. Out of scope for SILO. | [2] |
| **Physical and component layer** | The equipment itself and how it is instrumented. Out of scope for SILO; instrumented per vendor using existing device-class specifications. | [2] |
| **Vendor-neutral** | Not tied to any single manufacturer's formats or products, so data from any vendor can be interpreted the same way. | [1][2] |
| **Policy-driven optimisation** | In WDPC, decision-making where each component acts on predefined policies and data available on the bus, rather than central control commands. | [4] |

## 3. Semantic modelling

| Term | Definition | Source |
|---|---|---|
| **Semantic model** | A vendor-neutral data model defining the meaning, relationships and context of operational metrics, with common taxonomies, metadata and engineering units. | [1][2] |
| **Ontology** | A structured definition of the things in a domain and how they relate. The SILO page describes SILO's semantic models as a vendor-neutral ontology and metadata framework. | [1] |
| **Canonical model** | The single agreed form into which all vendor telemetry is translated. | [1][2] |
| **Taxonomy** | An agreed classification of types, such as categories of equipment or metric. | General usage, as applied in [1][2] |
| **Metadata** | Data that describes other data, such as which asset a reading belongs to, its units or its context. | General usage, as applied in [1][2] |
| **Engineering units** | Standard units of measurement attached to a value, such as kilowatts or degrees Celsius. | General usage, as applied in [1][2] |
| **Device-class schema** | An existing standard schema for a type of equipment, such as DMTF Redfish for GPUs and accelerators. SILO references these rather than redefining them. | [2] |
| **Sustainability metadata** | Information existing hardware schemas generally lack, such as expected device lifespan, embodied-carbon linkage or environmental operating context. Whether SILO should define an extension for it is an open issue. | [2] |
| **Metric** (WDPC usage) | In WDPC, a one-way message reporting the current status or historical performance of a component. | [4] |
| **Metric** (SILO usage) | A standardised operational measurement exposed through SILO, such as PUE, energy consumption or carbon emissions. New metric types go through the SILO governance process. | [1][2] |
| **Signal** | In WDPC, a two-way message conveying intent, forecasts or policy requirements that influence future behaviour, rather than reporting current state. | [4] |
| **Intent-based signal** | A WDPC signal that conveys operational intent or forecasting information rather than current measurements alone. | [4] |
| **Ticker symbol** | In WDPC, a standard identifier for a specific data stream on the bus, similar to an identifier in financial market data. | [4] |

## 4. Grid and energy

| Term | Definition | Source |
|---|---|---|
| **Grid signal** | Data about the electricity grid relevant to sustainability decisions, including availability, carbon intensity and operating constraints. | [2] |
| **Grid interface** (SILO usage) | Phase 1 of the draft SILO specification includes a two-way grid interface. It ingests grid signals and outputs facility and workload responses to grid conditions. Whether this should be one interface or two is an open issue. | [2] |
| **Ingestion** | The direction of the grid interface that receives grid signals into the facility. | [2] |
| **Control-direction output** | The direction of the grid interface that expresses how the facility or workloads respond to grid conditions. | [2] |
| **Carbon intensity** | The carbon emitted per unit of electricity at a given time and place. SILO Phase 1 includes carbon-intensity and renewable composition signals. | [2][7] |
| **Supply composition** | The mix of sources behind the power drawn at a given moment, such as low-carbon generation versus diesel backup. The draft SILO specification identifies this, not efficiency alone, as what determines sustainability. | [2] |
| **Demand response** | Changing power consumption in response to grid operator requests or market signals. | [4] |
| **Workload flexibility** | The ability of workloads to adjust power use, timing or resource allocation in response to constraints or external signals. | [4] |
| **Grid-destabilising power event** | A rapid change in power consumption that exceeds grid operator stability thresholds, typically over 50 MW in under a second. | [4] |
| **Marketplace framework** | In WDPC, the data and communication infrastructure that supports energy trading, carbon optimisation and demand response. | [4] |
| **Power quality** | Electrical characteristics of the supply, including harmonic distortion, power factor and voltage stability. | [4] |

## 5. Cooling and facility systems

| Term | Definition | Source |
|---|---|---|
| **CDU** | Coolant Distribution Unit. Equipment that circulates liquid coolant to computing hardware. CDU telemetry is deferred to a future SILO phase. | [2][5] |
| **Liquid cooling system** | A thermal management system that uses liquid coolant to move heat away from computing hardware, in single-phase or two-phase forms. | [4] |
| **BMS** | Building Management System. The facility control system that holds much of the existing data stream SILO builds on. | [2][5] |
| **Municipal heat network** | A district heating system that distributes heat to buildings. WDPC supports coordinating data centre waste heat delivery to these networks. | [3][4] |
| **Heat reuse optimisation** | Coordinating waste heat delivery to district heating or other reuse. Listed as a SILO use case, but it may need control interfaces beyond SILO's scope. | [1][2] |

## 6. Sustainability metrics

| Term | Definition | Source |
|---|---|---|
| **PUE** | Power Usage Effectiveness. The ratio of total facility power to the power delivered to IT equipment. A PUE of 1.0 means every watt goes to IT equipment. | [7] |
| **WUE** | Water Usage Effectiveness. The water counterpart to PUE, relating facility water use to IT energy. | General usage, as applied in [1][2] |
| **CUE** | Carbon Usage Effectiveness. The carbon counterpart to PUE, relating facility carbon emissions to IT energy. | General usage, as applied in [1][2] |
| **Embodied carbon** | Emissions from manufacturing and disposing of hardware, as distinct from emissions during operation. SILO is focused on operational data. | General usage, as applied in [2] |
| **Composite sustainability score** | A single combined rating for hardware or a facility. Explicitly out of scope for SILO because of unresolved methodology disputes. | [2] |

## 7. Roles and stakeholders

| Term | Definition | Source |
|---|---|---|
| **Operator** | The organisation responsible for running a data centre day to day. Distinct from the organisation that designed it. | [2] |
| **Facility operator** | The people who operate and maintain installed infrastructure day to day. | [2] |
| **Telemetry provider** | An organisation supplying the instrumentation, schemas or data feeds that populate the data bus. | [2] |
| **Electrical design engineer / EPC** | The organisation that designs power distribution infrastructure, such as transformer step-downs. EPC stands for Engineering, Procurement and Construction. | [2] |
| **OEM** | Original Equipment Manufacturer. Makers of chillers, UPS units, GPUs and accelerators, CDUs and similar equipment. | [2] |
| **BMS engineer** | An engineer who owns the building management system data stream. | [2] |
| **Grid operator** | The organisation managing the electricity grid, and the source of grid signals and constraints. | [2][4] |
| **ESG policymaker or analyst** | Someone who may classify SILO-derived data for regulatory purposes. | [2] |

## 8. Standards process and drafting

| Term | Definition | Source |
|---|---|---|
| **Normative reference** | A document whose content is required in order to apply a specification. SILO takes WDPC and DMTF Redfish as normative references. | [2] |
| **Shall / should / may / can** | ISO drafting language used in the SILO specification: shall means mandatory, should means recommended, may means permitted, and can means possible. | [2] |
| **Open issue** | A deliberately unresolved point in the draft specification, kept open for reviewer input before requirements are fixed. The current draft has four. | [2] |
| **Conformance** | Meeting a specification's requirements. For SILO, it means exposing Phase 1 telemetry through the semantic model, implementing the APIs and meeting the interoperability requirements. It does not imply any sustainability outcome. | [2] |
| **Phase 1** | The first release scope of SILO in the current draft, covering power and grid-interaction telemetry. Cooling, environmental and network domains are deferred to later phases. | [2] |
| **Standards lifecycle** | The stages a GSF standard moves through: Proposal, Pre-Draft, Draft, Consistency Review, Working Group Approval, Steering Committee Ratification and Publication. | [1] |
| **Committee Draft** | A formal draft submitted for committee review on the path towards ISO standardisation. | [2][5] |

## 9. Related standards and technologies

| Term | Definition | Source |
|---|---|---|
| **DMTF Redfish** | A management interface standard for servers and accelerators. It is the normative reference in SILO for GPU and accelerator telemetry. | [2] |
| **OCP liquid cooling / CDU schema** | A unified telemetry schema for liquid cooling and CDUs being developed by the Open Compute Project. It is the intended reference for a future SILO cooling phase. | [2] |
| **Open Compute Project Redfish Monitoring Framework** | A normative reference in WDPC for hardware monitoring. | [4] |
| **MQTT Sparkplug B** | An industrial messaging standard that WDPC uses to integrate edge, SCADA and building management systems. | [4] |
| **Apache Kafka / Apache Pulsar** | Message bus platforms named by WDPC as implementation options for the data bus. | [4] |
| **SCADA** | Supervisory control and data acquisition systems used in industrial and facility control. WDPC bridges them onto the data bus. | [4] |
| **SNIA** | Storage Networking Industry Association. Named in the SILO Q&A as a relevant existing standards body. | [5] |
| **OpenTelemetry** | An open standard for software observability telemetry. Named in the SILO Q&A as relevant to SILO. | [5] |

## 10. Regulation

| Term | Definition | Source |
|---|---|---|
| **EED** | EU Energy Efficiency Directive (2023/1791). Since September 2024, it requires data centres with 500 kW or more of IT power demand to submit annual sustainability reports. | [7] |
| **Article 12(5)** | The EED provision requiring the European Commission to assess reported data and, where appropriate, introduce minimum performance standards. | [7] |
| **CSRD** | Corporate Sustainability Reporting Directive (2022/2464). It requires large companies to publish detailed ESG disclosures. | [7] |
| **Scope 2 emissions** | Emissions from purchased electricity. | [7] |
| **Scope 3 emissions** | Indirect emissions across the value chain. The white paper highlights those attributable to IT infrastructure. | [7] |
| **ESG** | Environmental, Social and Governance. | [2] |

## Abbreviations

| Abbreviation | Meaning |
|---|---|
| API | Application programming interface |
| BMS | Building Management System |
| CDU | Coolant Distribution Unit |
| CSRD | Corporate Sustainability Reporting Directive |
| CUE | Carbon Usage Effectiveness |
| DMTF | Distributed Management Task Force |
| EED | Energy Efficiency Directive |
| EPC | Engineering, Procurement and Construction |
| ESG | Environmental, Social and Governance |
| GSF | Green Software Foundation |
| OCP | Open Compute Project |
| OEM | Original Equipment Manufacturer |
| PUE | Power Usage Effectiveness |
| SCADA | Supervisory Control and Data Acquisition |
| SCI | Software Carbon Intensity |
| SNIA | Storage Networking Industry Association |
| UPS | Uninterruptible Power Supply |
| WDPC | Workload Dynamic Power and Cooling |
| WUE | Water Usage Effectiveness |

## References

1. Green Software Foundation. *SILO: Sustainability Interoperability Layer for Operations*. https://greensoftware.foundation/standards/silo/
2. GSF Hardware Standards Working Group. *SILO draft baseline specification* (pre-standard working draft), GitHub, GSF members. https://github.com/Green-Software-Foundation/silo
3. Green Software Foundation. *WDPC: Workload Dynamic Power and Cooling*. https://greensoftware.foundation/standards/wdpc/
4. Green Software Foundation. *Workload Dynamic Power and Cooling (WDPC) Specification*, GitHub. https://github.com/Green-Software-Foundation/Workload-Dynamic-Power-and-Cooling/blob/dev/WDPC-Spec.md
5. Green Software Foundation. *SILO Project Q&A*, 3 August 2026. https://greensoftware.foundation/policy/research/silo-project-qa/
6. Green Software Foundation. *Companion Technical Note: Completing the Architecture, The Internal Interoperability Layer*, 22 July 2026. https://greensoftware.foundation/policy/research/silo-companion-technical-note/
7. GSF Hardware Standards Working Group. *Bridging the Sustainability Gap*, white paper (draft, not yet approved), GitHub. https://github.com/Green-Software-Foundation/sci-policy-and-legislation-alignment-white-paper-series/blob/main/whitepapers/Interoperability%20Layer%20for%20Real-Time%20Data%20Centre%20Sustainability%20Optimisation.md
8. Green Software Foundation. *Project Mycelium*. https://greensoftware.foundation/assemblies/project-mycelium
9. Green Software Foundation. *Assemblies*. https://greensoftware.foundation/assemblies/
