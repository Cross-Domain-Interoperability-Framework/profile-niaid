# AGENTS.md: AI agent guidance for CDIF NIAID (domain profile)

## Project context

This repository publishes the **CDIF NIAID profile** (`cdifNIAID`,
`https://w3id.org/cdif/niaid/1.0`). It is for dataset records from the NIAID Data
Discovery Portal, and composes cdifCore with the niaidDataset block.

## Key files

- `cdifNIAIDStructuredSchema.json`: JSON Schema (generated)
- `niaidRules.shacl`: merged SHACL shapes (generated)
- `CDIFNIAIDImplementationGuide.md`: implementation guide (generated draft, hand-written introduction)
- `examples/`: validated JSON-LD examples

## Synced files: do not hand-edit

The schema, the SHACL and `examples/exampleCDIFniaid.json` are generated in
metadataBuildingBlocks. Change the source there and re-sync with
`python tools/sync_release_repos.py --apply --repo profile-niaid`, run from that repo.

- Source profile: `metadataBuildingBlocks/_sources/profiles/cdifCompositeProfile/cdifNIAID/`.
- NIAID blocks: `metadataBuildingBlocks/_sources/niaidProperties/`.
- Converter that makes the records: `converters/NIAID/`.

## Branches

GitHub Pages serves `main`, and w3id resolves to it. `main` is the current release. Sync
onto `updates`, and move changes to `main` only by pull request at release time.

## Validation

Records are validated after framing, against every profile their catalog record
claims, by `ConformanceValidate.py` in the validation repo. The SHACL rules can also be
run directly:

```bash
pyshacl -s niaidRules.shacl -i rdfs -w -df json-ld examples/<file>.json
```
