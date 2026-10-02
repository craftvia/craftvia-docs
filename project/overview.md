# CraftVia Project Overview

> [!IMPORTANT]
> **Pre-release documentation — Unverified hardware**  
> CraftVia v1 Rev0 hardware has been frozen and ordered, but it has not yet been assembled, powered, or validated. This document describes the intended platform and the frozen Rev0 design; it does not claim successful hardware operation.

## Purpose

CraftVia is an open embedded-development platform for moving a microcontroller circuit through a practical development path:

```text
Develop, program, and measure on a Station
    -> move the Core to a prototype or application-specific Carrier
    -> integrate the proven Core circuit into a custom PCB when appropriate
```

The platform separates the minimum circuit needed to operate a microcontroller from development-only facilities such as the debugger, USB interface, operator controls, breakout wiring, and measurement hardware.

## Platform elements

### Core

A Core is a compact MCU circuit containing the MCU and the circuitry required for its intended operating configuration. A Core-S implementation follows the Core-S mechanical and electrical interface and publishes an implementation-specific pin map.

The first implementation is [CraftVia Core-S G031](https://github.com/craftvia/craftvia-core-s-g031), based on the STM32G031K8T6.

### Station

A Station provides the facilities used while developing and validating a Core: power, programming and debugging, communication, breakout access, controls, and measurement. Station-S Rev0 is designed primarily for Core-S G031 Rev0 and also includes manually selected paths intended for future Core profiles.

See [CraftVia Station-S](https://github.com/craftvia/craftvia-station-s).

### Carrier

A Carrier is an application-specific board, wiring assembly, or mechanical installation that hosts a Core. Core-S defines the mating geometry and shared electrical constraints, but it does not make application signals interchangeable between different Core implementations.

### MakerCard

MakerCard is a reference path between Station-based development and a fully custom Carrier or integrated MCU board. MakerCard-S Rev0 combines the Core-S G031 circuit with breakout and prototyping areas in a shareable card format.

See [CraftVia MakerCard-S](https://github.com/craftvia/craftvia-makercard-s).

## What is standardized

CraftVia common documentation standardizes:

- terminology and document status;
- the relationship between Core, Station, Carrier, and MakerCard;
- the Core-S mechanical interface, contact identifiers, keying, and shared power rules;
- compatibility and conformance terminology;
- release identification using product version and PCB revision.

Product repositories define implementation-specific circuits, MCU mappings, options, manufacturing outputs, and validation evidence.

## Current public hardware

| Hardware | Version and revision | Design state | Hardware state |
| --- | --- | --- | --- |
| Core-S G031 | v1 Rev0 | Frozen for prototype fabrication | Ordered; unassembled and unverified |
| Station-S | v1 Rev0 | Frozen for prototype fabrication | Ordered; unassembled and unverified |
| MakerCard-S | v1 Rev0 | Frozen for prototype fabrication | Ordered; unassembled and unverified |

## Documentation model

English documents are canonical. A Japanese translation is stored beside each English document using the `.ja.md` suffix. Common requirements live in this repository; revision-specific requirements and test evidence live in the applicable hardware repository.

When documents disagree, use this precedence:

1. the frozen design source and manufacturing release for the identified hardware revision;
2. the product revision specification in the product repository;
3. the common interface specification;
4. explanatory guides and historical design notes.

An inconsistency must be recorded and corrected; precedence is not permission to ignore it.

