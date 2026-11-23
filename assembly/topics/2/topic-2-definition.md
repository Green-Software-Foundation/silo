## Topic 2: How Data Flows and What the APIs Serve

#### At a glance

- **Closes:** GitHub issue #3
- **Runs:** in parallel with Topics 1, 3 and 4. No decision depends on another Topic's answer.

#### Purpose

This Topic decides who carries the cost of translating vendor data and what the systems using SILO actually receive. In the current architecture, the SILO APIs draw data from Protocol Adapters while promising normalized data. If consumers receive raw vendor data, they still need a separate integration for every vendor, which is the problem SILO exists to remove. WDPC also defines Signals, which convey intent, forecasts or policy, alongside Metrics, and the architecture does not yet say how Signals reach the systems that use them. This is expected to be the most contested Topic.

#### What this Topic must decide

**D1 Who is responsible for translating source data into the SILO Semantic Layer?** (Choice)

Translation includes unit conversion.

- **A.** Vendor software and adapters. They publish data already translated, in addition to their native protocol.
- **B.** The interoperability layer an operator runs. It translates data from every source.
- **C.** Shared. Vendor software and adapters translate the data they support, and the interoperability layer an operator runs translates everything else.

These answers hold whatever Topic 1 decides about Protocol Adapters and Mapping and Translation.

**D2 What may the SILO APIs serve?** (Choice)

- **A.** Normalized data only.
- **B.** Normalized data, with raw data available through a separate, clearly marked route.
- **C.** Normalized and raw data through the same route, with every value marked as raw or normalized.

**D3 How do Signals move?** (Choice)

- **A.** Through SILO in both directions, as Metrics do: the SILO APIs serve Signals and pass them on toward infrastructure.
- **B.** SILO makes Signals visible to consumers but does not pass them on; Signals reach infrastructure directly on the WDPC Data Bus.
- **C.** SILO serves Metrics only; Signals travel directly on the WDPC Data Bus, as WDPC defines.

Carrying a Signal is not acting on it. Whether SILO operates or controls infrastructure is Topic 1's decision.

Starting position: data from Infrastructure and Data Sources reaches SILO through the WDPC Data Bus. Participants can challenge this, for example where a source connects through Protocol Adapters without using the bus.

#### Terms this Topic adds

- **Translation:** converting source data, including its schema, protocol format and units, into the SILO Semantic Layer.
- **Normalized data:** data that has been translated into the SILO Semantic Layer.
- **Raw data:** data as the source reported it, before translation.

#### Required shape and level of detail

Candidates follow the Topic 2 candidate template [to be written]. They say who does what and what consumers receive. They may name a protocol only as an example. They do not describe API endpoints or methods, message formats, data fields or protocol mapping tables.

#### Discover questions

**1 Who should do the work of translating vendor data into a common form?**
*It could be the vendor, before data leaves their product, the operator, inside the interoperability layer they run, or a mix, with the operator translating whatever vendors do not. Drawing on integrations you have built or run, say who did this work, what it cost them, and what happened when the translation was poor.*

**2 What should a system that uses SILO data receive?**
*Say whether it should only ever see data in the common form, or whether there are good reasons to reach data as the source reported it, such as diagnosing a faulty sensor. If raw data is allowed, say how someone using it would tell it apart from translated data.*

**3 How should forecasts and instructions travel, as well as readings?**
*WDPC calls these Signals: messages that convey intent, forecasts or policy, such as a planned rise in workload. Say whether SILO should carry them, only show them, or leave them to the WDPC Data Bus, and what goes wrong in your experience when this kind of message reaches the wrong place or arrives late.*

#### Ground rules

- Vendor neutrality and "augment, don't replace" apply. Vendors keep their native protocols.
- Must be achievable by enterprise and colocation operators, not only hyperscalers.
- Builds on existing open standards and GSF work, including WDPC, rather than duplicating them.
- This Topic does not decide whether SILO operates or controls infrastructure.

#### What this Topic does not cover

- **Decided in other Topics:** which elements are part of SILO and what each conformance target must do (Topic 1); where units are declared and the minimum measurements (Topic 3); validation and lineage (Topic 4).
- **Out of scope for this Assembly:** API endpoint or method design, protocol-specific mapping tables, transport and security mechanisms.

Material another Topic owns is deferred, not excluded. Candidates leave it out, and the Discover synthesis records it on the deferred-items list for Topic 5.

#### How this fits with other Topics

This Topic decides responsibilities and outcomes without assuming where Topic 1 draws the boundary. Topic 5 applies them to that boundary. For example, if D1 gives translation to vendors and Topic 1 places Protocol Adapters in context, Topic 5 decides how translation done in vendor software and adapters can be required.
