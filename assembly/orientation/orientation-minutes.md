# SILO Assembly Orientation
### Session Summary for Participants

> **📅 Session date:** 18 November 2026
> **🎙️ Hosted by:** Russ Trow (Operations and Education, GSF) and Jabari George (Hardware Standards, GSF), with Jamie Cowan (Membership, GSF)
> **🚀 Assembly starts:** Monday 23 November 2026

Thank you for joining the SILO Assembly orientation. Whether you attended live or are catching up, this summary covers everything you need before the Assembly begins.

---

## 📋 Contents

1. [Your Assembly Team](#-your-assembly-team)
2. [What Is SILO?](#-what-is-silo)
3. [What Is Already Set](#-what-is-already-set)
4. [What We Need Your Help With](#-what-we-need-your-help-with)
5. [Questions From the Session](#-questions-from-the-session)
6. [How the Assembly Works](#-how-the-assembly-works)
7. [Timeline](#-timeline)
8. [What Comes Out of It](#-what-comes-out-of-it)
9. [What We Ask of You](#-what-we-ask-of-you)
10. [Before Monday: Your Checklist](#-before-monday-your-checklist)
11. [Questions?](#-questions)

---

## 👥 Your Assembly Team

| Name | Role |
|:---|:---|
| **Lilach** · ZutaCore | **SILO Project Lead.** Directs the project and leads it through GSF's specification development process. |
| **Jabari George** · GSF | **Specification link.** Connects the Assembly to the specification. Your first contact for technical questions about SILO. |
| **Russ Trow** · GSF | **Assembly process.** Runs the Assembly. Your first contact for questions about how the process works. |
| **Jamie Cowan** · GSF | **Membership and partnerships.** Supports organisations, academia and nonprofits working with GSF. |

More than 30 people applied to take part, bringing expertise across data centre design, operations, sustainability and academia. You will be working alongside a genuinely broad mix of perspectives.

---

## 🧩 What Is SILO?

**SILO** stands for **Standardized Interoperability Layer for Real-Time Sustainability Optimization**. It addresses a problem many of you will know first-hand.

In a typical data centre, telemetry is locked inside each domain. Cooling systems report temperatures and pressures, power systems report their own measures, and compute, storage and network each have their own data. Each is designed to optimise its own layer. Making decisions that depend on more than one layer is very hard, because you are dealing with different vendors, different formats and different purposes for the equipment.

> 💡 **The goal:** translate telemetry from every domain into a **common semantic model** that everyone can read, agree on and use, opening up better sustainability and efficiency decisions across the whole facility.

### The four parts of SILO

| # | Component | What it does |
|:---:|:---|:---|
| 1 | **Semantic models** | Define what each metric means |
| 2 | **APIs** | Provide access to the data |
| 3 | **Interoperability framework** | Handles translation and validation |
| 4 | **Governance** | Keeps it all maintained |

### What it could unlock

- **🌡️ Adaptive cooling:** cooling decisions informed not only by cooling parameters, but by signals from other layers, such as early warning of workload changes or power quality issues.
- **⚖️ Better load orchestration:** visibility beyond power draw, including the type of power generation available and where it is used.
- **🪞 Stronger digital twins:** today's twins are limited by the type and quality of the data feeding them.
- **📊 More complete energy management and analytics:** closing blind spots that exist because the relevant data sits in another layer.
- **🔧 Predictive maintenance** and **📈 consistent PUE, WUE and related reporting** across facilities.

### Building on what already exists

SILO is not starting from scratch. It is designed to work alongside established standards and protocols, including:

`Redfish` · `OpenTelemetry` · `Open Compute Project (OCP)` · `GSF WDPC`

Over the past two years, GSF's **WDPC** work focused on getting power and cooling systems to communicate with each other, from server fans through to rack and row CDUs, fan walls, CRAC units and the cooling plant.

> 🔌 **Example:** if the power layer predicts an issue, the cooling layer could receive an advance signal and prepare, rather than running at its original setpoint right up to the event.

That work also raised practical questions, such as how to handle data arriving at very different speeds from different layers, which feed directly into this Assembly.

---

## 🔒 What Is Already Set

A few principles shape SILO and are **not up for debate** in this Assembly:

| | Principle |
|:---:|:---|
| ✅ | **Vendor neutral** |
| ✅ | **Builds on existing standards** and prior GSF work |
| ✅ | **Works alongside existing protocols** rather than replacing them |
| ✅ | **Focused on what happens inside the data centre** |
| ✅ | **Achievable by everyone**, not just large hyperscalers but also enterprise and colocation operators |

---

## 🎯 What We Need Your Help With

These are the questions the Assembly will work through.

> ⚠️ **Note:** any examples given during the orientation were illustrative only. We want **your** expertise to shape the answers.

### Topic 1 · Conformance Boundary
**What counts as SILO conformance?**
- If you make equipment or build software for facilities, what would claiming conformance mean for you?
- Is it enough for one part of a facility (for example, cooling) to conform, or must every layer conform?
- Who carries responsibility: a conformant **device**, or a conformant **facility**?

### Topic 2 · Normalisation
**Where does translation happen?**
- On the equipment side?
- Or at the operator layer, where the operator ingests and translates the data?

### Topic 3 · Metric Set and Units
**What is the minimum everyone must provide?**
- What are the core metrics in each domain, and in what units?
- How often should each be measured and delivered?
- Each choice has real implications for equipment, data transmission and complexity.

### Topic 4 · Trust and Provenance
**How do we make the data trustworthy?**
- Where should data be checked, and how?
- What is mandatory, so that sustainability figures built on SILO can be relied on?

> 🔜 A possible **fifth topic** is still being confirmed. We will let you know.

---

## 💬 Questions From the Session

<details open>
<summary><strong>How does SILO relate to OCP?</strong></summary>

SILO aims to **reuse what OCP has already produced** rather than duplicate it. For example, OCP projects define the critical measurements for equipment such as CDUs (inlet and outlet temperatures, delta T, approach temperature and so on), the units they should be in, and the protocols used.

Many people contribute to both GSF and OCP, so building on that open work makes sense. Rack-level telemetry is one part of the picture; where decisions need telemetry beyond the rack, the Assembly can identify what needs to be added.

*Jabari noted for transparency that he also leads an OCP cooling project.*

</details>

<details open>
<summary><strong>Will SILO feed back into operations, for example validating that systems behave as expected after an orchestrator acts?</strong></summary>

The current thinking is that SILO provides **observability** at the semantic layer, and operators decide how to use that information.

The risk of malfunctioning equipment feeding poor data into SILO is real. Options for handling it, such as maintenance expectations or validating data against vendor operating parameters before it reaches SILO, belong in the **Trust and Provenance** discussion.

Your views on where SILO's boundary should sit are very welcome in **Topic 1**.

</details>

---

## ⚙️ How the Assembly Works

> 📧 **There are no meetings.** Everything happens by email, in your own time, within clear deadlines.

This will probably feel different from standards work you have done elsewhere. The process is designed so that everyone's expertise counts equally, not just the loudest voices or the people who can make a particular call.

Each topic moves through three phases:

```
   DISCOVER   ──▶   DELIBERATE   ──▶   DECIDE
  Answer the       Score and         Endorse,
  questions        refine            consent
                   candidates        or object
```

### 1️⃣ Discover
You receive an email with questions on the topic. Reply with your expertise, in as much or as little detail as you like.

### 2️⃣ Deliberate
We synthesise everyone's responses into **candidates**: possible consensus positions that show where the group agrees, where views diverge, and what is still unclear.

You **rate and review** the candidates, scoring them and telling us what works and what doesn't. We refine them based on your feedback until the group converges.

### 3️⃣ Decide
Once there is clear alignment, you vote on the leading candidate:

| Vote | Meaning |
|:---|:---|
| 🟢 **Endorse** | I fully support this and would champion it publicly. |
| 🟡 **Consent** | I have reservations, but I can live with it. |
| 🔴 **Object** | I fundamentally disagree. Please tell us **why**, and **what would resolve** your objection. |

> 🙌 **Objection is welcome.** It is far easier to object in writing than to stand up in a meeting and disagree, and objections with proposed resolutions make the final output stronger.

A topic closes when there are **no unresolved objections**, and we have mechanisms in place so that this does not run indefinitely.

### 🤖 Behind the scenes
We use an AI-assisted tool to synthesise your input, but **there is always a human in the loop.** Jabari and Lilach review every candidate before it reaches you, to make sure viewpoints are fairly represented and stay relevant to the topic.

### 🍳 A quick example: the GSF canteen

In the session, we tried the process on a question everyone has a view on: *if the GSF canteen could serve only one egg dish, which should it be?*

| Step | What happened |
|:---|:---|
| **Deliberate** | Participants scored scrambled, poached and fried eggs from 1 to 10. |
| **Converge** | Scrambled scored highest and became the leading candidate. |
| **Decide** | Most endorsed or consented. A few objected. |
| **Resolve** | Objectors proposed compromises, such as serving other options on certain days. |

That is exactly the pattern we expect: **score, converge, vote, and resolve objections through compromise.**

---

## 🗓️ Timeline

| When | What |
|:---|:---|
| **Mon 23 Nov 2026** | Topic 1 (Conformance Boundary) Discover email arrives |
| **Each week** | A phase opens at the start of the week and closes at the end, when we consolidate responses and move to the next step |
| **Christmas** | A break in the schedule |
| **Around start of 2027** | Target for the Assembly report |

> 📌 **[Placeholder: insert full topic-by-topic schedule]**

---

## 📄 What Comes Out of It

The Assembly will produce a **report setting out the baseline requirements** for the SILO specification, based entirely on what the group contributes.

It is a **starting point, not a finished specification.** GSF has a track record of developing specifications quickly and taking them through to ISO, as with its previous measurement specifications.

> 🌍 You are helping to take the first steps towards a **new industry standard.**

---

## 🤝 What We Ask of You

| | Ask | Why it matters |
|:---:|:---|:---|
| ⏱️ | **Respond within the deadline** | Every email states one clearly, and timely responses keep the whole group moving. |
| 🎁 | **Share generously** | Long prose, a few lines, or a transcribed voice note are all fine. |
| 🎯 | **Be direct** | If you disagree, say so. That is what makes the final output genuinely representative. |
| 📬 | **Follow the instructions in each email** | Every message tells you exactly what to do. |

---

## ✅ Before Monday: Your Checklist

- [ ] **If you are not from a GSF member organisation:** complete the non-member participation form. We cannot add you to the Assembly without it. It is short and simply confirms our IP and contribution process. **[Link]**
- [ ] **Check your junk folder** and safelist Assembly emails from **[sending address]**.
- [ ] **Watch the recording** if you missed the session: **[Link]**
- [ ] **Look out for the Topic 1 Discover email** on **Monday 23 November**.

---

## ❓ Questions?

| Topic | Contact |
|:---|:---|
| **SILO or the specification** | Jabari George · **[email]** |
| **The Assembly process** | Russ Trow · **[email]** |

---

<p align="center"><strong>Thank you for bringing your expertise to SILO.<br>We are looking forward to working with you.</strong></p>

<p align="center"><em>Green Software Foundation</em></p>
