# Safety Documentation Standard

## Integrated Industrial System Lifecycle Framework

Status: Draft  
Last Updated: 2026-02-20

---

# 1. Methodology Overview

This framework defines an integrated engineering lifecycle for industrial systems. It formally separates and then reconnects:

- Functional Requirements and Constraints
    
- Hazard Analysis (HA)
    
- Safety Requirements Specification (SRS)
    
- Architecture and Drawing-Based Design
    
- FMEA (Architecture-Level and Detailed)
    
- Software Architecture
    
- FAT / SAT (Functional, FMEA, and Safety Verification)
    
- Startup & Commissioning
    
- Proof Testing (for residual inherent DU only)
    
- Operational Governance
    

The framework enforces a clear distinction between **intended system behavior** and **risk reduction behavior**, while ensuring both are treated as primary design drivers.

---

## Core Principles

1. **Functional requirements define intended system behavior.**  
    They describe what the system must do to achieve its process objectives.
    
2. **Hazard analysis identifies unacceptable risk.**  
    It evaluates what can go wrong and determines where risk reduction is required. Hazard analysis does not define solutions.
    
3. **The Safety Requirements Specification (SRS) defines required protective behavior.**  
    Derived from hazard analysis, the SRS translates risk reduction needs into explicit, testable safety functions and integrity targets.  
    The SRS defines _what protection must exist_ and _how reliable it must be_, without prescribing architecture.
    
4. **Requirements drive architecture.**  
    Both functional and safety requirements shape system structure, segregation, diagnostics, response timing, and fault handling.
    
5. **Drawings are the navigation backbone of implementation.**  
    They are one of the few artifacts where electrical, mechanical, software interfaces, and safety mechanisms converge.  
    Drawings provide the physical correlation layer between architecture and implementation and serve as the traceability anchor for verification and maintenance.
    
6. **FMEA is a design driver, not post-design documentation.**  
    FMEA evaluates whether architecture and implementation adequately satisfy functional and safety requirements.  
    Unmitigated or undetected failure modes require design iteration.  
    FMEA exists to drive design improvement, not to record it after the fact.
    
7. **Commissioning capability is a design requirement.**  
    FAT, SAT, and startup are validation activities, but the ability to commission and test the system must be engineered into the architecture from the beginning.  
    The system shall:
    
    - Provide defined test points and observability
        
    - Allow safe fault injection and failure mode verification
        
    - Support staged energization and subsystem isolation
        
    - Enable verification of both functional and safety requirements
        
    - Avoid hidden or non-verifiable behaviors
        
    
    A system that cannot be safely energized, observed, isolated, fault-injected, and verified in a controlled sequence is not fully designed.
    
8. **Functional and safety requirements are co-equal.**  
    A system that achieves its SIL target but fails to perform its process function is a design failure.  
    A system that performs its process function but does not control risk is also a design failure.
    
9. **Constraints bound the design space.**  
    Regulatory, physical, interface, environmental, and operational constraints must be captured before architecture selection.
    

---

## Structural Separation of Authority

The lifecycle maintains the following upstream authority structure:

- **Functional Requirements** define what the system must do.
    
- **Hazard Analysis** defines where risk reduction is required.
    
- **SRS** defines the protective functions and integrity levels required to reduce risk to tolerable levels.
    

The SRS is derived from hazard analysis but remains independent of drawings and implementation details. It specifies required safety behavior and integrity targets without prescribing specific architectural solutions.

Architecture and drawings implement both functional and safety requirements but do not redefine them.

---

## Lifecycle Integrity

This framework aligns with Conceptual Design (CD), Preliminary Design (PD), and Detailed Design (DD) phases, with formal review gates ensuring:

- Traceability from hazard → SRS → architecture → implementation → verification
    
- Iterative FMEA-driven design refinement
    
- Design-for-testability and design-for-commissioning embedded upstream
    
- Validation of both functional and safety performance before operational release
    

Design is not complete when drawings are issued.  
Design is complete when requirements — functional and safety — are demonstrably satisfied under controlled validation conditions.

---

# 2. Engineering Lifecycle and Review Gates

## Lifecycle Authority Statement

This lifecycle exists to ensure that risk definition, architectural decisions, and operational authorization remain aligned throughout the system’s life.

Hazard analysis defines required risk reduction.  
The Safety Requirements Specification defines required protective behavior.  
Architecture implements both functional and safety intent.  
Interfaces formalize responsibility boundaries.  
FMEA enforces design adequacy.  
Traceability ensures nothing is implemented without purpose and nothing required is left unverified.  
Commissioning and startup are governed transitions — not discovery exercises.

No system progresses to operation without demonstrating that requirements, risk controls, interfaces, and validation activities are coherent and complete.

The engineering lifecycle progresses through defined phases.  
Each review gate requires specific deliverables with defined maturity targets.

A gate may not be passed unless all required deliverables meet the stated completion criteria.

Lifecycle progression:

CD → CDR  
PD → PDR  
DD → DDR  
FAT → SAT → PSSR → Startup → Operational Readiness Review  
Operation → Proof Test Cycle

### Graduated Operational Authorization

The system architecture and commissioning plan shall support progressive validation and authorization of operation.

It shall be possible to:

- Energize and validate subsystems independently
    
- Operate subsystems in defined limited modes
    
- Expand operational scope only after meeting defined validation criteria
    

A system that requires full energization before any meaningful validation can occur is not architecturally mature.

Deliverables are categorized as:

- Defined (conceptually complete and approved)
    
- Substantially Complete (~60–80%, structurally coherent)
    
- Complete (100%, internally consistent, reviewable, and testable)
    

No architecture shall proceed to DDR if subsystem isolation, validation boundaries, and operational state transitions are not clearly defined.

## 2.1 CDR – Concept Design Review

_(End of CD)_

### Required Deliverables

|Deliverable|Maturity Requirement|
|---|---|
|Functional Requirements Specification (FRS)|Defined (100% scope defined, performance criteria identified)|
|Constraints Register|Defined|
|Hazard Analysis|Complete|
|Safety Function List|Complete|
|Initial SRS|Defined (all safety functions identified, integrity targets assigned)|
|High-Level Architecture Concept|Defined|
|Safety Integrity Allocation (SIL / PL)|Assigned and justified|

### Gate Intent

Confirm that:

- What the system must do is clear
    
- What must not happen is understood
    
- Required risk reduction is defined
    
- A feasible conceptual architecture exists
    

No Preliminary Design begins without safety intent formally defined.

## 2.2 PDR – Preliminary Design Review

_(End of PD)_

### Required Deliverables

|Deliverable|Maturity Requirement|
|---|---|
|FRS|Validated against architecture|
|SRS|Refined and traceable to HA|
|System Architecture|Substantially Complete (~80%)|
|Diagnostic Strategy|Defined|
|Safe State & Reset Philosophy|Defined|
|Startup Gate Model|Defined|
|System-Level FMEA|≥ 60% complete|
|Integrity Calculations (PFDavg / PL)|Preliminary complete and defensible|
|Commissioning Strategy|Defined at architectural level|
|Operational State Model|Defined (subsystem boundaries, isolation strategy, limited-operation modes, progression criteria defined)|
|Interface Control Documents (ICDs)|Defined (interfaces identified, responsibilities assigned, signal/data/energy boundaries defined)|

### Gate Intent

Confirm that the architecture:

- Can satisfy FRS and SRS
    
- Can achieve integrity targets
    
- Has diagnosable failure behavior
    
- Can be commissioned in a staged and controlled manner
    

At PDR, commissioning strategy must exist at the architectural level — not as a test checklist, but as a structural property of the system. The architecture shall support staged validation and controlled progression from limited operation to full operation. All external and internal system interfaces shall be formally defined to prevent ambiguity in responsibility, safety allocation, and validation scope. ICDs define the validation boundary for subsystem SAT authorization.

## 2.3 DDR – Detailed Design Review

_(End of DD)_

### Required Deliverables

|Deliverable|Maturity Requirement|
|---|---|
|Detailed Drawings|100% Complete|
|Detailed FMEA|100% Complete|
|SRS|Final|
|Integrity Calculations|Final|
|Diagnostic Coverage Analysis|Final|
|Proof Test Procedures|Derived and documented|
|FAT Procedures|100% Complete|
|SAT Procedures|100% Complete|
|Commissioning Plan|Approved|
|Interface Control Documents (ICDs)|Final and internally consistent|
|Requirements Traceability Matrix (RTM)|100% Complete and internally consistent|

FAT/SAT procedures are DDR deliverables and shall explicitly verify:

- Functional Requirements (FRS validation)
    
- Safety Requirements (SRS validation)
    
- Failure mode response and detectability (FMEA validation)
    

### Requirements Traceability Matrix (RTM)

The RTM shall demonstrate bidirectional traceability between:

- Functional Requirements (FRS)
    
- Hazard Analysis items
    
- Safety Requirements (SRS)
    
- Architecture elements
    
- ICDs
    
- FMEA entries
    
- Drawings
    
- Software modules
    
- FAT/SAT validation steps
    
- Proof test procedures (where applicable)
    

No requirement, safety function, or identified failure mode shall exist without:

- Architectural allocation
    
- Implementation reference
    
- Defined validation method
    

No implementation element shall exist without a governing requirement.

At DDR, all physical, logical, and safety interface definitions shall be fully resolved and reflected in implementation artifacts.

### Gate Intent

Confirm that:

- Implementation matches architectural intent
    
- All requirements are testable
    
- Commissioning can proceed in a controlled, observable sequence
    
- No hidden or unverifiable behaviors remain
    

Design is not complete at DDR unless every functional requirement, safety requirement, interface definition, and identified failure mode is traceable to both implementation and validation within the commissioning plan. FAT and SAT execution shall not proceed without an approved RTM demonstrating complete requirement-to-validation traceability.

# 2.4 FAT – Factory Acceptance Testing

Purpose:

Validate functional and safety behavior in a controlled environment prior to site integration.

FAT validates:

- Process functions (FRS)
    
- Safety functions (SRS)
    
- Diagnostic behavior
    
- Defined fault responses
    

FAT does not authorize startup.

# 2.5 SAT – Site Acceptance Testing

Purpose:

Validate installed system behavior and progressively authorize subsystem operation under controlled conditions.

SAT shall be structured to:

- Validate subsystems independently where feasible
    
- Allow defined limited-operation modes
    
- Enforce startup gates before expanding operational scope
    
- Validate functional behavior (FRS)
    
- Validate safety behavior (SRS)
    
- Validate failure response (FMEA)
    

SAT may authorize:

- Limited subsystem operation
    
- Restricted operational envelopes
    
- Controlled expansion to full operational state
    

The ability to safely operate subsystems in limited or expanded modes must be designed into the architecture during PD.

SAT confirms:

- Integration correctness
    
- Field device functionality
    
- Communication integrity
    
- Safety system performance in installed state
    

SAT may include controlled hazardous energization under defined safeguards but does not authorize unrestricted startup or routine production.

# 2.6 PSSR – Pre-Startup Safety Review

PSSR authorizes introduction of hazardous energy, materials, or motion.

### Required Deliverables

|Deliverable|Maturity Requirement|
|---|---|
|Startup Gate Checklist|Complete|
|Safety Validation Records|Complete for startup-critical functions|
|Temporary Safeguards Register|Documented|
|Residual Risk Register|Updated|
|Operator Training Confirmation|Complete|
|Emergency Procedures|Verified|

### Gate Intent

Confirm that:

- All safety-critical startup conditions are satisfied
    
- Risk is controlled to tolerable levels
    
- Energization and initial operation can proceed safely
    

PSSR authorizes startup — not routine production.

# 2.7 Startup

Startup is the controlled expansion from validated subsystem operation to full system operation.

Startup shall:

- Follow defined progression criteria
    
- Require explicit gate satisfaction before scope expansion
    
- Allow rollback to prior validated states
    
- Prohibit transition to full operation without satisfying SRS-defined safety requirements
    

Startup does not invent operational capability — it activates capability intentionally designed during architecture development.

---

# 2.8 Operational Readiness Review

Operational Readiness authorizes transition from startup state to routine operation.

### Required Deliverables

|Deliverable|Maturity Requirement|
|---|---|
|FAT Records|Complete|
|SAT Records|Complete|
|Startup Records|Complete|
|Safety Validation Records|Complete|
|Proof Test Schedule|Approved|
|Operational Governance Plan|Approved|

### Gate Intent

Confirm that:

- Functional performance meets defined criteria
    
- Safety integrity targets have been achieved
    
- Residual risks are documented
    
- Ongoing proof testing and governance are in place
    

Operational Readiness authorizes sustained production operation.

---

# 2.9 Operation and Proof Test Cycle

Where inherent Dangerous Undetected (DU) failure modes remain:

- Proof test intervals defined per SRS
    
- Procedures derived from FMEA
    
- Governance maintains lifecycle compliance
    

Purpose: Preserve original safety intent over operational life.

---

# 2A. Dual-Standard Coexistence

A single project may contain safety functions governed by different standards. A process interlock protecting against overpressure may be governed by IEC 62061 (SIL path), while a machine guard protecting an access door may be governed by ISO 13849 (PL path). This is normal industrial practice, and the framework accommodates both pathways within a single lifecycle.

**The governing standard is declared at the HA level, per safety function.** Each HA entry carries a `Governing Standard` field (e.g., `IEC 62061`, `ISO 13849`) and an `Integrity Target` field (e.g., `SIL 2`, `PLd`). These fields flow through the SRS and FMEA wherever the verification math diverges by standard.

**The lifecycle methodology is common to both pathways.** The engineering phases (CD/PD/DD), review gates (CDR/PDR/DDR/PSSR), traceability model, FMEA philosophy, and commissioning structure do not change based on the governing standard. Only the technical integrity verification diverges:

- **SIL path** (IEC 61508 / IEC 61511 / IEC 62061): quantified in SIL level, PFDavg / PFH, HFT, Route 1H/2H
    
- **PL path** (ISO 13849): quantified in PLa–e, PFHd, architecture Categories (B–4), MTTFd, DCavg
    

The SRS contains Section 6A (SIL path calculations) and Section 6B (PL path calculations). Each SF entry in the SRS uses the section appropriate to its governing standard. FMEA entries inherit the governing standard from the SF they implement, and verification follows the corresponding pathway.

---

# 3. Normative and Informative References

This framework implements and integrates recognized international standards. It does not invent methodology — it provides a structured, integrated implementation of established practice.

The following table lists all standards referenced across the framework, organized by domain. Individual framework documents reference the subset they implement; this section provides the master list.

## 3.1 Primary Functional Safety

|Standard|Title|Framework Application|
|---|---|---|
|IEC 61511 (Parts 1-3)|Functional safety — Safety instrumented systems for the process industry sector|Primary standard. This framework implements Clauses 8–17 across all documents.|
|IEC 61508 (Parts 1-7)|Functional safety of E/E/PE safety-related systems|Parent standard. SIL framework, PFDavg calculation methods, architectural constraints, software safety requirements.|
|IEC 62061|Safety of machinery — Functional safety of safety-related control systems|SIL-based functional safety for machinery applications. Used when the governing standard for a safety function is IEC 62061.|

## 3.2 Hazard Analysis and Risk Assessment

|Standard|Title|Framework Application|
|---|---|---|
|IEC 61882|Hazard and operability studies (HAZOP studies) — Application guide|HAZOP methodology implemented in `02_Hazard_Analysis_Standard`|
|IEC 31010|Risk management — Risk assessment techniques|Risk assessment framework referenced in `02_Hazard_Analysis_Standard`|

## 3.3 FMEA

|Standard|Title|Framework Application|
|---|---|---|
|IEC 60812|Failure modes and effects analysis (FMEA and FMECA)|FMEA methodology implemented in `05_FMEA_Standard`|

## 3.4 Requirements Documentation

|Standard|Title|Framework Application|
|---|---|---|
|ISA-5.6|Functional Requirements Documentation for Control Software Applications|Functional requirements documentation methodology implemented in `01_Functional_Requirements_Standard`|
|ISA-84 (IEC 61511)|Safety Instrumented Systems (SIS)|Safety requirements specification methodology implemented in `03_SRS_Standard`|

## 3.5 Drawings and Documentation

|Standard|Title|Framework Application|
|---|---|---|
|IEC 61082|Preparation of documents used in electrotechnology|Drawing format, cross-referencing, and grid reference systems in `04_Industrial_Systems_Drawing_Standard`|
|IEC 81346|Structuring principles and reference designations|Device designation letter codes in `04_Industrial_Systems_Drawing_Standard`|
|IEC 60445|Basic and safety principles — Identification of equipment terminals and conductor terminations|Terminal and conductor marking in `04_Industrial_Systems_Drawing_Standard`|
|ISA-5.1|Instrumentation Symbols and Identification|P&ID symbology and instrument identification referenced in `01_Functional_Requirements_Standard` and `04_Industrial_Systems_Drawing_Standard`|
|ISA-5.4|Instrument Loop Diagrams|Loop diagram standards referenced in `04_Industrial_Systems_Drawing_Standard`|

## 3.6 PLC and Software

|Standard|Title|Framework Application|
|---|---|---|
|IEC 61131-3|Programmable controllers — Programming languages|PLC programming language standards (Ladder Diagram, Function Block Diagram, Structured Text) in `06_Industrial_Control_Software_Architecture_Standard`|
|IEC 61508-3|Functional safety — Software requirements|Safety software lifecycle, software architectural design, and coding standards in `06_Industrial_Control_Software_Architecture_Standard`|

## 3.7 Testing and Commissioning

|Standard|Title|Framework Application|
|---|---|---|
|IEC 62381|Automation systems in the process industry — Factory acceptance testing (FAT), site acceptance testing (SAT), and site integration testing (SIT)|FAT/SAT methodology in `07_SAT_FAT_Standard`|
|IEC 62382|Automation systems in the process industry — Electrical and instrumentation loop checking|Loop check methodology in `07_SAT_FAT_Standard`|
|IEC 62337|Commissioning of electrical, instrumentation and control systems in the process industry|Structured commissioning methodology in `08_Startup_and_Commissioning_Standard`|

## 3.8 Alarm Management

|Standard|Title|Framework Application|
|---|---|---|
|ISA-18.2 / IEC 62682|Management of Alarm Systems for the Process Industries|Alarm rationalization and lifecycle management; referenced where alarm strategy intersects with functional requirements and FMEA|

## 3.9 Electrical Installation

|Standard|Title|Framework Application|
|---|---|---|
|NEC (NFPA 70)|National Electrical Code|US installation requirements in `04_Industrial_Systems_Drawing_Standard`|
|UL 508A|Industrial Control Panels|Panel construction standards in `04_Industrial_Systems_Drawing_Standard` and `07_SAT_FAT_Standard`|
|IEC 61439|Low-voltage switchgear and controlgear assemblies|Panel and enclosure standards in `07_SAT_FAT_Standard`|

## 3.10 Cybersecurity

|Standard|Title|Framework Application|
|---|---|---|
|IEC 62443|Industrial communication networks — Network and system security|Security considerations for networked control and safety systems|

## 3.11 Machine Safety — Performance Level (PL)

|Standard|Title|Framework Application|
|---|---|---|
|ISO 13849-1|Safety of machinery — Safety-related parts of control systems — Part 1: General principles for design|PL framework, Categories (B–4), MTTFd, DCavg, achieved PL determination. Used for PL-path safety functions.|
|ISO 13849-2|Safety of machinery — Safety-related parts of control systems — Part 2: Validation|Validation methodology for PL path safety functions.|

## 3.13 IEC 61511 Clause Mapping

This framework is structured to align with IEC 61511 (Part 1) without reproducing standard text. The following mapping provides audit traceability between the methodology and recognized functional safety practice.

|Framework Phase|Framework Document|IEC 61511 Clause Reference|
|---|---|---|
|Functional Requirements and Constraints|`01_Functional_Requirements_Standard`|§10 – Safety Requirements Specification (functional context)|
|Hazard Analysis|`02_Hazard_Analysis_Standard`|§8 – Hazard and Risk Assessment|
|Safety Requirements Specification (SRS)|`03_SRS_Standard`|§10 – Safety Requirements Specification|
|Drawing-Based Design|`04_Industrial_Systems_Drawing_Standard`|§11, §12 – SIS Design and Engineering|
|FMEA|`05_FMEA_Standard`|§11 – SIS Design (verification)|
|Software Architecture|`06_Industrial_Control_Software_Architecture_Standard`|§12 – Design and Engineering of SIS (application programming)|
|FAT / SAT|`07_SAT_FAT_Standard`|§14 – Installation, Commissioning and Validation|
|Startup & Commissioning / PSSR|`08_Startup_and_Commissioning_Standard`|§15 – SIS Safety Validation|
|Operation & Maintenance|(operational governance)|§16 – Operation and Maintenance|
|Proof Testing (where inherent DU exists)|`07_SAT_FAT_Standard` (proof test section)|§16.3 – Proof Testing|
|Modification Management|(change management sections across all documents)|§17 – Management of Change|

---

# 4. Governance Model

The following roles are required for lifecycle integrity:

- Functional Safety Lead
    
- Electrical Design Lead
    
- Controls / Software Lead
    
- Commissioning Lead
    
- Operations Representative
    

Formal approval is required at:

- CDR
    
- PDR
    
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

---

## 5.2 Maturity Summary Table

|Document|CD Maturity|PD Maturity|DD Maturity|
|---|---|---|---|
|Functional Requirements Specification (FRS)|Process function and performance criteria defined; operating modes identified|Validated against proposed architecture; functional FAT/SAT scope defined|Frozen — functional FAT/SAT procedures derived from FRS entries|
|Constraints|All constraint types identified and documented|Validated against proposed architecture; conflicts resolved|Frozen — verification methods defined; procurement verified|
|Hazard Analysis|Complete — HAZOP, SFs, SIL targets; no drawing references|Stable — referenced by SRS and FMEA|Frozen — changes require formal MOC|
|SRS|Functional intent defined; integrity targets assigned|Architecture selected; preliminary integrity math complete|Final hardware selected; integrity target verified|
|FMEA|Concept-level sketch only; no worksheet|Architecture-level FMEA; designable DU identified and eliminated|Detailed device-level FMEA; all DU inherent only|
|Drawings|Functional block diagrams only|Architecture-level; device tags assigned; diagnostics provisioned|Fully detailed; SF references embedded|
|Software|Concept only|Module structure defined; deterministic gateway rules defined|Full implementation; deterministic enforcement active|
|FAT / SAT|Not present|Scope defined from architecture|Final procedures derived from FRS, SRS, FMEA|
|Interface Control Documents (ICDs)|Functional interface intent identified; external systems listed|Interfaces defined — signal/data/energy boundaries; responsibilities assigned; safety allocation resolved|Final and internally consistent; aligned with drawings and software|
|Requirements Traceability Matrix (RTM)|Not present|Structure defined; traceability fields established|Complete — bidirectional traceability across all lifecycle artifacts|

---

## 5.3 Concept Design (CD)

**Purpose:** Define the problem, establish process function, and define required risk reduction.

### FRS at CD

- Process function and performance criteria defined
    
- Operating modes identified
    
- Preliminary availability targets established
    
- Interface requirements defined at a functional level
    

### Constraints at CD

- Regulatory constraints identified
    
- Physical/environmental constraints documented
    
- Interface constraints identified
    
- Design standards collected
    
- Operational constraints captured
    

Regulatory and interface constraints must be captured before architecture selection.

### Hazard Analysis at CD

- HAZOP complete
    
- Safety functions identified with integrity targets
    
- `HA-XXX-NNN` entries produced
    
- `SF-XXX-NNN` identifiers assigned
    
- No drawing references
    

### SRS at CD

Functional intent only:

- What the safety function must do
    
- Integrity target (SIL or PLr)
    
- Governing standard
    
- Preliminary T_I (SIL path only)
    
- No hardware selection
    
- No detailed architecture
    

### FMEA at CD

No formal FMEA. Only concept-level identification of obvious single-point architectural risks.

### Drawings at CD

Block diagrams only. No device tags. No wiring.

### Software at CD

Conceptual only.

---

### CD Exit Gate — **CDR**

**Gate question:** Can this system, in principle, achieve the required risk reduction?

At CDR the team confirms:

- FRS defined
    
- Constraints defined
    
- Hazards and risk reduction defined
    
- Integrity targets assigned
    
- SRS functional intent defined
    
- A plausible architecture exists
    

If not — redesign before entering PD.

---

## 5.4 Preliminary Design (PD)

**Purpose:** Convert intent into architecture and iterate until viable.

Core feedback loop:

Architecture ↔ FMEA ↔ SRS math ↔ Drawing update ↔ Software structure ↔ ICD refinement

This loop runs until convergence criteria are met.

---

### FRS at PD

- Validated against architecture
    
- Performance achievable
    
- Interface requirements mapped to devices
    
- Functional FAT/SAT scope defined
    

### Constraints at PD

- Architecture validated against all constraints
    
- Trade studies performed where required
    

### SRS at PD

- Architecture selected (voting/category defined)
    
- Preliminary PFDavg (SIL path) or PL verification (PL path)
    
- Beta/CCF assumptions validated
    
- Hardware fault tolerance validated
    
- Architectural constraint checks complete
    

If integrity target not achieved → architecture changes.

---

### Architecture-Level FMEA at PD

Produces:

- DD vs DU classification
    
- Identification of **designable DU**
    
- Required detection additions
    
- Defined system reaction
    
- Reset philosophy
    
- Safe state definition
    

**Convergence criterion for PDR:**  
All designable DU eliminated. Remaining DU justified as inherent.

---

### ICDs at PD

- Internal and external interfaces formally defined
    
- Signal direction, data type, timing defined
    
- Failure handling defined
    
- Safety allocation across interface boundaries resolved
    
- Responsibilities assigned
    

Interfaces must be architecturally unambiguous before PDR.

---

### Drawings at PD

- Device tags assigned
    
- Diagnostics provisioned
    
- Architecture defined; wiring flexible
    

### Software Architecture at PD

- Object model defined
    
- Deterministic gateway rules defined
    
- Sheet modules mapped
    

---

### PD Exit Gate — **PDR**

**Gate question:** Does this architecture achieve the integrity target and support staged commissioning?

PDR exit criteria:

- All designable DU eliminated
    
- Integrity math meets target
    
- Every DD failure has detection and reaction
    
- Safe states defined
    
- Reset philosophy defined
    
- Commissioning and operational state model defined
    
- Subsystem isolation and validation boundaries defined
    

If subsystem-level validation cannot be described → architecture incomplete.

---

## 5.5 Detailed Design (DD)

**Purpose:** Lock the design. Replace architecture with implementation.

No new architectural decisions are made in DD.  
Architectural deficiencies discovered at DD require formal escalation and re-entry into PD governance.

---

### FRS at DD

- Frozen
    
- FAT/SAT procedures derived
    

### Constraints at DD

- Verification methods defined
    
- Frozen
    

### SRS at DD

- Final hardware selected
    
- Final integrity math verified
    

### FMEA at DD

- Device-level failure rates
    
- MTTR confirmed
    
- Proof test coverage calculated
    

**No designable DU permitted at DD.**  
All DU must be inherent only.

Inherent DU → mapped to proof test.

---

### Drawings at DD

- Final wiring complete
    
- SF references embedded
    

### Software at DD

- Full implementation
    
- Deterministic enforcement active
    
- Test surfaces exposed
    

### ICDs at DD

- Verified against final drawings and software
    
- No ambiguous ownership
    
- Safety allocations fully resolved
    

---

### FAT/SAT at DD

Derived from:

- FRS entries
    
- SRS requirements
    
- FMEA detection entries
    
- Drawing modules
    
- ICD boundaries
    

Each safety test step enforces full fault lifecycle:

Normal → Induce fault → Verify reaction → No reset while fault active → Remove fault → No auto-restart → Reset → Verify recovery

Procedures are complete before construction begins.

---

### Requirements Traceability Matrix (RTM) at DD

RTM demonstrates bidirectional traceability between:

- FRS
    
- HA
    
- SRS
    
- ICDs
    
- Architecture
    
- FMEA
    
- Drawings
    
- Software modules
    
- FAT/SAT steps
    
- Proof test procedures
    

No requirement without implementation and validation.  
No implementation without governing requirement.

---

### DD Exit Gate — **DDR**

**Gate question:** Does implementation match architectural intent and satisfy integrity requirements?

DDR exit criteria:

- Integrity target confirmed
    
- All DU inherent only
    
- Proof test procedures derived (if required)
    
- FAT/SAT complete and traceable
    
- RTM complete and internally consistent
    
- No unresolved diagnostic gaps
    
- Deterministic enforcement active
    

After DDR: construction-ready. Changes require formal MOC.

---

## 5.6 Commissioning Phase

Commissioning begins after DDR.

Commissioning validates execution — bottom-up — through defined Validation Levels and Startup Gates as specified in `08_Startup_and_Commissioning_Standard`.

Commissioning executes the **Graduated Operational Authorization** model defined during PD:

- Subsystems validated independently
    
- Limited-operation states enforced
    
- Operational scope expands only after validation criteria satisfied
    

Commissioning does not change design intent.  
If architectural deficiencies are discovered, the system re-enters formal design governance.

Design phase answers: _Is the design correct?_  
Commissioning answers: _Was the design built correctly?_

These questions must never be conflated.

---

# 6. Traceability Numbering and Cross-Reference Model

## 6.1 Principle

This framework enforces structured, bidirectional traceability across requirements, architecture, implementation, failure analysis, and validation.

Three distinct classes of identifiers are used, each answering a different question:

|Identifier Class|Examples|Question Answered|
|---|---|---|
|Requirement and Safety Function IDs|FR-PRES-001, SF-PRES-001, HA-PRES-001|**Why does this system exist?**|
|Device Tags|PT-201A, CV-101, K-101|**What physical element implements it?**|
|Drawing Sheet Numbers|Sheet 201, Sheet 320|**Where is the implementation defined?**|

These identifiers are not interchangeable. Each serves a distinct governance purpose.

The Requirements Traceability Matrix (RTM) enforces bidirectional mapping across all identifier classes. ICDs define interface boundaries and responsibilities and are referenced by the RTM to ensure each interface is allocated, implemented, and validated.

---

## 6.2 Requirement IDs on Drawings — Upstream Traceability (Why)

Hazard Analysis identifiers (HA-XXX-NNN), Safety Function identifiers (SF-XXX-NNN), and Functional Requirement identifiers (FR-XXX-NNN) appear in drawing title blocks and notes to answer:

> Why does this implementation exist?

- **FR-XXX-NNN** in a drawing title block identifies the functional requirement implemented on that sheet.
    
- **SF-XXX-NNN** identifies the safety function implemented.
    
- **HA-XXX-NNN** links implementation to the originating hazard scenario.
    

These references provide upstream traceability — connecting implementation to intent.

Drawing sheets implement requirements.  
Requirements do not originate in drawings.

If a drawing sheet cannot be traced to at least one FR or SF identifier, its existence must be justified through the RTM.

---

## 6.3 Device Tags in FMEA — Implementation Traceability (What Fails)

Device tags (PT-201A, CV-101, K-101) appear in FMEA entries to answer:

> What physical element experiences this failure mode?

Failure modes belong to devices, not sheets.

The same device may appear on:

- Loop diagrams
    
- Wiring diagrams
    
- Control logic sheets
    
- Panel layouts
    

The device tag uniquely identifies the physical component across all representations.

From a device tag, an engineer can:

- Locate the device in the plant
    
- Locate all drawing sheets referencing that device
    
- Locate all FMEA entries associated with it
    
- Locate all FAT/SAT procedures that exercise it
    

Device tags anchor failure analysis to physical reality.

---

## 6.4 Drawing Sheet Numbers — Implementation Scope (Where It Lives)

Drawing sheet numbers define implementation scope and validation boundary.

**In FMEA:**  
Each FMEA entry references the drawing sheet that contains the relevant control or safety logic.  
The sheet is the analyzable scope — grouping devices, wiring, and logic into a coherent unit.

**In FAT/SAT:**  
Procedures reference the sheet(s) they validate.  
Functional FAT/SAT procedures may be numbered by sheet (`FFAT-[Sheet]`).  
The sheet number defines the test boundary.

Sheets organize implementation.  
Device tags identify components.  
Requirements justify existence.

---

## 6.5 Full Traceability Chain

The complete lifecycle traceability chain is:

Why does it exist?      → FR-XXX-NNN or SF-XXX-NNN (Requirement / Safety Function)  
        │  
        ▼  
What hazard drove it?   → HA-XXX-NNN (Hazard Analysis entry)  
        │  
        ▼  
Where is it designed?   → Drawing Sheet Number (Implementation scope)  
        │  
        ▼  
What devices implement it? → Device Tags (PT-201A, CV-101)  
        │  
        ▼  
What can fail?          → FMEA entry (Device tag + Sheet reference + Failure mode)  
        │  
        ▼  
How is it validated?    → FAT/SAT procedure (Sheet + Device tag + Requirement ID)  
        │  
        ▼  
How is integrity maintained? → Proof test procedure (if inherent DU exists)

The RTM formalizes this chain and enforces bidirectional traceability.

---

## 6.6 Cross-Reference Summary

|Reference Appears In|Identifier Used|Traceability Purpose|
|---|---|---|
|Drawing title blocks|FR-XXX-NNN / SF-XXX-NNN|Why the sheet exists|
|Drawing notes|HA-XXX-NNN|Hazard origin reference|
|FMEA entries|Device tag|Physical element under failure analysis|
|FMEA entries|Sheet number|Implementation scope|
|SAT/FAT procedures|Sheet number|Test boundary|
|SAT/FAT procedures|Device tag|Specific device under test|
|SAT/FAT procedures|FR-XXX-NNN / SF-XXX-NNN|Requirement being validated|
|Proof test procedures|Device tag + SF ID|Inherent DU validation linkage|
|RTM|All identifier classes|Governance-level traceability enforcement|

---

## 6.7 Governance Rule

The following conditions are prohibited:

- A drawing sheet without at least one governing FR or SF reference
    
- A requirement without architectural allocation
    
- A device appearing in implementation without FMEA consideration
    
- An FMEA entry without a corresponding validation method
    
- A validation step without a governing requirement
    

Traceability gaps are design failures, not documentation omissions.

# End Safety Documentation Standard