# CDIF NIAID (domain profile)

This repository holds the published files for the **CDIF NIAID profile**, the
`cdifNIAID` building block from the
[metadataBuildingBlocks](https://github.com/Cross-Domain-Interoperability-Framework/metadataBuildingBlocks)
source register. Its conformance URI is **`https://w3id.org/cdif/niaid/1.0`**.

> **Scope.** `cdifNIAID` is for dataset records from the
> [NIAID Data Discovery Portal](https://data.niaid.nih.gov/). It composes cdifCore with
> niaidDataset, which constrains the NIAID (`nde:`), Bioschemas (`bios:`) and
> `cdifniaid:` properties those records carry. A record with discovery content claims
> `https://w3id.org/cdif/discovery/1.1` as well, as its own `conformsTo` entry.

## Specification

- **[CDIFNIAIDImplementationGuide.md](CDIFNIAIDImplementationGuide.md)**: the
  implementation guide (an auto-generated draft, with a hand-written introduction).
- **[cdifNIAIDStructuredSchema.json](cdifNIAIDStructuredSchema.json)**: the resolved
  JSON Schema (Draft 2020-12), generated from the source register.
- **[niaidRules.shacl](niaidRules.shacl)**: self-contained SHACL shapes, merged from
  cdifCore and the NIAID blocks. cdifNIAID has no shapes of its own.

| URI | Serves |
|---|---|
| `https://w3id.org/cdif/niaid/1.0/schema` | `cdifNIAIDStructuredSchema.json` |
| `https://w3id.org/cdif/niaid/1.0/shacl` | `niaidRules.shacl` |
| `https://w3id.org/cdif/niaid/1.0/guide` | the implementation guide |
| `https://w3id.org/cdif/niaid/1.0` | by `Accept`: the schema (JSON), the shapes (Turtle), else the guide |

## Examples

`examples/exampleCDIFniaid.json` is a converted portal record. For 140 more, all valid
against this profile, see
[converters/NIAID/cdifJSON-LD](https://github.com/Cross-Domain-Interoperability-Framework/converters/tree/main/NIAID/cdifJSON-LD).

The JSON Schema applies to a record after framing. The
[validation](https://github.com/Cross-Domain-Interoperability-Framework/validation)
repository's `ConformanceValidate.py` frames a record, then validates it against every
profile its catalog record claims:

```bash
python ConformanceValidate.py examples/exampleCDIFniaid.json -v
```

The SHACL rules need no framing:

```bash
pyshacl -s niaidRules.shacl -i rdfs -w -df json-ld examples/exampleCDIFniaid.json
```

## Synced from metadataBuildingBlocks

These generated files are re-synced when the source register changes, by
metadataBuildingBlocks' `python tools/sync_release_repos.py --apply --repo profile-niaid`:

| file | source command |
|---|---|
| `cdifNIAIDStructuredSchema.json` | `python tools/resolve_schema.py cdifNIAID -o cdifNIAIDStructuredSchema.json` |
| `niaidRules.shacl` | `python tools/validate_shacl.py cdifNIAID --emit-shapes niaidRules.shacl` |
| `examples/exampleCDIFniaid.json` | copied from the source profile directory |

Source profile: `_sources/profiles/cdifCompositeProfile/cdifNIAID/`.

GitHub Pages serves `main`, which is the current release. Changes are made on `updates`
and reach `main` by pull request.

## Changelog: v1.0.0

First publication, 2026-11-09, from metadataBuildingBlocks main.

## License

[CC-BY-4.0](LICENSE).
