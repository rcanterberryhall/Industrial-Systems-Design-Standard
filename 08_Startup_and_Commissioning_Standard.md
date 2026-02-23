
# Startup and Commissioning Standard
## Structured Validation and Operational Gating for Industrial Systems

**Status:** Draft

---

# 1. Purpose

This standard defines a structured, staged startup and commissioning process
for industrial control systems.

Commissioning is not a post-design activity.
Commissioning is part of the design lifecycle.

This document establishes:

- Bottom-up technical validation order
- Startup gates (operational envelopes)
- Alignment with Drawings, Software, FMEA, FAT/SAT, and PSSR
- Rules for deferred scope and temporary safeguards
- A feedback loop from commissioning into design

---

# 2. Standards References

| Standard | Title | Application |
|----------|-------|-------------|
| IEC 61511-1 | Functional safety — Safety instrumented systems for the process industry | Clauses 14–15 — installation, commissioning, validation, and pre-startup safety review |
| IEC 62382 | Automation systems in the process industry — Electrical and instrumentation loop checking | Loop check methodology as prerequisite to commissioning |
| IEC 62337 | Commissioning of electrical, instrumentation and control systems in the process industry | Structured commissioning process for process automation systems |

This standard implements the commissioning and validation requirements of IEC 61511-1 Clauses 14–15 and the structured commissioning methodology of IEC 62337.

For the complete list of standards referenced across this framework, see the Safety Documentation Standard (`00_Safety_Documentation_Standard`), Section 3.

---

# 3. Commissioning as a Design Activity

Commissioning requirements shall be considered during design.

The following must be defined before startup:

- Startup gates
- Minimum validation levels for each gate
- Required FAT/SAT coverage per gate
- Commissioning modes in software
- Deterministic gateways for actuation
- Temporary safeguard handling rules

Software architecture shall support staged commissioning.

---

# 4. Bottom-Up Validation Order

Systems shall be validated from foundational layers upward.

Validation shall proceed in the following order unless explicitly justified otherwise:

## Level 0 – Power High
- Verify mains supply, phase rotation, grounding
- Confirm protective devices
- Confirm no unintended motion on energization

## Level 1 – Power Low
- Verify control power integrity (24V, UPS (Uninterruptible Power Supply), etc.)
- Confirm safe default PLC (Programmable Logic Controller) boot state
- Confirm safety circuits de-energize outputs

## Level 2 – I/O Transport
- Verify I/O module communication health and diagnostics
- Confirm PLC I/O addressing matches drawings (software configuration, not wiring — wiring is verified by point-to-point before this stage)

## Level 3 – Sensors
- Validate scaling and plausibility
- Confirm sensor fault detection
- Verify quality propagation where required

## Level 4 – Output Relays and Safety Output Chains
- Verify relay/contactor actuation
- Verify feedback contacts (reaction evidence)
- Verify reset gating behavior

## Level 5 – Output Interfaces
- Validate analog outputs and communication-based outputs
- Confirm fail-safe behavior on loss of control signal

## Level 6 – Drive Controls (Jog)
- Validate STO (Safe Torque Off) and enable logic
- Verify jog functionality with bounded limits
- Confirm stop and reaction evidence behavior

## Level 7 – Drive Controls (Profile)
- Validate ramps, motion profiles, coordinated motion
- Enable higher-level control algorithms as appropriate

Higher validation levels shall not proceed until lower levels are stable and repeatable.

---

# 5. Startup Gates (Operational Envelope Model)

Startup Gates define what level of operation is permitted.

Validation Levels prove technical readiness.
Startup Gates authorize operational behavior.

Example gate structure:

## Gate A – Energization
- Power applied only
- No motion allowed

## Gate B – Safe Motion
- Limited manual or jog motion
- Safety envelope proven
- Deterministic gateways validated

## Gate C – Module Operation
- Individual modules operational
- Local sequencing allowed
- Integration disabled or limited

## Gate D – Integrated Operation
- Coordinated systems enabled
- Reduced speed or throughput limits
- Virtual control layer partially enabled

## Gate E – Full Production
- All operational modes enabled
- All safety SAT items complete
- All functional FAT/SAT items complete (per `01_Functional_Requirements_Standard`)
- No temporary safeguards active

Each gate shall define:

- Allowed operating envelope
- Required validation level
- Required FAT/SAT completion
- Required documentation state
- Required sign-off authority

---

# 6. Alignment with FAT and SAT

Safety FAT and SAT test cases are produced per the SAT/FAT Standard (`07_SAT_FAT_Standard`). Functional FAT/SAT test cases are produced per the Functional Requirements Standard (`01_Functional_Requirements_Standard`). Both functional and safety test results are required evidence for gate passage.

For commissioning tracking purposes, each test case should record:

- Drawing Sheet reference (already required by FAT/SAT Standard)
- Primary Software Module
- Validation Level completed at the time of testing
- Minimum Startup Gate this test unlocks or satisfies

These commissioning tracking fields are recorded in the commissioning register, not in the FAT/SAT procedure itself.

Startup shall not rely on informal test completion.

Gate passage requires documented completion of required tests.

---

# 7. Alignment with Software Architecture

Software shall support commissioning by:

- Exposing Test Surfaces at Sheet Modules
- Exposing fault lifecycle status
- Exposing reset gating status
- Supporting commissioning modes explicitly
- Preventing virtual control layers from bypassing module safety logic

Virtual control layers may be disabled during early startup gates.

---

# 8. Temporary Safeguards and Deferred Scope

Deferred scope is permitted only if:

- It is not required for the current gate envelope, or
- A temporary safeguard exists and is documented

Temporary safeguards must:

- Be visible in software and/or physically
- Have an assigned owner
- Have an expiration or removal criterion
- Require re-test upon removal

No undocumented bypasses are permitted.

---

# 9. Feedback Loop into Design

Commissioning discoveries shall trigger review of:

- Drawings
- Software
- FMEA
- FAT/SAT procedures
- Safety documentation

Commissioning changes are design changes.

All changes shall follow formal change control procedures.

---

# 10. Transition to PSSR

Final startup authorization (PSSR) shall confirm:

- All required startup gates have been passed
- All temporary safeguards removed or formally accepted
- All required SAT items complete
- Proof test procedures defined and scheduled

PSSR is the final operational release gate.

---

