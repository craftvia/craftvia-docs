# CraftVia Core-S Debug, Programming, and USB Port v1

> [!WARNING]
> **Status: unverified specification**
> This specification has not yet been verified with a native-USB Core-S and a conforming Station-S. English is canonical. See the [Japanese translation](core-s-debug-port-v1.ja.md).

## 1. Scope

This document defines the common development-port profiles carried by Core-S north contacts N1 through N8. It separates basic debug and download signals, optional JTAG/trace signals, and native USB so that a target USB connection does not replace the primary recovery interface.

A Core declares only the profiles it implements. Contacts belonging to an undeclared profile remain implementation-specific GPIOs or NC. A Station must not drive a profile based only on contact position.

## 2. Common contacts

Signal directions are stated relative to the Core.

| Contact | Common name | Basic purpose | Profile-dependent use |
| --- | --- | --- | --- |
| N1 | `DBG_RESET` | Reset or enable | Polarity, pull network, and electrical method are declared by the Core profile |
| N2 | `DBG_DATA0` | Bidirectional data or Core receive | SWDIO, UART RXD from probe TX, or JTAG TMS |
| N3 | `DBG_DATA1` | Clock or Core transmit | SWCLK, UART TXD to probe RX, or JTAG TCK |
| N4 | `DBG_BOOT` | Boot or download-mode selection | The Station is normally High-Z; polarity and reset sequence are profile-specific |
| N5 | `DBG_AUX0` | Extended debug input | JTAG TDI; otherwise implementation-specific GPIO or NC |
| N6 | `DBG_AUX1` | Extended debug output | JTAG TDO or SWO; otherwise implementation-specific GPIO or NC |
| N7 | `USB_DM` | Target USB D- | USB only when the Core declares the native USB profile; otherwise GPIO or NC |
| N8 | `USB_DP` | Target USB D+ | USB only when the Core declares the native USB profile; otherwise GPIO or NC |

N7 and N8 form an adjacent differential pair. K-NE/GND is adjacent to N8 and should connect to the Station ground plane with a short path. Do not route ground between N7 and N8.

## 3. Profiles

### 3.1 `CVDBG-SWD`

| Contact | Assignment |
| --- | --- |
| N1 | nRESET / NRST |
| N2 | SWDIO |
| N3 | SWCLK |
| N4 | BOOT or a logical boot request |

N2 is bidirectional. The Station keeps N4 High-Z except while executing the Core's documented boot sequence. If N3 and N4 reach the same MCU node, the Core specification must define isolation and prohibit conflicting drive.

### 3.2 `CVDBG-SWD-TRACE`

This profile adds `N6=SWO` to `CVDBG-SWD`. A Station must leave N6 disconnected for a Core that does not declare trace support.

### 3.3 `CVDBG-UART-DL`

| Contact | Assignment |
| --- | --- |
| N1 | RESET / EN |
| N2 | Core RXD, driven by probe TX |
| N3 | Core TXD, received by probe RX |
| N4 | BOOT / download-mode selection |
| N5/N6 | Optional handshaking or unused |

The Core must boot normally with the Station disconnected. UART download support does not by itself claim breakpoint debugging.

### 3.4 `CVDBG-JTAG`

| Contact | Assignment |
| --- | --- |
| N1 | Target reset |
| N2 | TMS |
| N3 | TCK |
| N4 | BOOT or profile-specific control |
| N5 | TDI |
| N6 | TDO |

nTRST is not assigned by this common profile. A Core that requires nTRST must document its implementation or declare JTAG unsupported. MCU pin-remap rules, security settings, option bytes, and errata remain Core-specific.

### 3.5 `CVDBG-USB`

| Contact | Assignment |
| --- | --- |
| N7 | USB_DM |
| N8 | USB_DP |

N7/N8 carry the target's native USB interface. The individual Core specification states whether that interface supports a ROM bootloader, firmware update, console, integrated USB Serial/JTAG, application USB, or another function. USB connectivity does not imply SWD/JTAG-equivalent debugging.

## 4. Electrical and ownership rules

### 4.1 Core responsibilities

- MCU- or PHY-specific D+/D- series termination, pulls, and biasing;
- PHY power decoupling and clock requirements;
- safe default RESET, EN, and BOOT states without a Station;
- MCU-to-contact routing and disclosure of reset/unpowered states;
- option-byte, pin-remap, security, and errata constraints.

Do not add a generic USB resistor network when the selected MCU already integrates the required termination or pull-up.

### 4.2 Station or Carrier responsibilities

- USB connector and, for USB-C, CC and port-role circuitry;
- VBUS protection and power switching;
- low-capacitance connector-side ESD protection;
- USB path selection or isolation;
- debug-probe and UART-path selection;
- High-Z safe state for all unselected drivers.

USB VBUS must not be connected directly to the Core-S +3V3 contact. A Station must isolate USB from N7/N8 when the installed Core does not declare `CVDBG-USB`, and isolate JTAG/trace drivers from N5/N6 when the Core does not declare those profiles.

## 5. Host behavior

- Detect or explicitly select the installed Core profile before enabling a driver.
- Default to all development-port drivers disconnected when identification fails.
- Do not connect USB to N2/N3.
- Do not connect SWD, UART, or JTAG drivers to N7/N8.
- Do not connect multiple probes or independently powered outputs to one contact.
- Use a USB 2.0-capable low-capacitance switch when USB switching is required.
- Keep USB stubs short and route N7/N8 over a continuous reference plane toward 90-ohm differential impedance.
- Perform Core insertion and removal only while power is off.

## 6. Core declaration requirements

Each Core specification publishes:

- supported profile names;
- N1-N8 net, MCU pin, and package pin mapping;
- direction, voltage, pulls, and reset/unpowered state;
- RESET/EN and BOOT polarity and operating sequence;
- programming, breakpoint debug, console, trace, and USB feature scope;
- recovery procedure and required tools;
- USB PHY-specific parts and Station requirements;
- conflicts with GPIO, clock, option-byte, or security functions.

## 7. Legacy N2/N3 USB draft

An earlier pre-verification draft allowed `N2=USB_D-` and `N3=USB_D+`. No released Core-S declares that profile. It is withdrawn and must not be used for new Core designs.

Station-S v1 Rev0 physically implements the withdrawn N2/N3 USB path. That board remains usable for its primary ST-LINK/SWD purpose, but does not conform to `CVDBG-USB` without documented rework. Its frozen design files remain authoritative records of the Rev0 hardware.

## 8. Conformance and verification

A design must not claim verified conformance until the declared profiles are exercised on identified hardware. At minimum verify:

- reset, boot, programming, recovery, and unselected-driver isolation;
- signal voltage and target-voltage sensing;
- UART direction where declared;
- JTAG or SWO routing where declared;
- N7/N8 polarity, enumeration, sustained USB transfer, and SWD recovery where USB is declared;
- safe behavior with unsupported profile paths disconnected.
