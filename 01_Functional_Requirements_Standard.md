# Functional Requirements and Constraints Standard
## Process Functional Requirements and Design Constraints for Industrial Systems

**Status:** Draft
**Scope:** Definition and documentation of process functional requirements and design constraints for industrial control systems. Defines what the system must do under normal operation (requirements) and what boundaries limit design freedom (constraints).

---

## Table of Contents

1. [Purpose and Scope](#1-purpose-and-scope)
2. [Standards References](#2-standards-references)
3. [Relationship to Other Documents](#3-relationship-to-other-documents)
4. [Requirements and Constraints — Definitions](#4-requirements-and-constraints--definitions)
5. [Numbering and Identification](#5-numbering-and-identification)
6. [Functional Requirement Entry Format](#6-functional-requirement-entry-format)
7. [Constraint Entry Format](#7-constraint-entry-format)
8. [Worked Example](#8-worked-example)
9. [Functional FAT/SAT and Constraint Verification](#9-functional-fatsat-and-constraint-verification)
10. [CD / PD / DD Maturity](#10-cd--pd--dd-maturity)
11. [Change Management](#11-change-management)

---

## 1. Purpose and Scope

### 1.1 Purpose

This standard defines the methodology for documenting process functional requirements and design constraints for industrial systems.

**Functional requirements** capture what the system must *do* under normal operation — the process function that justifies the system's existence.

**Constraints** capture what boundaries limit design freedom — the regulatory, physical, interface, operational, and design standard limits that the system must comply with regardless of the functional approach chosen.

This document is the complement to the Safety Requirements Specification (SRS). The SRS captures what the system must achieve to be safe; this standard captures what the system must do to be functional.

A system that meets its SIL target but fails to perform its process function is a design failure. A system that performs its process function but violates a constraint is equally a design failure. Safety, function, and constraints are co-requirements.

### 1.2 Scope

This standard applies to:

- Process functional requirements for industrial control systems
- Design constraints that bound the implementation space
- P&ID references and process design basis for each functional requirement
- Theory of operations (operating narratives, sequence descriptions, control philosophy)
- Performance criteria (setpoints, tolerances, ranges, response characteristics)
- Operating mode definitions (normal, startup, shutdown, degraded)
- Availability and uptime requirements
- Interface requirements between systems
- Regulatory, physical, operational, and design standard constraints
- Traceability from requirements and constraints to implementation and verification

This standard does **not** define:

- Safety requirements — see the SRS Standard (`03_SRS_Standard`)
- Hazard analysis methodology — see the Hazard Analysis Standard (`02_Hazard_Analysis_Standard`)
- Drawing conventions — see the Industrial Systems Drawing Standard (`04_Industrial_Systems_Drawing_Standard`)
- FMEA methodology — see the FMEA Standard (`05_FMEA_Standard`)
- FAT/SAT safety test procedures — see the SAT/FAT Standard (`07_SAT_FAT_Standard`)

### 1.3 Design Philosophy

**Functional requirements are upstream of everything.** Hazards are risks arising from the process function. Safety requirements protect people and equipment from the consequences of those hazards.

Without a clear definition of what the system must do, every downstream activity lacks its anchor. 

**Constraints bound the design space.** Before selecting architecture, the design team must know what limits apply — regulatory, physical, interface, and operational. Constraints are not requirements to be optimized; they are boundaries to be respected. Failing to capture a constraint upstream results in rework when the constraint is discovered during detailed design or construction. A constraint discovered after equipment is procured is a change order and lost time. A constraint discovered after during commissioning can be a considerable set back.

**Theory of operations are vital design inputs.** Functional requirements are derived from the process design — The theory of operations describes how it is intended to work. This document is where those process-level descriptions are translated into testable, traceable requirements for the control system.  A theory of operations without traceable FR entries is an unverifiable narrative.

**FRS is distinct from SRS.** Functional requirements do not carry SIL targets, PFDavg calculations, or proof test intervals. They define process intent and performance expectations. Where a functional requirement generates a safety concern, the hazard analysis identifies the hazard, and the SRS specifies the safety function that protects people and equipment from the consequences. FRS can have a reliability and uptime component requiring calculation.

**One document per project.** Like the SRS and HA, the functional requirements and constraints document is a single project-level document containing one entry per functional requirement and one entry per constraint.

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

## 3. Relationship to Other Documents

### 3.1 Document Flow

```
P&IDs + Theory of Operations + Plant Standards + Regulatory Codes
     │
     ▼
Functional Requirements (FR-XXX-NNN) + Constraints (CON-XXX-NNN)
     │
     ├──► Hazard Analysis — hazards are risks TO the function defined here
     │         │
     │         ▼
     │    SRS (SF-XXX-NNN) — safety requirements PROTECT people and equipment
     │
     ├──► Drawings — implement requirements within constraint boundaries
     │
     ├──► Functional FAT/SAT — validates the function performs as specified
     │
     ├──► Constraint Verification — confirms design respects all constraints
     │
     └──► Commissioning — functional and constraint verification are gate requirements
```

### 2.2 Relationship to P&IDs and Theory of Operations

**P&IDs** define the physical process — equipment, piping, instrumentation, and control elements. They are produced by the process discipline and are the primary input to this document. Each functional requirement shall reference the P&ID(s) that define the process it controls.

**Theory of operations** (also called operating narrative, control philosophy, or sequence description) describes how the process is intended to work — the operating intent behind the P&ID. This includes startup sequences, normal operating regimes, shutdown procedures, and transitions between modes. The theory of operations is captured within this document as part of the FR entry (operating modes, process function description), or referenced as a companion document when a standalone narrative exists.

P&IDs and the theory of operations are not produced by this standard — they are consumed by it. This standard translates process intent into testable, traceable control system requirements.

### 2.3 Relationship to Hazard Analysis (`02_Hazard_Analysis_Standard`)

Functional requirements are upstream of hazard analysis. The HAZOP study examines deviations from the *design intent* — that design intent is defined by functional requirements. Each HA node's "Design Intent" statement should trace to one or more FR entries. Constraints (particularly regulatory and environmental) may also generate hazard analysis inputs.

### 2.4 Relationship to SRS (`03_SRS_Standard`)

Each safety function (SF-XXX-NNN) in the SRS protects people and equipment from hazardous events. Functional requirements do not replace safety requirements — they provide the process context that makes safety requirements meaningful.

The relationship between FRs and safety functions is not 1:1. Some hazards arise directly from a deviation in a defined process function — these trace cleanly to a specific FR entry. Others arise from equipment failure modes, external events, or environmental conditions that are not process-function deviations. Where a clear process function link exists, the SRS entry should reference the corresponding FR-XXX-NNN. Where no clear link exists, the SRS entry stands on its own, grounded in the hazard analysis.

### 2.5 Relationship to Drawings (`04_Industrial_Systems_Drawing_Standard`)

Drawings implement both functional and safety requirements within constraint boundaries. Non-safety sheets implement functional requirements; safety-critical sheets implement both. The FR reference may appear in drawing title blocks alongside (or instead of) the SF reference for non-safety sheets.

### 2.6 Relationship to FAT/SAT (`07_SAT_FAT_Standard`)

Functional FAT/SAT validates that the system performs its intended process function. This is distinct from safety FAT/SAT, which validates that safety functions operate correctly. Both are required for a complete commissioning package.

### 2.7 Relationship to Commissioning (`08_Startup_and_Commissioning_Standard`)

Functional FAT/SAT completion and constraint verification are evidence required for startup gate passage. A system that passes safety validation but fails functional validation or violates a design constraint is not ready for operation.

---

## 4. Requirements and Constraints — Definitions

### 4.1 Functional Requirement (FR)

A statement of what the system must *do* — a process function it must perform.

Functional requirements are:
- **Testable** — it must be possible to objectively determine whether the function is performed
- **Performance-bounded** — they include quantitative criteria for how well the function must be performed
- **Traceable** — each requirement traces to P&IDs and theory of operations (upstream) and to implementing drawings and test procedures (downstream)
- **Implementation-independent** — they describe *what*, not *how*

Functional requirements answer: *What must this system do, and how well must it do it?*

### 4.2 Performance Criteria

Quantitative bounds on how well a functional requirement must be performed — setpoints, tolerances, response times, accuracy, stability. Performance criteria are captured within FR entries as a required field, not as separate entries.

### 4.3 Constraint (CON)

A boundary condition that limits design freedom. Constraints are not functions the system performs — they are imposed limits from outside the system boundary that the design must respect.

Constraints originate from sources external to the control system design:

| Constraint Type | Source | Examples |
|----------------|--------|----------|
| **Regulatory / Code** | Laws, codes, standards, permits, AHJ requirements | IEC 61511, NEC Article 500, area classification (Class I Div 2), environmental permits, OSHA PSM |
| **Physical / Environmental** | Site conditions, physical reality | Ambient temperature range, humidity, elevation, corrosive atmosphere, seismic zone, available space, noise limits |
| **Interface** | Existing infrastructure that cannot be changed | Existing DCS platform, network architecture, power distribution, communication protocols, field bus standards |
| **Operational** | How the facility is operated and maintained | Maintenance access requirements, operator skill levels, spare parts strategy, turnaround schedule, staffing model |
| **Design Standard** | Owner/operator or EPC mandated practices | PLC platform, HMI standard, wiring practices, panel fabrication standards, vendor preferences, naming conventions |

### 4.4 The Distinction

Requirements define what the system must *achieve*. Constraints define what the system must *comply with*.

A functional requirement can be met by many possible designs. Together, requirements and constraints define the design space.

**Requirements are optimized.** A design should meet performance criteria as effectively as possible.

**Constraints are satisfied.** A design either complies with a constraint or it does not. There is no partial compliance.

If a constraint conflicts with a requirement, the conflict must be resolved explicitly — not by silently violating the constraint or degrading the requirement. Resolution requires documented justification and stakeholder approval.

---

## 5. Numbering and Identification

### 5.1 Document ID

**Format:** `FR-[Project]`

The functional requirements and constraints document is a single project-level document. Its identifier is the project code. Example: `FR-RefineryXYZ`.

### 5.2 Functional Requirement Entry ID

**Format:** `FR-XXX-NNN`

| Component | Description | Example |
|-----------|-------------|---------|
| `FR` | Functional Requirement prefix | FR |
| `XXX` | System abbreviation code (same codes as HA and SRS) | PRES |
| `NNN` | Sequential requirement number within that system | 001 |

**Examples:**

- `FR-PRES-001` — Functional requirement for Pressure system, first requirement
- `FR-TEMP-002` — Functional requirement for Temperature system, second requirement
- `FR-FLOW-001` — Functional requirement for Flow system, first requirement

### 5.3 Constraint Entry ID

**Format:** `CON-XXX-NNN`

| Component | Description | Example |
|-----------|-------------|---------|
| `CON` | Constraint prefix | CON |
| `XXX` | System abbreviation code, or `GEN` for project-wide constraints | PRES, GEN |
| `NNN` | Sequential constraint number within that system | 001 |

**Examples:**

- `CON-PRES-001` — Constraint specific to Pressure system (e.g., area classification around vessel)
- `CON-GEN-001` — Project-wide constraint (e.g., mandated PLC platform)
- `CON-GEN-002` — Project-wide constraint (e.g., ambient temperature rating)

Use `GEN` for constraints that apply across multiple systems or the entire project. Use a system code when the constraint applies only to a specific system.

### 5.4 System Abbreviation Codes

Uses the same system abbreviation codes defined in the Hazard Analysis Standard Section 4.3:

| Code | System Type |
|------|-------------|
| PRES | Pressure |
| TEMP | Temperature |
| FLOW | Flow |
| LEV | Level |
| FIRE | Fire |
| TOX | Toxic |
| COMB | Combustible |
| COMP | Composition |
| REAC | Reaction |
| MECH | Mechanical |
| ELEC | Electrical |
| ENV | Environmental |
| GEN | General / Project-wide (constraints only) |

Additional codes may be added for project-specific needs per HA Standard Section 4.3 rules.

---

## 6. Functional Requirement Entry Format

### 6.1 Required Fields per Entry

Each FR-XXX-NNN entry within the document shall contain:

| Section | Content Required |
|---------|-----------------|
| **Header** | FR ID (FR-XXX-NNN), system/subsystem name, revision |
| **Source Documents** | P&ID reference(s), theory of operations reference (or inline narrative) |
| **Process Function Description** | What the system must do — a clear, testable statement of the intended function |
| **Performance Criteria** | Setpoints, tolerances, ranges, response characteristics, accuracy requirements |
| **Operating Modes** | Normal operation, startup, shutdown, degraded operation — with criteria for each |
| **Availability Requirements** | Uptime targets, maximum allowable downtime, redundancy expectations |
| **Interface Requirements** | Inputs (sensors, signals, other systems), outputs (actuators, signals, other systems) |
| **Applicable Constraints** | CON-XXX-NNN entries that apply to this requirement's implementation |
| **Implementing Sheets** | Drawing sheet numbers implementing this functional requirement |
| **Validation Method** | Functional FAT/SAT reference — how the requirement will be proven |

### 6.2 Source Documents

Each FR entry shall reference the process documentation it is derived from:

**P&ID References:** The P&ID sheet(s) and revision(s) that define the physical process controlled by this functional requirement. The P&ID defines what equipment exists, what instrumentation is installed, and what control elements are available. Format: `P&ID-NNN Rev X`.

**Theory of Operations:** The operating narrative that describes how the process is intended to work. This may be:

- **Inline** — captured directly in the FR entry's process function description and operating modes sections. Preferred for simple systems where the operating intent can be stated concisely.
- **Referenced** — a standalone document (control philosophy, operating narrative, sequence description) produced by the process or controls discipline. Referenced by document number and revision. Preferred for complex systems with multi-step sequences, batch operations, or coordinated unit interactions.

The theory of operations answers: *how does the operator expect this system to behave?* The FR entry translates that expectation into testable criteria.

### 6.3 Process Function Description

The process function description shall be:

- **Testable** — it must be possible to objectively determine whether the function is performed
- **Specific** — it must define what "correct operation" means in measurable terms
- **Complete** — it must cover all operating modes the system will encounter
- **Independent of implementation** — it describes *what*, not *how*

**Good example:** "Maintain vessel pressure between 80 and 120 psig during normal operation by modulating the outlet control valve."

**Poor example:** "Control pressure." (Not testable, not specific, not complete.)

### 6.4 Performance Criteria

Performance criteria define how well the function must be performed:

| Criterion | Description | Example |
|-----------|-------------|---------|
| Setpoint | Target operating value | 100 psig |
| Control range | Acceptable operating band | 80–120 psig |
| Accuracy | Maximum deviation from setpoint under steady state | +/- 2 psig |
| Response time | Maximum time to reach setpoint from a defined disturbance | < 30 seconds for 10% step change |
| Overshoot | Maximum transient excursion beyond setpoint | < 5 psig |
| Stability | Steady-state oscillation limits | < 1 psig peak-to-peak |

### 6.5 Operating Modes

Each functional requirement shall define behavior for applicable operating modes:

| Mode | Definition |
|------|-----------|
| **Normal** | Steady-state operation within design parameters |
| **Startup** | Transition from cold/idle state to normal operation |
| **Shutdown** | Controlled transition from normal operation to idle/cold state |
| **Degraded** | Operation with reduced capability (e.g., single sensor, backup equipment) |
| **Emergency** | Response to abnormal conditions (handoff to safety systems) |

**Operating modes will be specific to individual projects**

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

## 8. Worked Example

### 8.1 Functional Requirement — FR-PRES-001: Vessel XYZ Pressure Control

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

### 8.2 Constraints

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

### 8.3 How Constraints Shape the Design

The constraints above directly affect the implementation of FR-PRES-001:

- **CON-PRES-001** (area classification) determines that PT-201A, PT-201B, CV-101, and all associated wiring must be Class I, Div 2, Group D rated. This constrains instrument selection, wiring methods, and junction box specifications.
- **CON-GEN-001** (PLC platform) determines that the PID control for CV-101 will be implemented in Allen-Bradley ControlLogix. This constrains software architecture, I/O module selection, and communication protocols.
- **CON-GEN-002** (ambient temperature) determines that PT-201A, PT-201B, and CV-101 must be rated for -20°F to 120°F outdoor service. This constrains instrument procurement specifications.

None of these constraints change *what* the system must do (FR-PRES-001). They change *how* the design team is allowed to implement it. This is the distinction between requirements and constraints.

---

## 9. Functional FAT/SAT and Constraint Verification

### 9.1 Functional FAT/SAT — Purpose

Functional FAT/SAT proves that the system performs its intended process function under normal conditions. This is distinct from safety FAT/SAT, which proves that safety functions operate correctly under fault conditions.

### 9.2 Functional FAT/SAT — Scope

Functional FAT/SAT validates:

- Process control functions operate within specified performance criteria
- All operating modes (normal, startup, shutdown, degraded) behave as defined
- Interface requirements are met (correct signals, correct ranges)
- Availability mechanisms work (backup switchover, degraded mode operation)

### 9.3 Functional FAT/SAT — Format

No prescribed format is mandated. Functional FAT/SAT procedures are project-specific and may use whatever test methodology is appropriate for the system. However, all functional FAT/SAT procedures must:

- **Trace to FR entries** — every test step must reference the FR-XXX-NNN it validates
- **Define pass/fail criteria** — derived from the performance criteria in the FR entry
- **Produce records** — test results must be documented and retained as commissioning evidence
- **Be completed before or alongside safety testing** — functional testing should precede or accompany safety FAT/SAT, not follow it

### 9.4 Functional FAT/SAT — Numbering

**Format:** `FFAT-[Sheet]`

Functional FAT/SAT procedures are numbered by the primary implementing sheet, prefixed with `FFAT` to distinguish from safety FAT/SAT (`SAT`).

**Example:** `FFAT-150` — Functional FAT/SAT for the control system on Sheet 150.

### 9.5 Constraint Verification

Constraints are verified separately from functional requirements. Constraint verification typically uses inspection, analysis, or demonstration — not functional testing.

**Constraint verification records shall document:**

- CON-XXX-NNN reference
- Verification method used (I, A, T, or D)
- Evidence of compliance (datasheet reference, calculation, inspection record)
- Verified by / date
- Status (compliant / non-compliant / deviation approved)

Constraint verification may occur at any project phase — some constraints (e.g., PLC platform) are verified at procurement, others (e.g., area classification compliance) at installation, others (e.g., ambient temperature rating) at equipment selection.

### 9.6 Comparison — Functional FAT/SAT vs. Safety FAT/SAT vs. Constraint Verification

| Aspect | Functional FAT/SAT | Safety FAT/SAT                      | Constraint Verification |
|--------|-------------------|-------------------------------------|------------------------|
| Purpose | Prove the system does what it should | Prove the system is safe            | Prove the design respects all boundaries |
| Reference | FR-XXX-NNN entries | SF-XXX-NNN entries via FMEA         | CON-XXX-NNN entries |
| Test conditions | Normal operation, mode transitions | Fault injection, failure simulation | Inspection, analysis, demonstration |
| Pass criteria | Performance within FR tolerances | Fault detection, safe state achieved | Compliance with constraint statement |
| Requirement | Project-defined | IEC 61511 mandated for SIS          | Project-defined |
| Standard | This document | `07_SAT_FAT_Standard`               | This document |

### 9.7 Results as Commissioning Evidence

Functional FAT/SAT results and constraint verification records are required evidence for commissioning gate passage. A system that passes safety validation but fails functional validation or has unresolved constraint non-compliances is not ready for operation. Both functional and safety test results, along with constraint verification records, shall be available at the Operational Readiness Review and referenced in PSSR documentation.

---

## 10. CD / PD / DD Maturity

### 10.1 Concept Design (CD)

At CD, the document defines:

**Functional Requirements:**
- P&ID references or preliminary process flow diagrams — at least one process reference must exist for each system
- Theory of operations — operating narrative or control philosophy for each system

Note: P&IDs and the theory of operations may be developed in either order. In some projects, the control philosophy (THEOP) precedes the P&ID and informs its development. In others, the P&ID is issued first and the THEOP is derived from it. At CD, both must exist in sufficient detail to define what each system must do and how it is intended to work.
- Process function and performance criteria for each system
- Operating mode requirements (derived from the theory of operations)
- Preliminary availability targets
- Interface requirements at a functional level (what signals, not what devices)

**Constraints:**
- Regulatory and code constraints identified (area classification, applicable standards)
- Physical and environmental constraints documented (site conditions survey)
- Interface constraints identified (existing systems inventory)
- Design standard constraints collected (plant standards, vendor mandates)
- Operational constraints captured (maintenance philosophy, staffing model)

**CD exit criterion:** Can the team state what each system must do, how well it must do it, what operating modes it must support, and what constraints limit the design?

Regulatory and interface constraints **must** be captured before architecture selection. Selecting architecture without knowing constraints risks choosing a design that cannot comply.

### 10.2 Preliminary Design (PD)

At PD, requirements and constraints are validated against the proposed architecture:

**Functional Requirements:**
- Performance criteria confirmed achievable with selected control strategy
- Interface requirements mapped to specific devices and sheets
- Availability requirements validated against proposed redundancy
- Degraded mode behavior defined for all credible single-point failures
- Functional FAT/SAT scope defined

**Constraints:**
- Proposed architecture validated against all constraints
- Equipment selections verified against environmental and regulatory constraints
- Communication architecture verified against interface constraints
- Any constraint that cannot be met triggers a design trade study or constraint negotiation with documented resolution

**PD exit criterion:** Does the proposed architecture achieve the functional requirements within the constraint boundaries?

### 10.3 Detailed Design (DD)

At DD, verification procedures are derived from requirements and constraints:

**Functional Requirements:**
- Test procedures written with specific pass/fail criteria from FR performance criteria
- Test steps mapped to implementing sheets and device tags
- Functional FAT/SAT procedures complete before construction
- FR entries frozen — changes require formal change management

**Constraints:**
- Constraint verification methods defined for each CON entry
- Procurement specifications verified against constraint requirements
- Installation specifications include constraint compliance requirements
- CON entries frozen — changes require formal change management

**DD exit criterion:** Are functional FAT/SAT procedures and constraint verification methods complete and traceable to FR and CON entries?

---

## 11. Change Management

### 11.1 Revision Triggers

The functional requirements and constraints document shall be reviewed and revised when:

| Trigger | Action Required |
|---------|----------------|
| P&ID revision | Review all FR entries referencing the revised P&ID; update process function descriptions, interfaces, and performance criteria as needed |
| Theory of operations change | Review affected FR operating mode definitions and sequence descriptions |
| Process design change | Review affected FR entries; revise performance criteria if process conditions change |
| Operating mode change | Review and update mode definitions and transition criteria |
| Equipment change | Review interface requirements and availability assumptions |
| Regulatory change | Review all CON entries citing the affected code or standard; update constraint statements and verification methods |
| Plant standard revision | Review all CON entries citing the affected plant standard; update constraint statements |
| Environmental survey update | Review physical/environmental CON entries; update constraint statements if site conditions have changed |
| Interface change from adjacent system | Review interface CON entries; update constraint statements and affected FR entries |
| Commissioning findings | Update FR entries if functional FAT/SAT reveals requirements that are unachievable or incomplete; update CON entries if constraint verification reveals non-compliance |
| Periodic revalidation | Review all FR and CON entries at intervals aligned with HA revalidation (5 years maximum) |

### 11.2 Impact on Downstream Documents

Changes to functional requirements or constraints may cascade to:

- **Hazard Analysis** — if the process function changes, hazard scenarios may change
- **SRS** — if the process function changes, the hazards arising from it may change, and safety function specifications may need revision
- **Drawings** — if interface, performance, or constraint requirements change, implementation may need revision
- **FMEA** — if constraints change available detection or diagnostic capability, FMEA entries may need revision
- **Functional FAT/SAT** — test procedures and acceptance criteria must be updated
- **Constraint Verification** — verification methods and evidence must be updated

### 11.3 Revision Control

The functional requirements and constraints document uses letter revision designations (Rev A, Rev B, etc.), consistent with the HA and SRS revision conventions.

---

# End Functional Requirements and Constraints Standard
