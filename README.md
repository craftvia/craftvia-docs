# CraftVia Documentation

> [!IMPORTANT]
> **Pre-release documentation**  
> CraftVia is in early hardware development. Specifications may change as Rev0 hardware is assembled and verified. English is the canonical language. Current Rev0 product descriptions are frozen-design references, not hardware-verification claims.

[日本語](README.ja.md) · [CraftVia](https://craftvia.org) · [GitHub organization](https://github.com/craftvia)

This repository contains the canonical common documentation for the CraftVia open embedded-development platform. Internal planning notes and earlier Japanese design studies are inputs to the published documents, not specifications by themselves.

Product-specific editable design sources, manufacturing files, and release notes belong in the relevant hardware repository.

## Documentation map

| Public document | English canonical |
| --- | --- |
| Detailed project overview | [`project/overview.md`](project/overview.md) |
| Terminology | [`project/glossary.md`](project/glossary.md) |
| Versioning and status | [`standards/versioning-and-status.md`](standards/versioning-and-status.md) |
| Core-S interface v1 | [`standards/core-s-interface-v1.md`](standards/core-s-interface-v1.md) |
| Compatibility policy and matrix | [`standards/compatibility.md`](standards/compatibility.md) |
| Rev0 getting started | [`guides/getting-started.md`](guides/getting-started.md) |

Manufacturing data remains in the [Core-S G031](https://github.com/craftvia/craftvia-core-s-g031), [Station-S](https://github.com/craftvia/craftvia-station-s), and [MakerCard-S](https://github.com/craftvia/craftvia-makercard-s) product repositories.

## Documentation policy

- English is the source of truth.
- Japanese is maintained as an official translation beside the English file using the `.ja.md` suffix.
- Specifications must not be duplicated in `craftvia-web`.
- Product-specific manufacturing data belongs in product repositories.
- A document must state its status when it is a concept, draft, unverified specification, or verified specification.
- If translations differ, the English version takes precedence after an English canonical document has been reviewed and published.

## Status vocabulary

| Status | Meaning |
| --- | --- |
| Concept | Directional material; not a requirement |
| Draft | Under active review and subject to change |
| Unverified | Defined but not yet demonstrated on hardware |
| Verified | Checked against identified hardware, revision, and test evidence |
| Superseded | Retained for history; replaced by a named document or revision |

## License and contributions

Unless a file-specific notice says otherwise, documentation in this repository is licensed under [CC BY 4.0](LICENSE). Hardware designs are licensed under CERN-OHL-P-2.0 and software under Apache-2.0 when those categories are included and identified. See the [complete licensing policy](LICENSES/README.md).

The CraftVia name and logos are not covered by those open licenses. They are owned by Kohei Ikeda and governed by the [CraftVia Trademark Policy](LICENSES/TRADEMARK_POLICY.md). Contributions are accepted on the basis that they may be distributed under the applicable repository license; a separate contribution policy will define the detailed process.
