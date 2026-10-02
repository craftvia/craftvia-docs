# Versioning and Document Status

## Product identifiers

CraftVia uses two identifiers for released hardware:

- **Version (`v`)** identifies a product or interface generation.
- **Revision (`Rev`)** identifies a PCB design iteration within that version.

Examples:

```text
v1 Rev0   first PCB revision of product generation 1
v1 Rev1   later PCB revision within the same generation
v2 Rev0   first PCB revision after a generation-level change
```

The corresponding Git tag format is:

```text
v1-rev0
v1-rev1
v2-rev0
```

## When to change each identifier

A new **version** is required when a change intentionally breaks the published product or interface compatibility contract, including a change to mating geometry, shared power assignment, or a major product role.

A new **revision** is required when the physical design or manufacturing definition changes without creating a new product generation. Examples include schematic or routing corrections, footprint changes, part substitutions that affect the design, or silkscreen changes used for hardware identification.

Documentation-only corrections do not by themselves require a new hardware revision. They must not silently change the meaning of a frozen hardware design.

## Status vocabulary

| Status | Meaning |
| --- | --- |
| **Concept** | Directional material; not a requirement and not ready to implement. |
| **Draft** | Under active review and subject to change. |
| **Frozen** | The identified design files and manufacturing outputs have been fixed. Hardware may still be unverified. |
| **Unverified** | A requirement or implementation has not yet passed its required hardware validation. |
| **Verified** | Validation passed against identified hardware and retained evidence. |
| **Rejected** | Tested and found not to meet the acceptance criteria. The record is retained. |
| **Superseded** | Retained for history but replaced by an identified document, version, or revision. |

`Frozen` describes change control. `Unverified` and `Verified` describe evidence. A frozen Rev0 can therefore be unverified.

## Branch, tag, and release state

- `main` normally represents the latest verified hardware.
- `develop` represents the design being developed, fabricated, assembled, or validated.
- Before any verified revision exists, an unverified Rev0 may be published on `main` if the warning is prominent.
- The exact commit used for fabrication receives an annotated version-and-revision tag.
- A GitHub Release made before validation is marked as a pre-release and states the unverified scope.
- A tag is never moved or reused. A design correction creates a new revision.
- Passing validation updates the status and evidence without replacing the tagged design.

## Document identity

A revision-specific document MUST identify:

- product name;
- product version and PCB revision;
- document status;
- applicable design release or tag;
- verification state;
- controlling source when the document is a reference rather than a manufacturing master.

English is canonical. Japanese translations use the same filename with `.ja.md` inserted before the extension.

