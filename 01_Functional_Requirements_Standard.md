# Functional Requirements and Constraints Standard
## Process Functional Requirements and Design Constraints for Industrial Systems

**Status:** Draft
**Scope:** Definition and documentation of process functional requirements and design constraints for industrial control systems. Defines what the system must do under normal operation (requirements) and what boundaries limit design freedom (constraints).

---

## Table of Contents

1. [Purpose and Scope](#1-purpose-and-scop)
    
2. [Standards References](#2-standards-references)
    
3. [Relationship to Other Documents](#3-relationship-to-other-documents)
    
4. [Requirements and Constraints — Definitions](#4-requirements-and-constraints--definitions)
    
5. [Numbering and Identification](#5-numbering-and-identification)
    
6. [Functional Requirement Entry Format](#6-functional-requirement-entry-format)
    
7. [Constraint Entry Format](#7-constraint-entry-format)

8. [CD / PD / DD Maturity](#9-cd--pd--dd-maturity)
9. [Change Management](#10-change-management)

---

## 1. Purpose and Scope

### 1.1 Purpose

This standard defines the methodology for documenting **process functional requirements** and **design constraints** for industrial systems.

**Functional requirements (FR)** define the system’s intended behavior under normal and defined non-hazard operating modes — i.e., what the system must do to achieve its process objectives. FR entries include performance criteria, operating modes, and acceptance criteria used for functional verification.

The **Functional Requirements Specification (FRS)** is the project-level authority document that contains and governs those `FR-XXX-NNN` entries.

**Constraints (CON)** define non-negotiable boundaries that limit design freedom — regulatory, physical, interface, environmental, operational, and design-standard limits that must be satisfied regardless of the functional approach selected.

This standard is complementary to the **Safety Requirements Specification (SRS)**:

- The **FRS** defines intended process behavior and performance expectations.
    
- The **SRS** defines required protective behavior and integrity targets to reduce risk to tolerable levels.
    

Functional requirements and safety requirements are co-equal drivers of design. A system that meets its SIL/PL target but fails its process function is a design failure. A system that performs its process function but violates constraints is also a design failure. Safety, function, and constraints must be satisfied together.
### 1.2 Scope

This standard applies to:

- Process functional requirements for industrial control systems (FRS)
    
- Design constraints that bound the implementation space (CON)
    
- P&ID references and process design basis supporting each functional requirement
    
- Theory of operations (operating narratives, sequence descriptions, control philosophy)
    
- Performance criteria (setpoints, tolerances, ranges, response characteristics)
    
- Operating mode definitions (normal, startup, shutdown, degraded, maintenance/bypass where applicable)
    
- Availability, uptime, and recovery requirements
    
- Interface requirements between systems (functional-level interface intent; detailed interfaces governed by ICDs)
    
- Regulatory, physical, interface, environmental, operational, and design-standard constraints
    
- Traceability from functional requirements and constraints to architecture, implementation artifacts, and verification evidence (via the RTM)
    

This standard does **not** define:

- Safety requirements — see the SRS Standard (`03_SRS_Standard`)
    
- Hazard analysis methodology — see the Hazard Analysis Standard (`02_Hazard_Analysis_Standard`)
    
- Interface Control Document (ICD) structure and governance — see the ICD Standard (if separate) or `09_Interface_Control_Document_Standard` (as applicable)
    
- Drawing conventions — see the Industrial Systems Drawing Standard (`04_Industrial_Systems_Drawing_Standard`)
    
- FMEA methodology — see the FMEA Standard (`05_FMEA_Standard`)
    
- FAT/SAT procedure authoring and execution — see the SAT/FAT Standard (`07_SAT_FAT_Standard`)
    
- Commissioning governance and startup gate model — see the Startup & Commissioning Standard (`08_Startup_and_Commissioning_Standard`)

### 1.3 Design Philosophy

**Functional requirements are a foundational exercise.**  
Without a clear definition of what the system must do, every downstream activity — hazard analysis, SRS development, architecture, FMEA, drawings, software, FAT/SAT — lacks its anchor.

The FRS defines intended behavior. All design and verification activities trace back to it.

---

**Constraints bound the design space.**  
Before selecting architecture, the design team must understand all applicable boundaries — regulatory, physical, interface, environmental, operational, and design-standard limits.

Constraints are not goals to be optimized; they are boundaries to be respected.

A constraint discovered late in the lifecycle creates rework:

- Discovered during detailed design → architectural rework
    
- Discovered after procurement → change order and schedule impact
    
- Discovered during commissioning → operational delay and potential safety risk
    

Capturing constraints at CD prevents downstream instability.

---

**Theory of Operations is a design input, not documentation afterthought.**  
Functional requirements are derived from the process design. The Theory of Operations describes how the system is intended to behave across modes and conditions.

This standard formalizes the translation of narrative process intent into structured, testable, and traceable FRS entries.

A Theory of Operations without traceable FRS identifiers is an unverifiable narrative.

---

**FRS is distinct from SRS.**  
Functional requirements do not carry SIL targets, PFDavg calculations, proof test intervals, or safety integrity verification math. They define process intent and performance expectations.

Where a functional requirement introduces a safety concern:

1. Hazard Analysis identifies the hazard.
    
2. The SRS defines the required protective function and integrity target or performance level required.
    
3. Architecture implements both.
    

The FRS may include availability, reliability, recovery time, and uptime requirements — but these are operational performance expectations, not safety integrity allocations.

---

**One document per project.**  
Like the Hazard Analysis and the SRS, the FRS and Constraints Register are single, living, project-level documents.

- One entry per functional requirement (`FR-XXX-NNN`)
    
- One entry per constraint (`CON-XXX-NNN`)
    

These entries mature from CD to PD to DD under the Document Maturity Model. Parallel versions are prohibited. Divergent document sets are governance failures.

---

## 2. Standards References

| Standard | Title | Application |
|----------|-------|-------------|
| ISA-5.6 | Functional Requirements Documentation for Control Software Applications | Methodology for documenting control software functional requirements |
| IEC 61511-1 | Functional safety — Safety instrumented systems for the process industry | Clause 10 — requirements specification lifecycle; relationship between functional and safety requirements |
| ISA-5.1 | Instrumentation Symbols and Identification | P&ID symbology and instrument identification referenced in source documents |

This standard implements the functional requirements documentation practices described in ISA-5.6 within the IEC 61511 safety lifecycle framework. Functional requirements provide the process context for Clause 10 safety requirements specified in the SRS.

For the complete list of standards referenced across this framework, see the Safety Documentation Standard (`00_Safety_Documentation_Standard`), Section 3.

---

# 3. Relationship to Other Documents

## 3.1 Document Flow

P&IDs + Theory of Operations + Plant Standards + Regulatory Codes  
     │  
     ▼  
Functional Requirements (FR-XXX-NNN) + Constraints (CON-XXX-NNN)  
     │  
     ├──► Hazard Analysis — examines deviations from defined process intent  
     │         │  
     │         ▼  
     │    SRS (SF-XXX-NNN) — defines protective functions to reduce risk  
     │  
     ├──► Drawings — implement requirements within constraint boundaries  
     │  
     ├──► Functional FAT/SAT — validates process performance as specified  
     │  
     ├──► Constraint Verification — confirms compliance with all defined boundaries  
     │  
     └──► Commissioning — functional and constraint validation are gate requirements

Functional requirements define intended behavior.  
Hazard analysis examines deviations from that intent.  
The SRS defines protective behavior where risk reduction is required.  
Architecture and implementation must satisfy all three.

---

## 3.2 Relationship to P&IDs and Theory of Operations

**P&IDs** define the physical process — equipment, piping, instrumentation, and control elements. They are produced by the process discipline and are primary inputs to this document. Each functional requirement shall reference the P&ID(s) that define the process it governs.

**Theory of Operations** (operating narrative, control philosophy, sequence description) describes how the process is intended to behave across modes and transitions. This includes startup sequences, normal operating regimes, shutdown procedures, and degraded-mode operation.

This standard translates process intent into structured, testable, and traceable FRS entries.

The Theory of Operations may be:

- Embedded directly within FR entries (operating modes, functional description), or
    
- Maintained as a standalone narrative referenced by FR identifiers.
    

P&IDs and Theory of Operations are not produced by this standard — they are consumed by it.

---

## 3.3 Relationship to Hazard Analysis (`02_Hazard_Analysis_Standard`)

Hazard analysis evaluates deviations from defined design intent.

Design intent is defined by the Functional Requirements Specification. Each HAZOP node’s “Design Intent” statement should trace to one or more FR entries. Where applicable, constraints (particularly regulatory, environmental, or interface constraints) may also inform hazard identification.

Functional requirements do not define hazards; they define intended operation. Hazard analysis evaluates what can go wrong relative to that intent.

---

## 3.4 Relationship to SRS (`03_SRS_Standard`)

Each safety function (`SF-XXX-NNN`) in the SRS defines protective behavior required to reduce risk to tolerable levels.

Functional requirements do not replace safety requirements — they provide the process context that makes safety requirements meaningful.

The relationship between FRs and safety functions is not 1:1:

- Some hazards arise directly from deviation of a defined process function — these trace clearly to a specific `FR-XXX-NNN`.
    
- Other hazards arise from equipment failure modes, external events, or environmental conditions not tied to a specific functional behavior.
    

Where a clear process-function linkage exists, the SRS entry shall reference the corresponding FR identifier. Where no direct linkage exists, the SRS entry stands independently, grounded in hazard analysis.

Architecture implements both functional requirements (FRS) and protective requirements (SRS) without redefining either.

---

## 3.5 Relationship to Drawings (`04_Industrial_Systems_Drawing_Standard`)

Drawings implement both functional and safety requirements within defined constraint boundaries.

Drawing title blocks shall reference the governing identifiers:

- `FR-XXX-NNN` for functional implementation
    
- `SF-XXX-NNN` for safety implementation
    
- `HA-XXX-NNN` where hazard-origin traceability is required
    

A drawing sheet implementing functional behavior shall trace to at least one FR entry via the RTM.

---

## 3.6 Relationship to FAT/SAT (`07_SAT_FAT_Standard`)

Functional FAT/SAT validates that the system performs its intended process function as defined in the FRS.

Safety FAT/SAT validates that safety functions perform as defined in the SRS.

These are distinct validation activities:

- Functional FAT/SAT → performance verification
    
- Safety FAT/SAT → risk reduction verification
    

Both are required for commissioning authorization.

Functional FAT/SAT procedures are derived from FRS entries, including performance criteria, operating modes, and interface requirements.

---

## 3.7 Relationship to Commissioning (`08_Startup_and_Commissioning_Standard`)

Commissioning consumes evidence generated by:

- Functional FAT/SAT
    
- Safety FAT/SAT
    
- Constraint verification activities
    

Functional validation and constraint compliance are required conditions for startup gate passage.

A system that passes safety validation but:

- Fails functional validation, or
    
- Violates a defined constraint
    

is not ready for operational authorization.

Safety integrity alone does not constitute readiness for operation.

---
## 3.8 Theory of Operations Traceability Model

### 3.8.1 Purpose

The Theory of Operations (THEOP) defines process intent. The Functional Requirements Specification (FRS) formalizes that intent into structured, testable, and traceable requirements.

To ensure stable, auditable traceability between narrative process intent and formal requirements, this standard establishes a structured section identifier model for the Theory of Operations.

Traceability shall be based on stable section identifiers — not paragraph numbers or line numbers.

---

### 3.8.2 Theory of Operations Section Identifiers

Theory of Operations documents shall be organized using stable identifiers in the format:

THEOP-XXX

Where:

- `XXX` is a three-digit numeric identifier.
    
- Identifiers remain stable across document revisions.
    
- Section renumbering due to formatting or pagination changes is prohibited.
    

Example structure:

THEOP-001  Process Overview  
THEOP-002  Startup Sequence  
THEOP-003  Normal Operation  
THEOP-004  Shutdown Sequence  
THEOP-005  Degraded Mode Operation  
THEOP-006  Inter-System Coordination

Subsections may use hierarchical extensions:

THEOP-002-A  
THEOP-002-B

These identifiers are governance anchors and shall not change unless the underlying operational intent changes materially.

---

### 3.8.3 FRS Source of Intent Field

Each Functional Requirement (`FR-XXX-NNN`) shall include a **Source of Intent** field referencing:

- One or more `THEOP-XXX` identifiers, and
    
- One or more P&ID identifiers, where applicable.
    

Example:

FR-PRES-001  
  
Source of Intent:  
    THEOP-002  
    P&ID-301

This ensures:

- Every FR entry has documented process-basis justification.
    
- The narrative intent is formally linked to structured requirements.
    
- Bidirectional traceability can be enforced through the RTM.
    

---

### 3.8.4 Prohibited Traceability Methods

Traceability based on paragraph numbers, page numbers, or line numbers is prohibited.

Such references are unstable under revision and undermine lifecycle governance.

Only stable identifiers (e.g., `THEOP-XXX`, `FR-XXX-NNN`, `P&ID-###`) shall be used for cross-document traceability.

---

### 3.8.5 Relationship to RTM

The Requirements Traceability Matrix (RTM) may include linkage between:

- `FR-XXX-NNN` → `THEOP-XXX`, where applicable.
    

The foundational objective of the FRS phase is engineering alignment:

- The engineering team and stakeholders agree on what the system must do.
    
- Acceptance criteria for each requirement are defined.
    
- The verification method for each requirement is identified.
    

Traceability supports this alignment but does not replace it.


# 4. Requirements and Constraints — Definitions

## 4.1 Functional Requirement (FR)

A Functional Requirement is a statement of what the system must _do_ — a process function it must perform.

Functional requirements are:

- **Objective** — the required behavior is clearly defined.
    
- **Performance-bounded** — quantitative criteria define how well the function must be performed.
    
- **Traceable** — each requirement traces upstream to process intent and downstream to implementation and verification artifacts.
    
- **Implementation-independent** — they describe _what_ the system must achieve, not _how_ it is implemented.
    
- **Verifiable** — a defined verification method exists.
    

Functional requirements answer:

> What must this system do, and how well must it do it?

Verification of a functional requirement may be achieved through:

- Functional testing (FAT/SAT/commissioning)
    
- Analysis or engineering calculation
    
- Inspection
    
- Demonstration
    
- Documentation review
    

The required verification method shall be identified within each FR entry.

A functional requirement without a defined verification method is incomplete.
---

## 4.2 Performance Criteria

Performance criteria define quantitative bounds on how well a functional requirement must be performed.

These may include:

- Setpoints and allowable tolerances
    
- Response times and ramp rates
    
- Accuracy and stability
    
- Control bandwidth or deadband
    
- Availability or recovery targets
    

Performance criteria are captured within FR entries as required fields. They are not separate requirements unless they define independent functional behavior.

Performance criteria form the basis of Functional FAT/SAT validation.

---

## 4.3 Constraint (CON)

A Constraint is a boundary condition that limits design freedom.

Constraints are not functions the system performs. They are imposed limits that the design must respect.

Constraints shall be stated quantitatively wherever possible to enable objective compliance determination.

Constraints originate from sources external to the control system implementation:

|Constraint Type|Source|Examples|
|---|---|---|
|**Regulatory / Code**|Laws, codes, standards, permits, AHJ requirements|IEC 61511, NEC Article 500, Class I Div 2 area classification, environmental permits, OSHA PSM|
|**Physical / Environmental**|Site conditions and physical realities|Ambient temperature range, humidity, elevation, corrosive atmosphere, seismic zone, available space, noise limits|
|**Interface**|Existing infrastructure that cannot be changed|Existing DCS platform, network architecture, power distribution, communication protocols, field bus standards|
|**Operational**|How the facility is operated and maintained|Maintenance access requirements, operator skill levels, spare parts strategy, turnaround schedule, staffing model|
|**Design Standard**|Owner/operator or EPC mandated practices|PLC platform, HMI standard, wiring practices, panel fabrication standards, vendor preferences, naming conventions|

Constraints are documented as individual entries (`CON-XXX-NNN`) within the Constraints Register.

---

## 4.4 Verification and Traceability

Requirements define what the system must _achieve_.  
Constraints define what the system must _comply with_.

Both Functional Requirements (`FR-XXX-NNN`) and Constraints (`CON-XXX-NNN`) shall include a defined **Verification Method**.

Verification methods may include:

- Test (execution-based validation)
    
- Analysis (calculation, modeling, engineering evaluation)
    
- Inspection (physical or documentation inspection)
    
- Demonstration (observed behavior without full quantitative test)
    
- Certification or compliance confirmation
    

The Requirements Traceability Matrix (RTM) shall document:

- Requirement / Constraint identifier
    
- Implementing artifact (drawing, software module, calculation, etc.)
    
- Verification method
    
- Verification evidence reference
    

Traceability ensures that:

- No requirement or constraint exists without defined verification.
    
- No implemented element exists without a governing requirement or constraint.
    

Verification method is determined by the nature of the requirement — not by phase. SAT is one verification mechanism among several.

---

## 4.5 The Distinction

- **Requirements are optimized.** The design should meet performance criteria as effectively and robustly as practical.
    
- **Constraints are satisfied.** A design either complies with a constraint or it does not.
    

There is no partial compliance with a constraint.

If a constraint conflicts with a requirement, the conflict shall be resolved explicitly through documented trade study and stakeholder approval. Silent degradation of performance or implicit violation of constraints is prohibited.
# 5. Numbering and Identification

## 5.1 Document ID

**Format:** `FRS-[ProjectCode]`

The Functional Requirements Specification (FRS) is a single, project-level document.

Its identifier shall use the project code.

**Examples:**

- `FRS-RefineryXYZ`
    
- `FRS-TerminalExpansion01`
    

The document identifier remains constant across revisions. Revisions do not alter the document ID.

The FRS is the functional counterpart to the Safety Requirements Specification (SRS). Both are project-level authority documents.

---

## 5.2 Functional Requirement Entry ID

**Format:** `FR-XXX-NNN`

|Component|Description|Example|
|---|---|---|
|`FR`|Functional Requirement prefix|FR|
|`XXX`|System abbreviation code (same codes as HA and SRS)|PRES|
|`NNN`|Sequential requirement number within that system|001|

**Examples:**

- `FR-PRES-001` — Pressure system, first requirement
    
- `FR-TEMP-002` — Temperature system, second requirement
    
- `FR-FLOW-001` — Flow system, first requirement
    

Functional Requirement IDs:

- Shall be unique within the project.
    
- Shall not be reused.
    
- Shall not be renumbered after issuance.
    
- May be retired but not reassigned.
    

Identifier stability is required to preserve lifecycle traceability.

---

## 5.3 Constraint Entry ID

**Format:** `CON-XXX-NNN`

|Component|Description|Example|
|---|---|---|
|`CON`|Constraint prefix|CON|
|`XXX`|System abbreviation code, or `GEN` for project-wide constraints|PRES, GEN|
|`NNN`|Sequential constraint number within that system|001|

**Examples:**

- `CON-PRES-001` — Pressure system constraint
    
- `CON-GEN-001` — Project-wide constraint (e.g., mandated PLC platform)
    
- `CON-GEN-002` — Project-wide constraint (e.g., ambient temperature rating)
    

Use `GEN` for constraints that apply across multiple systems or the entire project.  
Use a system code when the constraint applies only to a specific system.

Constraint IDs follow the same immutability rules as FR identifiers.

---

## 5.4 System Abbreviation Codes

System abbreviation codes shall match those defined in the Hazard Analysis Standard (Section 4.3).

These codes shall be used consistently across:

- Hazard Analysis (`HA-XXX-NNN`)
    
- Safety Requirements (`SF-XXX-NNN`)
    
- Functional Requirements (`FR-XXX-NNN`)
    
- Constraints (`CON-XXX-NNN`)
    

Alignment of system codes across lifecycle documents is mandatory to maintain RTM integrity.

---

# 6. Functional Requirement Entry Format

## 6.1 Required Fields per Entry

Each `FR-XXX-NNN` entry within the FRS shall contain the following fields:

|Section|Content Required|
|---|---|
|**Header**|FR ID (`FR-XXX-NNN`), system/subsystem name, revision|
|**Source Documents**|P&ID reference(s); Theory of Operations reference (or inline narrative)|
|**Process Function Description**|Clear, testable statement of intended system behavior|
|**Performance Criteria**|Quantitative bounds: setpoints, tolerances, ranges, response characteristics, accuracy|
|**Operating Modes**|Behavior definition for each applicable mode|
|**Availability Requirements**|Uptime targets, maximum allowable downtime, redundancy expectations (if applicable)|
|**Interface Requirements**|Inputs (sensors, signals, other systems); outputs (actuators, signals, other systems)|
|**Applicable Constraints**|`CON-XXX-NNN` entries governing implementation|
|**Implementing Artifacts**|Drawing sheet numbers, software modules, or calculations implementing this requirement|
|**Verification Method**|Defined method by which the requirement will be verified|
|**Verification Evidence**|Reference to test record, analysis document, inspection record, or validation artifact|

The Verification Method field shall identify one of the following (as applicable):

- Test (FAT, SAT, commissioning execution)
    
- Analysis (engineering calculation, modeling)
    
- Inspection (physical or documentation review)
    
- Demonstration
    
- Certification or compliance confirmation
    

A functional requirement without a defined verification method is incomplete.

---

## 6.2 Source Documents

Each FR entry shall reference the process documentation from which it is derived.

### P&ID References

The P&ID sheet(s) and revision(s) defining the physical process controlled by this requirement.

The P&ID defines:

- Equipment
    
- Instrumentation
    
- Control elements
    
- Process interconnections
    

Format:

P&ID-301 Rev 3

---

### Theory of Operations

The Theory of Operations describes how the process is intended to behave across operating modes.

This may be:

- **Inline** — captured directly within the FR entry (preferred for simple systems).
    
- **Referenced** — a standalone document (control philosophy, operating narrative, sequence description), referenced by document number and revision (preferred for complex or multi-step systems).
    

The Theory of Operations answers:

> How does the operator expect this system to behave?

The FR entry translates that expectation into structured, measurable, and verifiable criteria.

---

## 6.3 Process Function Description

The Process Function Description shall be:

- **Objective** — clearly describes required behavior
    
- **Testable** — allows objective determination of compliance
    
- **Specific** — defines measurable criteria
    
- **Complete** — covers all applicable operating modes
    
- **Implementation-independent** — describes _what_, not _how_
    

**Good example:**  
“Maintain vessel pressure between 80 and 120 psig during normal operation.”

**Poor example:**  
“Control pressure.”  
(Not measurable, not bounded, not verifiable.)

Implementation details (e.g., PID loop type, valve model, PLC function block selection) shall not appear in this section.

---

## 6.4 Performance Criteria

Performance criteria define how well the function must be performed.

|Criterion|Description|Example|
|---|---|---|
|Setpoint|Target operating value|100 psig|
|Control range|Acceptable operating band|80–120 psig|
|Accuracy|Maximum steady-state deviation|±2 psig|
|Response time|Maximum time to reach setpoint from defined disturbance|< 30 seconds for 10% step change|
|Overshoot|Maximum transient excursion beyond setpoint|< 5 psig|
|Stability|Allowable steady-state oscillation|< 1 psig peak-to-peak|

Performance criteria form the basis for verification and shall be stated quantitatively wherever possible.

---

## 6.5 Operating Modes

Each FR entry shall define behavior for applicable operating modes.

|Mode|Definition|
|---|---|
|**Normal**|Steady-state operation within design parameters|
|**Startup**|Transition from idle/cold state to normal operation|
|**Shutdown**|Controlled transition from normal to idle/cold state|
|**Degraded**|Operation with reduced capability (e.g., single sensor, backup equipment)|
|**Emergency**|Defined functional response prior to safety system takeover (if applicable)|

Operating modes shall be defined per project and may include additional states where required (e.g., maintenance, manual override, bypass).

Operating mode definitions shall align with the Operational State Model defined during Preliminary Design.

---
# 6.6 Verification Method Definition Rules

Each Functional Requirement (`FR-XXX-NNN`) shall include a defined **Verification Method** and **Verification Evidence Reference**.

Verification shall be appropriate to the nature of the requirement. The method selected shall be capable of objectively determining compliance with the defined performance criteria.

## 6.6.1 Acceptable Verification Methods

The following verification methods are permitted:

|Method|Description|Typical Use Case|
|---|---|---|
|**Test**|Execution-based validation under controlled conditions (FAT, SAT, commissioning)|Control loops, sequencing, dynamic behavior|
|**Analysis**|Engineering calculation, modeling, or documented technical evaluation|Capacity limits, heat load, control stability analysis|
|**Inspection**|Physical or documentation review|Wiring compliance, equipment spacing, nameplate verification|
|**Demonstration**|Observed behavior without full quantitative instrumentation|HMI workflow, alarm annunciation behavior|
|**Certification / Compliance Review**|Confirmation of vendor documentation or third-party certification|UL listing, environmental rating|

The selected verification method shall be documented within the FR entry.

---

## 6.6.2 Verification Planning

The Verification Method field shall:

- Identify the planned verification phase (Design Review, FAT, SAT, Commissioning, etc.)
    
- Reference the applicable procedure or calculation document
    
- Define objective acceptance criteria
    

Verification planning shall occur during Preliminary Design and be finalized during Detailed Design.

A functional requirement without a defined verification method and acceptance criteria is incomplete and shall not pass design review.

---

## 6.6.3 Traceability to RTM

The Requirements Traceability Matrix (RTM) shall include:

- FR identifier
    
- Implementing artifact(s)
    
- Verification method
    
- Verification evidence reference
    

Traceability ensures:

- Every requirement has a defined method of validation.
    
- Verification evidence is preserved for lifecycle governance.
    
- No implemented functionality exists without a governing requirement.
    

Verification method is determined by the nature of the requirement — not by phase alone.

---
### 6.7 Worked Example - Functional Requirement

```
FR-PRES-001: Vessel XYZ Pressure Control
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Header:
  FR ID:        FR-PRES-001
  System:       Pressure Control — Refinery Vessel XYZ
  Revision:     A

Source Documents:
  P&IDs:        P&ID-201 Rev D (Vessel XYZ and pressure control loop)
                P&ID-101 Rev C (Unit A feed system — upstream context)
  Theory of Ops: Control Philosophy Doc CP-RefineryXYZ Rev B, Section 3.2
                 (Vessel XYZ pressure control narrative)

Process Function Description:
  Maintain vessel pressure between 80 and 120 psig during normal operation
  by modulating outlet control valve CV-101. Vessel receives hydrocarbon
  feed from Unit A at variable rate (200–500 GPM) and discharges to Unit B.
  The pressure control function ensures stable downstream supply pressure
  and prevents process upsets that would trigger safety system activation.

Performance Criteria:
  - Setpoint: 100 psig (operator-adjustable, range 80–120 psig)
  - Control range: 80–120 psig under all normal feed rates
  - Accuracy: +/- 2 psig at steady state
  - Response time: < 30 seconds to recover from 10% feed rate step change
  - Overshoot: < 5 psig on step disturbance
  - Stability: < 1 psig peak-to-peak oscillation at steady state

Operating Modes:
  Normal:   PID control of outlet valve CV-101 to maintain setpoint
  Startup:  Ramp pressure from atmospheric to setpoint over 15 minutes
            using controlled inlet valve opening sequence
  Shutdown: Controlled depressurization to atmospheric over 30 minutes
  Degraded: If pressure transmitter PT-201A fails, switch to PT-201B
            (backup) with alarm. Manual control if both fail.

Availability Requirements:
  - Minimum 99.5% uptime (< 44 hours unplanned downtime per year)
  - Maximum single-event downtime: 4 hours
  - Backup pressure indication available for manual control

Interface Requirements:
  Inputs:
    - Pressure transmitter PT-201A (primary) — 4-20mA
    - Pressure transmitter PT-201B (backup) — 4-20mA
    - Feed flow rate FT-101 — for feedforward compensation
  Outputs:
    - Outlet control valve CV-101 — 4-20mA positioning signal
    - Pressure indication to BPCS HMI
    - High/low pressure process alarms (PAH at 130 psig, PAL at 70 psig)

Applicable Constraints: CON-PRES-001, CON-GEN-001, CON-GEN-002

Implementing Sheets: 150, 320
Functional FAT/SAT Reference: FFAT-150

Related Safety Function:
  SF-PRES-001 (SIL 3) protects people and equipment from overpressure
  when this control function fails. The safety function activates at
  170 psig — well above the functional control range.
  See SRS entry SF-PRES-001.
```

**Relationship to safety:** FR-PRES-001 defines the process function. When this function fails (pressure exceeds control range), the hazard analysis (HA-PRES-001) identifies the overpressure risk to people and equipment. The SRS entry SF-PRES-001 specifies the safety function that protects people and equipment from the consequences of that hazard. The functional requirement defines the context — the safety function defines the protection.

---
## 7. Constraint Entry Format

### 7.1 Required Fields per Entry

Each CON-XXX-NNN entry within the document shall contain:

| Section | Content Required |
|---------|-----------------|
| **Header** | CON ID (CON-XXX-NNN), constraint type (Regulatory, Physical, Interface, Operational, Design Standard), revision |
| **Source** | Regulatory citation, plant standard reference, physical measurement, interface specification, or other authoritative source |
| **Constraint Statement** | Clear, unambiguous statement of the limit or boundary |
| **Rationale** | Why this constraint exists — the external reality that imposes it |
| **Affected Requirements** | FR-XXX-NNN entries whose implementation is bounded by this constraint |
| **Verification Method** | How compliance will be confirmed: Inspection (I), Analysis (A), Test (T), or Demonstration (D) |

### 7.2 Constraint Statement

The constraint statement shall be:

- **Unambiguous** — a design either complies or it does not
- **Sourced** — traceable to an external authority, measurement, or specification
- **Bounded** — states a specific limit, not a general aspiration

**Good example:** "All field instruments in the Vessel XYZ area shall be rated for Class I, Division 2, Group D per NEC Article 500."

**Poor example:** "Equipment should be suitable for the environment." (Not bounded, not sourced, not verifiable.)

### 7.3 Verification Methods

Constraints are verified differently from functional requirements:

| Method | Code | Description | Example |
|--------|------|-------------|---------|
| **Inspection** | I | Visual or document review confirms compliance | Area classification labels on equipment |
| **Analysis** | A | Engineering calculation or study confirms compliance | Heat dissipation analysis for enclosure temperature |
| **Test** | T | Physical test confirms compliance | Ambient temperature cycling test |
| **Demonstration** | D | Operational demonstration confirms compliance | Communication protocol interoperability demonstration |

Most constraints are verified by inspection or analysis, not by functional testing. Constraint verification is a separate activity from functional FAT/SAT.

---

### 7.4 Worked Example - Constraints

```
CON-PRES-001: Area Classification — Vessel XYZ
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Header:
  CON ID:           CON-PRES-001
  Constraint Type:  Regulatory / Code
  Revision:         A

Source:
  NEC Article 500; Area Classification Drawing AC-201 Rev B;
  Facility Hazardous Area Dossier HAD-RefineryXYZ Rev C

Constraint Statement:
  The Vessel XYZ area is classified Class I, Division 2, Group D
  per NEC Article 500. All field instruments, wiring methods,
  junction boxes, and connections within this area shall be rated
  and installed for Class I, Div 2, Group D service.

Rationale:
  Vessel XYZ processes hydrocarbon (Group D) with potential for
  flammable vapor release under abnormal conditions. The area
  classification is established by the facility hazardous area
  study and is not negotiable by the controls discipline.

Affected Requirements: FR-PRES-001
Verification Method: Inspection (I) — equipment nameplates and
  installation reviewed against area classification drawing
```

```
CON-GEN-001: PLC Platform
━━━━━━━━━━━━━━━━━━━━━━━━━

Header:
  CON ID:           CON-GEN-001
  Constraint Type:  Design Standard
  Revision:         A

Source:
  Plant Standard PS-001 Rev F, Section 4.2 — Control System Platform

Constraint Statement:
  All new BPCS (Basic Process Control System) logic shall be
  implemented on Allen-Bradley ControlLogix platform. Safety
  instrumented functions shall be implemented on Allen-Bradley
  GuardLogix or equivalent SIL 3 certified platform.

Rationale:
  The facility has standardized on Allen-Bradley for BPCS to
  maintain spare parts commonality, operator familiarity, and
  maintenance staff competency. Deviation requires plant
  engineering manager approval.

Affected Requirements: All FR entries (project-wide)
Verification Method: Inspection (I) — hardware procurement
  records and software project files
```

```
CON-GEN-002: Ambient Temperature Rating
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Header:
  CON ID:           CON-GEN-002
  Constraint Type:  Physical / Environmental
  Revision:         A

Source:
  Site meteorological data (30-year record); Plant Standard
  PS-003 Rev D, Section 2.1 — Environmental Design Criteria

Constraint Statement:
  All outdoor field instruments and enclosures shall be rated
  for continuous operation from -20°F to 120°F (-29°C to 49°C).
  Indoor panel-mounted equipment shall be rated for 32°F to
  104°F (0°C to 40°C) with HVAC-controlled environment.

Rationale:
  Site experiences temperature extremes per 30-year meteorological
  record. Indoor environments are HVAC-controlled but design must
  account for HVAC failure during brief periods.

Affected Requirements: All FR entries (project-wide)
Verification Method: Inspection (I) — equipment datasheet review
  against temperature rating requirement
```

### 7.5 How Constraints Shape the Design

The constraints above directly affect the implementation of FR-PRES-001:

- **CON-PRES-001** (area classification) determines that PT-201A, PT-201B, CV-101, and all associated wiring must be Class I, Div 2, Group D rated. This constrains instrument selection, wiring methods, and junction box specifications.
- **CON-GEN-001** (PLC platform) determines that the PID control for CV-101 will be implemented in Allen-Bradley ControlLogix. This constrains software architecture, I/O module selection, and communication protocols.
- **CON-GEN-002** (ambient temperature) determines that PT-201A, PT-201B, and CV-101 must be rated for -20°F to 120°F outdoor service. This constrains instrument procurement specifications.

None of these constraints change *what* the system must do (FR-PRES-001). They change *how* the design team is allowed to implement it. This is the distinction between requirements and constraints.

---

# 8. CD / PD / DD Maturity

This section defines how Functional Requirements (`FR-XXX-NNN`) and Constraints (`CON-XXX-NNN`) mature across Concept Design (CD), Preliminary Design (PD), and Detailed Design (DD) in alignment with the Lifecycle Framework.

---

## 8.1 Concept Design (CD)

At CD, the FRS establishes process intent and design boundaries.

### Functional Requirements

At minimum, the following shall exist:

- P&ID references or preliminary process flow diagrams — at least one process reference per system
    
- Theory of Operations (THEOP) — operating narrative or control philosophy per system
    

> P&IDs and Theory of Operations may be developed in either order.  
> In some projects, the THEOP informs the P&ID. In others, the P&ID informs the THEOP.  
> At CD, both must exist in sufficient detail to define what each system must do and how it is intended to behave.

Each FR entry shall define:

- Process function and measurable performance criteria
    
- Operating modes derived from the Theory of Operations
    
- Preliminary availability targets
    
- Functional interface requirements (signals and interactions, not devices)
    

### Constraints

The following constraint classes shall be identified:

- Regulatory and code constraints (area classification, applicable standards)
    
- Physical and environmental constraints (site conditions)
    
- Interface constraints (existing systems inventory)
    
- Design standard constraints (plant standards, vendor mandates)
    
- Operational constraints (maintenance philosophy, staffing model)
    

Constraints must be captured before architecture selection.

### CD Exit Criterion

The team shall be able to clearly state:

- What each system must do
    
- How well it must do it
    
- What operating modes it must support
    
- What external constraints limit the design
    

If this cannot be stated unambiguously, CD is incomplete.

---

## 8.2 Preliminary Design (PD)

At PD, requirements and constraints are validated against the proposed architecture.

### Functional Requirements

FR entries shall be validated against the proposed control strategy:

- Performance criteria confirmed achievable
    
- Interface requirements mapped to specific devices and drawing sheets
    
- Availability targets validated against redundancy strategy
    
- Degraded mode behavior defined for credible single-point failures
    
- Verification phase identified (Design Review, FAT, SAT, etc.)
    

### Constraints

Constraints shall be validated against architecture:

- Equipment selections verified against environmental and regulatory constraints
    
- Communication architecture verified against interface constraints
    
- Installation approach reviewed for compliance with physical constraints
    

Any constraint that cannot be satisfied shall trigger:

- A documented trade study, or
    
- Formal constraint negotiation with stakeholder approval
    

Silent non-compliance is prohibited.

### PD Exit Criterion

The team shall be able to answer:

> Does the proposed architecture satisfy all functional requirements within the defined constraint boundaries?

If subsystem-level degraded operation or constraint compliance cannot be described, PD is incomplete.

---

## 8.3 Detailed Design (DD)

At DD, verification artifacts are derived and requirements are frozen.

### Functional Requirements

- Verification procedures derived from FR performance criteria
    
- Test steps mapped to implementing sheets and device tags
    
- Verification method finalized (Test, Analysis, Inspection, Demonstration)
    
- FR entries frozen — changes require formal change management
    

### Constraints

- Verification method defined for each CON entry
    
- Procurement specifications verified for compliance
    
- Installation specifications include constraint compliance requirements
    
- CON entries frozen — changes require formal change management
    

Constraint verification may occur during:

- Procurement (platform standards)
    
- Detailed design review (environmental ratings)
    
- Installation (area classification compliance)
    
- Commissioning (communication interoperability)
    

### DD Exit Criterion

The team shall be able to demonstrate:

- All FR entries have defined verification methods and traceable procedures
    
- All CON entries have defined compliance verification methods
    
- No requirement or constraint remains unallocated to implementation
    

After DD, modifications require formal Management of Change (MOC).
---

# 9. Change Management

This section defines revision triggers and governance rules for the Functional Requirements Specification (FRS).

The FRS is a controlled lifecycle document. Changes shall follow formal Management of Change (MOC) procedures once the project has passed CD.

---

## 9.1 Revision Triggers

The FRS shall be reviewed and revised when any of the following occur:

|Trigger|Action Required|
|---|---|
|P&ID revision|Review all FR entries referencing the revised P&ID; update process function descriptions, interfaces, and performance criteria as required|
|Theory of Operations revision|Review affected FR operating modes, sequences, and transition criteria|
|Process design change|Review affected FR entries; revise performance criteria, ranges, or availability expectations|
|Operating mode modification|Review and update mode definitions and transition behavior|
|Equipment change|Review interface requirements, degraded mode assumptions, and availability expectations|
|Regulatory or code revision|Review all CON entries citing the affected authority; update constraint statements and verification methods|
|Plant standard revision|Review affected CON entries; revise statements and verification approach|
|Environmental survey update|Review physical/environmental CON entries; update as required|
|Interface change from adjacent system|Review interface-related FR and CON entries; update boundaries and verification methods|
|Commissioning findings|Update FR entries if functional validation reveals incomplete or unachievable requirements; update CON entries if compliance gaps are identified|
|Periodic revalidation|Review all FR and CON entries aligned with Hazard Analysis revalidation cycle (maximum 5-year interval)|

Failure to evaluate revision triggers constitutes a governance gap.

---

## 9.2 Impact on Downstream Documents

Changes to FR or CON entries may require cascading review of:

- **Hazard Analysis (HA)** — Process function changes may alter hazard scenarios or design intent statements
    
- **SRS** — Changes to process function may affect safety function context or protective requirements
    
- **Drawings** — Interface, performance, or constraint changes may require implementation updates
    
- **ICDs** — Interface definition changes may require signal boundary or responsibility updates
    
- **FMEA** — Changes affecting diagnostics, redundancy, or constraints may require failure analysis revision
    
- **Verification Procedures** — Updated requirements may require updated validation methods and acceptance criteria
    
- **RTM** — Traceability relationships must be updated to maintain bidirectional consistency
    

No revision to FR or CON entries is complete until RTM alignment is restored.

---

## 9.3 Phase-Specific Governance

- **CD Phase:** Revisions are expected and iterative.
    
- **PD Phase:** Revisions require cross-discipline review.
    
- **DD Phase:** FR and CON entries are frozen at DDR. Post-DD changes require formal MOC and impact assessment across all downstream artifacts.
    

After DDR, changes shall not be made informally.

---

## 9.4 Revision Control

The FRS uses letter-based revision designations (Rev A, Rev B, etc.), consistent with Hazard Analysis and SRS documents.

Each revision shall include:

- Summary of changes
    
- Impacted FR and CON identifiers
    
- Downstream document impact assessment
    
- Approval signatures per governance model
    

---

# End Functional Requirements Specification (FRS)
