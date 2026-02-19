# Industrial Control Software Architecture Standard

## PLC Runtime Architecture for Testable and Diagnosable Industrial Systems

**Version:** 0.1 (Draft)\
**Status:** Working Draft\
**Scope:** Recommended software architecture patterns for PLC and
embedded control systems that align runtime behavior with FMEA, FAT/SAT,
and proof testing methodology.

------------------------------------------------------------------------

# 1. Purpose and Scope

## 1.1 Purpose

This standard defines a reference architecture for PLC and embedded
control software used in industrial control systems.

The goal is to ensure that:

-   Software behavior aligns naturally with the failure lifecycle tested
    during FAT, SAT, and proof testing.
-   Failure detection, reaction, reset behavior, and recovery are
    explicit and inspectable.
-   Failure modes identified in the FMEA map directly to software
    constructs.
-   Testing becomes an exercise of designed behavior rather than a
    procedural ritual.

This standard converts commonly held tribal knowledge into a repeatable
and teachable architecture.

------------------------------------------------------------------------

## 1.2 Relationship to Other Standards

This document extends the Industrial Systems Documentation suite by
introducing the software layer of the lifecycle.

Updated lifecycle:

Hazard Analysis → SRS → Drawings → Software → FMEA → FAT/SAT → Proof
Tests

Software, drawings, and FMEA are peer disciplines that iterate together
until testing is successfully completed.

Failures discovered during testing or operation may trigger iteration
anywhere in the loop.

All good design is iterative.\
This architecture exists to shorten and structure iteration, not
eliminate it.

------------------------------------------------------------------------

## 1.3 Scope

This standard applies to:

-   PLC control software
-   Safety and non-safety control systems
-   Equipment control modules
-   Skid and machine control
-   Process control logic

This standard defines:

-   Software architecture patterns
-   Fault lifecycle modeling
-   Mode and state structure
-   Reset and recovery philosophy
-   Diagnostics and testability requirements

This standard does NOT define:

-   Programming language conventions
-   Naming conventions
-   HMI design standards
-   Cybersecurity requirements
-   Vendor-specific implementations

------------------------------------------------------------------------

# 2. Design Philosophy

## 2.1 Iterative Co-Design

Industrial control systems are not developed sequentially.

Drawings, software, and FMEA iterate together until testing is complete.

If testing reveals deficiencies: - Software may change - Drawings may
change - FMEA may change

If new hazards are discovered, the lifecycle restarts.

Iteration is expected and necessary.

The purpose of this architecture is to make iteration predictable and
efficient.

------------------------------------------------------------------------

## 2.2 Hardware--Software Co-Design

Industrial control systems are integrated electromechanical systems.

Sensors, wiring, logic, actuators, diagnostics, and operator interfaces
form a single system.

Hardware and software shall be designed together.

Neither discipline shall assume the other has solved a problem.\
Neither discipline shall assume the other must solve a problem.

Solutions frequently require both hardware and software elements.

Diagnostics and testability often require hardware signals such as: -
Feedback contacts - Limit switches - Status words - Redundant signals

Electrical design and software architecture must support each other.

------------------------------------------------------------------------

## 2.3 Testability-First Design

The FMEA defines how the system can fail.\
The FAT/SAT standard defines how failures are tested.

Software shall be structured so the tested behavior exists by design.

The system shall naturally support verification of:

1.  Detection\
2.  Reaction\
3.  Persistence\
4.  Reset lockout\
5.  Recovery

Testing shall exercise designed states rather than rely on operator
procedure.

------------------------------------------------------------------------

# 3. Architectural Overview

PLC software shall be structured using two interacting models:

### 1) Control State Model

Describes what the system is trying to do.

Examples: - STOPPED - STARTING - RUNNING - STOPPING - MAINTENANCE

### 2) Fault Lifecycle Model

Describes how failures are handled.

These models are separate but coupled.

Control states may only advance when the fault lifecycle allows it.

------------------------------------------------------------------------

# 4. Core Pattern Catalog

## Pattern 1 --- Fault Object

### Intent

Represent each failure presentation as a first-class software object.

### Required Behavior

Each fault shall support the lifecycle:

-   Present
-   Reacted
-   Latched
-   Clearable
-   Reset Pending
-   Recovered

### Required Signals

Each fault object shall include:

-   ConditionPresent
-   ReactionComplete
-   Latched
-   ResetRequest
-   ResetAllowed
-   Cleared
-   AlarmActive

Faults shall not be implemented as simple boolean bits.

------------------------------------------------------------------------

## Pattern 2 --- Reset Gate

### Intent

Prevent unsafe or premature reset.

### Rules

Reset shall be a request, not an immediate action.

Reset shall only succeed when:

1.  Fault condition no longer present\
2.  Safe reaction achieved\
3.  Operator reset performed

Automatic reset is prohibited.

------------------------------------------------------------------------

## Pattern 3 --- Reaction Evidence

### Intent

Verify that commanded safe actions actually occurred.

Protective actions shall provide confirmation signals when practical.

Examples: - Motor stopped feedback - Valve closed limit switch - Relay
feedback contact - Drive status word

The system shall verify reaction completion before allowing reset.

------------------------------------------------------------------------

## Pattern 4 --- Mode and Fault Separation

Operational mode logic and fault logic shall be separate.

Faults shall guard transitions between modes.

Example rule:

STOPPED → RUNNING allowed only if no blocking faults.

------------------------------------------------------------------------

## Pattern 5 --- Detection-Point Aggregation

Multiple physical root causes that produce the same observable failure
shall be represented by a single software fault.

Example:

"Signal Low" may represent: - Transmitter failure - Cable open - I/O
failure

------------------------------------------------------------------------

# 5. Canonical Example --- Motor Control

### Faults

-   Start failure
-   Run feedback lost
-   Overload trip
-   Emergency stop active

### Reaction Evidence

-   Run feedback contact
-   Drive running status
-   Contactor auxiliary contact

### Reset Gate Behavior

Motor cannot restart until: - Stop confirmed - Fault cleared - Operator
reset performed

------------------------------------------------------------------------

# 6. Implementation Checklist

-   All failure presentations implemented as Fault Objects
-   Reset gated by condition removal and reaction evidence
-   Control states separated from fault states
-   Protective actions verified by feedback where practical
-   Diagnostic information available to operator interface

------------------------------------------------------------------------

**End of Draft v0.1**
