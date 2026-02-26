
# Industrial Control Software Architecture Standard  
## PLC Runtime Architecture for Testable and Diagnosable Industrial Systems

**Status:** Draft

---
# 1. Purpose

This standard defines a reference PLC (Programmable Logic Controller) software architecture that:

- Aligns runtime behavior with drawings, FMEA, FAT/SAT, and proof testing
- Preserves determinism required for machine control
- Reduces tribal knowledge and commissioning friction
- Enables repeatable, testable machine software

Drawings remain the **source of truth**.  
Software is a projection of the drawings.

---
# 2. Standards References

| Standard | Title | Application |
|----------|-------|-------------|
| IEC 61131-3 | Programmable controllers — Programming languages | PLC programming language standards (Ladder Diagram, Function Block Diagram, Structured Text) |
| IEC 61508-3 | Functional safety — Software requirements | Software safety lifecycle, software architectural design, coding standards for safety-related software. Applies to SIL path functions and PLe functions. |
| IEC 61511-1 | Functional safety — Safety instrumented systems for the process industry | Clause 12 — SIS software requirements; application programming |
| ISO 13849-1 | Safety of machinery — Safety-related parts of control systems | Software requirements for PL path functions (PLa–PLd). Simplified software approach applicable. See Section 2A. |

This standard implements the software architecture requirements of IEC 61508-3 and IEC 61511-1 Clause 12 for PLC-based industrial control and safety systems, and the ISO 13849-1 software requirements for PL path safety functions.

For the complete list of standards referenced across this framework, see the Safety Documentation Standard (`00_Safety_Documentation_Standard`), Section 3.

---
# 2A. Software Requirements by Pathway

The applicable software standard depends on the governing standard declared for the safety function at the HA level:

| Safety Function Path | Governing Standard | Integrity Target | Software Standard |
|----------------------|--------------------|-----------------|-------------------|
| SIL path | IEC 61511 / IEC 62061 | SIL 1–3 | IEC 61508-3 rigor applies |
| PL path | ISO 13849 | PLa–PLd | ISO 13849-1 simplified software approach applicable |
| PL path (high demand) | ISO 13849 | PLe | IEC 61508-3 rigor applies (PLe corresponds to SIL 3 equivalent) |

**ISO 13849-1 Simplified Software Approach (PLa–PLd):**

For safety functions on the PL path with PLr of PLa through PLd, ISO 13849-1 permits a simplified software approach. Key requirements:
- Software shall be validated and documented
- Source code shall be available for review
- Embedded software (firmware) in safety-rated components (e.g., safety relay controllers) is validated by the component manufacturer; project-specific application code covering PL path logic shall follow structured programming practices
- No formal V&V cycle (as required for IEC 61508-3 SIL 1–3) is mandated, but functional testing shall be performed and recorded

**IEC 61508-3 Requirements (SIL path, or PLe):**

For any safety function on the SIL path (SIL 1–3) or a PLe function, the full IEC 61508-3 software safety lifecycle applies. This includes:
- Software safety requirements specification
- Software architectural design
- Software module design and coding
- Integration testing
- Software validation
- Coding standards (prohibited language constructs, defensive programming)

**Mixed projects:** In a project containing both SIL and PL safety functions, the software architecture shall clearly separate the application code implementing each function. SIL path code and PL path code may reside in different program organization units (POUs) within the same PLC, provided the separation is documented and the SIL path code is developed to IEC 61508-3 rigor throughout.

---
# 3. Lifecycle Integration

Updated lifecycle:

Hazard → SRS → Drawings → Software → FMEA → FAT/SAT → Proof Tests (where inherent DU exists)

Drawings, software, and FMEA iterate until testing succeeds.  
All good design is iterative.

---
# 4. Determinism First

Determinism is a primary design constraint.

The control core shall:
- Have bounded execution time
- Have defined execution order
- Avoid asynchronous control dependencies
- Produce repeatable outputs for repeatable inputs

State machines are the preferred sequencing method.

Service-oriented or asynchronous architectures are prohibited in the control core unless bounded latency and execution order are proven.

---
# 5. Deterministic Actuation Gateway

HMI (Human-Machine Interface)/SCADA (Supervisory Control and Data Acquisition) are non-deterministic interfaces.

Any action causing motion or state change must pass through a deterministic gateway.

Examples:
- Hardwired Start/Reset/Acknowledge pushbuttons
- Key switches / mode selectors
- Safety-rated reset circuits

HMI issues requests only.  
Modules decide if actuation is allowed.

---
# 6. HMI Action Tiers

## Tier 0 – Informational
Viewing data only.

## Tier 1 – Low consequence
Alarm acknowledge, minor tuning.

## Tier 2 – Operational influence
Setpoints, recipe selection, limits, ramps.

Must use **Staged → Committed parameter pattern**.

## Tier 3 – Actuation
Start/Stop/Reset/Bypass.

Requires deterministic confirmation.

---
# 7. Staged → Committed Parameter Pattern

Parameters are:
- Staged (HMI writes)
- Committed (control uses)

Transfer from staged → committed requires deterministic confirmation.

---
# 8. Software Layering

Layer 0 – Signals (I/O)  
Layer 1 – Device Objects  
Layer 2 – Sheet Modules (primary test scope)  
Layer 3 – Virtual Control Layer

Virtual control may compute requests but never actuates hardware directly.

---
# 9. Object Model

## Device Object
Owns I/O semantics, device faults, reaction evidence.

Required parts:
- Identity (device tag)
- I/O Interface
- Command Interface
- Fault Lifecycle
- Diagnostics

## Module Object
Owns behavior derived from drawings.

Required parts:
- Identity (function tag)
- Requests/Responses
- Sequencing state machine
- Module faults
- Diagnostics

## Manager Object
Coordinates modules.

Managers:
- Issue requests only
- Never actuate hardware
- May manage other managers
- Should read like a “grocery list” of function calls

## Application Functions
Math-heavy algorithms only.
No sequencing or actuation.

---
# 10. Sheet Modules

Each testable drawing sheet shall have a primary software module.

SAT/FAT shall map to these modules.

Fault lifecycle behavior must be co-located in the owning sheet module.

---
# 11. Test Surfaces

Each module shall expose a Test Surface containing:
- Fault states
- Reaction evidence
- Reset status
- Block reasons
- Mode/state

SAT execution should require opening only the relevant Sheet Module and dependencies.

---
# 12. TRACE Tag Convention

Traceability shall use IDs only.

Example:
TRACE: SF=SF-PRES-001; FR=FR-EM-MTR-005-START-001; DWG=201

Do not duplicate requirement text in code.

---
# 13. Commissioning Reality Requirements

Architecture shall support commissioning without code hacks.

Simulation/substitution shall be:
- Mode gated
- Visible
- Traceable

Virtual control may be disabled during SAT without invalidating safety proof.
