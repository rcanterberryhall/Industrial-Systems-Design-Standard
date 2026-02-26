# Safety Documentation Standard
## Integrated Industrial System Lifecycle Framework

Status: Draft
Last Updated: 2026-02-20

---

# 1. Methodology Overview

This framework defines an integrated engineering lifecycle for industrial systems that unifies:

- Functional Requirements and Constraints
- Hazard Analysis
- Safety Requirements Specification (SRS)
- Drawing-Based Design
- FMEA (Architecture and Detailed)
- Software Architecture
- FAT / SAT (Functional and Safety)
- Startup & Commissioning
- Proof Testing (for residual inherent DU only)
- Operational Governance

The methodology is built on seven core principles:

1. Hazards drive requirements.
2. Requirements drive architecture.
3. Drawings are the navigation backbone of implementation — not the origin of safety intent.
4. FMEA is a design lens, not a verification afterthought.
5. Commissioning is part of the design lifecycle.
6. Safety and function are co-requirements. A system that achieves its SIL target but fails to perform its process function is a design failure.
7. Constraints bound the design space. Regulatory, physical, interface, and operational constraints must be captured upstream — before architecture selection.

The drawing set serves as the navigation spine for implementation, testing, and maintenance, while Hazard Analysis and the SRS remain upstream and independent of the drawing structure.

This framework aligns with CD / PD / DD engineering stages and embeds formal review gates to ensure lifecycle integrity.

---

# 2. Engineering Lifecycle and Review Gates

The engineering lifecycle follows a structured progression with defined review gates:

CD → PDR  
PD → CDR  
DD → DDR  
FAT/SAT → Operational Readiness Review  
Startup → PSSR  
Operation → Proof Test Cycle (where inherent DU exists)

## 2.1 PDR – Preliminary Design Review (End of Concept Design)

Verifies:
- Functional requirements defined (process function and performance criteria)
- Design constraints identified (regulatory, physical, interface, operational, design standard)
- Hazard Analysis complete
- Safety Functions identified
- Initial SRS drafted
- High-level architecture defined
- Integrity targets (SIL or PL as applicable per safety function) assigned, with governing standard identified for each safety function

Purpose:
Confirm the concept can meet functional and safety requirements within identified constraints.

## 2.2 CDR – Critical Design Review (End of Preliminary Design)

Verifies:
- Functional requirements validated against proposed architecture
- Design constraints validated against proposed architecture
- Architecture-level FMEA complete
- Diagnostic strategy defined
- Safe states and reset philosophy defined
- Startup gate model defined
- Software architecture defined
- Architecture achieves integrity target — PFDavg < SIL target (SIL path) or achieved PL ≥ PLr (PL path)

Purpose:
Confirm the architecture can achieve functional requirements, safety targets, and integrity intent within all design constraints.

## 2.3 DDR – Detailed Design Review (End of Detail Design)

Verifies:
- Detailed drawings complete
- Detailed FMEA refinement complete
- Proof test procedures derived
- FAT/SAT procedures complete (both functional and safety)
- Functional FAT/SAT procedures derived from FR entries
- Constraint verification methods defined for all CON entries
- Deterministic gateways implemented in software

Purpose:
Confirm implementation matches functional and safety design intent.

## 2.4 Operational Readiness Review

Verifies:
- Functional FAT/SAT complete — process functions validated
- Constraint verification complete — all CON entries confirmed compliant
- Safety FAT/SAT items required for startup gates complete
- Temporary safeguards documented
- Validation levels achieved

## 2.5 PSSR – Pre-Startup Safety Review

Verifies:
- All required startup gates passed
- All safety documentation complete
- No uncontrolled bypasses active
- Proof testing defined and scheduled

---

# 2A. Dual-Standard Coexistence

A single project may contain safety functions governed by different standards. A process interlock protecting against overpressure may be governed by IEC 62061 (SIL path), while a machine guard protecting an access door may be governed by ISO 13849 (PL path). This is normal industrial practice, and the framework accommodates both pathways within a single lifecycle.

**The governing standard is declared at the HA level, per safety function.** Each HA entry carries a `Governing Standard` field (e.g., `IEC 62061`, `ISO 13849`) and an `Integrity Target` field (e.g., `SIL 2`, `PLd`). These fields flow through the SRS and FMEA wherever the verification math diverges by standard.

**The lifecycle methodology is common to both pathways.** The engineering phases (CD/PD/DD), review gates (PDR/CDR/DDR/PSSR), traceability model, FMEA philosophy, and commissioning structure do not change based on the governing standard. Only the technical integrity verification diverges:

- **SIL path** (IEC 61508 / IEC 61511 / IEC 62061): quantified in SIL level, PFDavg / PFH, HFT, Route 1H/2H
- **PL path** (ISO 13849): quantified in PLa–e, PFHd, architecture Categories (B–4), MTTFd, DCavg

The SRS contains Section 6A (SIL path calculations) and Section 6B (PL path calculations). Each SF entry in the SRS uses the section appropriate to its governing standard. FMEA entries inherit the governing standard from the SF they implement, and verification follows the corresponding pathway.

---

# 3. Normative and Informative References

This framework implements and integrates recognized international standards. It does not invent methodology — it provides a structured, integrated implementation of established practice.

The following table lists all standards referenced across the framework, organized by domain. Individual framework documents reference the subset they implement; this section provides the master list.

## 3.1 Primary Functional Safety

| Standard              | Title                                                                           | Framework Application                                                                                                        |
| --------------------- | ------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| IEC 61511 (Parts 1-3) | Functional safety — Safety instrumented systems for the process industry sector | Primary standard. This framework implements Clauses 8–17 across all documents.                                               |
| IEC 61508 (Parts 1-7) | Functional safety of E/E/PE safety-related systems                              | Parent standard. SIL framework, PFDavg calculation methods, architectural constraints, software safety requirements.         |
| IEC 62061             | Safety of machinery — Functional safety of safety-related control systems       | SIL-based functional safety for machinery applications. Used when the governing standard for a safety function is IEC 62061. |

## 3.2 Hazard Analysis and Risk Assessment

| Standard | Title | Framework Application |
|----------|-------|----------------------|
| IEC 61882 | Hazard and operability studies (HAZOP studies) — Application guide | HAZOP methodology implemented in `02_Hazard_Analysis_Standard` |
| IEC 31010 | Risk management — Risk assessment techniques | Risk assessment framework referenced in `02_Hazard_Analysis_Standard` |

## 3.3 FMEA

| Standard | Title | Framework Application |
|----------|-------|----------------------|
| IEC 60812 | Failure modes and effects analysis (FMEA and FMECA) | FMEA methodology implemented in `05_FMEA_Standard` |

## 3.4 Requirements Documentation

| Standard | Title | Framework Application |
|----------|-------|----------------------|
| ISA-5.6 | Functional Requirements Documentation for Control Software Applications | Functional requirements documentation methodology implemented in `01_Functional_Requirements_Standard` |
| ISA-84 (IEC 61511) | Safety Instrumented Systems (SIS) | Safety requirements specification methodology implemented in `03_SRS_Standard` |

## 3.5 Drawings and Documentation

| Standard | Title | Framework Application |
|----------|-------|----------------------|
| IEC 61082 | Preparation of documents used in electrotechnology | Drawing format, cross-referencing, and grid reference systems in `04_Industrial_Systems_Drawing_Standard` |
| IEC 81346 | Structuring principles and reference designations | Device designation letter codes in `04_Industrial_Systems_Drawing_Standard` |
| IEC 60445 | Basic and safety principles — Identification of equipment terminals and conductor terminations | Terminal and conductor marking in `04_Industrial_Systems_Drawing_Standard` |
| ISA-5.1 | Instrumentation Symbols and Identification | P&ID symbology and instrument identification referenced in `01_Functional_Requirements_Standard` and `04_Industrial_Systems_Drawing_Standard` |
| ISA-5.4 | Instrument Loop Diagrams | Loop diagram standards referenced in `04_Industrial_Systems_Drawing_Standard` |

## 3.6 PLC and Software

| Standard | Title | Framework Application |
|----------|-------|----------------------|
| IEC 61131-3 | Programmable controllers — Programming languages | PLC programming language standards (Ladder Diagram, Function Block Diagram, Structured Text) in `06_Industrial_Control_Software_Architecture_Standard` |
| IEC 61508-3 | Functional safety — Software requirements | Safety software lifecycle, software architectural design, and coding standards in `06_Industrial_Control_Software_Architecture_Standard` |

## 3.7 Testing and Commissioning

| Standard | Title | Framework Application |
|----------|-------|----------------------|
| IEC 62381 | Automation systems in the process industry — Factory acceptance testing (FAT), site acceptance testing (SAT), and site integration testing (SIT) | FAT/SAT methodology in `07_SAT_FAT_Standard` |
| IEC 62382 | Automation systems in the process industry — Electrical and instrumentation loop checking | Loop check methodology in `07_SAT_FAT_Standard` |
| IEC 62337 | Commissioning of electrical, instrumentation and control systems in the process industry | Structured commissioning methodology in `08_Startup_and_Commissioning_Standard` |

## 3.8 Alarm Management

| Standard | Title | Framework Application |
|----------|-------|----------------------|
| ISA-18.2 / IEC 62682 | Management of Alarm Systems for the Process Industries | Alarm rationalization and lifecycle management; referenced where alarm strategy intersects with functional requirements and FMEA |

## 3.9 Electrical Installation

| Standard | Title | Framework Application |
|----------|-------|----------------------|
| NEC (NFPA 70) | National Electrical Code | US installation requirements in `04_Industrial_Systems_Drawing_Standard` |
| UL 508A | Industrial Control Panels | Panel construction standards in `04_Industrial_Systems_Drawing_Standard` and `07_SAT_FAT_Standard` |
| IEC 61439 | Low-voltage switchgear and controlgear assemblies | Panel and enclosure standards in `07_SAT_FAT_Standard` |

## 3.10 Cybersecurity

| Standard | Title | Framework Application |
|----------|-------|----------------------|
| IEC 62443 | Industrial communication networks — Network and system security | Security considerations for networked control and safety systems |

## 3.11 Machine Safety — Performance Level (PL)

| Standard | Title | Framework Application |
|----------|-------|----------------------|
| ISO 13849-1 | Safety of machinery — Safety-related parts of control systems — Part 1: General principles for design | PL framework, architecture Categories (B–4), MTTFd, DCavg, achieved PL determination. Used in `02_Hazard_Analysis_Standard`, `03_SRS_Standard`, and `05_FMEA_Standard` for safety functions on the PL path. |
| ISO 13849-2 | Safety of machinery — Safety-related parts of control systems — Part 2: Validation | Validation methodology for PL path safety functions. |

## 3.13 IEC 61511 Clause Mapping

This framework is structured to align with IEC 61511 (Part 1) without reproducing standard text. The following mapping provides audit traceability between the methodology and recognized functional safety practice.

| Framework Phase | Framework Document | IEC 61511 Clause Reference |
|----------------|-------------------|---------------------------|
| Functional Requirements and Constraints | `01_Functional_Requirements_Standard` | §10 – Safety Requirements Specification (functional context) |
| Hazard Analysis | `02_Hazard_Analysis_Standard` | §8 – Hazard and Risk Assessment |
| Safety Requirements Specification (SRS) | `03_SRS_Standard` | §10 – Safety Requirements Specification |
| Drawing-Based Design | `04_Industrial_Systems_Drawing_Standard` | §11, §12 – SIS Design and Engineering |
| FMEA | `05_FMEA_Standard` | §11 – SIS Design (verification) |
| Software Architecture | `06_Industrial_Control_Software_Architecture_Standard` | §12 – Design and Engineering of SIS (application programming) |
| FAT / SAT | `07_SAT_FAT_Standard` | §14 – Installation, Commissioning and Validation |
| Startup & Commissioning / PSSR | `08_Startup_and_Commissioning_Standard` | §15 – SIS Safety Validation |
| Operation & Maintenance | (operational governance) | §16 – Operation and Maintenance |
| Proof Testing (where inherent DU exists) | `07_SAT_FAT_Standard` (proof test section) | §16.3 – Proof Testing |
| Modification Management | (change management sections across all documents) | §17 – Management of Change |

---

# 4. Governance Model

The following roles are required for lifecycle integrity:

- Functional Safety Lead
- Electrical Design Lead
- Controls / Software Lead
- Commissioning Lead
- Operations Representative

Formal approval is required at:

- PDR
- CDR
- DDR
- Startup Gate Authorizations
- PSSR

Governance ensures technical rigor and regulatory defensibility.

---

# 5. Document Maturity Model (CD / PD / DD)

## 5.1 Principle

Every document in this framework is a single living object that matures across design phases. There are no separate CD documents, PD documents, or DD documents. There is one Hazard Analysis. One SRS. One FMEA. One set of drawings. Each is authored at CD maturity and progressively refined to PD and then DD maturity.

This eliminates the common failure mode of parallel document sets that diverge, and the equally common failure mode of FMEA and drawings being developed independently then reconciled at the end.

Every document must serve at least one of three purposes at every phase:

- Create a design constraint
- Force a design decision
- Validate a design decision

If a document does none of these, it does not belong in the phase.

## 5.2 Maturity Summary Table

| Document | CD Maturity | PD Maturity | DD Maturity |
|----------|-------------|-------------|-------------|
| Functional Requirements | Process function and performance criteria defined; operating modes identified | Validated against proposed architecture; functional FAT/SAT scope defined | Frozen — functional FAT/SAT procedures derived from FR entries |
| Constraints | All constraint types identified and documented (regulatory, physical, interface, operational, design standard) | Validated against proposed architecture; conflicts resolved | Frozen — constraint verification methods defined; procurement verified against constraints |
| Hazard Analysis | Complete — HAZOP, SFs, SIL targets; no drawing references | Stable — referenced by SRS and FMEA; no substantive changes expected | Frozen — changes require formal MOC |
| SRS | Intent defined — functional requirement, integrity target (SIL or PL), preliminary response requirement | Architecture defined — proposed voting, preliminary PFDavg or PFHd, beta/CCF assumptions, proof test interval (SIL path) | Verified — final hardware selected, integrity target verified: final PFDavg (SIL path) or achieved PL (PL path) confirmed |
| FMEA | Concept sketch — high-level architecture risk, obvious single-point failures; no math | Architecture-level — all detectable vs. undetectable paths identified; designable DU eliminated; architecture iterated until viable | Detailed — device-specific failure rates, vendor data, MTTR, proof test coverage; no designable DU permitted |
| Drawings | Block diagrams — functional intent only; no device tags, no wiring | Architecture-level — device tags assigned, feedback loops and diagnostics provisioned, still flexible | Fully detailed — final wiring, terminal numbers, wire numbers, SF and FR references in title blocks |
| Software | Not yet present | Module structure defined, deterministic gateway rules established, object model defined | Full implementation, deterministic enforcement active, full test surfaces exposed |
| FAT / SAT | Not yet present | Outline derived from architecture; scope defined for both functional and safety testing | Final procedures derived from FR entries (functional) and FMEA detection entries, drawing sheets, and SRS requirements (safety) |

## 5.3 Concept Design (CD)

**Authority document:** `02_Hazard_Analysis_Standard`

**Purpose:** Define the problem, establish the process function, and establish the required risk reduction.

### Functional Requirements at CD — `01_Functional_Requirements_Standard`

- Process function and performance criteria defined for each system
- Operating mode requirements identified
- Preliminary availability targets established
- Interface requirements defined at a functional level

### Constraints at CD — `01_Functional_Requirements_Standard`

- Regulatory and code constraints identified (area classification, applicable standards, permits)
- Physical and environmental constraints documented (site conditions survey)
- Interface constraints identified (existing systems inventory)
- Design standard constraints collected (plant standards, vendor mandates)
- Operational constraints captured (maintenance philosophy, staffing model)

Regulatory and interface constraints must be captured before architecture selection.

### Hazard Analysis at CD — `02_Hazard_Analysis_Standard`

- HAZOP complete
- Safety functions identified with integrity targets (SIL or PL, with governing standard identified)
- `HA-XXX-NNN` entries produced
- `SF-XXX-NNN` identifiers assigned
- No drawing sheet references — implementation does not yet exist

### SRS at CD — `03_SRS_Standard`

Functional intent only. The CD-maturity SRS answers: *what must this function achieve?*

- Functional requirement stated (what the safety function must do)
- Integrity target (SIL level for SIL path, or PLr for PL path)
- Governing standard for this safety function
- Preliminary proof test interval (T_I) — SIL path only
- No hardware selection
- No detailed architecture
- No PFDavg or PFHd math beyond high-level feasibility check

### FMEA at CD — `05_FMEA_Standard`

No formal FMEA exists at CD. A concept-level sketch may flag obvious single-point failure paths that would prevent SIL achievement, but no worksheet is produced and no calculations are performed.

### Drawings at CD — `04_Industrial_Systems_Drawing_Standard`

Block diagrams only. Functional intent shown. No device tags, no sheet numbers, no wiring.

### Software at CD — `06_Industrial_Control_Software_Architecture_Standard`

Conceptual architecture only. No module structure, no implementation.

### CD Exit Gate — PDR

**Gate question:** Can this system, in principle, achieve the required risk reduction?

At PDR the team can state:

- What each system must do (functional requirements defined)
- What constraints bound the design (constraints documented)
- What hazards exist and what risk reduction is required
- What integrity target (SIL or PL) is assigned to each safety function, with governing standard identified
- What each safety function must do
- That a plausible architecture exists

If the answer to the gate question is no — redesign the concept before entering PD.

## 5.4 Preliminary Design (PD)

**Purpose:** Turn intent into architecture, and iterate until the architecture is demonstrably viable.

PD is the primary design engine. The core activity is a multi-document feedback loop:

```
Architecture  ↔  FMEA  ↔  SRS math update  ↔  Drawing update  ↔  Software structure update
```

This loop is not a linear sequence. It runs until convergence criteria are met.

### Functional Requirements at PD — `01_Functional_Requirements_Standard`

Functional requirements are validated against the proposed architecture:

- Performance criteria confirmed achievable with selected control strategy
- Interface requirements mapped to specific devices and sheets
- Availability requirements validated against proposed redundancy
- Functional FAT/SAT scope defined

### Constraints at PD — `01_Functional_Requirements_Standard`

- Proposed architecture validated against all constraints
- Equipment selections verified against environmental and regulatory constraints
- Any constraint that cannot be met triggers a design trade study or documented deviation

### SRS at PD — `03_SRS_Standard`

The SRS owns the math at PD. If the architecture does not achieve the integrity target, the SRS drives the architecture change.

- Architecture selected (e.g., 2oo3 voting for SIL path; Category 3 for PL path)
- Target T_I confirmed — SIL path only
- Preliminary PFDavg calculation (SIL path) or PFHd / achieved PL determination (PL path)
- Beta factor (CCF) assumptions — SIL path; CCF scoring per ISO 13849-1 Annex F — PL path
- Hardware fault tolerance (HFT) validation — SIL path; Category + MTTFd + DCavg determination — PL path
- Architectural constraint checks (Route 1H / Route 2H) — SIL path

### Architecture-Level FMEA at PD — `05_FMEA_Standard`

The FMEA formally exists at PD. Its purpose is not to calculate final PFDavg — it is to force architectural decisions.

At PD the FMEA must produce:

- Detection classification for every failure path (DD vs. DU)
- Identification of all **designable DU** — failures that are undetected because the architecture lacks the means to detect them, and which can be made detectable by adding feedback contacts, diagnostic outputs, or monitoring capability
- Specification of detection additions required (fed back into drawings)
- Definition of system reaction for each DD failure
- Feedback loop definitions
- Reset philosophy and safe state per safety function

**Convergence criterion for CDR:** All designable DU resolved. Remaining DU justified as inherent — a physical property of the device, not a consequence of architectural omission.

### Drawings at PD — `04_Industrial_Systems_Drawing_Standard`

- Sheet numbers assigned
- Device tags assigned
- Feedback contacts provisioned (per FMEA requirements)
- Diagnostics provisioned
- Architecture defined; wiring details still flexible

### Software Architecture at PD — `06_Industrial_Control_Software_Architecture_Standard`

- Object model defined
- Deterministic gateway rules defined
- Sheet modules mapped to drawing sheet numbers

### PD Exit Gate — CDR

**Gate question:** Does this architecture achieve the integrity target, and is the diagnostic strategy complete?

CDR exit criteria:

- **All designable DU resolved. Remaining DU justified as inherent.**
- Architecture mathematically achieves integrity target — preliminary PFDavg < SIL target (SIL path) or achieved PL ≥ PLr (PL path)
- Every DD failure mode has a defined detection mechanism and system reaction
- Reset philosophy defined
- Safe state defined for each safety function
- Software architecture defined and consistent with hardware architecture

CDR is not a hardware validation. It is an architecture validation. The team is confirming that the design *as conceived* is capable of achieving the required integrity — before committing to detailed implementation.

## 5.5 Detailed Design (DD)

**Purpose:** Lock the design. Replace architecture with implementation.

DD is refinement, not architecture. No new architectural decisions are made in DD.

### Functional Requirements at DD — `01_Functional_Requirements_Standard`

- FR entries frozen — changes require formal change management
- Functional FAT/SAT procedures derived from FR entries
- Test procedures written with specific pass/fail criteria from FR performance criteria

### Constraints at DD — `01_Functional_Requirements_Standard`

- Constraint verification methods defined for each CON entry
- Procurement specifications verified against constraint requirements
- CON entries frozen — changes require formal change management

### SRS at DD — `03_SRS_Standard`

- Final hardware selected
- Final PFDavg calculation using device-specific failure rate data (SIL path), or confirmed achieved PL from Category + MTTFd + DCavg (PL path)
- Final T_I confirmed — SIL path only
- Formal integrity demonstration — PFDavg < SIL target (SIL path) or achieved PL ≥ PLr (PL path)

### FMEA at DD — `05_FMEA_Standard`

- Device-level failure rates from vendor safety manuals
- MTTR confirmed
- Proof test coverage calculated per derived procedure
- All DU classified as inherent

**No designable DU is permitted at DD.** A DU that surfaces at DD that could have been eliminated by architectural change is a CDR failure — it must be escalated, not accepted.

Where inherent DU failure modes remain, proof test procedures are derived from the DD FMEA. Each inherent DU failure mode maps to one or more proof test steps in the PT procedure. A design with no inherent DU requires no proof testing — this is the design objective.

### Drawings at DD — `04_Industrial_Systems_Drawing_Standard`

- Final wiring complete
- Terminal numbers assigned
- Wire numbers assigned
- SF references (`SF-XXX-NNN`) in title blocks of all safety-critical sheets

### Software at DD — `06_Industrial_Control_Software_Architecture_Standard`

- Full implementation
- Sheet modules complete
- Deterministic enforcement active on all motion-producing outputs
- Full test surfaces exposed for FAT/SAT

### FAT/SAT at DD — `07_SAT_FAT_Standard`

**Safety FAT/SAT** procedures derived from:

- FMEA detection entries — each DD failure mode → fault injection test
- Drawing sheet modules — scope, device tags, wire numbers
- SRS requirements — setpoints, response times, voting behaviour, reset conditions

**Functional FAT/SAT** procedures derived from:

- FR entries — each functional requirement → performance validation test
- Implementing sheets — scope, device tags
- FR performance criteria — setpoints, tolerances, response characteristics

Fault lifecycle sequence enforced on every safety test step: establish normal → induce fault → verify reaction → confirm no reset while fault active → remove fault → verify no auto-restart → reset → verify recovery.

Procedures are complete before construction begins.

### DD Exit Gate — DDR

**Gate question:** Does the implementation match architectural intent and satisfy SRS integrity requirements?

DDR exit criteria:

- Integrity target confirmed: PFDavg < SIL target (SIL path) or achieved PL ≥ PLr (PL path), verified with device-specific data
- All DU classified as inherent — no designable DU remaining
- Proof test procedures derived for any remaining inherent DU failure modes (if none exist, no proof test is required)
- Safety FAT/SAT procedures complete and traceable to FMEA and drawings
- Functional FAT/SAT procedures complete and traceable to FR entries
- No unresolved diagnostic gaps
- Deterministic enforcement implemented in software

After DDR: construction-ready. All changes require formal MOC.

## 5.6 Commissioning Phase — `08_Startup_and_Commissioning_Standard`

The Startup and Commissioning Standard activates after DDR.

Commissioning does not change design intent. It validates execution — bottom-up, through defined Validation Levels (0–7) and Startup Gates (A–E). Both functional and safety FAT/SAT records are the primary evidence consumed by gate passage decisions.

Commissioning is the answer to: *was the design built correctly?* The design phase answered: *is the design correct?* These are distinct questions and must not be conflated.

---

# 6. Traceability Numbering and Cross-Reference Model

## 6.1 Principle

Three distinct classes of identifiers are used across this framework, each answering a different traceability question:

| Identifier Class | Examples | Question Answered |
|-----------------|---------|------------------|
| Requirement and Safety Function IDs | FR-PRES-001, SF-PRES-001, HA-PRES-001 | Why does this system exist? |
| Device Tags | PT-201A, CV-101, K-101 | Where is the device? |
| Drawing Sheet Numbers | Sheet 201, Sheet 320 | Where is the implementation documented? |

These are not interchangeable. Each serves a distinct traceability purpose.

## 6.2 Requirement IDs on Drawings — Upstream Traceability (Why)

Hazard Analysis identifiers (HA-XXX-NNN), Safety Function identifiers (SF-XXX-NNN), and Functional Requirement identifiers (FR-XXX-NNN) appear in drawing title blocks and notes to answer: *why does this system exist?*

- **FR-XXX-NNN** in a drawing title block: identifies the functional requirement this sheet implements
- **SF-XXX-NNN** in a drawing title block: identifies the safety function this sheet implements
- **HA-XXX-NNN** in notes or title blocks: links implementation to the originating hazard scenario

These references are upstream traceability. They connect implementation to intent. A reviewer reading a drawing should be able to follow the chain from the drawing sheet to the requirement or hazard that justified its design.

Drawing sheets implement requirements. Requirements do not originate in drawings — they originate in the HA, SRS, and FR documents upstream.

## 6.3 Device Tags in FMEA — Implementation Traceability (Where)

Device tags (PT-201A, CV-101, K-101) appear in FMEA entries to answer: *where would the engineer look — in the plant or in the drawing set — to find the failing component?*

FMEA entries reference the device tag rather than the sheet number because failure modes belong to devices. The same device may appear on multiple drawing sheets (loop diagram, wiring diagram, control logic, panel layout). The device tag uniquely identifies the physical component regardless of which sheet it appears on.

From a device tag, an engineer can:

- Locate the physical device in the plant using the instrument index or panel schedule
- Find all drawing sheets that reference that device
- Identify the FAT/SAT test steps that exercise that device

## 6.4 Drawing Sheet Numbers — Verification Scope (Where Implementation Lives)

Drawing sheet numbers define the scope of FMEA analysis and FAT/SAT testing.

**In FMEA:** Each FMEA entry is associated with the drawing sheet that contains the relevant control or safety logic. The sheet is the organizational unit that groups related devices, logic, and wiring into an analyzable and testable scope.

**In SAT/FAT:** Safety FAT/SAT procedures reference the sheet(s) they validate. Functional FAT/SAT procedures are numbered by sheet (`FFAT-[Sheet]`). The sheet number defines the test boundary.

The traceability chain is:

```
Why does it exist?      → FR-XXX-NNN or SF-XXX-NNN (requirement / safety function)
        │
        ▼
Where is it designed?   → Drawing Sheet Number (implementation scope)
        │
        ▼
What devices are used?  → Device Tags (PT-201A, CV-101)
        │
        ▼
What can fail?          → FMEA entry (device tag + sheet reference + failure mode)
        │
        ▼
How is it tested?       → FAT/SAT procedure (sheet reference + device tag)
```

## 6.5 Cross-Reference Summary

| Reference Appears In | Identifier Used | Traceability Purpose |
|--------------------|----------------|---------------------|
| Drawing title blocks | FR-XXX-NNN or SF-XXX-NNN | Why this sheet exists — upstream requirement |
| FMEA entries | Device tag | The physical device experiencing the failure mode |
| FMEA entries | Sheet number | The implementation scope of the FMEA entry |
| SAT/FAT procedures | Sheet number | The scope of the test |
| SAT/FAT procedures | Device tag | The specific device under test |
| SAT/FAT procedures | FR-XXX-NNN or SF-XXX-NNN | The requirement validated by the test |

---

# End Safety Documentation Standard

