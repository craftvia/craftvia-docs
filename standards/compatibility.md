# CraftVia Compatibility Policy and Current Matrix

> [!WARNING]
> The current matrix records design intent, not completed hardware validation. All Rev0 combinations remain unverified until linked test evidence is published.

## Compatibility dimensions

Compatibility is not a single yes/no property. CraftVia records it in layers:

1. **Mechanical** — outline, contacts, keying, stack height, and clearance.
2. **Power** — supply assignment, voltage range, current budget, ground, and power-source isolation.
3. **System** — programming, debug, reset, boot, and any selected USB/debug profile.
4. **Application signals** — the implementation-specific pin map and peripheral conflicts.
5. **Validated combination** — the exact product versions and revisions tested together.

A Core that can be inserted physically is not automatically safe to power, and a Core that can be programmed is not automatically application-signal compatible with another Core.

## Current Rev0 matrix

| Item | Interface relationship | Design status | Validation status |
| --- | --- | --- | --- |
| Core-S G031 v1 Rev0 | Implements Core-S v1 and the STM32 system-contact profile | Frozen | Unverified |
| Station-S v1 Rev0 DEV/DUT socket + Core-S G031 v1 Rev0 | Intended full development combination: power, SWD, reset, boot selection, VCP UART, controls, and measurement | Frozen | Unverified |
| Station-S v1 Rev0 CTRL footprint + Core-S G031 v1 Rev0 | Intended control-Core connection; CTRL is not connected to on-board STLINK SWD | Frozen; CTRL socket parts are excluded from the authoritative Rev0 BOM | Unverified |
| MakerCard-S v1 Rev0 | Integrates the Core-S G031 circuit and exposes its Core-S contact mapping | Frozen | Unverified |
| MakerCard-S v1 Rev0 + Station-S v1 Rev0 | Electrical mapping is intended to correspond; mechanical clearance and mating are not yet claimed | Frozen | Unverified |

## Rules for future entries

- Record both product version and PCB revision.
- Distinguish “designed for” from “verified with.”
- Link verification evidence and identify the tested serial number or sample.
- Record jumper, population, firmware, and power configuration when they affect the result.
- Never infer compatibility solely from a matching `Core-S` suffix.
- A failure remains in the matrix or linked errata even after a later revision fixes it.

## Firmware portability

Core-S standardizes physical integration and selected system functions. It does not guarantee that firmware can move unchanged between different MCU implementations. Firmware portability depends on the MCU, pin map, peripheral instances, clock tree, startup configuration, and software platform.

