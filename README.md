# Polarimeter — Photodiode Analog Front-End

A 4-layer mixed-signal PCB that reads optical polarization by measuring the
photocurrent from a pair of photodiodes through a low-noise transimpedance
signal chain. Designed in KiCad; this repository contains the full schematic,
layout, fabrication outputs, and bill of materials.

## What it does

Light passing through a polarizing optical stage lands on two photodiodes
(`D1`, `D2`). Each diode's photocurrent is converted to a voltage by a
transimpedance amplifier (TIA), filtered, and buffered for acquisition. By
comparing the two channels, the relative polarization / intensity of the
incident beam can be recovered. The board carries its own low-noise power
regulation and a precision voltage reference so the analog measurement is clean
and ratiometric.

## Signal chain

| Stage | Part | Role |
|-------|------|------|
| Photodiodes | `D1`, `D2` (TO-5) | Convert incident light to photocurrent |
| Transimpedance amps | OPA381 (precision, low-bias TIA) | I→V conversion of diode current |
| Gain / buffer | OPA320 / OPA2320 (low-noise, R-R CMOS) | Second-stage gain and buffering |
| Precision reference | REF3425 (2.5 V) | Stable ratiometric reference for the ADC path |
| Connector | 2×24 header (`J1`) + barrel jack (`J2`) | Signal breakout and DC input |

## Power

- **LT8609** synchronous step-down buck — primary rail regulation from the DC input jack.
- **LP5912-3.3** low-noise LDO — clean 3.3 V rail for the precision analog section.
- Local decoupling throughout (0.1 µF / 1 µF / 10 µF) to keep the TIA front-end quiet.

## Board

- **4 copper layers:** `F.Cu`, `In1.Cu`, `In2.Cu`, `B.Cu`
- Surface-mount construction, 0603/0805 passives
- Gerbers and drill files included for direct fabrication

## Repository layout

```
Polarimeter.kicad_pro      KiCad project
Polarimeter.kicad_sch      Schematic
Polarimeter.kicad_pcb      PCB layout (4-layer)
Polarimeter.csv            Bill of materials
Gerbers for AMO/           Fabrication outputs (Gerber + Excellon drill)
```

## Bill of materials

The full BOM lives in [`Polarimeter.csv`](Polarimeter.csv) (designator,
footprint, quantity, value). Key actives: OPA381, OPA320/OPA2320, REF3425,
LT8609, LP5912-3.3.

## Tools

Designed in [KiCad](https://www.kicad.org/). Open `Polarimeter.kicad_pro` to
view or edit the schematic and layout.

---

*Author: Christian Hearn*
