# Getting Started with CraftVia Rev0

> [!WARNING]
> All current CraftVia Rev0 boards are unverified engineering prototypes. Do not treat the published files as production-qualified hardware.

## Choose the relevant repository

- [Core-S G031](https://github.com/craftvia/craftvia-core-s-g031): compact STM32G031 Core design.
- [Station-S](https://github.com/craftvia/craftvia-station-s): development, debug, breakout, power, and measurement platform.
- [MakerCard-S](https://github.com/craftvia/craftvia-makercard-s): integrated G031 reference circuit with breakout and prototyping areas.

Read the repository README, revision specification, verification plan, and release notes before using manufacturing files.

## Understand the release artifacts

| Artifact | Role |
| --- | --- |
| EasyEDA project in `source/` | Authoritative editable design source |
| Gerber ZIP in `fabrication/` | Canonical PCB fabrication upload for the identified release |
| BOM CSV in `assembly/` | Authoritative populated-part list |
| CPL / pick-and-place CSV | Full coordinate export; may include DNP and non-BOM rows and must be reconciled with the BOM |
| Schematic PDF in `docs/` | Human-readable circuit reference, not the fabrication master |
| PCB/assembly PDF | Visual reference, not a substitute for the BOM or Gerber ZIP |
| `SHA256SUMS.txt` | Integrity manifest for frozen release files |

## Before ordering

1. Select the exact version-and-revision release.
2. Read every warning and known condition in `RELEASE_NOTES.md`.
3. Verify file hashes against `SHA256SUMS.txt`.
4. Upload the complete Gerber ZIP without editing or recompressing it.
5. Review the manufacturer's Gerber preview for outline, layer count, drills, masks, and silkscreen.
6. Reconcile the CPL against the authoritative BOM; do not assume every CPL row is populated.
7. Confirm through-hole connector dimensions and the intended mechanical stack before assembly.

## Before first power

1. Follow the product verification plan.
2. Inspect orientation, soldering, shorts, DNP state, and jumper state.
3. Check resistance between every supply rail and GND.
4. Use a current-limited supply for first power.
5. Record board identity, configuration, instruments, measurements, and evidence.
6. Stop if any acceptance limit is exceeded; do not continue by increasing the current limit.

## Reporting results

Report the exact product, version, revision, assembly state, and test ID. A useful report includes photographs, instrument readings, firmware or command versions, jumper state, and whether the result passed, failed, or could not be completed.

