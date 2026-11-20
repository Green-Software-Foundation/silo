# Topic 1: Conformance Boundary

## At a glance

- **Closes:** GitHub issue #5
- **Builds on:** Nothing. This is the first Topic.

## Purpose

Anyone claiming SILO conformance needs to know what that claim commits them to, whether they make equipment, build software platforms or run a data center. Today that is unclear, because the SILO architecture names its elements but does not say which of them SILO itself defines. How much depends on where the line falls is shown by Protocol Adapters: if they are part of SILO, the specification has to define an adapter interface and say which protocols are mandatory, roughly a third of its content. Vendors need this answer before they commit engineering time.

## What this Topic must decide

**D1 What can conform to SILO?** (List)

Candidate conformance targets:

- Equipment and devices
- Vendor software and adapters
- The interoperability layer an operator runs
- A data center facility or site
- Consuming applications

**D2 Which architectural elements does SILO specify?** (Choice for each: SILO or context)

- Protocol Adapters
- Mapping and Translation
- SILO Semantic Layer
- SILO APIs

Protocol Adapters carry the most weight. If they are SILO, the specification must define an adapter interface, name the mandatory protocols and set rules for partial protocol support. If they are context, SILO starts at Mapping and Translation and the named protocols are examples only. A middle position, where SILO defines the adapter interface but makes no protocol mandatory, is also open.

Starting position: Infrastructure and Data Sources, the WDPC Data Bus, the External Interface Specification, and Applications and Consumers are context. SILO is an internal interoperability layer. It sits between infrastructure telemetry, including the WDPC Data Bus, and any external-facing interface, such as grid-signal ingestion or ESG reporting. The WDPC Data Bus is a normative reference that SILO connects with but does not define. SILO also draws on existing standards such as Redfish and OpenTelemetry for standardization and interoperability. Participants can challenge this.

**D3 What must each conformance target do?** (List per target)

The minimum obligations each target agreed in D1 must meet, against the elements agreed as SILO in D2. Each obligation is stated precisely enough that a vendor, platform builder or operator could tell whether their product meets it. For a facility or site, and for the interoperability layer an operator runs, this includes whether a conformance claim may cover some domains, such as power and cooling, and not others.

**D4 What does SILO explicitly not require?** (List)

Things implementers might assume are needed but are not, stated so vendors can rule them out.

Starting position: SILO makes operational data available, including Signals that convey intent, forecasts or policy requirements. It does not operate or control infrastructure. Acting on SILO data stays with the systems and people that consume it. Participants can challenge this.

## Agreement and difference

Candidates are generated from the Discover responses. Where the responses agree on an answer, every candidate gives that answer in the same words, so participants can see what is already shared. Candidates differ only where the responses disagree. Every disagreement the Discover synthesis records has each side taken by at least one candidate. An alternative candidate challenges the emerging agreement only on answers a minority of responses supports. Each candidate's position sentence names the answers on which it differs from the others.

A starting position stands in every candidate unless at least one response challenges it. Where few responses speak for a conformance target, candidates state its obligations only as precisely as those responses support, and the Discover synthesis records that the evidence for that target is thin.

## Terms candidates build on

Candidates use these terms as defined here, not in their everyday sense. SILO terms are taken from the SILO Conceptual Architecture (pre-draft). External interface terms are taken from the GSF Companion Technical Note, Completing the Architecture. WDPC terms are taken from the WDPC Technical Specification.

**SILO terms**

- **SILO:** a common semantic model and interoperability layer that enables consistent understanding and exchange of infrastructure operational data across vendors, systems and management domains.
- **Conformance target:** a product, platform, system or facility that makes a SILO conformance claim. D1 decides which kinds can.
- **Conformance claim:** a statement that a conformance target meets SILO's obligations. How claims are tested or certified is out of scope for this Assembly.
- **Infrastructure and Data Sources:** the compute, cooling, power, facility, network and storage systems, and their telemetry and events, that produce operational data.
- **Domain:** one of the kinds of system that Infrastructure and Data Sources covers: compute, cooling, power, facility, network and storage.
- **Protocol Adapters:** the layer that connects to infrastructure and data sources through their native protocols, such as Redfish, BACnet, Modbus, SNMP, MQTT and OpenTelemetry, and passes their data to Mapping and Translation and the SILO APIs.
- **Mapping and Translation:** maps source schemas and protocols to the SILO semantic model.
- **SILO Semantic Layer:** the Common Information Model, a common semantic model that standardizes the meaning of operational data across the data center infrastructure lifecycle.
- **SILO APIs:** standard APIs for secure access to normalized data and services.
- **Applications and Consumers:** the systems that use SILO data, such as DCIM and infrastructure management, workload orchestrators, digital twins and simulation, energy management and optimization, and analytics and AI/ML applications.
- **Context:** an element SILO connects with or refers to but does not define, and against which it sets no obligations.

**External interface terms**

- **External Interface Specification:** the layer above SILO that connects the data center to the outside world, covering grid signal ingestion, power source awareness and ESG output. It relies on SILO for unified internal data. SILO connects with it but does not define it.

**WDPC terms**

- **WDPC (Workload Dynamic Power and Cooling):** a GSF Technical Specification establishing a framework for standardized distribution of operational data between workloads, power infrastructure and cooling systems through a central data bus. It covers data standardization and high-performance distribution, not control system implementation. It does not define conformance.
- **WDPC Data Bus:** the WDPC central data bus, a distributed communication architecture where all system components connect directly to a shared data ring, enabling bidirectional information flow without hierarchical intermediaries. WDPC requires its components, including workloads, infrastructure, sensors and external systems, to connect directly to the bus.
- **Computational workload:** a software process or application that consumes computational resources and generates predictable power and thermal demands within a data center, capable of communicating directly on the data bus.
- **Protocol Buffer (protobuf) data model:** a standardized message structure defined with Google Protocol Buffers, enabling efficient serialization, schema evolution and cross-platform compatibility. WDPC exchanges all data on the bus in this form.
- **Message bus implementation:** the high-performance system that carries the data bus, such as Apache Kafka or Apache Pulsar, using protobuf serialization.
- **Metric:** a one-way protobuf message giving the current status or historical performance of a system component.
- **Signal:** a two-way protobuf message conveying intent, forecasting information or policy requirements that influence future system behavior.
- **Ticker symbol:** a standardized identifier for a specific data stream on the data bus.

## Required shape and level of detail

Candidates follow the Topic 1 candidate template: a title, a one-sentence position, a short plain-language summary of how the boundary works with one example, a decision table with fixed rows in a fixed order, trade-offs, and where the candidate came from. The table carries the agreed answer to each decision. The summary states the principle behind the boundary and does not restate the table. Word limits apply to each part so candidates stay comparable.

Candidates may name a protocol only as an example, never as a list of what SILO supports. They do not describe message formats, data fields, units, test procedures or API endpoints. Those belong to later Topics or are out of scope.

## Discover questions

**1 Which part of what you build, run or rely on would you expect to claim SILO conformance?**
*It might be equipment, vendor software, an operator's interoperability layer, a whole site or a consuming application. Name yours, or the one you depend on, and say what someone relying on the claim would assume it means. Say if any of these should not be able to claim conformance.*

**2 Where should SILO's own definition start and stop?**
*Start with Protocol Adapters: should SILO define them, define only their interface without making any protocol mandatory, or leave them to vendors? Drawing on integrations you have built or run, say who would carry the work under your answer and what it would cost them. Then name anything else you would move in or out of SILO, such as the WDPC Data Bus.*

**3 For each part that can conform, what is the least it must do for a conformance claim to mean something?**
*Describe it so you could check a real product or site against it, drawing on any claims you have checked before. For a site, say whether a claim could cover some domains, such as power and cooling, and not others.*

**4 What might someone assume SILO conformance requires that it should not?**
*Describe a time a standard, in any sector, asked for more than it needed, and what that cost.*

## Ground rules

- Vendor neutrality and "augment, don't replace" apply.
- Whatever the D2 answer on Protocol Adapters, vendors must not have to change their native protocols for their products to conform.
- SILO conformance must be achievable by enterprise and colocation operators, not only hyperscalers.
- SILO builds on existing open standards and GSF work rather than duplicating them.

## What this Topic does not cover

- **Decided in later Topics:** how data flows and what the APIs serve (Topic 2); units and the metric set (Topic 3); validation and lineage (Topic 4).
- **Out of scope for this Assembly:** test suites, certification or badging schemes.

Material a later Topic owns is deferred, not excluded. Leave it out silently. Where a response states an obligation as a specific metric, unit or sampling rate, candidates keep the obligation and defer the specifics to Topic 3.

## What later Topics rely on from this one

Later Topics can only place responsibilities on elements this Topic agrees are part of SILO. For example, unit conversion (Topic 3) and validation (Topic 4) can only sit in adapters if D2 places Protocol Adapters inside SILO.
