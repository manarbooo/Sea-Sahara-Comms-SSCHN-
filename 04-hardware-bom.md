# 04 — Hardware Bill of Materials (BOM)

**Project:** SSCHN — Sea & Sahara Comms  
**Version:** 0.3  
**Status:** Proposed — pending engineering validation

## 1. Core Hardware

| ID | Component | Qty. | Specification / candidate | Purpose |
|---|---|---:|---|---|
| HW-01 | ESP32 + LoRa development board | 3 | Heltec WiFi LoRa 32 V3, HF variant (ESP32-S3 + SX1262), subject to approval | Node A, Node B, and gateway radio interface |
| HW-02 | LoRa antennas | 3 | Compatible with the selected boards and approved operating band; check package contents | Wireless transmission and reception |
| HW-03 | USB-C data cables | 3 | Compatible with the selected boards; verify data support | Programming, serial debugging, and gateway-to-laptop communication |
| HW-04 | Laptop | 1 | Existing development computer | Runs gateway application, backend, database, dashboard, and development tools |
| HW-05 | Jumper wires / compatible connectors | 1 set | Suitable for the selected boards and any required external connections | Prototyping and troubleshooting |
| HW-06 | Breadboard or prototyping board | 1–2 | Compatible with the physical board layout | Optional temporary assembly; use only if needed |
| HW-07 | USB power sources | As required | Suitable USB ports or approved power adapters | Powers the boards during bench testing |
| HW-08 | Multimeter | 1 | Standard digital multimeter | Checks voltage, continuity, and wiring; borrow if possible |

## 2. Power and Portable Operation

| ID | Component | Qty. | Specification | Status |
|---|---|---:|---|---|
| PW-01 | LiPo batteries | 2 | Compatible with the selected boards' battery connector, voltage, current needs, and charging requirements | Optional; confirm with engineer |
| PW-02 | Battery charging arrangement | As required | Use only a charging method approved for the selected board and battery | Required only if using batteries |
| PW-03 | Battery holders / connectors | As required | Must match the chosen battery and board | Only if needed |
| PW-04 | Enclosures | 2–3 | Sized for the assembled boards, antennas, and power source | Optional for the demo |

Start with USB-powered bench testing. Do not buy batteries or a separate charger until the engineer verifies the board's charging circuitry, connector, and battery requirements.

## 3. Software-Development and Debugging Accessories

| ID | Component | Qty. | Purpose | Status |
|---|---|---:|---|---|
| DEV-01 | USB data cables | Included in HW-03 | Connect boards to the laptop | Core |
| DEV-02 | USB hub | 1 | Provides additional USB ports if the laptop has insufficient ports | Only if needed |
| DEV-03 | USB-to-serial adapter | 0–1 | Provides serial access if the selected hardware does not expose a suitable interface | Only if needed |
| DEV-04 | Soldering equipment and supplies | 0–1 set | Used only if the selected assembly requires soldering | Borrow or defer if possible |

The integrated development-board approach is intended to avoid separate ESP32 boards, separate LoRa modules, and unnecessary wiring. Additional adapters or soldering equipment should be purchased only if the chosen hardware requires them.

## 4. Proposed Board Allocation

Use three compatible boards, if the proposed model is approved.

- **Board A — Node A:** Creates, transmits, receives, and parses text and SOS packets.
- **Board B — Node B:** Performs the same functions as Node A.
- **Board C — Gateway radio interface:** Receives supported radio packets and transfers packet data to the laptop over USB serial.

The laptop is the computing host, not a LoRa radio receiver by itself. Board C requires appropriate firmware and configuration; its reception of node traffic must be tested separately.

## 5. Optional Future Hardware

Do not purchase these for the first working radio demonstration.

| Component | Qty. | Purpose |
|---|---:|---|
| GNSS/GPS module | 1–2 | Adds real location data if location support is implemented |
| Additional ESP32 + LoRa board | 1 or more | Supports later relay or multi-hop experiments |
| External power-management module | As required | Used only if the selected portable power design requires it |
| Rugged enclosure | 2–3 | Improves physical protection for field testing |
| Advanced sensors | As required | Outside the initial MVP |
| Satellite modem and antenna | Not required | Future concept only |
| Drone and associated hardware | Not required | Future concept only |

Simulated coordinates may be used during software development without purchasing a GPS module, provided they are clearly labelled as simulated.

## 6. Engineering Checks Before Purchase

The engineer must confirm:

1. Exact board model, revision, and HF variant availability.
2. Applicable Algerian radio requirements and approved operating configuration.
3. Antenna compatibility and whether antennas are included.
4. Power, voltage, logic-level, and connector compatibility.
5. Firmware and radio-library compatibility.
6. Whether the third board can serve as the gateway interface using the selected firmware.
7. Whether any additional cables, connectors, or tools are actually required.

The Heltec WiFi LoRa 32 V3 is a candidate because it combines the ESP32-S3 and SX1262 radio on one board. The final model and frequency configuration remain subject to approval.

## 7. Procurement Status

| Item group | Status |
|---|---|
| Three integrated development boards | Proposed; awaiting approval |
| Antennas and USB data cables | Verify package contents |
| Laptop | Existing resource; verify availability |
| Wiring and prototyping accessories | Buy only what the assembly requires |
| USB power | Use existing suitable sources where possible |
| Batteries and enclosures | Defer until bench testing succeeds |
| Optional GPS and future hardware | Not required for initial MVP |

Record the exact model, supplier, price, currency, availability, and purchase status once verified. No component should be marked purchased, approved, or tested until that has actually happened.

## 8. First Hardware Milestone

1. Connect and program Node A.
2. Connect and program Node B.
3. Establish direct LoRa text-packet communication in both directions.
4. Connect and program the gateway radio interface.
5. Verify gateway reception and USB serial transfer.
6. Record the hardware configuration and test results.

**MVP purchase target:** Three engineer-approved integrated ESP32 + LoRa boards, their compatible antennas, suitable USB data cables, and only the necessary assembly accessories. Batteries, GPS, enclosures, and future expansion hardware can wait.

**Document status:** Draft for engineering review; no hardware purchase or radio configuration is yet confirmed.