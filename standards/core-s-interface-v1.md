# CraftVia Core-S Interface v1

> [!WARNING]
> **Status: Unverified specification**  
> The interface is implemented by frozen Rev0 designs, but mechanical fit, connector selection, insertion behavior, current capacity, and complete electrical operation have not yet been validated on hardware.

## 1. Scope

Core-S v1 defines a 25.40 mm square, 3.3 V MCU Core interface for use with a Station, Carrier, fixture, or prototype wiring. It standardizes geometry, contact identity, orientation, shared power, and an STM32 system-contact profile.

Except for declared system contacts, Core-S does **not** assign a universal UART, I2C, SPI, ADC, PWM, USB, or CAN function to a physical contact. Each Core implementation publishes its own mapping.

## 2. Interface summary

| Item | Core-S v1 requirement |
| --- | --- |
| PCB outline | 25.40 mm x 25.40 mm square, nominal |
| PCB thickness | 1.60 mm nominal |
| Signal contacts | 32 total; eight on each side |
| Key contacts | Three: `K-NW`, `K-NE`, `K-SW` |
| Total contacts | 35 |
| Pitch | 2.54 mm |
| Shared supply | 3.3 V nominal |
| Reference logic level | 3.3 V CMOS |
| Key assignment | `K-NW`=GND, `K-NE`=GND, `K-SW`=+3V3; no `K-SE` contact |
| Reference connector | 2.54 mm pitch, nominal 0.64 mm square pin |
| Insertion | Power off only; hot-plugging is not supported |

## 3. Orientation and numbering

Coordinates are defined while viewing the Core component side from above. North is up, east is right, the board center is `(0, 0)`, +X is east, and +Y is north.

```text
                              NORTH

      K-NW  N1 N2 N3 N4 N5 N6 N7 N8  K-NE
       GND   o  o  o  o  o  o  o  o    GND

      W8 o                              o E1
      W7 o                              o E2
      W6 o                              o E3
      W5 o           Core-S             o E4
      W4 o                              o E5
      W3 o                              o E6
      W2 o                              o E7
      W1 o                              o E8

       3V3   o  o  o  o  o  o  o  o
      K-SW  S8 S7 S6 S5 S4 S3 S2 S1   no K-SE

                              SOUTH
```

The missing southeast key contact makes the intended rotation unique. This asymmetry does not protect against powered partial insertion.

## 4. Mechanical requirements

### 4.1 Outline and contacts

| Item | Requirement |
| --- | --- |
| Width and height | 25.40 mm nominal |
| Recommended outline tolerance | within +/-0.20 mm |
| Contact center from board edge | 1.27 mm nominal |
| Finished hole | 1.00 mm recommended |
| Pad diameter | 1.80-2.00 mm recommended |
| Reference pin section | 0.64 mm square nominal |
| Reference pin projection below Core | 6.0 mm nominal; subject to Rev0 validation |
| Component overhang | No component may extend outside the PCB outline |

### 4.2 Contact-center coordinates

| Contact | X coordinate (mm) | Y coordinate (mm) |
| --- | ---: | ---: |
| `K-NW` | -11.43 | +11.43 |
| `K-NE` | +11.43 | +11.43 |
| `K-SW` | -11.43 | -11.43 |
| `N1-N8` | -8.89, -6.35, -3.81, -1.27, +1.27, +3.81, +6.35, +8.89 | +11.43 |
| `E1-E8` | +11.43 | +8.89, +6.35, +3.81, +1.27, -1.27, -3.81, -6.35, -8.89 |
| `S1-S8` | +8.89, +6.35, +3.81, +1.27, -1.27, -3.81, -6.35, -8.89 | -11.43 |
| `W1-W8` | -11.43 | -8.89, -6.35, -3.81, -1.27, +1.27, +3.81, +6.35, +8.89 |

The reference implementation uses downward-projecting male pins on the Core and mating female contacts on the host. Final connector type, stack height, insertion force, and repeated-insertion life remain validation items.

## 5. Electrical requirements

### 5.1 Shared power

| Contact | Assignment |
| --- | --- |
| `K-NW` | GND |
| `K-NE` | GND |
| `K-SW` | +3V3 input to the Core |

The recommended host supply range is 3.135-3.465 V (3.3 V +/-5%). The provisional Core-only current design target is no more than 500 mA; this limit remains subject to connector and temperature validation.

Core-S v1 provides no shared 5 V or raw-supply contact. It does not guarantee reverse-polarity, overcurrent, surge, powered-insertion, or back-power protection. These protections belong in the host and the implementation-specific design.

### 5.2 Signal contacts

- Signal contacts use 3.3 V logic unless an implementation specification states a stricter condition.
- Do not apply 5 V merely because a particular MCU pin may be 5 V tolerant; tolerance depends on mode, supply state, and device limits.
- Do not drive a signal into an unpowered Core unless the implementation specification explicitly permits it.
- Absolute maximum ratings, analog limits, drive current, and reset-state behavior come from the Core implementation and its component documentation.

## 6. STM32 system-contact profile

An STM32 Core claiming **Core-S v1 STM32 System Compatible** MUST implement:

| Contact | Series signal | Requirement |
| --- | --- | --- |
| `N1` | `SYS_NRST` | Active-low MCU reset |
| `N2` | `SYS_SWDIO` | SWD data input/output |
| `N3` | `SYS_SWCLK` | SWD clock; may share an MCU boot function |
| `N4` | `SYS_BOOT` | Host boot-mode request; implementation-specific circuit and sequence |

`SYS_BOOT` is a logical request and need not be a direct MCU BOOT pin. The Core specification MUST state its active level, electrical circuit, reset sequence, option-byte assumptions, and prohibited simultaneous-drive conditions.

For Core-S G031 Rev0, N3 and N4 reach the same PA14/BOOT0 MCU pin through different resistors. A host MUST isolate the SWCLK driver before actively driving `SYS_BOOT`.

## 7. Optional development-port profiles

Detailed requirements are defined by [Core-S Debug, Programming, and USB Port v1](core-s-debug-port-v1.md).

### 7.1 Extended debug on N5/N6

A Core MAY declare `N5=DBG_AUX0` and `N6=DBG_AUX1`. The common JTAG profile assigns TDI to N5 and TDO to N6; the SWD trace profile may assign SWO to N6. Without an explicit declaration, a Station must treat N5/N6 as implementation-specific contacts and must not connect a debug driver to them.

### 7.2 Native USB on N7/N8

A Core MAY declare a USB 2.0 device profile using `N7=USB_DM` and `N8=USB_DP`. This does not make USB universal across Core-S products. Without that declaration, a Station must treat N7/N8 as implementation-specific contacts and isolate its USB path.

The Core supplies MCU- or PHY-specific termination, pull, bias, power-decoupling, and clock provisions. The Station supplies connector-side CC, VBUS protection, ESD protection, and path isolation. USB VBUS must not connect directly to the Core-S +3V3 contact.

The earlier pre-verification `N2=USB_D-`, `N3=USB_D+` draft profile is withdrawn and must not be used for new Core designs. N2/N3 remain the basic debug/data contacts defined by the selected profile.

## 8. Implementation-specific contacts

Unless a Core declares an optional development-port profile, `N5-N8` are implementation-specific. `E1-E8`, `S1-S8`, and `W1-W8` have physical identities but no universal peripheral mapping. An implementation specification MUST publish, for every contact:

- MCU or circuit node;
- package-pin number where applicable;
- representative alternate functions;
- reset and power-off behavior;
- electrical limitations;
- conflicts or mutually exclusive uses;
- NC or reserved state.

## 9. Host requirements

A Core-S v1 host MUST:

- preserve the contact positions, orientation, and missing `K-SE` key;
- connect both ground keys and the +3V3 key correctly;
- keep all active drivers high impedance while a Core is inserted or removed;
- prevent two independently powered sources from being directly paralleled;
- document the exact Core implementation or profile it supports;
- avoid assuming implementation-specific functions from contact position alone.

## 10. Conformance labels

| Label | Minimum meaning |
| --- | --- |
| **Core-S v1 Mechanical Compatible** | Outline, contact coordinates, key arrangement, and mating orientation conform. |
| **Core-S v1 Compatible** | Mechanical requirements, shared power, voltage rules, safety constraints, and required implementation documentation conform. |
| **Core-S v1 STM32 System Compatible** | Core-S v1 Compatible plus the N1-N4 STM32 system-contact profile conforms. |

A frozen but untested design may state **designed for** one of these labels. It must not state verified conformance until the relevant validation plan has passed.

## 11. Required validation before verification

- PCB outline, thickness, contact coordinates, hole size, and key position;
- header and socket dimensions, stack height, polarity, and mating clearance;
- power and ground continuity with no short;
- supply voltage and current under representative load;
- contact continuity and adjacent-contact isolation;
- reset, debug, and boot operation for each declared system profile;
- insertion and removal only while unpowered;
- temperature rise and contact suitability at the declared maximum current.
