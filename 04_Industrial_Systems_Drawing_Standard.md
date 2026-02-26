# Industrial Systems Drawing Standard
## Device, Wire, and Drawing Numbering Convention

**Status:** Draft
**Scope:** Electrical drawing organization, device tagging, wire numbering, title block requirements, and cross-referencing conventions for industrial control systems.

---

## Table of Contents

1. [Purpose and Scope](#1-purpose-and-scope)
2. [Standards References](#2-standards-references)
3. [Standard Definitions Sheet](#3-standard-definitions-sheet)
4. [Drawing Organization](#4-drawing-organization)
5. [Device Numbering](#5-device-numbering)
6. [Wire Numbering](#6-wire-numbering)
7. [Grid System and Cross-Referencing](#7-grid-system-and-cross-referencing)
8. [Title Block Requirements](#8-title-block-requirements)
9. [Drawing Set Organization](#9-drawing-set-organization)
10. [Interaction with Other Documentation](#10-interaction-with-other-documentation)
11. [CAD Implementation Requirements](#11-cad-implementation-requirements)
12. [Change Management](#12-change-management)
13. [Implementation Checklist](#13-implementation-checklist)

---

## 1. Purpose and Scope

### 1.1 Purpose

This standard defines a consistent numbering scheme for electrical drawings, devices, and wires such that any person with a device tag, wire number, or document number can immediately determine where to find related information — without lookup tables.

The numbering system encodes physical location and drawing references directly into tags and labels. This enables self-documenting drawings, scoped revision control, and fast field troubleshooting.

### 1.2 Scope

This standard applies to:

- Electrical schematic drawings (control, power, instrumentation)
- Device tagging and terminal designation
- Wire numbering and labeling
- Drawing title blocks and revision control
- Cross-referencing between sheets

This standard does **not** define:

- Safety documentation content (Hazard Analysis, Safety Function Specifications, FMEA, SAT, Proof Tests) — these are covered in a separate Safety Documentation Standard that references this drawing standard for numbering conventions.
- P&ID conventions — P&IDs are produced independently; this standard defines how P&ID references are carried into electrical drawings.
- PLC programming conventions — software documentation references device tags defined by this standard.

### 1.3 Design Philosophy

**The drawing is the source of truth.** The numbering system's job is to get a technician or engineer to the correct drawing quickly. It is not a substitute for reading the drawing.

Principles:

- Numbers encode relationships and location — minimal memorization required.
- Voltage identification and signal type are conveyed through conductor marking per applicable code, not through wire numbering.
- External references (P&ID tags, Hazard Analysis IDs) are carried as description fields, not embedded in the primary tag.
- Safety documentation (FMEA, SAT) uses sheet-based numbering from this standard to enable traceability, but the content and lifecycle of those documents is defined separately.

---

## 2. Standards References

| Standard | Title | Application |
|----------|-------|-------------|
| IEC 61082 | Preparation of documents used in electrotechnology | Drawing format, cross-referencing |
| IEC 81346 | Structuring principles and reference designations | Device designation letter codes |
| IEC 60445 | Basic and safety principles — Identification of equipment terminals and conductor terminations | Terminal and conductor marking |
| NEC (NFPA 70) | National Electrical Code | US installation requirements |
| UL 508A | Industrial Control Panels | Panel construction and wire marking (US) |
| ISA-5.1 | Instrumentation Symbols and Identification | P&ID symbology and instrument identification conventions |
| ISA-5.4 | Instrument Loop Diagrams | Loop diagram format and content standards |

For safety-critical systems, the Safety Documentation Standard (`00_Safety_Documentation_Standard`) references IEC 61508 and IEC 61511. For the complete list of standards referenced across this framework, see Section 3 of that document.

---

## 3. Standard Definitions Sheet

Every drawing set shall include a Standard Definitions sheet (typically Sheet 002 or similar early-sequence general sheet) containing the following:

### 3.1 Symbol Legend

All electrical symbols used in the drawing set, per IEC 61082 or project-specific conventions.

### 3.2 Device Letter Codes

Device type designations per IEC 81346:

| Letter | Device Type | Examples |
|--------|-------------|----------|
| **B** | Transducer, Transmitter | B301.1 (Pressure transmitter) |
| **F** | Fuse, Protective device | F112.1 (Control power fuse) |
| **H** | Alarm, Indicator | H118.1 (High pressure alarm) |
| **K** | Relay, Contactor | K115.1 (Safety interlock relay) |
| **M** | Motor | M201.1 (Feed pump motor) |
| **Q** | Circuit Breaker, Disconnector | Q110.1 (Main breaker) |
| **S** | Switch (Manual) | S125.1 (Selector switch) |
| **T** | Transformer | T105.1 (Control transformer) |
| **U** | Converter, Drive | U220.1 (Variable frequency drive) |
| **X** | Terminal Strip, Connector | X115.1 (Terminal strip) |

Additional designations as needed: A (assembly), E (miscellaneous), G (generator), L (inductor), R (resistor), V (semiconductor), W (transmission path), Y (electrically actuated device), Z (filter/termination).

### 3.3 Wire Color Conventions

Wire colors per applicable code. Define project-specific conventions here:

- AC phase identification per NEC Article 210.5 or IEC 60445
- DC polarity identification
- Safety/grounding conductor colors
- Control circuit conventions

### 3.4 Abbreviations

Standard abbreviations used in the drawing set:

| Abbreviation | Meaning |
|--------------|---------|
| N.O. | Normally Open (contact) |
| N.C. | Normally Closed (contact) |
| PE | Protective Earth |
| +24V / 0V | DC power rail designations |
| L1, L2, L3 | AC line conductors |
| N | Neutral conductor |

### 3.5 Location Code Definitions

Project-specific cabinet and location codes (see [Section 4.1](#41-sheet-numbering)):

| Location Code | Description | Sheet Range |
|---------------|-------------|-------------|
| +100 | Main control cabinet | 100–199 |
| +200 | Motor control center | 200–299 |
| +300 | Field junction boxes / devices | 300–399 |
| ... | As needed per project | ... |

---

## 4. Drawing Organization

### 4.1 Sheet Numbering

Sheets are numbered in blocks of 100 by cabinet/enclosure location:

| Sheet Range | Location Code | Typical Usage |
|-------------|---------------|---------------|
| 010–099 | General | Title, legend, cable schedules, layouts |
| 100–199 | +100 | Main control cabinet |
| 200–299 | +200 | Motor control center |
| 300–399 | +300 | Field junction boxes / field devices |
| 400–499 | +400 | Remote I/O cabinet |
| 500+ | +500, etc. | Additional systems as needed |

**Rule: Each sheet belongs to exactly one cabinet.** A sheet in the 200–299 range documents only devices physically located in cabinet +200. Devices in other cabinets that connect to circuits on this sheet are shown as inter-sheet references (see [Section 6.5](#65-inter-sheet-connections)), not as local devices.

**Sheet number directly indicates physical location.** Sheet 237 is in cabinet +200. No exceptions.

### 4.2 Sheet Allocation Strategy

Within each 100-sheet block:

**Leave gaps during initial design.** Use sheets 110, 115, 120, 125 — not 110, 111, 112, 113. This allows insertion of related circuits nearby without renumbering.

**Group related circuits in adjacent sheet numbers:**

Example within +100 (sheets 100–199):

- 110–119: Power distribution
- 120–129: Overpressure protection logic
- 130–139: Temperature control
- 140–149: Utility systems

### 4.3 Late Addition Sheets

For additions after initial numbering, use decimal notation: Sheet 115.01, 115.02, etc.

- Keeps additions near related systems.
- Maintains cabinet assignment (115.01 is still in +100).
- Avoids renumbering the entire drawing set.

### 4.4 Drawing Flow Convention

For IEC-compliant drawings:

- **Top-to-bottom flow** — power/signal flows down the page.
- **Vertical circuit layout** — devices arranged vertically within grid columns.

---

## 5. Device Numbering

### 5.1 Device Tag Format

**Format:** `+[Location]-[Device][Sheet].[Sequence]`

| Component | Description | Example |
|-----------|-------------|---------|
| `+[Location]` | Physical cabinet/location code | +100, +200, +300 |
| `[Device]` | IEC 81346 device letter code | K, B, M, Q, etc. |
| `[Sheet]` | Sheet number where device is primarily documented | 115, 237, 301 |
| `.[Sequence]` | Device sequence on that sheet (per device type) | .1, .2, .3 |

**Examples:**

- `+100-K115.1` → Cabinet +100, Relay, Sheet 115, first relay on that sheet
- `+300-B301.1` → Cabinet +300, Transmitter, Sheet 301, first transmitter on that sheet
- `+200-M220.1` → Cabinet +200, Motor starter, Sheet 220, first motor device on that sheet

**Reading the tag:**

- Location (+100) → which cabinet
- Device letter (K) → device type
- Sheet number (115) → which drawing
- Sequence (.1) → which device of that type on that sheet

### 5.2 Device Numbering Rules

**Sequential numbering restarts on each sheet, per device type:**

- First relay on Sheet 115: `+100-K115.1`
- Second relay on Sheet 115: `+100-K115.2`
- First relay on Sheet 116: `+100-K116.1`

**All devices on a sheet belong to that sheet's cabinet.** A sheet in the +200 range contains only `+200-` devices. (See [Section 4.1](#41-sheet-numbering).)

**Scalability:** Each sheet supports up to 99 devices of each type (.1 through .99).

### 5.3 Description Field — External References

Devices that correspond to items on other documents carry those references in the description field, not in the device tag.

**P&ID references:**
```
+300-B301.1
Desc: Pressure Transmitter #1 (P&ID: PT-201)
```

**Hazard Analysis references (safety-critical devices):**
```
+200-K201.1
Desc: Safety Relay — Valve Close Command (HA: HA-PRES-001)
```

The description field format for external references shall be consistent and parseable: `(P&ID: XX-NNN)`, `(HA: HA-XXX-NNN)`.

### 5.4 Terminal Designation

Add terminal number after device tag using colon separator:

**Format:** `+[Location]-[Device][Sheet].[Sequence]:[Terminal]`

**Examples:**

- `+100-K115.1:A1` → Relay K115.1, coil terminal A1
- `+300-B301.1:2` → Transmitter B301.1, terminal 2
- `+300-X315.1:12` → Terminal strip X315.1, terminal 12

**Terminal numbering conventions:**

- Relay coils: A1, A2 (or per manufacturer)
- Contacts: Numbered pairs (1-2, 3-4 for N.O.; 11-12, 13-14 for N.C.)
- Terminal strips: Sequential numbers (1, 2, 3, 4…)
- Motor terminals: U, V, W (3-phase) or T1, T2, T3

### 5.5 Parent/Child Devices (Multi-Sheet Elements)

When a device has elements on multiple sheets (e.g., relay coil on one sheet, contacts on others):

**The device tag is determined by where the control element (parent) is located.** All child elements (contacts, auxiliary elements) carry the same device tag.

**Example:**

| Sheet | Element | Tag | Cross-Reference |
|-------|---------|-----|-----------------|
| 115 | Relay coil (parent) | +100-K115.1 | Contacts: Sheets 120, 125, 130 |
| 120 | N.O. contact (child) | +100-K115.1 | Coil: Sheet 115 |
| 125 | N.O. contact (child) | +100-K115.1 | Coil: Sheet 115 |
| 130 | N.C. contact (child) | +100-K115.1 | Coil: Sheet 115 |

**Rules:**

- The parent element (coil, actuator) determines the device tag.
- Child elements use the same tag — they are never given separate device numbers.
- The parent sheet lists all child locations.
- Each child sheet shows a cross-reference to the parent: `(115)`.
- BOM lists the device once, under the parent sheet.

**Incorrect:** Giving a contact on Sheet 120 the tag `K120.1` — this implies a different device and breaks traceability.

### 5.6 Cross-Reference Notation (IEC 61082)

**On parent sheet (coil):** Show where contacts are used.
```
+100-K115.1 (Relay Coil)
Grid 4E
Contacts: Sheet 120 (3B), Sheet 125 (2C), Sheet 130 (4D)
```

**On child sheet (contact):** Show where parent is located.
```
+100-K115.1 (N.O. Contact 1-2)
Grid 3B
Coil: Sheet 115 (4E)
```

**Graphical notation:** The number in parentheses below a contact symbol indicates the parent sheet.
```
    +100-K115.1
       │ │
    ┌──┘ └──┐
    │  N.O. │
    └───────┘
       (115)
```

**Note on intentional redundancy:** The cross-reference `(115)` repeats information already encoded in the device tag `K115.1`. This redundancy follows IEC 61082 convention, aids quick navigation, and reduces errors — especially for technicians who may not be fluent in the tag format. It is intentional and beneficial.

---

## 6. Wire Numbering

### 6.1 Core Principles

**A wire number is an identity, not a location.** It tells you where the wire originates — which sheet and column document the circuit it belongs to.

**A wire keeps its number across terminal strips, junction boxes, and cabinet boundaries.** The number does not change when a wire physically crosses into a different enclosure.

**A wire gets a new number only when it passes through a protective device** (fuse, circuit breaker, disconnect). The new number references the sheet where the protective device is documented. This means every unique wire number downstream of a protective device defines a branch circuit, which maps directly to branch protection analysis and SCCR calculations.

### 6.2 Wire Number Format

**Format:** `[Sheet]-[Column].[Sequence]`

| Component | Description | Example |
|-----------|-------------|---------|
| `[Sheet]` | Sheet number where wire originates | 215, 120, 301 |
| `[Column]` | Grid column number where wire originates | 1, 2, 3, 4… |
| `.[Sequence]` | Sequential wire number within that column (top-to-bottom) | .1, .2, .3 |

**Examples:**

- `215-1.1` → Sheet 215, Column 1, first wire
- `120-4.2` → Sheet 120, Column 4, second wire
- `301-2.1` → Sheet 301, Column 2, first wire

### 6.3 Wire Numbering Through Protective Devices

When a wire passes through a protective device, the load side receives a new wire number referencing the sheet where the protective device is documented.

**Example — DC distribution from +100 to multiple cabinets:**

```
Sheet 120 (DC Power Supply in +100):
  Supply output:         120-4.1 (+24V)
  
  Wire 120-4.1 arrives at +200 terminal strip — still 120-4.1
  Wire 120-4.1 arrives at +300 terminal strip — still 120-4.1
  
Sheet 215 (Branch fuse F215.1 in +200):
  Fuse input (line side):   120-4.1
  Fuse output (load side):  215-4.1  ← new number, new branch circuit

Sheet 315 (Branch fuse F315.1 in +300):
  Fuse input (line side):   120-4.1
  Fuse output (load side):  315-4.1  ← new number, new branch circuit
```

**What this tells a technician:**

- Wire `120-4.1` in any cabinet → originates from Sheet 120 in +100, unprotected distribution
- Wire `215-4.1` → downstream of a protective device on Sheet 215, branch circuit
- A wire number from a "foreign" sheet range (e.g., `120-x.x` found in +300) indicates an inter-cabinet connection

### 6.4 Vertical Column Organization

Each numbered grid column represents one vertical wire path from source (top) to load (bottom).

**Standard column allocation (example for motor circuits):**

- Columns 1–3: Motor power (L1/U, L2/V, L3/W)
- Column 4: +24V control power
- Column 5: 0V control return
- Columns 6–8: Control signals, status, feedback
- Columns 9–10: Reserved for expansion

**Design rules:**

- Each column = one continuous vertical wire path.
- Group related conductors in adjacent columns.
- Reserve columns between functional groups for expansion.
- Minimize wire crossings between columns.

### 6.5 Inter-Sheet Connections

When a wire crosses from one sheet to another (including across cabinets), the wire **retains its original number**.

**On the originating sheet:**
```
Wire: 215-1.3
From: +200-K215.1:2 @ Grid 1E
To: Sheet 320, +300-M320.1:U
Cable: CBL-215-01
```

**On the destination sheet:**
```
Wire: 215-1.3
From: Sheet 215, +200-K215.1:2
To: +300-M320.1:U @ Grid 3G
Cable: CBL-215-01
```

The wire number `215-1.3` appears on both sheets. A technician in +300 seeing wire `215-1.3` knows immediately that this wire originates from Sheet 215 in the +200 cabinet range.

### 6.6 Inter-Column Connections

When a wire crosses horizontally between columns on the same sheet:

**At the connection point, document both wire segments:**
```
Column 4: Wire 215-4.2 ends at relay contact K215.1:14 @ Grid 4D
Horizontal jumper at Row D
Column 6: Wire 215-6.3 begins at Grid 6D
```

### 6.7 Power Rails and Common Conductors

Main power distribution uses descriptive designations across all sheets:

- **AC:** L1, L2, L3, N, PE
- **DC:** +24V (or L+), 0V (or L-)

These designations apply across the drawing set and are not column-specific. Point-to-point connections use the sheet-column-sequence format.

### 6.8 Wire Label Content

**Minimum required:**
```
215-1.1
L1 → M215.1:U
```

**Optional additions (include when applicable):**
```
215-1.1
L1 → M215.1:U
(BLK, 12 AWG)
CBL-215-01
```

Cable references are **mandatory** for inter-cabinet wiring and multi-conductor cables.

### 6.9 Understanding Wire Numbers vs Grid References

**Wire numbers** use sequential counting: `[Sheet]-[Column].[Sequence]` — the sequence (.1, .2, .3) is a count of wires top-to-bottom, not a grid row letter.

**Grid references** use spatial coordinates: `[Column][Row]` — e.g., 4E means Column 4, Row E.

These are distinct systems. Wire column numbers align with grid column numbers (1=1, 2=2). Wire sequence numbers do not correspond to grid row letters. This is an intentional trade-off: sequential numbering enables CAD automation, while grid references provide exact spatial location for devices.

**To locate a wire from its number:**

1. Go to the sheet indicated.
2. Find the grid column indicated.
3. Count wires top-to-bottom to find the sequence position.

---

## 7. Grid System and Cross-Referencing

### 7.1 Grid Format

All sheets shall include a grid reference system per IEC 61082-1:

- **Columns:** 1, 2, 3, 4, 5, 6, 7, 8… (numbers, left to right)
- **Rows:** A, B, C, D, E, F, G, H… (letters, top to bottom)
- **Grid spacing:** 40mm × 40mm recommended
- **Grid labels:** Shown in drawing margins

**Grid Reference Notation:** `[Column][Row]` — e.g., 4E = Column 4, Row E.

### 7.2 Device Grid References

Every device on a sheet shall have a grid reference:

```
+200-K215.1 (Motor Contactor)
Sheet 215, Grid 4E
Coil terminals: A1, A2
Main contacts:
  1-2: Grid 1E
  3-4: Grid 2E
  5-6: Grid 3E
Auxiliary contact 13-14: Sheet 220, Grid 3B
```

### 7.3 Wire-to-Device Correlation

Wire numbers and device grid references work together:

```
Wire: 215-1.2 (Sheet 215, Column 1, 2nd wire)
From: Q215.1:2 @ Grid 1C
To:   K215.1:1 @ Grid 1E
```

The wire is in Column 1 (from wire number), running between devices at Grid 1C and Grid 1E (from grid references). Column alignment between wire number and device grid confirms correct placement.

---

## 8. Title Block Requirements

### 8.1 All Sheets — Minimum Required

Every drawing sheet shall include:

1. **Sheet number** and total sheet count
2. **Sheet title/description**
3. **Cabinet/Location code** (+100, +200, etc.)
4. **Revision** — letter or number, date, description
5. **Project information** — project name, client, contractor
6. **Approvals** — drawn by, checked by, approved by (with dates)
7. **Drawing standards reference** — "Per IEC 61082" or "Per NEC" as applicable
8. **Grid reference diagram** — showing column/row layout

### 8.2 Safety-Critical Sheets — Additional Fields

Sheets implementing safety functions shall additionally include:

1. **Safety classification:** "SAFETY-CRITICAL SYSTEM" or "SIL X SYSTEM"
2. **Safety Function reference:** e.g., SF-PRES-001 (SIL 3)
3. **Hazard Analysis reference:** e.g., HA-PRES-001
4. **Architecture:** e.g., 2oo3 Pressure Voting, HFT=1
5. **FMEA reference:** e.g., FMEA 201.1
6. **Proof Test reference and interval (if inherent DU exists):** e.g., PT-201 (6-month interval). If the FMEA identifies no inherent DU failure modes, this field reads "No proof test required — no inherent DU."
7. **Related sheets:** Cross-references to other sheets in the safety system

The content and lifecycle of these safety documents is defined in the separate Safety Documentation Standard. The FMEA and SAT numbering in that standard uses the sheet numbers defined here as its basis.

### 8.3 Non-Safety Sheets — Clear Identification

Non-safety sheets shall be marked: **"NON-SAFETY SYSTEM"**

Include applicable specification reference (e.g., "Per NEC Article 210") and functional test reference if applicable. Do not include SIL, FMEA, or proof test fields.

### 8.4 Title Block Example — Safety-Critical

```
┌──────────────────────────────────────────────────────────────┐
│ Sheet 201: Overpressure Protection Control Logic             │
│ Cabinet: +200                                    Rev: 5      │
│                                                              │
│ ╔════════════════════════════════════════════════════════╗  │
│ ║           SAFETY-CRITICAL SYSTEM (SIL 3)               ║  │
│ ╚════════════════════════════════════════════════════════╝  │
│                                                              │
│ SF: SF-PRES-001 (SIL 3)     HA: HA-PRES-001                │
│ Architecture: 2oo3, HFT=1   FMEA: 201.1                    │
│ Proof Test: PT-201 (6-month) Related: 301, 302              │
│                                                              │
│ Drawn: J. Smith 2025-01-15   Checked: R. Jones 2025-01-20   │
│ Approved: T. Brown 2025-01-22                                │
│                                                              │
│ Project: Refinery Vessel XYZ                                 │
│ Client: ABC Chemical Co.     Contractor: XYZ Engineering     │
└──────────────────────────────────────────────────────────────┘
```

### 8.5 Revision History Table

Every sheet shall include a revision history:

```
┌─────┬────────────┬────────────────────────────────┬──────────┐
│ Rev │ Date       │ Description                    │ By       │
├─────┼────────────┼────────────────────────────────┼──────────┤
│  5  │ 2025-01-22 │ Updated per SF-PRES-001 Rev D  │ J. Smith │
│  4  │ 2024-11-10 │ Added transmitter B301.3        │ J. Smith │
│  1  │ 2024-03-15 │ Initial issue                  │ J. Smith │
└─────┴────────────┴────────────────────────────────┴──────────┘
```

---

## 9. Drawing Set Organization

### 9.1 Table of Contents Structure

Organize by cabinet location, then by function within each cabinet:

```
DRAWING INDEX

GENERAL (Sheets 010–099)
  010: Title Sheet and Drawing Index
  011: Standard Definitions (Symbols, Wire Colors, Device Codes)
  015–019: Cable Schedules
  020–029: Terminal Strip Schedules
  030–039: Panel Layouts (Physical)
  040–044: Grounding and Bonding
  045–049: Conduit and Cable Routing

CABINET +100 — Main Control Cabinet (Sheets 100–199)
  110–119: Power Distribution
  120–129: Overpressure Protection Logic (SIL 3)
  130–139: Temperature Control
  140–149: PLC and HMI
  150–159: Utility Systems (Non-Safety)

CABINET +200 — Motor Control Center (Sheets 200–299)
  210–219: MCC Power Distribution
  220–229: Motor Starters
  235–244: VFD Drives

CABINET +300 — Field Devices (Sheets 300–399)
  310–319: Safety Instrumentation (SIL 3)
  320–339: Process Instrumentation (Non-Safety)
  350–359: Field Junction Boxes
```

### 9.2 Sheet Allocation Best Practices

- Reserve blocks of 5–10 sheets per subsystem.
- Don't use consecutive numbers initially — leave room for insertion.
- Use decimal notation (115.01) for post-design additions.
- Group SIL-rated systems together within each cabinet's range for clarity during safety reviews.

---

## 10. Interaction with Other Documentation

### 10.1 P&ID Cross-Reference

P&IDs are produced before electrical design and use their own tagging convention (e.g., PT-201, XV-201). The electrical drawings use IEC 81346 device tags as the primary identifier.

**P&ID tags are carried in the device description field:**
```
+300-B301.1
Desc: Pressure Transmitter #1 (P&ID: PT-201)
```

The description field format `(P&ID: XX-NNN)` shall be consistent across the drawing set so that cross-reference reports can be auto-generated from the CAD database.

**The electrical tag is always the primary identifier.** P&ID references are metadata for cross-discipline traceability.

### 10.2 Hazard Analysis Cross-Reference

Hazard Analysis documents are produced before detailed electrical design. Safety-critical sheets carry HA references in the title block and in device description fields where applicable:

```
+200-K201.1
Desc: Safety Relay — Valve Close (HA: HA-PRES-001)
```

The HA reference format `(HA: HA-XXX-NNN)` shall be consistent and parseable.

### 10.3 Safety Documentation Numbering Basis

The separate Safety Documentation Standard uses sheet numbers from this drawing standard as the basis for its numbering:

| Safety Document | Numbering Convention | Example |
|----------------|----------------------|---------|
| FMEA | `FMEA [Sheet].[Sequence]` | FMEA 201.1 → analyzes system on Sheet 201 |
| SAT | `SAT [Sheet]` | SAT 201 → validates systems on Sheet 201 |
| Proof Test (where inherent DU exists) | `PT-[Sheet]` | PT-201 → periodic test for Sheet 201 inherent DU failure modes |

This alignment means that seeing "FMEA 201.1" immediately directs the reader to Sheet 201 for the implementation details — maintaining the self-documenting property across the drawing and safety documentation packages.

### 10.4 I/O Lists

I/O lists are exported from the CAD tool and import into PLC programming software. They shall include:

| Field | Source | Example |
|-------|--------|---------|
| PLC Address | CAD assignment | %I0.0 |
| Device Tag | Per this standard | +300-B301.1 |
| Description | Device desc field | Pressure Transmitter #1 (P&ID: PT-201) |
| Cabinet | Location code | +300 |
| Sheet | Sheet number | 301 |
| Grid | Grid reference | 2B |

### 10.5 Bill of Materials

BOM references device tags and parent sheet numbers. Parent/child devices (see [Section 5.5](#55-parentchild-devices-multi-sheet-elements)) are listed once under the parent sheet.

| Tag | Description | Qty | Cabinet | Parent Sheet |
|-----|-------------|-----|---------|-------------|
| +300-B301.1 | Pressure Transmitter (P&ID: PT-201) | 1 | +300 | 301 |
| +100-K115.1 | Safety Interlock Relay | 1 | +100 | 115 |

### 10.6 Cable Schedules

Cable schedules reference device tags from drawings:

| Cable ID | From | To | Type | Length | Sheets |
|----------|------|----|------|--------|--------|
| CBL-201-01 | +300-B301.1 | +200-X201.1:5,6 | 18AWG 2C shielded | 150 ft | 201, 301 |

---

## 11. CAD Implementation Requirements

This section defines what the CAD system must produce, not which menus to click. Platform-specific configuration guides (ACADE, EPLAN) are maintained separately.

### 11.1 Required CAD Outputs

The CAD system shall be configured to produce:

1. **Device tags** in the format `+[Location]-[Device][Sheet].[Sequence]`
2. **Wire numbers** in the format `[Sheet]-[Column].[Sequence]`, auto-assigned based on vertical column position
3. **Grid overlay** on all sheets — numbered columns, lettered rows, consistent spacing
4. **Cross-references** for parent/child devices showing sheet and grid location
5. **I/O list export** including device tag, description, PLC address, cabinet, sheet, and grid
6. **BOM export** with parent sheet references

### 11.2 Vertical Ladder / Column Alignment

For IEC top-to-bottom layout, the CAD vertical ladder rungs shall align with grid columns:

- Rung 1 = Grid Column 1
- Rung 2 = Grid Column 2
- Rung N = Grid Column N

Wire numbers are assigned automatically based on rung/column position and sequential count.

### 11.3 Title Block Templates

CAD templates shall include all fields from [Section 8](#8-title-block-requirements), with separate templates for safety-critical and non-safety sheets.

### 11.4 Cross-Platform Projects

When multiple CAD platforms are used on the same project:

- All platforms must produce the same tag, wire, and grid formats.
- I/O lists, BOMs, and cable schedules use neutral exchange formats (Excel/CSV).
- One platform should be designated primary to avoid conflicts.

---

## 12. Change Management

### 12.1 Adding Devices to an Existing Sheet

New device receives the next available sequence number for its type on that sheet. Only the affected sheet is revised. If safety-critical, review the corresponding FMEA and SAT per the Safety Documentation Standard.

### 12.2 Adding a New Sheet

Use the next available number within the cabinet's range, or a decimal addition (115.01) if inserting between existing sheets. Update the drawing index.

### 12.3 Removing Devices

**For safety-critical systems (preferred):** Mark device as "NOT USED — REMOVED PER ECN-XXXX" to preserve the numbering sequence and prevent tag reuse.

**For non-critical systems:** Device may be removed entirely. The sequence number is not reused.

### 12.4 Major Redesign

Keep the same sheet numbers (physical location unchanged). Update revision drastically with clear notation: "COMPLETE REDESIGN, Rev X." Archive previous revisions for historical record.

### 12.5 Field Changes and As-Built

Field additions follow the numbering standard. Document via Field Change Notice (FCN). As-built drawings are marked "AS-BUILT" in the title block and list all incorporated FCNs.

---

## 13. Implementation Checklist

- [ ] Define cabinet locations and assign codes (+100, +200, +300, etc.)
- [ ] Allocate sheet ranges to cabinets
- [ ] Create Standard Definitions sheet (Sheet 002) with symbols, colors, device codes
- [ ] Configure CAD per [Section 11](#11-cad-implementation-requirements)
- [ ] Create title block templates (safety-critical and non-safety)
- [ ] Establish drawing index structure
- [ ] Define P&ID and HA description field formats
- [ ] Set up I/O list and BOM export formats
- [ ] Coordinate tag import format with PLC programmer
- [ ] Train design team on numbering conventions
- [ ] Establish revision control and change management procedures

---

