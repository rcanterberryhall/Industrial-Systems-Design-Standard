# Safety Documentation Standard
## Integrated Industrial System Lifecycle Framework

Status: Draft
Last Updated: 2026-02-20

---

# 1. Methodology Overview

This framework defines an integrated engineering lifecycle for industrial systems that unifies:

- Hazard Analysis
- Safety Requirements Specification (SRS)
- Drawing-Based Design
- FMEA (Architecture and Detailed)
- Software Architecture
- FAT / SAT
- Startup & Commissioning
- Proof Testing
- Operational Governance

The methodology is built on five core principles:

1. Hazards drive requirements.
2. Requirements drive architecture.
3. Drawings are the navigation backbone of implementation — not the origin of safety intent.
4. FMEA is a design lens, not a verification afterthought.
5. Commissioning is part of the design lifecycle.

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
Operation → Proof Test Cycle  

## 2.1 PDR – Preliminary Design Review (End of Concept Design)

Verifies:
- Hazard Analysis complete
- Safety Functions identified
- Initial SRS drafted
- High-level architecture defined
- SIL targets assigned

Purpose:
Confirm the concept can meet safety requirements.

## 2.2 CDR – Critical Design Review (End of Preliminary Design)

Verifies:
- Architecture-level FMEA complete
- Diagnostic strategy defined
- Safe states and reset philosophy defined
- Startup gate model defined
- Software architecture defined

Purpose:
Confirm the architecture can achieve safety and SIL intent.

## 2.3 DDR – Detailed Design Review (End of Detail Design)

Verifies:
- Detailed drawings complete
- Detailed FMEA refinement complete
- Proof test procedures derived
- FAT/SAT procedures complete
- Deterministic gateways implemented in software

Purpose:
Confirm implementation matches safety design intent.

## 2.4 Operational Readiness Review

Verifies:
- FAT/SAT items required for startup gates complete
- Temporary safeguards documented
- Validation levels achieved

## 2.5 PSSR – Pre-Startup Safety Review

Verifies:
- All required startup gates passed
- All safety documentation complete
- No uncontrolled bypasses active
- Proof testing defined and scheduled

---

# 3. IEC 61511 Alignment Mapping

This framework is structured to align with IEC 61511 (Part 1) without reproducing standard text.

| Framework Phase | IEC 61511 Clause Reference |
|----------------|---------------------------|
| Hazard Analysis | §8 – Hazard and Risk Assessment |
| Safety Requirements Specification (SRS) | §10 – Safety Requirements Specification |
| Architectural Design (PD) | §11 – Safety Instrumented System Design |
| Detailed Design (DD) | §12 – Design and Engineering of SIS |
| FAT | §14 – Installation, Commissioning and Validation |
| SAT | §14 – Validation |
| Startup & PSSR | §15 – Safety Validation |
| Operation & Maintenance | §16 – Operation and Maintenance |
| Proof Testing | §16.3 – Proof Testing |
| Modification Management | §17 – Management of Change |

This mapping provides audit traceability between the methodology and recognized functional safety practice.

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
| Hazard Analysis | Complete — HAZOP, SFs, SIL targets; no drawing references | Stable — referenced by SRS and FMEA; no substantive changes expected | Frozen — changes require formal MOC |
| SRS | Intent defined — functional requirement, SIL target, preliminary response requirement | Architecture defined — proposed voting, preliminary PFDavg, beta assumptions, proof test interval | Verified — final hardware selected, final PFDavg confirmed, SIL formally demonstrated |
| FMEA | Concept sketch — high-level architecture risk, obvious single-point failures; no math | Architecture-level — all detectable vs. undetectable paths identified; designable DU eliminated; architecture iterated until viable | Detailed — device-specific failure rates, vendor data, MTTR, proof test coverage; no designable DU permitted |
| Drawings | Block diagrams — functional intent only; no device tags, no wiring | Architecture-level — device tags assigned, feedback loops and diagnostics provisioned, still flexible | Fully detailed — final wiring, terminal numbers, wire numbers, SF references in title blocks |
| Software | Not yet present | Module structure defined, deterministic gateway rules established, object model defined | Full implementation, deterministic enforcement active, full test surfaces exposed |
| FAT / SAT | Not yet present | Outline derived from architecture; scope defined | Final procedures derived from FMEA detection entries, drawing sheets, and SRS requirements |

## 5.3 Concept Design (CD)

**Authority document:** `01_Hazard_Analysis_Standard`

**Purpose:** Define the problem and establish the required risk reduction.

### Hazard Analysis at CD — `01_Hazard_Analysis_Standard`

- HAZOP complete
- Safety functions identified with SIL targets
- `HA-XXX-NNN` entries produced
- `SF-XXX-NNN` identifiers assigned
- No drawing sheet references — implementation does not yet exist

### SRS at CD — `02_SRS_Standard`

Functional intent only. The CD-maturity SRS answers: *what must this function achieve?*

- Functional requirement stated (what the safety function must do)
- SIL target
- Preliminary proof test interval (T_I)
- No hardware selection
- No detailed architecture
- No PFDavg math beyond high-level feasibility check

### FMEA at CD — `04_FMEA_Standard`

No formal FMEA exists at CD. A concept-level sketch may flag obvious single-point failure paths that would prevent SIL achievement, but no worksheet is produced and no calculations are performed.

### Drawings at CD — `03_Industrial_Systems_Drawing_Standard`

Block diagrams only. Functional intent shown. No device tags, no sheet numbers, no wiring.

### Software at CD — `05_Industrial_Control_Software_Architecture_Standard`

Conceptual architecture only. No module structure, no implementation.

### CD Exit Gate — PDR

**Gate question:** Can this system, in principle, achieve the required risk reduction?

At PDR the team can state:

- What hazards exist and what risk reduction is required
- What SIL target is assigned to each safety function
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

### SRS at PD — `02_SRS_Standard`

The SRS owns the math at PD. If the architecture does not achieve SIL, the SRS drives the architecture change.

- Architecture selected (e.g., 2oo3 voting)
- Target T_I confirmed
- Preliminary PFDavg calculation
- Beta factor (CCF) assumptions
- Hardware fault tolerance (HFT) validation
- Architectural constraint checks (Route 1H / Route 2H)

### Architecture-Level FMEA at PD — `04_FMEA_Standard`

The FMEA formally exists at PD. Its purpose is not to calculate final PFDavg — it is to force architectural decisions.

At PD the FMEA must produce:

- Detection classification for every failure path (DD vs. DU)
- Identification of all **designable DU** — failures that are undetected because the architecture lacks the means to detect them, and which can be made detectable by adding feedback contacts, diagnostic outputs, or monitoring capability
- Specification of detection additions required (fed back into drawings)
- Definition of system reaction for each DD failure
- Feedback loop definitions
- Reset philosophy and safe state per safety function

**Convergence criterion for CDR:** All designable DU resolved. Remaining DU justified as inherent — a physical property of the device, not a consequence of architectural omission.

### Drawings at PD — `03_Industrial_Systems_Drawing_Standard`

- Sheet numbers assigned
- Device tags assigned
- Feedback contacts provisioned (per FMEA requirements)
- Diagnostics provisioned
- Architecture defined; wiring details still flexible

### Software Architecture at PD — `05_Industrial_Control_Software_Architecture_Standard`

- Object model defined
- Deterministic gateway rules defined
- Sheet modules mapped to drawing sheet numbers

### PD Exit Gate — CDR

**Gate question:** Does this architecture achieve the SIL target, and is the diagnostic strategy complete?

CDR exit criteria:

- **All designable DU resolved. Remaining DU justified as inherent.**
- Architecture mathematically achieves SIL target (preliminary PFDavg < target)
- Every DD failure mode has a defined detection mechanism and system reaction
- Reset philosophy defined
- Safe state defined for each safety function
- Software architecture defined and consistent with hardware architecture

CDR is not a hardware validation. It is an architecture validation. The team is confirming that the design *as conceived* is capable of achieving the required integrity — before committing to detailed implementation.

## 5.5 Detailed Design (DD)

**Purpose:** Lock the design. Replace architecture with implementation.

DD is refinement, not architecture. No new architectural decisions are made in DD.

### SRS at DD — `02_SRS_Standard`

- Final hardware selected
- Final PFDavg calculation using device-specific failure rate data
- Final T_I confirmed
- Formal SIL demonstration — PFDavg < target

### FMEA at DD — `04_FMEA_Standard`

- Device-level failure rates from vendor safety manuals
- MTTR confirmed
- Proof test coverage calculated per derived procedure
- All DU classified as inherent

**No designable DU is permitted at DD.** A DU that surfaces at DD that could have been eliminated by architectural change is a CDR failure — it must be escalated, not accepted.

Proof test procedures are derived from the DD FMEA. Each DU failure mode maps to one or more proof test steps in the PT procedure.

### Drawings at DD — `03_Industrial_Systems_Drawing_Standard`

- Final wiring complete
- Terminal numbers assigned
- Wire numbers assigned
- SF references (`SF-XXX-NNN`) in title blocks of all safety-critical sheets

### Software at DD — `05_Industrial_Control_Software_Architecture_Standard`

- Full implementation
- Sheet modules complete
- Deterministic enforcement active on all motion-producing outputs
- Full test surfaces exposed for FAT/SAT

### FAT/SAT at DD — `06_SAT_FAT_Standard`

FAT/SAT procedures derived from:

- FMEA detection entries — each DD failure mode → fault injection test
- Drawing sheet modules — scope, device tags, wire numbers
- SRS requirements — setpoints, response times, voting behaviour, reset conditions

Fault lifecycle sequence enforced on every safety test step: establish normal → induce fault → verify reaction → confirm no reset while fault active → remove fault → verify no auto-restart → reset → verify recovery.

Procedures are complete before construction begins.

### DD Exit Gate — DDR

**Gate question:** Does the implementation match architectural intent and satisfy SRS integrity requirements?

DDR exit criteria:

- PFDavg < SIL target confirmed with device-specific data
- All DU classified as inherent — no designable DU remaining
- Proof test procedures derived and coverage assumptions validated
- FAT/SAT procedures complete and traceable to FMEA and drawings
- No unresolved diagnostic gaps
- Deterministic enforcement implemented in software

After DDR: construction-ready. All changes require formal MOC.

## 5.6 Commissioning Phase — `07_Startup_and_Commissioning_Standard`

The Startup and Commissioning Standard activates after DDR.

Commissioning does not change design intent. It validates execution — bottom-up, through defined Validation Levels (0–7) and Startup Gates (A–E). FAT/SAT records are the primary evidence consumed by gate passage decisions.

Commissioning is the answer to: *was the design built correctly?* The design phase answered: *is the design correct?* These are distinct questions and must not be conflated.

---

# End Safety Documentation Standard
