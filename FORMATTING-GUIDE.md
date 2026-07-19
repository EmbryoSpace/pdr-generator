# Formatting your SRR/SDR package for best results

PDR Generator reads real review packages, not a special template — but a few
habits change how much it can extract. This guide reflects what the extractor
actually does, and the failure modes are worth knowing because a package it
can't read looks the same as a broken import: zero requirements, empty tabs.

---

## 1. Choose the right file format

| Format | Text | **Tables** | Best for |
|---|---|---|---|
| **.pptx** | ✅ | ✅ | Review decks — the best all-round choice |
| **.xlsx / .csv** | ✅ | ✅ | Requirements lists, risk registers, budgets |
| .docx | ✅ | ❌ | Narrative documents |
| .pdf | ✅ | ❌ | Anything, but tables become flat text |
| .md / .txt | ✅ | ❌ | Notes, work packages |
| .vsdx, images, CAD | partial | — | Diagrams, product structure |

**The table column is the one that matters.** Only PowerPoint and Excel preserve
table structure. A risk register in a PDF becomes a wall of text, and risk
extraction — which needs real table columns — will find nothing.

> **If your package is PDF-only,** requirements still extract (they're found from
> ID + "shall" text), but expect no risks and no budget roll-up. Export the risk
> register and budgets separately as .xlsx and import them alongside.

**Import the source package, not a generated PDR.** If you re-import a document
this tool produced, you'll see far fewer requirements. Tell-tale signs you've
done it: text containing `confidence 85%` or `— Slide 412` citations.

---

## 2. Requirement identifiers

Give every requirement an ID with an **uppercase prefix, a dash or underscore,
and digits**. All of these work:

```
SYS-0101      PL-1        ADC-3        PHX-3.01
REQ-001       REQ-COMMS-01             SS_COMM_01
MAI-400       SR_12       AGSYS-01     L1-004
```

**Rules that matter:**

- **Put the ID immediately before the requirement text.** The extractor reads
  forward from the ID to the next ID.
- **The separator is required.** `SYS 0101` (space only) is not treated as an ID,
  deliberately — otherwise headings like "SYSTEM REQUIREMENTS 12" would be
  mistaken for requirements.
- **Requirement text needs a modal verb** — `shall`, `should`, `will`, or `must`
  — and roughly 25+ characters. Fragments are skipped.
- **Standards references are ignored on purpose:** `MIL-STD-1553`, `ISO-9001`,
  `NPR-7123`, `TRL-9`, `ECSS-…`, and unit-like prefixes never become
  requirements, so you can cite them freely.

**Good:**
```
SYS-0101   The spacecraft dry mass shall not exceed 240 kg at launch.
```
**Avoid:**
```
1.2.3      Dry mass limit (no ID prefix, no modal verb)
```

---

## 3. Risk register

Put risks in a **table** (a PowerPoint table or an Excel sheet). A header row
close to this is understood:

| Risk ID | Description | Likelihood | Impact | Impact Description | Risk Level | Mitigation Strategy | Subsystem |
|---|---|---|---|---|---|---|---|
| R-01 | Deployable hinge redesign after thermal cycling | 4 | 4 | Mass growth | High | Early qualification | Structures |

- **Risk IDs** may be numeric (`059`, `24-001`) or prefixed (`R-01`, `RISK-14`,
  `TR-003`).
- Only **Risk ID** and **Description** are essential; every other column adds
  value.
- **Subsystem** is worth filling in — it drives change-propagation analysis.

---

## 4. Allocations and margins — what powers the Decisions tab

This is the highest-leverage section. Without an allocation, the Decisions tab
has nothing to compute against.

### State caps explicitly

```
The spacecraft dry mass shall not exceed 240 kg at launch.
Orbit-average power consumption shall not exceed 320 W.
Total project cost shall not exceed 4200 kUSD.
Development shall not exceed 30 months.
```

Recognised phrasings: `shall not exceed`, `not to exceed`, `shall be less than`,
`no greater than`, `no more than`, `maximum … of`, `≤`.

Recognised units: **kg**, **W / kW**, **m/s**, **Mbps / kbps**, **GB / MB**,
**kUSD / MUSD / USD**, **months / weeks**.

> Allocations are found in requirement text **and** on budget slides, so
> "Dry Mass shall not exceed 1040 kg" on a mass-budget chart is picked up even
> if it isn't a numbered requirement.

### State margin requirements as percentages

```
The spacecraft shall maintain a dry mass margin of at least 15%.
The spacecraft shall maintain a power margin of at least 20%.
```

A margin requirement **outranks** the industry guideline: the tool measures
breach against your own limit (allocation × (1 − margin)), not the raw
allocation. If you require 15% of 240 kg, the effective cap is **204 kg**.

### Give the current estimate a system-level label

```
Mass Budget Summary. System total CBE 178 kg. MGA 12%.
```

- Use **CBE** or **current best estimate**, and **MGA / growth allowance /
  contingency**.
- **Put system-level words nearby** — *system*, *total*, *spacecraft*, *vehicle*,
  *dry mass*, *MEL*, *roll-up*, *summary*.
- Keep the CBE and its growth allowance **on the same slide/sheet**.

> **Why so fussy?** A component's "CBE 80 kg" lifted from an arbitrary slide,
> read against a 1040 kg vehicle allocation, would report a comfortable margin
> that doesn't exist. The tool rejects estimates outside 25–300% of the
> allocation and refuses to guess — it will tell you no CBE was found rather
> than invent a reassuring number.

---

## 5. TBD / TBR items

**Number them:** `TBD-07`, `TBR-02`. Unnumbered "TBD" text is ignored, because
it can't be tracked to closure.

Put the marker **inside the requirement it affects**:

```
SYS-0102  The spacecraft shall maintain a dry mass margin of at least 15%
          relative to the launch vehicle allocation (TBD-07 vehicle selection).
```

A TBD sitting inside a requirement that defines an allocation is flagged as
high-value: every margin decision beneath it is provisional until it closes.

---

## 6. Verification methods

Add a **Verification** column (or state it inline) using
**Test / Analysis / Inspection / Demonstration**. Requirements without one are
reported as V&V matrix gaps — a standard PDR entrance finding.

---

## 7. Getting the full decision layer working

Extraction alone gets you allocations and findings. Two more steps unlock the
quantified view:

1. **Link risks to what they threaten.** Open **3 · Decisions → Link risks to
   allocations**, set a probability and a min/likely/max effect. The tool will
   not invent these — a fabricated probability is worse than an honest gap.
2. **Include cost and schedule allocations** if you want a Joint Cost & Schedule
   Confidence Level (JCL). Link risks with cost/schedule consequences and the
   S-curves populate.

---

## Quick checklist

- [ ] Source package, not a previously generated PDR
- [ ] Risk register and budgets as **.pptx or .xlsx** (not PDF)
- [ ] Every requirement has an **ID with a dash/underscore** and a **shall**
- [ ] Allocations stated with a **number and a unit**
- [ ] Margin requirements stated as a **percentage**
- [ ] **CBE and MGA** on one slide, with system-level wording
- [ ] **TBD/TBR items numbered**
- [ ] Verification method per requirement
- [ ] Subsystem named on requirements and risks

---

<sub>© 2026 Embryo Space Inc. Questions: support@embryospace.com</sub>
