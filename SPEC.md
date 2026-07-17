# SILO — Standardized Interoperability Layer for Real-Time Sustainability Optimization

**Document type:** Draft baseline specification (pre-standard working draft)
**Proposed host:** Green Software Foundation (GSF), Hardware Standards Working Group,
with intended eventual submission to ISO
**Structure:** Aligned to ISO/IEC Directives, Part 2 clause conventions
**Status:** Open for community review — not yet balloted, not yet approved as a
Committee Draft

> Normative language in this document follows ISO drafting convention:
> **shall** = mandatory requirement, **should** = recommendation,
> **may** = permission, **can** = possibility/capability.
>
> Clauses marked **[OPEN ISSUE]** are unresolved working-group discussion points,
> retained deliberately so reviewers can weigh in before requirements are locked down.

---

## Foreword

This document was prepared by the GSF Hardware Standards Working Group, following a
project proposal submitted by ZutaCore and reviewed across working-group sessions
between May and July 2026. It builds on the GSF Workload-Dynamic Power and Cooling
(WDPC) specification, which this document takes as a normative reference rather than
supersedes.

This is a **baseline working draft**. It has not completed working-group balloting and
carries no formal standing with ISO or any other standards body. It is published here
to solicit structured community feedback ahead of formal Committee Draft submission.
Attention is drawn to the possibility that some elements of this document may be
subject to change as review proceeds, in particular the items listed in Annex D.

## Introduction

Efficiency and sustainability are not the same property. A data center can operate at
its best-ever Power Usage Effectiveness and still be unsustainable, because
sustainability depends on the relationship between power *demand* and power *supply
composition* — how much of the power drawn at any given moment is low-carbon versus,
for example, diesel backup — not on demand alone.

Coordinating IT workload behavior with real-time grid conditions requires that grid
signals and facility/workload telemetry be expressed in a common, interpretable form.
No such common form currently exists across vendors and domains. This document
specifies that common form: a semantic interoperability layer that normalizes
telemetry already collected under WDPC so that it can be consistently interpreted,
exchanged, and acted on — including on a sub-hourly basis — without requiring any
particular sustainability/performance tradeoff to be built into the standard itself.

---

## 1 Scope

This document specifies:

a) a vendor-neutral semantic model for normalizing operational telemetry across the
   power and grid-interaction domain (Phase 1; see 1.2);

b) application programming interfaces for discovering, querying, and streaming
   normalized telemetry;

c) an interoperability framework for translating and validating vendor- and
   protocol-specific telemetry into the semantic model; and

d) governance processes for maintaining the semantic model and evolving this
   specification.

This document does **not** specify:

- how telemetry is physically collected or transmitted onto the WDPC data bus (see
  Clause 2, WDPC);
- specific sustainability targets, KPIs, or reduction thresholds that any
  implementer shall achieve;
- a composite sustainability score for hardware or facilities;
- optimization, predictive-maintenance, or control-decision logic that consumes
  normalized data (out of scope; see 1.3).

### 1.1 Relationship to WDPC

WDPC defines how telemetry is collected and exchanged across the facility, rack, and
component domains and publishes that telemetry onto a shared data bus. This document
begins at the point where telemetry from multiple domains and multiple vendors on that
bus **shall** be interpreted consistently. This document is a standalone specification
that takes WDPC as a normative reference; it is not a revision of WDPC.

**[OPEN ISSUE]** The extent to which this document should state explicit minimum
data-availability requirements for content on the WDPC bus, versus stating assumptions
by reference to existing device-class schemas (e.g., DMTF Redfish for GPU/accelerator
management, OCP schemas for CDU/liquid-cooling telemetry), is unresolved. The current
working draft takes the reference-by-assumption approach (see 6.2).

### 1.2 Phased scope

This document specifies Phase 1 only. Phase 1 covers:

- power and grid-interaction telemetry, including renewable/carbon-intensity
  composition signals; and
- a bidirectional grid interface supporting both signal ingestion (grid availability,
  carbon intensity, constraints) and control-direction output (facility/workload
  response to grid conditions).

Cooling/thermal telemetry, environmental/physical sensing, and data-transfer/network
domain normalization are deferred to future phases and are out of scope for this
document. This phasing reflects a working-group decision that full multi-domain
coverage in a single release was not achievable; it is not a statement that other
domains are lower priority in the long term.

**[OPEN ISSUE]** Whether power/grid is the correct domain to sequence first, versus an
alternative such as cooling, is open for comment.

### 1.3 Explicit exclusions

- **Predictive maintenance and heat-reuse control** are referenced in Annex A as
  motivating use cases but require inference/analytics and control interfaces beyond
  what a semantic normalization layer provides. This document does not specify them.
- **Numeric targets or KPIs.** This document enables measurement; it shall not be
  interpreted as mandating any specific reduction outcome. Target-setting is left to
  regulatory or organizational frameworks that consume this document's normalized
  data as an input.
- **A composite hardware/facility sustainability score.** Considered and set aside by
  the working group due to unresolved methodology disputes; may be addressed by a
  future, separate specification.

## 2 Normative references

The following documents are referred to in the text in such a way that some or all of
their content constitutes requirements of this document.

- Green Software Foundation, *Workload-Dynamic Power and Cooling (WDPC) Specification*
- DMTF, *Redfish Specification* (GPU/accelerator management interface schema)
- OCP, *Unified telemetry schema for liquid cooling / Coolant Distribution Units*
  (in development at time of writing — see Annex D)

## 3 Terms and definitions

For the purposes of this document, the following terms and definitions apply.

**3.1 data bus**
shared telemetry exchange mechanism defined by WDPC onto which facility, rack, and
component-level operational data is published

**3.2 semantic layer**
the normalization and interpretation layer specified by this document, positioned
above the data bus (3.1), that establishes common meaning, relationships, and context
for telemetry already present on the bus

**3.3 normalization**
the process of translating vendor- or protocol-specific telemetry representations into
the canonical semantic model specified in Clause 6

**3.4 operator**
entity responsible for the day-to-day running of a data center facility, distinct from
an entity responsible for its electrical or mechanical design (see 3.7)

**3.5 grid signal**
data representing electricity grid state relevant to sustainability decision-making,
including availability, carbon intensity, and operating constraints

**3.6 telemetry provider**
entity supplying instrumentation, schemas, or data feeds that populate the data bus
(3.1), which this document's semantic layer consumes

**3.7 electrical design engineer / EPC**
entity responsible for the design of power distribution infrastructure (e.g.,
transformer step-downs), as distinct from an operator (3.4), who runs infrastructure
once installed

## 4 Symbols and abbreviated terms

| Abbreviation | Meaning |
|---|---|
| GSF | Green Software Foundation |
| WDPC | Workload-Dynamic Power and Cooling (specification) |
| SILO | Standardized Interoperability Layer for real-time sustainability Optimization |
| SCI | Software Carbon Intensity |
| PUE | Power Usage Effectiveness |
| WUE | Water Usage Effectiveness |
| CUE | Carbon Usage Effectiveness |
| OEM | Original Equipment Manufacturer |
| BMS | Building Management System |
| EPC | Engineering, Procurement, and Construction (firm) |
| ESG | Environmental, Social, and Governance |
| CDU | Coolant Distribution Unit |

## 5 Architecture

The architecture specified by this document consists of the following layers,
lowest to highest:

1. Physical/component layer (out of scope; instrumented per vendor and per OCP/DMTF
   device-class specifications)
2. WDPC data bus (normative reference; out of scope for modification by this document)
3. **SILO semantic/normalization layer** (this document, Clause 6)
4. **SILO APIs** (this document, Clause 7)
5. Consuming applications (out of scope — optimization engines, dashboards, reporting
   tools, grid-response systems)

The semantic layer **shall** sit above the WDPC data bus and database. It **shall
not** be positioned between the rack-sensing layer and the WDPC database, and it
**shall not** dictate how vendors instrument equipment at the source.

## 6 Semantic model requirements

### 6.1 General

The semantic model **shall** be vendor-neutral and **shall** define common
taxonomies, metadata, and engineering units sufficient to ensure consistent
interpretation of Phase 1 (power and grid-interaction) telemetry across
implementations.

### 6.2 Reference to existing schemas

Where an existing device-class schema already covers a Phase 1 telemetry type, this
document's semantic model **should** reference that schema rather than redefine
equivalent structures. At minimum:

- GPU/accelerator telemetry **should** be assumed to conform to the DMTF Redfish
  management interface schema.
- CDU/liquid-cooling telemetry (once in scope in a future phase) **should** be assumed
  to conform to the OCP unified schema referenced in Clause 2, subject to that
  schema's publication.

**[OPEN ISSUE]** Existing hardware interface schemas generally have no standard field
for sustainability-relevant metadata (e.g., expected device lifespan, embodied-carbon
linkage, environmental operating context). Whether this document should define an
extension block for such metadata, and what it should contain, is open for comment.

### 6.3 Grid interface

The semantic model **shall** support bidirectional grid signal exchange: ingestion of
grid availability/carbon-intensity/constraint signals, and expression of
control-direction signals responsive to grid conditions.

**[OPEN ISSUE]** Whether ingestion and control-direction should be modeled as a single
bidirectional interface or as two separate interfaces is unresolved.

## 7 API requirements

The specification **shall** provide standardized interfaces for:

a) discovering available normalized telemetry;
b) querying normalized telemetry, both real-time and historical; and
c) streaming normalized telemetry.

APIs **shall** decouple consuming applications from vendor-specific implementations
underneath the semantic layer.

## 8 Interoperability framework requirements

The interoperability framework **shall**:

a) normalize and translate telemetry from diverse protocols and vendor systems into
   the semantic model specified in Clause 6;
b) validate incoming telemetry for schema compliance, quality, and consistency; and
c) ensure reliable data exchange across implementations without requiring bespoke,
   per-vendor integration work by consuming applications.

## 9 Governance

Canonical semantic models **shall** be maintained by a SILO Technical Steering
Committee comprising data center, sustainability, and software domain experts. New
metric types **shall** be introduced through a formal review and approval process.
Versioning **shall** remain aligned with WDPC releases to preserve compatibility.

## 10 Conformance

An implementation conforms to this document if it:

a) exposes Phase 1 (power and grid-interaction) telemetry through the semantic model
   specified in Clause 6, including the reference schemas identified in 6.2 where
   applicable;
b) implements the API requirements of Clause 7; and
c) satisfies the interoperability framework requirements of Clause 8.

Conformance to this document does **not** imply, and **shall not** be represented as
implying, that an implementer has met any particular sustainability outcome, target,
or score. Success under this document is evaluated by the availability, consistency,
and interoperability of standardized metrics (PUE, WUE, CUE, energy/water consumption,
associated carbon emissions) — not by the values those metrics report.

---

## Annex A (informative) — Use cases

The following describe what becomes *possible* once this document's semantic layer
exists. They are not requirements of this document and are not conformance criteria.

- Adaptive cooling
- Dynamic workload placement
- Energy efficiency optimization
- Predictive maintenance *(requires capability beyond this document's scope)*
- Heat reuse optimization *(may require control interfaces beyond this document's
  scope)*
- Automated sustainability reporting

## Annex B (informative) — Stakeholders and personas

Identified by the working group as parties who should participate in further spec
development:

| Persona | Role |
|---|---|
| Data center operators | Primary implementers; balance cost and sustainability targets |
| Hardware/component OEMs & vendors | Chiller, UPS, GPU/accelerator, CDU manufacturers |
| Vendor software engineers | Management software for individual components |
| BMS engineers | Own the existing data stream much of this builds on |
| Grid operators / grid signal specialists | Grid-side signal ingestion and constraints |
| Facility operators | Day-to-day operation/maintenance of installed infrastructure |
| Electrical design engineers / EPC firms | Design power distribution and transformer infrastructure |
| Telemetry providers | May need to extend schemas to support this document |
| ESG policymakers/analysts | May classify SILO-derived data for regulatory purposes |
| Academic partners | EMPA (Switzerland), RISE (Sweden) have expressed interest |

## Annex C (informative) — Relationship to other standards and efforts

- **DMTF Redfish** — normative reference for GPU/accelerator telemetry (6.2)
- **OCP unified liquid-cooling/CDU schema** — in development; normative reference for
  a future phase (6.2)
- **Supplier Carbon Label standardization / embodied-carbon reporting** (Google,
  Schneider Electric, Microsoft) — addresses procurement-side embodied carbon,
  distinct from this document's operational focus; candidate for liaison
- **GSF Software Carbon Intensity (SCI) family**, including SCI for AI and SCI for
  Circularity — this document's normalized data could feed future SCI-style
  calculations, but this document does not itself define a score
- **GSF SCI for OpenTelemetry, Software Water Efficiency, Software Energy
  Efficiency** — adjacent GSF specifications at various stages; possible future
  integration points

## Annex D (informative) — Open issues log

Consolidated open issues from working-group discussion, for reviewer input:

1. Reference-by-assumption vs. explicit minimum data-availability requirements (1.1)
2. Whether to define a sustainability-metadata extension for existing hardware
   schemas, and its contents (6.2)
3. Whether power/grid is the correct Phase 1 domain, or another domain should be
   sequenced first (1.2)
4. Single bidirectional grid interface vs. two separate interfaces (6.3)

## Annex E (informative) — Roadmap

- [x] Project proposal drafted and reviewed (ZutaCore + GSF Hardware Standards WG)
- [x] Companion white paper (strategic) and technical document (tactical) drafted
      as distinct, connected documents
- [x] Project formally approved by working group (July 2026)
- [ ] Stakeholder/persona recruitment across GSF membership and academic partners
- [ ] This baseline circulated for working-group review
- [ ] Public review period
- [ ] GSF landing page and announcement
- [ ] Committee Draft submission
- [ ] ISO submission (following the path of other GSF specifications)

## Bibliography

[1] Green Software Foundation, *Workload-Dynamic Power and Cooling (WDPC) Specification*
[2] DMTF, *Redfish Specification*
[3] OCP, *Unified Coolant Distribution Unit / liquid cooling telemetry schema* (unpublished draft, referenced by working group members)
[4] Green Software Foundation, *Software Carbon Intensity (SCI) Specification*
