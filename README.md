# Priority Alarm Encoder (Hardware Logic Implementation)

> **Status:** **Work In Progress** — Schematic finalized, PCB layout & routing in progress.

A hardware-based 8-to-3 priority encoder designed to reduce alarm floods.

---

## How It Works

This circuit compresses 8 concurrent binary input signals ($D_0$ through $D_7$) into a 3-bit output code ($A_2, A_1, A_0$) representing the highest-active input index, alongside a validity flag.

### Core Logic Principles

1. **Information Compression:** The 256 possible input state combinations collapse into 8 distinct priority fault codes (plus a "no fault" state). For example, input state `1XXXXXXX` always activates Code 7 (`111₂`). The don't-care states (`X`) significantly simplify the logic implementation.
2. **Priority Masking:** Higher-order inputs dynamically suppress lower-order signals.
---

## Minimized Logic Equations

Derived via Boolean Logic principals from the 8-input truth table:
| Truth Table and Resulting Equations |
| :---: |
| ![Truth Table and Resulting Equations](Visuals/Truth%20Table%20%2B%20Equations%20-%20Sheet1.png) |
---

## Hardware & Components

Built using standard 74HC/74LS series discrete logic ICs:

* **Inverters:** `74HC04` (Hex Inverter)
* **AND Gates:** `74LS11` (Triple 3-Input AND), `74LS21` (Dual 4-Input AND)
* **OR Gates:** `HEF4072` / `CD4072` (Dual 4-Input OR)
* **Inputs/Outputs:** 8-position DIP Switch (`SW1`), 3x Output LEDs (`D1`–`D3`), status indicators

---

## Real-World Architecture Context

The masking and encoding structure used here mirrors several foundational hardware systems:

* **Interrupt Controllers (NVIC/APIC):** Microcontrollers and CPUs evaluate concurrent peripheral service requests and grant immediate execution to the highest-priority interrupt vector.
* **Master Warning Systems:** Aircraft avionics elevate critical safety alarms over secondary advisories.
* **Bus Arbitration:** Multi-master communication buses evaluate conflicting bus requests using strict priority encoding schemes.
* **Floating-Point Units (FPUs):** Leading-Zero Detectors (LZDs) used in floating-point normalization circuits rely on priority encoder structures.

