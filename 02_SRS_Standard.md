# Safety Requirements Specification Standard
## SRS Methodology for Safety Instrumented Functions

**Status:** Draft
**Scope:** Methodology for producing a Safety Requirements Specification (SRS) for industrial control systems. Defines the one-per-project SRS document structure, SF entry format, and all reliability calculation methods (PFDavg, SIL verification, CCF/beta analysis) used to design safety instrumented functions to their required SIL target.

---

## Table of Contents

1. [Purpose and Scope](#1-purpose-and-scope)
2. [Standards References](#2-standards-references)
3. [Definitions and Terminology](#3-definitions-and-terminology)
4. [Numbering and Identification](#4-numbering-and-identification)
5. [SRS Entry Structure](#5-srs-entry-structure)
6. [Reliability Calculations](#6-reliability-calculations)
7. [Traceability](#7-traceability)
8. [Lifecycle and Review](#8-lifecycle-and-review)
9. [Implementation Checklist](#9-implementation-checklist)

---

## 1. Purpose and Scope

### 1.1 Purpose

This standard defines the methodology for producing and maintaining a Safety Requirements Specification (SRS) for industrial control system projects. The SRS is the bridge between the Hazard Analysis (HA) — which identifies what must be protected against — and the FMEA and drawings — which define and verify how that protection is implemented.

The SRS answers three questions for every identified safety function:

1. **What must the safety function do?** (functional requirements: setpoints, voting, response time, reset)
2. **How well must it do it?** (integrity requirements: SIL, PFDavg, proof test interval)
3. **How is it built?** (architecture: sensor voting, HFT, separation, implementing sheets)

This standard also contains the authoritative reliability calculation methodology — PFDavg formulas, SIL verification, and common cause failure analysis — which belong here because they are design-intent mathematics used to specify and verify that the SRS integrity targets are achievable.

### 1.2 Scope

**One SRS document is produced per project.** The SRS document contains one entry per safety function. Each entry is identified by `SF-XXX-NNN`, matching the safety function identifier assigned during the HA/LOPA study.

This standard applies to:

- Production of SRS entries for all safety instrumented functions identified through HAZOP and LOPA
- PFDavg and SIL verification calculations supporting each SF entry
- Common cause failure (CCF) analysis and beta factor scoring
- Architectural constraint verification per IEC 61508-2
- Proof test interval determination

This standard does **not** cover:

- HAZOP and LOPA methodology — see the Hazard Analysis Standard
- FMEA worksheet structure — see the FMEA Standard (the FMEA consumes SRS entries as input and verifies the hardware achieves the targets set here)
- Electrical drawing conventions — see the Industrial Systems Drawing Standard

### 1.3 Design Philosophy

**The SRS owns the maths.** Failure rate calculations, PFDavg formulas, architectural constraint checks, and beta factor scoring are design-intent activities. They define what the design must achieve before any hardware is selected or analyzed. Placing them in the SRS — not the FMEA — keeps the intent separate from the verification. The FMEA checks whether the physical hardware matches the SRS targets; it does not define those targets.

**One document, many entries.** The SRS is not a per-function document — it is a project-level register. HA entry `HA-PRES-001` and SRS entry `SF-PRES-001` are entries within their respective project documents, not standalone files. This matters for document control: one revision history, one approval cycle, one document register entry per project.

**The SRS is the authority for proof test intervals.** The proof test interval (T_I) appears in the SRS, in the FMEA (as a calculation input), in the drawing title block, and in the proof test procedure. If these ever disagree, the SRS value governs. Changes to T_I require an SRS revision followed by FMEA recalculation.

---

## 2. Standards References

| Standard | Title | Application |
|----------|-------|-------------|
| IEC 61511-1 | Functional safety — Safety instrumented systems for the process industry | SRS requirements (Clause 10), SIL targets, proof testing |
| IEC 61511-2 | Functional safety — Guidelines for the application of IEC 61511-1 | Practical guidance for SRS preparation |
| IEC 61508-1 | Functional safety — General requirements | Safety lifecycle, SIL framework |
| IEC 61508-2 | Functional safety — Requirements for E/E/PE safety-related systems | PFDavg formulas, SFF, architectural constraints (Route 1H) |
| IEC 61508-6 | Functional safety — Guidelines on the application of Parts 2 and 3 | PFDavg calculation annexes, beta factor scoring (Annex D) |
| Hazard Analysis Standard | HAZOP and LOPA methodology | Source of SF-XXX-NNN identifiers, SIL targets, HA-XXX-NNN references |
| FMEA Standard | Failure Modes and Effects Analysis | Consumes SRS entry data; verifies hardware achieves SRS targets |

---

## 3. Definitions and Terminology

Terms used in this standard are consistent with the FMEA Standard definitions. Key terms:

| Term | Symbol | Definition |
|------|--------|------------|
| Probability of Failure on Demand (average) | PFDavg | The time-averaged probability that the safety function will fail to perform on demand. Primary metric for low-demand-mode SIFs. |
| Probability of Dangerous Failure per Hour | PFH | Failure rate metric for high-demand or continuous-mode SIFs (demand rate > 1 per year). |
| Dangerous Failure Rate | lambda_D | Total rate of failures that prevent the safety function from acting on demand. |
| Dangerous Undetected | lambda_DU | Dangerous failures not detected by automatic diagnostics; revealed by proof test or demand. |
| Dangerous Detected | lambda_DD | Dangerous failures detected automatically; repair can begin within MTTR. |
| Mean Time to Restoration | MTTR | Average time from detection of a dangerous detected failure to restoration of the function. |
| Proof Test Interval | T_I | Maximum time between comprehensive proof tests. A critical parameter in PFDavg. |
| Common Cause Failure | CCF | Simultaneous failure of multiple redundant channels from a single shared cause. |
| Beta Factor | beta | Fraction of dangerous undetected failures that are common cause (affect all redundant channels simultaneously). |
| Safe Failure Fraction | SFF | Fraction of total failure rate that is safe or dangerous-detected: SFF = (lambda_SD + lambda_SU + lambda_DD) / (lambda_total). |
| Hardware Fault Tolerance | HFT | Number of hardware faults tolerable before the safety function is lost. HFT=1 means two simultaneous faults are needed to cause loss. |
| Safety Integrity Level | SIL | Discrete level (1–3 per IEC 61511) representing required SIF reliability. |

### 3.1 SIL Definitions (Low Demand Mode, per IEC 61508/61511)

| SIL | PFDavg Range | Risk Reduction Factor |
|-----|-------------|----------------------|
| SIL 1 | ≥ 10⁻² to < 10⁻¹ | 10 to 100 |
| SIL 2 | ≥ 10⁻³ to < 10⁻² | 100 to 1,000 |
| SIL 3 | ≥ 10⁻⁴ to < 10⁻³ | 1,000 to 10,000 |

**Note:** SIL 4 is not addressed in IEC 61511 for the process industry. If a LOPA study indicates SIL 4 is required, the design shall be revisited to reduce inherent risk or add non-SIS protection layers.

---

## 4. Numbering and Identification

### 4.1 SRS Document ID

**Format:** `SRS-[Project]`

The SRS is a single project-level document. Its identifier is the project code, not a function code. Example: `SRS-RefineryXYZ`.

### 4.2 SRS Entry ID

**Format:** `SF-XXX-NNN`

Each safety function entry within the SRS is identified by the safety function identifier assigned in the HA/LOPA study. The same `SF-XXX-NNN` identifier is used throughout the documentation suite — in the HA, in the SRS, on drawing title blocks, in the FMEA scope, and in SAT/PT documents.

| Component | Description | Example |
|-----------|-------------|---------|
| `SF` | Safety Function prefix | SF |
| `XXX` | System abbreviation code (see Section 4.3) | PRES |
| `NNN` | Sequential safety function number within that system | 001 |

**Examples:**

- `SF-PRES-001` → Safety Function for Pressure system, first function (SRS entry within SRS-RefineryXYZ)
- `SF-TEMP-002` → Safety Function for Temperature system, second function
- `SF-LEV-001` → Safety Function for Level system, first function

### 4.3 System Abbreviation Codes

| Code | System | Examples |
|------|--------|----------|
| PRES | Pressure protection | Overpressure, underpressure, relief |
| TEMP | Temperature protection | High temperature, thermal runaway |
| FLOW | Flow protection | Low flow, reverse flow, overflow |
| LEV | Level protection | High level, low level, overflow |
| FIRE | Fire and gas detection | Fire detection, gas detection |
| TOX | Toxic release protection | H2S, CO, toxic gas |
| COMB | Combustible gas protection | LEL monitoring, explosion prevention |
| COMP | Composition protection | pH, O2, concentration |
| REAC | Reaction protection | Runaway reaction, exotherm |
| MECH | Mechanical protection | Vibration, overspeed, displacement |
| ELEC | Electrical protection | Arc flash, ground fault, overload |
| ENV | Environmental protection | Spill containment, emissions |

---

## 5. SRS Entry Structure

### 5.1 Required Fields per Entry

Each SF-XXX-NNN entry within the SRS document shall contain all of the following fields:

| Section | Content Required |
|---------|-----------------|
| **Header** | SF ID (SF-XXX-NNN), SF name, SIL target, source HA entry (HA-XXX-NNN), revision |
| **Functional Requirements** | Trip setpoint(s), voting logic description, required response time (sensor to final element action), reset mode (manual/auto), bypass conditions |
| **Integrity Requirements** | SIL target, required PFDavg, proof test interval (T_I), required diagnostic coverage, maximum MTTR assumption |
| **Architecture** | Sensor subsystem (voting, device count, HFT), logic solver (redundancy, HFT), final element (redundancy, HFT), physical separation requirements |
| **Interface Requirements** | Sensor tags and sheet references, logic solver location and sheet, final elements with tag and sheet references |
| **Bypass Requirements** | Permitted bypass conditions, maximum bypass duration per SIL level, required compensating measures, authorization requirements |
| **Failure Mode Requirements** | Required safe state on demand, action on detected failure (DD alarm vs. automatic safe-state action), action on diagnostic alarm |
| **Implementing Sheets** | Drawing sheet numbers implementing this SF |
| **Traceability** | FMEA reference, SAT reference, proof test reference |

### 5.2 Worked Example: SF-PRES-001

```
SF-PRES-001: Overpressure Protection — Refinery Vessel XYZ
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Header:
  SF ID:        SF-PRES-001
  Description:  High-pressure shutdown for Vessel XYZ
  SIL Target:   SIL 3
  Source HA:    HA-PRES-001, Scenario 1
  Revision:     A

Functional Requirements:
  - Monitor vessel pressure via three independent transmitters
    (+300-B301.1, +300-B301.2, +300-B301.3; Sheet 301)
  - Trip on 2-of-3 voting at 95% of design pressure (setpoint: 285 psig)
  - De-energize safety relay (+200-K201.1) to close isolation valve XV-106
  - Response time: < 1 second from setpoint to valve closure initiation
  - Manual reset required after trip (no auto-reset permitted)
  - Channel bypass permitted for single-channel testing only (1oo2 remaining)

Integrity Requirements:
  - SIL 3: PFDavg target < 1.0E-03
  - Proof test interval: 6 months (see Section 6 calculations)
  - Required DC: ≥ 60% for sensors, ≥ 90% for logic solver
  - Maximum MTTR assumption: 8 hours

Architecture:
  - Sensor:        2oo3 voting, HFT = 1 (three independent transmitters)
  - Logic Solver:  1oo1, safety-rated PLC (HFT = 0 with SFF ≥ 90%)
  - Final Element: 1oo1, de-energize-to-trip relay (HFT = 0 with SFF ≥ 90%)

Interface Requirements:
  - Sensors:        +300-B301.1, .2, .3 — Sheet 301 (Cabinet +300)
  - Logic Solver:   Safety PLC A201.1 — Sheet 201 (Cabinet +200)
  - Final Element:  Safety Relay +200-K201.1 — Sheet 201 (Cabinet +200)
                    ESD Valve XV-106 Solenoid +300-Y301.1 — Sheet 301

Bypass Requirements:
  - Single-channel bypass permitted for proof testing
  - SIL 3 maximum bypass duration: 8 hours per channel
  - Compensating measure: manual pressure monitoring during bypass
  - Authorization: Operations Manager

Implementing Sheets: 201, 301
FMEA Reference: FMEA 201.1
SAT Reference: SAT 201
Proof Test Reference: PT-201 (6-month interval)
```

### 5.3 SRS Cover Page Format

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│               SAFETY REQUIREMENTS SPECIFICATION             │
│               SRS-RefineryXYZ                                │
│                                                              │
│  Title:    Safety Requirements Specification                 │
│  Project:  Refinery Vessel XYZ Overpressure Protection       │
│  Client:   ABC Chemical Co.                                  │
│                                                              │
│  Revision: A                                                 │
│  Date:     2025-01-20                                        │
│  Status:   Approved                                          │
│                                                              │
│  Safety Functions Defined:                                   │
│    SF-PRES-001  SIL 3  Overpressure Protection               │
│    SF-TEMP-001  SIL 2  Overtemperature Protection            │
│    SF-LEV-001   SIL 1  Level Overflow Protection             │
│                                                              │
│  Prepared By:    J. Smith (Functional Safety Engineer)       │
│  Reviewed By:    R. Jones (Process Safety Engineer)          │
│  Approved By:    T. Brown (Plant Manager)                    │
│                                                              │
│  Source Document:                                            │
│    HA Document: HA-PRES-001 Rev A (Hazard Analysis)          │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

---

## 6. Reliability Calculations

This section defines the authoritative calculation methodology for all PFDavg calculations and SIL verification. These calculations are performed during SRS development to confirm that the intended architecture is capable of achieving the SIL target before hardware is detailed. The FMEA then verifies that the actual selected hardware achieves these targets.

### 6.1 PFDavg Formulas by Architecture

The following simplified formulas are from IEC 61508-6 for low-demand mode safety functions.

**Variables:**

- `lambda_DU` = dangerous undetected failure rate (per hour) for one channel
- `lambda_DD` = dangerous detected failure rate (per hour) for one channel
- `T_I` = proof test interval (hours)
- `MTTR` = mean time to restoration for detected faults (hours)
- `beta` = common cause beta factor for undetected dangerous failures
- `beta_D` = common cause beta factor for detected dangerous failures (typically beta/2)

**1oo1 Architecture (no redundancy, HFT=0):**

```
PFDavg = lambda_DU × T_I / 2 + lambda_DD × MTTR
```

**1oo2 Architecture (parallel redundancy, HFT=1):**

```
PFDavg = (1 - beta) × (1 - beta_D) × [ (lambda_DU)² × (T_I)² / 3
         + lambda_DU × lambda_DD × MTTR × T_I
         + (lambda_DD)² × MTTR² ]
         + beta/2 × lambda_DU × T_I
         + beta_D × lambda_DD × MTTR
```

For practical purposes with MTTR << T_I, the dominant term is:

```
PFDavg ≈ (1-beta)² × (lambda_DU)² × (T_I)² / 3 + beta × lambda_DU × T_I / 2
```

**2oo3 Architecture (majority voting, HFT=1):**

```
PFDavg = (1 - beta) × (1 - beta_D) × [ 3 × (lambda_DU)² × (T_I)² / 4
         + 3 × lambda_DU × lambda_DD × MTTR × T_I
         + 3 × (lambda_DD)² × MTTR² ]
         + beta/2 × lambda_DU × T_I
         + beta_D × lambda_DD × MTTR
```

For practical purposes with MTTR << T_I, the dominant term is:

```
PFDavg ≈ (1-beta)² × 3 × (lambda_DU)² × (T_I)² / 4 + beta × lambda_DU × T_I / 2
```

### 6.2 SIL Target Table (Low Demand Mode)

| SIL | PFDavg Range | Risk Reduction Factor |
|-----|-------------|----------------------|
| SIL 1 | 1.0E-02 to < 1.0E-01 | 10 to 100 |
| SIL 2 | 1.0E-03 to < 1.0E-02 | 100 to 1,000 |
| SIL 3 | 1.0E-04 to < 1.0E-03 | 1,000 to 10,000 |
| SIL 4 | 1.0E-05 to < 1.0E-04 | Not permitted per IEC 61511 |

### 6.3 Worked Example: PFDavg Calculation for SF-PRES-001

**Given parameters:**

| Parameter | Value | Basis |
|-----------|-------|-------|
| T_I (Proof Test Interval) | 4,380 hours (6 months) | SRS-specified requirement |
| MTTR (Mean Time to Restoration) | 8 hours | Site maintenance capability |
| beta (undetected CCF factor) | 0.05 (5%) | Beta factor scoring (see Section 6.5) |
| beta_D (detected CCF factor) | 0.025 (2.5%) | beta_D = beta / 2 per IEC 61508-6 |

**Failure rate inputs** (from FMEA 201.1 once hardware is selected; shown here as design targets):

| Subsystem | Architecture | lambda_DU (/hr) | lambda_DD (/hr) |
|-----------|-------------|-----------------|-----------------|
| Sensor (per channel) | 2oo3 | 5.65E-07 | 1.41E-06 |
| Logic Solver | 1oo1 | 1.09E-07 | 6.42E-07 |
| Final Element | 1oo1 | 3.35E-08 | 2.67E-07 |

#### 6.3.1 Sensor Subsystem PFDavg (2oo3 Pressure Transmitters)

```
PFDavg_sensor = (1 - beta)² × 3 × (lambda_DU)² × (T_I)² / 4
                + beta × lambda_DU × T_I / 2
```

Calculate each term:

**Independent random failure term (DU):**
```
(1 - 0.05)² × 3 × (5.65E-07)² × (4380)² / 4
= 0.9025 × 3 × 3.19E-13 × 1.918E+07 / 4
= 0.9025 × 4.59E-06
= 4.14E-06
```

**Common cause failure term (DU):**
```
0.05 × 5.65E-07 × 4380 / 2
= 6.19E-05
```

**PFDavg_sensor ≈ 6.61E-05**

Note: The CCF term (6.19E-05) dominates. This is characteristic of redundant architectures — the beta factor limits achievable PFDavg regardless of channel count.

#### 6.3.2 Logic Solver Subsystem PFDavg (1oo1 Safety PLC)

```
PFDavg_logic = lambda_DU × T_I / 2 + lambda_DD × MTTR
PFDavg_logic = 1.09E-07 × 4380 / 2 + 6.42E-07 × 8
PFDavg_logic = 2.39E-04 + 5.14E-06
PFDavg_logic ≈ 2.44E-04
```

#### 6.3.3 Final Element Subsystem PFDavg (1oo1 Safety Relay)

```
PFDavg_final = lambda_DU × T_I / 2 + lambda_DD × MTTR
PFDavg_final = 3.35E-08 × 4380 / 2 + 2.67E-07 × 8
PFDavg_final = 7.34E-05 + 2.14E-06
PFDavg_final ≈ 7.55E-05
```

#### 6.3.4 Overall SIF PFDavg

```
PFDavg_SIF = PFDavg_sensor + PFDavg_logic + PFDavg_final
PFDavg_SIF = 6.61E-05 + 2.44E-04 + 7.55E-05
PFDavg_SIF = 3.86E-04
```

**Result: PFDavg = 3.86E-04, which is within the SIL 3 range (1.0E-04 to < 1.0E-03). PASS.**

**PFDavg budget breakdown:**

| Subsystem | PFDavg | % of Total |
|-----------|--------|-----------|
| Sensor (2oo3) | 6.61E-05 | 17.1% |
| Logic Solver (1oo1) | 2.44E-04 | 63.2% |
| Final Element (1oo1) | 7.55E-05 | 19.6% |
| **Total SIF** | **3.86E-04** | **100%** |

The logic solver is the dominant contributor. Margin to SIL 3 upper limit: (1.0E-03 − 3.86E-04) / 1.0E-03 = 61.4%.

### 6.4 Architectural Constraints (IEC 61508-2, Route 1H)

IEC 61508-2 Table 2 specifies minimum hardware fault tolerance based on SFF and SIL target. The SFF is calculated from the FMEA failure rate data.

**Safe Failure Fraction (SFF):**

```
SFF = (lambda_SD + lambda_SU + lambda_DD) / (lambda_SD + lambda_SU + lambda_DD + lambda_DU)
```

**Route 1H — Minimum HFT Requirements:**

| SFF | SIL 1 | SIL 2 | SIL 3 | SIL 4 |
|-----|-------|-------|-------|-------|
| < 60% | HFT=0 | HFT=1 | HFT=2 | Not allowed |
| 60% to < 90% | HFT=0 | HFT=0 | HFT=1 | HFT=2 |
| 90% to < 99% | HFT=0 | HFT=0 | HFT=0 | HFT=1 |
| ≥ 99% | HFT=0 | HFT=0 | HFT=0 | HFT=0 |

**Verification for SF-PRES-001 (SIL 3):**

| Subsystem | SFF | Required HFT (SIL 3) | Actual HFT | Result |
|-----------|-----|----------------------|------------|--------|
| Sensor | 83.4% (60–90% range) | HFT ≥ 1 | HFT = 1 (2oo3) | **PASS** |
| Logic Solver | 92.7% (90–99% range) | HFT ≥ 0 | HFT = 0 (1oo1) | **PASS** |
| Final Element | 93.3% (90–99% range) | HFT ≥ 0 | HFT = 0 (1oo1) | **PASS** |

**Resolution when architectural constraints fail:** If the initial analysis shows a constraint failure (e.g., a final element with SFF < 90% in a 1oo1 architecture for SIL 3), three options are available:

- **Option A: Increase redundancy** — add a second independent device in series (e.g., 1oo2 final element) to achieve HFT=1
- **Option B: Improve diagnostics** — select a device with higher DC achieving SFF ≥ 90%, allowing HFT=0 at SIL 3
- **Option C: Route 2H (prior use)** — per IEC 61511 Clause 11.5, use prior-use justification for proven-in-use devices with relaxed architectural constraints

The chosen resolution shall be documented in this SRS entry with the revised SFF calculation and verification result.

### 6.5 Proof Test Interval and PFDavg Sensitivity

The proof test interval (T_I) directly affects PFDavg. The maximum allowable T_I for each SIF shall be determined by sensitivity analysis during SRS preparation.

**Sensitivity analysis for SF-PRES-001 overall PFDavg:**

| T_I | PFDavg_sensor | PFDavg_logic | PFDavg_final | PFDavg_SIF | SIL Achieved |
|-----|--------------|-------------|-------------|-----------|-------------|
| 3 months (2,190 hr) | 1.69E-05 | 1.22E-04 | 3.78E-05 | 1.77E-04 | SIL 3 |
| 6 months (4,380 hr) | 6.61E-05 | 2.44E-04 | 7.55E-05 | 3.86E-04 | SIL 3 |
| 12 months (8,760 hr) | 2.53E-04 | 4.86E-04 | 1.51E-04 | 8.89E-04 | SIL 3 (marginal) |
| 18 months (13,140 hr) | 5.58E-04 | 7.29E-04 | 2.27E-04 | 1.51E-03 | **SIL 2 (FAIL)** |

**Conclusion for SF-PRES-001:** The maximum proof test interval for SIL 3 compliance is approximately 12 months, with significant margin reduction. The SRS specifies 6 months to maintain adequate margin and to align with typical turnaround schedules. PT-201 shall specify this interval.

**Any change to the proof test interval requires an SRS revision and FMEA recalculation.**

### 6.6 Common Cause Failure Analysis

#### 6.6.1 Beta Factor Model (IEC 61508-6, Annex D)

Common cause failures affect all redundant channels simultaneously. The beta factor represents the fraction of dangerous undetected failures that are common cause:

```
lambda_DU_common      = beta × lambda_DU
lambda_DU_independent = (1 - beta) × lambda_DU
```

For detected dangerous failures (using beta_D = beta/2 per IEC 61508-6):

```
lambda_DD_common      = beta_D × lambda_DD
lambda_DD_independent = (1 - beta_D) × lambda_DD
```

#### 6.6.2 Beta Factor Scoring (IEC 61508-6, Annex D)

The beta factor is determined by scoring the following categories. Each category has subfactors scored as 0 (poor practice) or the indicated value (good practice):

| Category | Subfactors | Max Score |
|----------|-----------|-----------|
| Separation / Segregation | Physical separation of channels, separate cable routes, separate power supplies | 2.5 |
| Diversity / Redundancy | Different technology, different manufacturers, different measurement principles | 4.0 |
| Complexity / Design / Application | Simple design, well-understood application, low component count | 1.5 |
| Assessment / Analysis | Design review, FMEA performed, proven in use assessment | 3.0 |
| Maintenance / Operating Procedures | Documented procedures, competent personnel, staggered testing | 3.0 |
| Environmental Testing | Type tested to IEC 61508, environmental stress screening, EMC testing | 3.0 |
| Competence / Training | Trained maintenance staff, competent design team, functional safety management | 1.5 |
| Safety / Quality Management | Safety management system, quality system, change management | 1.5 |

**Scoring total range:** 0 to 20

**Beta value from score (IEC 61508-6, Table D.2):**

| Score Range | Beta (non-diverse) | Beta (diverse) |
|-------------|-------------------|----------------|
| 0 – 4 | 10% | 5% |
| 5 – 9 | 5% | 2.5% |
| 10 – 14 | 2% | 1% |
| 15 – 17 | 1% | 0.5% |
| 18 – 20 | 0.5% | 0.5% |

#### 6.6.3 Beta Factor Scoring for SF-PRES-001

**System: 2oo3 Pressure Transmitters (identical, non-diverse)**

| Category | Score | Justification |
|----------|-------|---------------|
| Separation | 2.0 | Separate cable routes, separate junction boxes, same power supply (−0.5 deducted) |
| Diversity | 0.0 | Identical transmitters, same manufacturer, same model (no diversity credit) |
| Complexity | 1.5 | Simple 4-20 mA loop, well-understood pressure measurement |
| Assessment | 2.5 | FMEA performed, design review complete, limited prior use data (−0.5 deducted) |
| Maintenance | 2.0 | Documented procedures, trained staff, testing not staggered (−1.0 deducted) |
| Environmental | 2.5 | Devices type-tested, EMC tested, limited stress screening (−0.5 deducted) |
| Competence | 1.0 | Trained staff, some FS training, not fully certified (−0.5 deducted) |
| Safety/Quality | 1.0 | Quality system in place, safety management partially implemented (−0.5 deducted) |
| **Total** | **12.5** | |

Score 12.5 falls in the 10–14 range for non-diverse redundancy: **scored beta = 2%**.

A conservative value of **beta = 5%** is used in the worked example above to account for the identical transmitter type and shared process connection. If diversity measures are added (staggered testing, diverse process connections), the scored beta of 2% may be applied with documented justification.

#### 6.6.4 Impact of CCF on 2oo3 PFDavg

```
PFDavg_2oo3 = Independent term + CCF term

Independent term = (1-beta)² × 3 × lambda_DU² × T_I² / 4
CCF term         = beta × lambda_DU × T_I / 2
```

| Beta | Independent Term | CCF Term | Total PFDavg | CCF % of Total |
|------|-----------------|----------|-------------|---------------|
| 1% | 4.42E-06 | 1.24E-05 | 1.68E-05 | 73.7% |
| 2% | 4.26E-06 | 2.47E-05 | 2.90E-05 | 85.3% |
| 5% | 3.95E-06 | 6.19E-05 | 6.58E-05 | 94.0% |
| 10% | 3.55E-06 | 1.24E-04 | 1.27E-04 | 97.2% |

**Key insight:** Even at beta = 1%, the CCF term dominates the 2oo3 PFDavg. Adding more redundant channels reduces the independent term but does not reduce the CCF term. The most effective way to improve PFDavg in redundant architectures is to reduce the beta factor through diversity, physical separation, and staggered maintenance.

---

## 7. Traceability

### 7.1 Traceability Chain

Each SRS entry sits at the center of the traceability chain:

```
HA-PRES-001       Hazard: blocked outlet → vessel overpressure
     │
     ▼
SF-PRES-001       SRS entry: SIL 3, 2oo3 voting, PFDavg < 1.0E-03,
(in SRS-RefineryXYZ)         T_I = 6 months, Sheet 201
     │
     ├──► FMEA 201.1      Verifies hardware achieves SRS targets
     │
     ├──► Sheet 201       Implements the safety function in hardware
     │     Sheet 301
     │
     ├──► SAT 201         Validates the installed system
     │
     └──► PT-201          Maintains the safety function during operation
```

### 7.2 Bidirectional Requirements

| From → To | Forward Reference | Reverse Reference |
|-----------|-------------------|-------------------|
| HA → SRS | HA entry lists `SF-XXX-NNN (pending SRS)` | SRS entry header cites source HA entry |
| SRS → Drawing | SRS entry lists implementing sheet numbers | Drawing title block carries SF-XXX-NNN reference |
| SRS → FMEA | SRS specifies SIL target and T_I | FMEA scope section references SF-XXX-NNN and SRS T_I |
| SRS → SAT | SRS specifies functional requirements (setpoints, timing) | SAT acceptance criteria reference SRS requirements |
| SRS → PT | SRS specifies T_I | Proof test procedure cover page specifies same T_I |

### 7.3 SRS as Design Authority

If any other document disagrees with the SRS on a safety requirement, the SRS governs. Specifically:

- If the FMEA achieves a lower PFDavg than the SRS target, the SRS target still applies (the design has margin, which is acceptable)
- If the FMEA fails to achieve the SRS PFDavg target, the SRS target stands and the design must be revised
- If a proof test procedure specifies a different T_I than the SRS, the SRS governs; the proof test must be updated
- If a drawing implements a different architecture than specified in the SRS, the SRS governs; either the drawing or the SRS must be revised through formal change control

---

## 8. Lifecycle and Review

### 8.1 When the SRS Is Created

The SRS document is initiated after the LOPA study identifies safety functions and assigns SIL targets. The creation sequence is:

1. HAZOP study completes → hazard entries documented
2. LOPA study completes → SF-XXX-NNN identifiers assigned, SIL targets set
3. **SRS entry created** → functional and integrity requirements defined, architecture selected, reliability calculations performed
4. Electrical drawings produced → implement the architecture specified in the SRS
5. FMEA produced → verifies the actual hardware achieves the SRS targets

The SRS must be approved before drawings are issued for construction.

### 8.2 Management of Change Triggers

The SRS shall be reviewed and revised when any of the following occur:

| Trigger | Action Required |
|---------|----------------|
| Process setpoint change | Review functional requirements; revise if setpoints change |
| Architecture change (additional channels, voting logic change) | Revise architecture section; recalculate PFDavg |
| Proof test interval change | Revise T_I; recalculate PFDavg; verify SIL target still met |
| Failure rate data update | Review PFDavg; revise calculation if result changes |
| Device replacement with different type | Review DC and SFF assumptions; update FMEA; verify SRS targets still met |
| Periodic revalidation (≤5 years per IEC 61511) | Review all SRS entries; confirm calculations remain valid |
| LOPA revalidation result | Review SIL targets; revise if targets change |

### 8.3 Revision Control

The SRS uses letter revision designations (Rev A, Rev B, etc.). Each revision shall document:

| Field | Content |
|-------|---------|
| Rev | Letter designation |
| Date | Issue date |
| Description | Summary of changes (which SF entries changed, why) |
| Prepared By | Author name and role |
| Approved By | Approving authority name and role |

Changes to SRS integrity requirements (SIL target, PFDavg, T_I) require FMEA review and, if the FMEA result changes, FMEA revision.

---

## 9. Implementation Checklist

### SRS Preparation

- [ ] All SF-XXX-NNN identifiers received from HA/LOPA team
- [ ] SIL targets confirmed from LOPA worksheets
- [ ] SRS document initialized (cover page with project and all SF IDs)
- [ ] For each SF entry:
  - [ ] Header fields populated (SF ID, SIL target, source HA entry)
  - [ ] Functional requirements defined (setpoints, voting logic, response time, reset)
  - [ ] Architecture selected and documented (sensor, logic, final element, HFT)
  - [ ] Interface defined (all device tags and implementing sheet numbers)
  - [ ] Bypass requirements defined
  - [ ] Beta factor scoring completed for redundant subsystems
  - [ ] PFDavg calculation performed for each subsystem
  - [ ] Overall SIF PFDavg compared to SIL target
  - [ ] Proof test interval confirmed by sensitivity analysis
  - [ ] Architectural constraints verified (SFF and HFT per Route 1H)
  - [ ] Any constraint failures resolved with documented resolution

### Integration with Downstream Documents

- [ ] Implementing sheet numbers confirmed with drawing designer
- [ ] SIL targets, T_I, and architecture communicated to FMEA analyst
- [ ] Drawing title block safety fields match SRS entry
- [ ] FMEA scope references this SRS entry
- [ ] SAT acceptance criteria reference SRS functional requirements (setpoints, timing)
- [ ] Proof test procedure T_I matches SRS entry
- [ ] SRS referenced in Safety Documentation Standard document register

### Review and Approval

- [ ] SRS reviewed by independent functional safety engineer
- [ ] All SRS calculations independently checked
- [ ] SRS approved by management authority
- [ ] SRS issued to document control
- [ ] SRS distributed to drawing designer, FMEA analyst, and commissioning team
