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
  implementation guide: the namespaces, including `cdifniaid:`, and what the profile adds
  to cdifCore, whose own properties are in the cdifCore guide.
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

- **[`sourceNIAID/`](sourceNIAID/)** has 29 records as the portal's API returns them, one
  from each repository the portal harvests.
- **[`examples/`](examples/)** has the same 29 converted to CDIF, with the same file
  names (`.jsonld`), by the
  [NIAID converter](https://github.com/Cross-Domain-Interoperability-Framework/converters/tree/main/NIAID)
  at converters `1599f81`. Each one passes the JSON Schema and SHACL of every profile its
  catalog record claims.
- **`examples/exampleCDIFniaid.json`** is the profile's own example, synced from
  metadataBuildingBlocks.

All the converted records claim core and niaid. Those with discovery content also claim
discovery, and those that describe their files also claim manifest:

| Repository | Source | CDIF | Profiles claimed |
|---|---|---|---|
| accessclinicaldata@NIAID (ACD@NIAID) | [accessclinicaldata_tb-portals-natural-history-study](sourceNIAID/accessclinicaldata_tb-portals-natural-history-study.json) | [accessclinicaldata_tb-portals-natural-history-study](examples/accessclinicaldata_tb-portals-natural-history-study.jsonld) | core, manifest, niaid |
| Clinical Epidemiology Database (ClinEpiDB) | [clinepidb_ds_5c41b87221](sourceNIAID/clinepidb_ds_5c41b87221.json) | [clinepidb_ds_5c41b87221](examples/clinepidb_ds_5c41b87221.jsonld) | core, discovery, niaid |
| COVID Rapid Acceleration of Diagnostics (RADx) Data Hub | [phs002516](sourceNIAID/phs002516.json) | [phs002516](examples/phs002516.jsonld) | core, discovery, niaid |
| Data Discovery Engine (DDE) | [dde_0cf5149ad72810a2](sourceNIAID/dde_0cf5149ad72810a2.json) | [dde_0cf5149ad72810a2](examples/dde_0cf5149ad72810a2.jsonld) | core, discovery, niaid |
| Dryad Digital Repository (Dryad) | [dryad_c6c4bt8](sourceNIAID/dryad_c6c4bt8.json) | [dryad_c6c4bt8](examples/dryad_c6c4bt8.jsonld) | core, discovery, manifest, niaid |
| Electron Microscopy Public Image Archive (EMPIAR) | [empiar-10514](sourceNIAID/empiar-10514.json) | [empiar-10514](examples/empiar-10514.jsonld) | core, discovery, niaid |
| Eukaryotic Pathogen, Vector and Host Informatics Resource (VEuPathDB) | [ds_385db6b935](sourceNIAID/ds_385db6b935.json) | [ds_385db6b935](examples/ds_385db6b935.jsonld) | core, discovery, niaid |
| Figshare | [figshare_10932983](sourceNIAID/figshare_10932983.json) | [figshare_10932983](examples/figshare_10932983.jsonld) | core, niaid |
| Flow Repository | [flow_fr-fcm-zzuc](sourceNIAID/flow_fr-fcm-zzuc.json) | [flow_fr-fcm-zzuc](examples/flow_fr-fcm-zzuc.jsonld) | core, discovery, niaid |
| Harvard Dataverse | [dataverse_10.7910_dvn_07w79b](sourceNIAID/dataverse_10.7910_dvn_07w79b.json) | [dataverse_10.7910_dvn_07w79b](examples/dataverse_10.7910_dvn_07w79b.jsonld) | core, discovery, niaid |
| Human Cell Atlas (HCA) | [hca_0c3b7785-f74d-4091-8616-a68757e4c2a8](sourceNIAID/hca_0c3b7785-f74d-4091-8616-a68757e4c2a8.json) | [hca_0c3b7785-f74d-4091-8616-a68757e4c2a8](examples/hca_0c3b7785-f74d-4091-8616-a68757e4c2a8.jsonld) | core, niaid |
| Immunology Database and Analysis Portal (ImmPort) | [sdy1149](sourceNIAID/sdy1149.json) | [sdy1149](examples/sdy1149.jsonld) | core, discovery, niaid |
| Library of Integrated Network-based Cellular Signatures (LINCS) | [lds-1224](sourceNIAID/lds-1224.json) | [lds-1224](examples/lds-1224.jsonld) | core, discovery, niaid |
| Malaria Genomic Epidemiology Network (MalariaGEN) | [malariagen_gambian-genome-variation-project-open-access-data](sourceNIAID/malariagen_gambian-genome-variation-project-open-access-data.json) | [malariagen_gambian-genome-variation-project-open-access-data](examples/malariagen_gambian-genome-variation-project-open-access-data.jsonld) | core, niaid |
| Mass Spectrometry Interactive Virtual Environment (MassIVE) | [msv000083621](sourceNIAID/msv000083621.json) | [msv000083621](examples/msv000083621.jsonld) | core, discovery, niaid |
| MicrobiomeDB | [microbiome_gems1_case_control](sourceNIAID/microbiome_gems1_case_control.json) | [microbiome_gems1_case_control](examples/microbiome_gems1_case_control.jsonld) | core, niaid |
| National Omics Data Encyclopedia (NODE) | [node_oep00000195](sourceNIAID/node_oep00000195.json) | [node_oep00000195](examples/node_oep00000195.jsonld) | core, discovery, niaid |
| NCBI Database of Genotypes and Phenotypes (NCBI dbGaP) | [phs000239](sourceNIAID/phs000239.json) | [phs000239](examples/phs000239.jsonld) | core, discovery, niaid |
| NCBI Gene Expression Omnibus (NCBI GEO) | [gse128115](sourceNIAID/gse128115.json) | [gse128115](examples/gse128115.jsonld) | core, discovery, niaid |
| NICHD Data and Specimen Hub (NICHD DASH) | [nichd_dash_dataset_1132](sourceNIAID/nichd_dash_dataset_1132.json) | [nichd_dash_dataset_1132](examples/nichd_dash_dataset_1132.jsonld) | core, discovery, manifest, niaid |
| Omics Discovery Index (OmicsDI) | [pxd016017](sourceNIAID/pxd016017.json) | [pxd016017](examples/pxd016017.jsonld) | core, discovery, niaid |
| Project Tycho | [tycho_ao.840539006](sourceNIAID/tycho_ao.840539006.json) | [tycho_ao.840539006](examples/tycho_ao.840539006.jsonld) | core, discovery, niaid |
| Protein Data Bank (PDB) | [9j82](sourceNIAID/9j82.json) | [9j82](examples/9j82.jsonld) | core, discovery, niaid |
| ProteomeXchange | [pxd061439](sourceNIAID/pxd061439.json) | [pxd061439](examples/pxd061439.jsonld) | core, discovery, niaid |
| Repurposing, Focused Rescue, and Accelerated Medchem Database (REFRAMEdb) | [reframedb_a00230](sourceNIAID/reframedb_a00230.json) | [reframedb_a00230](examples/reframedb_a00230.jsonld) | core, discovery, niaid |
| SAGE Arthritis and Autoimmune and Related Diseases Knowledge Portal (SAGE ARK Portal) | [ark_syn52623570](sourceNIAID/ark_syn52623570.json) | [ark_syn52623570](examples/ark_syn52623570.jsonld) | core, discovery, niaid |
| The Network Data Exchange (NDEx) | [ndex_a3d84ced-f67c-11e9-bb65-0ac135e8bacf](sourceNIAID/ndex_a3d84ced-f67c-11e9-bb65-0ac135e8bacf.json) | [ndex_a3d84ced-f67c-11e9-bb65-0ac135e8bacf](examples/ndex_a3d84ced-f67c-11e9-bb65-0ac135e8bacf.jsonld) | core, discovery, niaid |
| VDJServer | [vdj_prjna272713](sourceNIAID/vdj_prjna272713.json) | [vdj_prjna272713](examples/vdj_prjna272713.jsonld) | core, discovery, niaid |
| Vivli | [vivli_40b1791e-dd8a-46ad-b438-35fd21b4d4bb](sourceNIAID/vivli_40b1791e-dd8a-46ad-b438-35fd21b4d4bb.json) | [vivli_40b1791e-dd8a-46ad-b438-35fd21b4d4bb](examples/vivli_40b1791e-dd8a-46ad-b438-35fd21b4d4bb.jsonld) | core, discovery, niaid |

These 29 are a subset of the 140 records in the converter's
[`niaidExamples/`](https://github.com/Cross-Domain-Interoperability-Framework/converters/tree/main/NIAID/niaidExamples)
and
[`cdifJSON-LD/`](https://github.com/Cross-Domain-Interoperability-Framework/converters/tree/main/NIAID/cdifJSON-LD).
They are copies, and are not re-synced: when the converter changes, copy them again from
those directories.

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

The sync leaves `sourceNIAID/` and the converted records in `examples/` alone.

Source profile: `_sources/profiles/cdifCompositeProfile/cdifNIAID/`.

GitHub Pages serves `main`, which is the current release. Changes are made on `updates`
and reach `main` by pull request.

## Changelog: v1.0.0

First publication, 2026-11-09, from metadataBuildingBlocks main.

## License

[CC-BY-4.0](LICENSE).
