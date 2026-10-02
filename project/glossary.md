# CraftVia Glossary

> Status: Published terminology for the pre-release v1 documentation set. Hardware-related statements remain unverified until supported by test evidence.

| Term | Definition |
| --- | --- |
| **Core** | A compact MCU circuit containing the MCU and the circuitry needed for its declared operating configuration. |
| **Core-S** | The small CraftVia Core form factor and interface defined by the Core-S specification. The suffix identifies the physical platform, not a fixed MCU pin-function map. |
| **Core implementation** | A product that realizes the Core-S interface with a particular MCU and circuit, such as Core-S G031. |
| **Station** | Development equipment that hosts a Core and supplies programming, debugging, power, communication, breakout, control, or measurement functions. |
| **Station-S** | A Station designed for the Core-S physical platform. |
| **DEV/DUT** | The Station socket and circuitry used for the Core under development or test. DUT means device under test. |
| **CTRL Core** | A Core used to operate Station functions such as measurement and user interface. It is separate from the DEV/DUT Core. |
| **Carrier** | An application-specific host for a Core. A Carrier may be a PCB, wiring assembly, fixture, or final device. |
| **MakerCard** | A CraftVia reference format combining an MCU implementation with breakout and prototyping space in a shareable card. |
| **Physical contact ID** | A location identifier such as `N1`, `E4`, or `K-SW`. It describes position, not a universal peripheral function. |
| **Signal contact** | One of the 32 contacts `N1-N8`, `E1-E8`, `S1-S8`, and `W1-W8`. |
| **Key contact** | One of the three asymmetric corner contacts `K-NW`, `K-NE`, and `K-SW`, used for orientation and shared power. There is no `K-SE` contact. |
| **System contact** | A contact reserved by a declared implementation profile for programming, debug, reset, boot, or another system function. |
| **Implementation profile** | The mapping and operating rules published by a specific Core implementation. |
| **DNP** | Do not populate. A footprint exists in the design but the part is intentionally absent from the authoritative BOM for that revision. |
| **Version (`v`)** | A generation of product or interface compatibility. A breaking change to the interface, outline, or major behavior requires a new version. |
| **Revision (`Rev`)** | A PCB design iteration within one product version. Routing fixes, part changes, and manufacturability changes normally require a new revision. |
| **Frozen** | The exact design and manufacturing outputs have been fixed for an order or release. Frozen does not mean validated. |
| **Unverified** | Defined or fabricated but not yet demonstrated by the required hardware tests. |
| **Verified** | Checked against identified hardware, revision, procedure, and retained evidence. |
| **Canonical** | The controlling version of a document or artifact. English Markdown is canonical unless a file-specific notice says otherwise. |
| **Reference export** | A human-readable rendering such as a schematic PDF or assembly PDF. It aids review but does not replace the identified editable source, BOM, or Gerber fabrication master. |

## Normative words

- **MUST / MUST NOT** indicate a requirement.
- **SHOULD / SHOULD NOT** indicate a recommendation that requires a documented reason when not followed.
- **MAY** indicates an allowed option.

