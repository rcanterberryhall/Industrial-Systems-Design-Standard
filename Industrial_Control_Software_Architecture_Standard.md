
# Industrial Control Software Architecture Standard  
## PLC Runtime Architecture for Testable and Diagnosable Industrial Systems

**Version:** 0.2 (Draft)  
**Status:** Working Draft

---
# 1. Purpose

This standard defines a reference PLC software architecture that:

- Aligns runtime behavior with drawings, FMEA, FAT/SAT, and proof testing
- Preserves determinism required for machine control
- Reduces tribal knowledge and commissioning friction
- Enables repeatable, testable machine software

Drawings remain the **source of truth**.  
Software is a projection of the drawings.

---
# 2. Lifecycle Integration

Updated lifecycle:

Hazard → SRS → Drawings → Software → FMEA → FAT/SAT → Proof Tests

Drawings, software, and FMEA iterate until testing succeeds.  
All good design is iterative.

---
# 3. Determinism First

Determinism is a primary design constraint.

The control core shall:
- Have bounded execution time
- Have defined execution order
- Avoid asynchronous control dependencies
- Produce repeatable outputs for repeatable inputs

State machines are the preferred sequencing method.

Service-oriented or asynchronous architectures are prohibited in the control core unless bounded latency and execution order are proven.

---
# 4. Deterministic Actuation Gateway

HMI/SCADA are non-deterministic interfaces.

Any action causing motion or state change must pass through a deterministic gateway.

Examples:
- Hardwired Start/Reset/Acknowledge pushbuttons
- Key switches / mode selectors
- Safety-rated reset circuits

HMI issues requests only.  
Modules decide if actuation is allowed.

---
# 5. HMI Action Tiers

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
# 6. Staged → Committed Parameter Pattern

Parameters are:
- Staged (HMI writes)
- Committed (control uses)

Transfer from staged → committed requires deterministic confirmation.

---
# 7. Software Layering

Layer 0 – Signals (I/O)  
Layer 1 – Device Objects  
Layer 2 – Sheet Modules (primary test scope)  
Layer 3 – Virtual Control Layer

Virtual control may compute requests but never actuates hardware directly.

---
# 8. Object Model

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
# 9. Sheet Modules

Each testable drawing sheet shall have a primary software module.

SAT/FAT shall map to these modules.

Fault lifecycle behavior must be co-located in the owning sheet module.

---
# 10. Test Surfaces

Each module shall expose a Test Surface containing:
- Fault states
- Reaction evidence
- Reset status
- Block reasons
- Mode/state

SAT execution should require opening only the relevant Sheet Module and dependencies.

---
# 11. TRACE Tag Convention

Traceability shall use IDs only.

Example:
TRACE: SF=SF-PRES-001; FR=FR-EM-MTR-005-START-001; DWG=201

Do not duplicate requirement text in code.

---
# 12. Commissioning Reality Requirements

Architecture shall support commissioning without code hacks.

Simulation/substitution shall be:
- Mode gated
- Visible
- Traceable

Virtual control may be disabled during SAT without invalidating safety proof.

---
# End Draft v0.2
