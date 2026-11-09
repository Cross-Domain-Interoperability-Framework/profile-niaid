# CDIF NIAID Profile — Implementation Guide

> **Draft.** This guide was auto-generated from the StructuredSchema. Edit freely — descriptions, ordering, and the introductory prose should be curated by hand.

# Purpose and scope

The **CDIF NIAID profile** (`cdifNIAID`) is a document-level CDIF profile for dataset records from the [NIAID Data Discovery Portal](https://data.niaid.nih.gov/). It composes cdifCore with niaidDataset, which constrains the NIAID (`nde:`), Bioschemas (`bios:`) and `cdifniaid:` properties those records carry.

cdifDiscovery is not composed, because about one portal record in six has no discovery content. A record that has it also claims `https://w3id.org/cdif/discovery/1.1` as its own `conformsTo` entry, and is validated against that profile separately.

Records in this profile are made from the portal's API by the table-driven converter in [converters/NIAID](https://github.com/Cross-Domain-Interoperability-Framework/converters/tree/main/NIAID). Its [`cdifJSON-LD/`](https://github.com/Cross-Domain-Interoperability-Framework/converters/tree/main/NIAID/cdifJSON-LD) directory holds 140 converted portal records that validate against this profile.

# Conformance

A resource conforms to the CDIF NIAID profile when its catalog record declares conformance to the profile identifier. The catalog record is carried on `schema:subjectOf` as a `dcat:CatalogRecord`:

```json
"schema:subjectOf": {
  "@type": ["schema:CreativeWork", "dcat:CatalogRecord"],
  "dcterms:conformsTo": [
    "https://w3id.org/cdif/niaid/1.0"
  ]
}
```

Other properties added in this profile are optional; conformance requires only that the constraints in the JSON Schema and SHACL rules are satisfied.

## Validation

Two validators ship with this repository:
- **JSON Schema** — `cdifNIAIDStructuredSchema.json` (Draft 2020-12), generated from the source register.
- **SHACL** — `niaidRules.shacl`, a self-contained shapes graph merged from every composing building block plus the profile-level shapes.

The JSON Schema applies to a record **after framing**: the CDIF frame selects the dataset node and wraps multi-valued properties as arrays. `ConformanceValidate.py`, in the [validation](https://github.com/Cross-Domain-Interoperability-Framework/validation) repository, frames the record. It then validates it against the schema and SHACL of every conformance URI the record's catalog record declares, fetched through w3id:

```bash
python ConformanceValidate.py examples/exampleCDIFniaid.json -v
```

The SHACL rules apply to the RDF graph directly, with no framing:

```bash
pyshacl -s niaidRules.shacl -i rdfs -w -df json-ld examples/exampleCDIFniaid.json
```

`-w` lets warnings pass; only `sh:Violation` results fail a record.

Validation is **open-world**: properties not described by the profile are allowed.

# Provenance of the artifacts

The schema and SHACL files are generated from the canonical source register, [metadataBuildingBlocks](https://github.com/Cross-Domain-Interoperability-Framework/metadataBuildingBlocks):

- `cdifNIAIDStructuredSchema.json` ← `tools/resolve_schema.py cdifNIAID`
- `niaidRules.shacl` ← `tools/validate_shacl.py cdifNIAID --emit-shapes`

Source profile directory: `_sources/profiles/cdifCompositeProfile/cdifNIAID/`.

# Dataset Properties added by the CDIF NIAID Profile

## schema:Dataset {#sec-schema-dataset}

CDIF profile for dataset records from the NIAID Data Discovery Portal. Composes cdifCore with niaidDataset, which constrains the NIAID (nde:), Bioschemas (bios:) and cdifniaid: properties those records carry. cdifDiscovery is not composed: about one record in six from the portal has no discovery content, so a record that has it claims and is validated against cdifDiscovery as well, as its own conformsTo entry.

### @context

- **Cardinality:** Optional
- **Content:** object
- **Description:** JSON-LD context declaring namespace prefixes used in the metadata record.

### @id

- **Cardinality:** Optional
- **Content:** string
- **Description:** The URI for the resource should be the @id value for the root of the JSON instance document tree. Must be an IRI (e.g. https://doi.org/..., urn:..., or a relative URI like #localid). Note that this identifier can be interpreted to identify the resource that is the subject of this metadata record, or the JSON-LD object that is the digital object containing the metadata information.

### @type

- **Cardinality:** Optional
- **Content:** array of string (`"schema:CreativeWork"` | `"schema:SoftwareApplication"` | `"schema:SoftwareSourceCode"` | `"schema:Product"` | `"schema:WebAPI"` | `"schema:Dataset"` | `"schema:DigitalDocument"` | `"schema:Collection"` | `"schema:ImageObject"` | `"schema:DataCatalog"` | `"schema:DefinedTermSet"` | `"schema:MediaObject"`)
- **Description:** a schema.org Class that specifies the expected information content for the metadata record. The array must include at least one schema.org type value. Default is schema:Dataset.

### schema:name

- **Cardinality:** Optional
- **Content:** string
- **Description:** A descriptive name of a dataset (e.g., 'Snow depth in Northern Hemisphere'). The name should uniquely identify the described resource for human use, in the scope of the metadata catalog containing this metadata record.

### schema:description

- **Cardinality:** Optional
- **Content:** string
- **Description:** A short summary describing a dataset. This text will be indexed by search applications, so the more information here, the better.

### schema:identifier

- **Cardinality:** Optional
- **Content:** one of: [object reference](#/$defs/Identifier), string
- **Description:** The primary identifier for the dataset; other identifiers should be listed in the sameAs field. Schema.org has three ways of encoding identifiers-- a text description, a URL, or by using the schema:PropertyValue field. The Science on Schema.org guidance strongly recommends using the PropertyValue approach. see https://github.com/ESIPFed/science-on-schema.org .... Dataset.md#identifier. Ideally, for any given data provided they would provide identifiers either all as strings or all as identifier_type.

### schema:additionalType

- **Cardinality:** Optional
- **Content:** array of [object reference](#/$defs/cdifConceptOrTermOrString)
- **Description:** identifiers for datatypes from other vocabularies (not schema.org) that apply to this metadata.

### schema:sameAs

- **Cardinality:** Optional
- **Content:** array of one of: string, [object reference](#/$defs/ObjectReference), [object reference](#/$defs/Identifier)
- **Description:** Other identifiers for the dataset, as IRI references, literal strings, or structured identifiers using schema:PropertyValue.

### schema:version

- **Cardinality:** Optional
- **Content:** string or number
- **Description:** The version number or identifier for this dataset (text or numeric). The values should sort from oldest to newest using an alphanumeric sort on version strings

### schema:inLanguage

- **Cardinality:** Optional
- **Content:** string
- **Description:** the language of the dataset content

### schema:dateModified

- **Cardinality:** Optional
- **Content:** string
- **Description:** ISO8601 formatted date (and optional time if relevant) when Dataset was last updated

### schema:datePublished

- **Cardinality:** Optional
- **Content:** string
- **Description:** ISO8601 formatted date (and optional time if relevant) when Dataset was made public.

### schema:conditionsOfAccess

- **Cardinality:** Optional
- **Content:** array of one of: string, [object reference](#/$defs/ObjectReference), [object reference](#/$defs/Reference)
- **Description:** text statement of conditions for use and access; if an online resource documents the restrictions or a URI is used to identify the conditions, recommend using schema:CreativeWork to provide a label (name) and an identifier (URI or URL).

### schema:license

- **Cardinality:** Optional
- **Content:** array of one of: string, [object reference](#/$defs/ObjectReference), [object reference](#/$defs/Reference)
- **Description:** legal statement of conditions for use and access; recommend using schema:CreativeWork to provide a label (name) for the license, and an identifier. Sources of license identifiers: https://opensource.org/licenses/, https://creativecommons.org/about/cclicenses/, https://spdx.org/licenses/, http://cor.esipfed.org/ont/earthcube/swl. If only a string is provided, it should be an identifier for the license, ideally a resolvable URI

### schema:url

- **Cardinality:** Optional
- **Content:** string
- **Description:** Web Location of a page describing the dataset (landing page), typically providing links or instructions to get the actual resource content; analogous to dcat:accessURL. If a direct link is available to get the data, put in distribution/contentUrl

### schema:distribution

- **Cardinality:** Optional
- **Content:** array of one of: object, object
- **Description:** specifies how to download the data in a specific format or access via a web API. This property describes where to get the data and in what format by using the schema:DataDownload type. If user must access data through a landing page, provide link to landing page in the 'url' property for the dataset

### schema:relatedLink

- **Cardinality:** Optional
- **Content:** array of object
- **Description:** Links to related resources. schema:linkRelationship says how the target relates to this resource. Defined by schemaorgProperties/linkRole since 2026-09-23; it was inline here, which is why schemaorgProperties/instrument could not reuse it and defined the same property as a labeled link instead.

### schema:publishingPrinciples

- **Cardinality:** Optional
- **Content:** array of one of: string, [object reference](#/$defs/ObjectReference), [object reference](#/$defs/Reference)
- **Description:** FDOF digitalObjectMutability, RDA digitalObjectPolicy, FDOF PersistencyPolicy. Policies related to maintenance, update, expected time to live. If an online resource documents the policies or a URI is used to identify the conditions, recommend using schema:CreativeWork to provide a label (name) and an identifier (URI or URL).

### schema:keywords

- **Cardinality:** Optional
- **Content:** [object reference](#/$defs/termsOrText)
- **Description:** NIAID's annotations on keyword terms, such as the dataset's EDAM topic categories.

### schema:creator

- **Cardinality:** Optional
- **Content:** object
- **Description:** author or orginator of intellectual content of dataset. Uset the JSON-LD @list construct to preserve author order. Use contributor with the Role property to specify other roles related to creation or stewardship of the resource.

### schema:contributor

- **Cardinality:** Optional
- **Content:** array of one of: [object reference](#/$defs/ObjectReference), [object reference](#/$defs/Person), [object reference](#/$defs/Organization), object
- **Description:** other parties who played a role in production of dataset

### schema:publisher

- **Cardinality:** Optional
- **Content:** one of: [object reference](#/$defs/ObjectReference), [object reference](#/$defs/Person), [object reference](#/$defs/Organization)
- **Description:** Party who made the dataset publicly available

### schema:provider

- **Cardinality:** Optional
- **Content:** array of one of: [object reference](#/$defs/ObjectReference), [object reference](#/$defs/Person), [object reference](#/$defs/Organization)
- **Description:** Party who maintains the distribution options for the dataset. If there are multiple distributions from different providers, use the provider property on distribution/DataDownload

### schema:funding

- **Cardinality:** Optional
- **Content:** one of: one of: [object reference](#/$defs/ObjectReference), object, array of one of: [object reference](#/$defs/ObjectReference), object
- **Description:** NIAID's grant details on CDIF's funding.

### prov:wasGeneratedBy

- **Cardinality:** Optional
- **Content:** array of object
- **Description:** Brief information about instruments, software or experimental protocols used

### prov:wasDerivedFrom

- **Cardinality:** Optional
- **Content:** array of one of: string, [object reference](#/$defs/ObjectReference), [object reference](#/$defs/Reference)
- **Description:** Brief information about sources of data used in aggregate datasets

### schema:subjectOf

- **Cardinality:** Optional
- **Content:** object
- **Description:** see https://github.com/Cross-Domain-Interoperability-Framework/Discovery/issues/13 for discussion on how to make assertion about the sample registration and metadata distinct from statements about the physical object

### schema:includedInDataCatalog

- **Cardinality:** Optional
- **Content:** one of: one of: [object reference](#/$defs/ObjectReference), one of: —, —, array of one of: [object reference](#/$defs/ObjectReference), one of: —, —
- **Description:** The repositories holding the dataset, which the portal aggregates from.

### nde:date

- **Cardinality:** Optional
- **Content:** [object reference](#/$defs/date)
- **Description:** The portal's summary date for the record.

### nde:species

- **Cardinality:** Optional
- **Content:** [object reference](#/$defs/terms)
- **Description:** Species the dataset was collected from or is about.

### schema:infectiousAgent

- **Cardinality:** Optional
- **Content:** [object reference](#/$defs/terms)
- **Description:** Infectious agents the dataset is about.

### schema:healthCondition

- **Cardinality:** Optional
- **Content:** [object reference](#/$defs/terms)
- **Description:** Health conditions the dataset is about.

### schema:measurementTechnique

- **Cardinality:** Optional
- **Content:** [object reference](#/$defs/termsOrText)
- **Description:** NIAID's annotations on the measurement techniques CDIF discovery describes.

### schema:variableMeasured

- **Cardinality:** Optional
- **Content:** [object reference](#/$defs/termsOrText)
- **Description:** NIAID's annotations on the variables CDIF discovery describes.

### nde:nctid

- **Cardinality:** Optional
- **Content:** one of: string, array of string
- **Description:** ClinicalTrials.gov identifier of the study.

### nde:citedBy

- **Cardinality:** Optional
- **Content:** one of: [object reference](#/$defs/work), array of [object reference](#/$defs/work)
- **Description:** Works that cite the dataset.

### schema:citation

- **Cardinality:** Optional
- **Content:** one of: [object reference](#/$defs/work), array of [object reference](#/$defs/work)
- **Description:** NIAID's journal and PubMed details on CDIF's citations.

### nde:curatedBy

- **Cardinality:** Optional
- **Content:** object
- **Description:** Who curated the record, and from which version of their catalog.

### nde:isBasisFor

- **Cardinality:** Optional
- **Content:** one of: object, array of object
- **Description:** Resources based on this dataset.

### nde:sample

- **Cardinality:** Optional
- **Content:** one of: [object reference](#/$defs/sample), object, array of one of: [object reference](#/$defs/sample), object
- **Description:** The samples used to generate the dataset, or a collection of them.

### schema:spatialCoverage

- **Cardinality:** Optional
- **Content:** one of: one of: [object reference](#/$defs/ObjectReference), object, array of one of: [object reference](#/$defs/ObjectReference), object
- **Description:** NIAID's administrative type on CDIF's spatial coverage.

### schema:sourceOrganization

- **Cardinality:** Optional
- **Content:** one of: object, array of object
- **Description:** Projects and programs the dataset comes from.

### bios:alternateIdentifier

- **Cardinality:** Optional
- **Content:** [object reference](#/$defs/texts)
- **Description:** Identifiers beyond the one CDIF's schema:identifier holds.

### cdifniaid:assayformat

- **Cardinality:** Optional
- **Content:** [object reference](#/$defs/texts)
- **Description:** The assay format, as the portal gives it.

### cdifniaid:publication

- **Cardinality:** Optional
- **Content:** one of: string, array of string
- **Description:** PubMed identifiers of publications about the dataset.

# Class Definitions

## cdifConceptOrTermOrString {#sec-cdifconceptortermorstring}

Shared shape for a CDIF property that carries either a controlled-vocabulary value or a bare string label. Wraps cdifConceptOrTerm (SKOS-concept @id-ref, schema:DefinedTerm, or inline cdif:Concept) with a plain-string alternative used for legacy or single-word labels not yet bound to a vocabulary.

## ObjectReference {#sec-objectreference}

A reference to a node defined elsewhere, by its @id.

### @id

- **Cardinality:** Required
- **Content:** string
- **Description:** resolvable @id of the referenced node

## Identifier {#sec-identifier}

Properties for a schema.org identifier (schema:PropertyValue pattern). **Union-type policy:** In CDIF profile UML models an attribute typed as schema:Identifier / schema:PropertyValue is represented by a single attribute of that class type. The JSON Schema implementation permits the property value to be EITHER a plain string (interpreted as the bare identifier value) OR a full schema:PropertyValue object (with explicit @type, propertyID, value). Consumers should accept either form.

### @type

- **Cardinality:** Optional
- **Content:** array of string

### schema:propertyID

- **Cardinality:** Optional
- **Content:** one of: string, [object reference](#/$defs/ObjectReference)
- **Description:** In this context for the schema:PropertyValue, this field is an identifier for the identifier schema, e.g. DOI, ARK. Get values from https://registry.identifiers.org/registry/ for interoperability. URI-shape values MUST be serialized as JSON-LD IRI references ({"@id":"..."}) so they participate in RDF entailment; free-label strings remain valid as strings.

### schema:value

- **Cardinality:** Optional
- **Content:** string
- **Description:** the identifier string. E.g. 10.5066/F7VX0DMQ

### schema:url

- **Cardinality:** Optional
- **Content:** string
- **Description:** web-resolveable string for the identifier; host name part is location of a resolver that will return some representation for the given identifier value. E.g. https://doi.org/10.5066/F7VX0DMQ

## Reference {#sec-reference}

Schema for a labeled link, a profile of schema.org/CreativeWork: a resolvable URL with an optional name and description. Optionally carries the DCAT relation surface (dcat:hadRole, dcterms:relation) for a link that expresses a typed relationship rather than a plain reference. Those two properties were a separate block, cdifDataType/cdifReference, which was an allOf of this schema plus exactly those two optional properties and nothing else -- its dcat:Relationship co-type mandate had already been removed because it made every labeled link unsatisfiable and broke every schema:license example that followed schema.org's own advice. Since both are optional, folding them in here changes no document's validity while removing a block and five levels of $defs/Reference indirection. cdifReference was retired 2026-09-23.

### @type

- **Cardinality:** Required
- **Content:** one of: —, —
- **Description:** Either construct, or both. A labeled link is a schema:CreativeWork at a URL; a dcat:Relationship is DCAT's association class for a typed relation to another resource. A node may declare both -- CDIF's own relation examples do -- but NEITHER IS REQUIRED TO ACCOMPANY THE OTHER. That is the whole point of the anyOf. Until 2026-09-08 this block's Relation half required contains: dcat:Relationship while the labeled-link half required contains: schema:CreativeWork, and under allOf both applied to every instance, so an ordinary labeled link was unsatisfiable. Of profile-core's licenses the 29 plain strings and 1 @id-reference passed while the 10 that followed schema.org's own recommendation -- "use schema:CreativeWork to provide a label (name) for the license" -- failed. 412782113 fixed that by deleting the dcat:Relationship mandate outright, which left the JSON Schema with no notion of dcat:Relationship at all while rules.shacl went on targeting it as a class. A pure DCAT relation then met a SHACL requirement with no schema counterpart. This anyOf restores the type to the schema WITHOUT restoring the conjunction.

### schema:name

- **Cardinality:** Optional
- **Content:** string

### schema:description

- **Cardinality:** Optional
- **Content:** string

### schema:url

- **Cardinality:** Optional
- **Content:** string

### dcat:hadRole

- **Cardinality:** Optional
- **Content:** one of: object, [object reference](#/$defs/cdifConceptOrTermOrString)
- **Description:** Role of the related resource. Present only on a link that expresses a relationship; a plain labeled link such as a license omits it. DCAT's declared range is dcat:Role (dcat.ttl: rdfs:range dcat:Role, and dcat:Role rdfs:subClassOf skos:Concept), so the DCAT-native form is a node typed dcat:Role. That form was NOT accepted here before 2026-10-01: this property was cdifConceptOrTermOrString alone, which matches a bare string, a sealed @id reference, a schema:DefinedTerm or a skos:Concept -- none of which a dcat:Role-typed node satisfies, because JSON Schema does no subclass reasoning. dcat:Role is added as a branch rather than replacing the others, so the DCAT-native form becomes valid without invalidating anything already written. Note this leaves CDIF LOOSER than DCAT, deliberately: DCAT's range is dcat:Role alone, and CDIF also accepts a plain skos:Concept, a DefinedTerm, an @id reference and a string. That is the same both-forms stance taken on dcterms:relation, and it is a choice rather than an oversight -- do not read the extra branches as something not yet tightened.

### dcterms:relation

- **Cardinality:** Optional
- **Content:** one of: [object reference](#/$defs/ObjectReference), string
- **Description:** The related resource -- the DCAT canonical pointer to what is being related to, which is distinct from schema:url, the presentation URL of the link itself. An @id reference is the RECOMMENDED form and a string is permitted, which is DCMI's own position: "Recommended practice is to identify the related resource by means of a URI. If this is not possible or feasible, a string conforming to a formal identification system may be provided." DCMI declares no rdfs:range for this property, and of the 13 DCMI properties carrying an "intended to be used with non-literal values" restriction, this is deliberately not one. dcat.ttl does not re-declare or constrain it at all -- the only triple mentioning it in the whole DCAT vocabulary is `dcat:distribution rdfs:subPropertyOf dcterms:relation`. So objectReference-only would be stricter than both DCAT and DCMI and would reject a form the specification sanctions. The anyOf matches how schema:additionalType is handled here: both forms valid, the object form used in examples and required only where a `contains` pins a specific value. It was string-only until 2026-10-01, which rejected the @id form outright. Reported from outside by a PSDI validator taking a things-not-strings approach (profile-core#16): their DCAT catalogue mirrors the DCAT-3 spec examples and wrote {"@id": ...}, which failed both layers -- while CDIF's own documented URI serialization policy (agents.md) says URI values SHOULD be {"@id": ...}. The register required the one form its own policy argues against.

## Person {#sec-person}

schema for cdif profile of schema.org/Person

### @id

- **Cardinality:** Optional
- **Content:** string

### @type

- **Cardinality:** Optional
- **Content:** array of string

### schema:name

- **Cardinality:** Optional
- **Content:** string
- **Description:** string label for person that is meaningful for human users, should format consistently. Recommend 'Family Name, Given name' format.

### schema:description

- **Cardinality:** Optional
- **Content:** string
- **Description:** additional information about the agent or their relation to the described resource

### schema:identifier

- **Cardinality:** Optional
- **Content:** one of: [object reference](#/$defs/Identifier), string
- **Description:** identifier for person, recommend ORCID

### schema:alternateName

- **Cardinality:** Optional
- **Content:** one of: string, array of string
- **Description:** other labels by which the person might be known. A list when there are several; a single label may be a plain string, as JSON-LD framing writes a one-item list.

### schema:affiliation

- **Cardinality:** Optional
- **Content:** [object reference](#/$defs/Organization)
- **Description:** if affiliation is present, value must be a schema:Organization.

### schema:contactPoint

- **Cardinality:** Optional
- **Content:** one of: —, —
- **Description:** An email address or a contact web page (a form, an issue tracker), or both; at least one is required. Schema.org also allows telephone and postal contacts. A URL-only contact is ordinary in DCAT (a vcard:Kind with only vcard:hasURL), so requiring email made such records invalid.

### schema:sameAs

- **Cardinality:** Optional
- **Content:** array of one of: string, [object reference](#/$defs/ObjectReference)
- **Description:** other identifiers for the person

## Organization {#sec-organization}

### @id

- **Cardinality:** Optional
- **Content:** string

### @type

- **Cardinality:** Optional
- **Content:** array of one of: string (`"schema:Organization"` | `"schema:FundingAgency"` | `"schema:Consortium"` | `"schema:Corporation"` | `"schema:EducationalOrganization"` | `"schema:FundingScheme"` | `"schema:GovernmentOrganization"` | `"schema:NGO"` | `"schema:Project"` | `"schema:ResearchOrganization"`)

### schema:additionalType

- **Cardinality:** Optional
- **Content:** array of [object reference](#/$defs/cdifConceptOrTermOrString)

### schema:name

- **Cardinality:** Optional
- **Content:** string
- **Description:** string label for organization that is meaningful for human users

### schema:alternateName

- **Cardinality:** Optional
- **Content:** one of: string, array of string
- **Description:** other labels by which the organization might be known. A list when there are several; a single label may be a plain string, as JSON-LD framing writes a one-item list.

### schema:description

- **Cardinality:** Optional
- **Content:** string
- **Description:** additional information about the agent or their relation to the described resource

### schema:identifier

- **Cardinality:** Optional
- **Content:** one of: [object reference](#/$defs/Identifier), string
- **Description:** identifier for organization

### schema:sameAs

- **Cardinality:** Optional
- **Content:** array of one of: string, [object reference](#/$defs/ObjectReference)
- **Description:** other identifiers for the organization

## NiaidDefinedTerm {#sec-niaiddefinedterm}

A schema:DefinedTerm with NIAID's annotations. The NIAID Data Discovery Portal annotates every term it attaches to a dataset (species, infectious agents, health conditions, measurement techniques, variables): whether a curator checked it, the text it was matched from, who or what curated it, and for a taxon its common name. Across the portal's records these properties appear on DefinedTerms and nowhere else, so this block is an extension of that type and requires it.

### @type

- **Cardinality:** Required
- **Content:** array of string

### nde:isCurated

- **Cardinality:** Optional
- **Content:** boolean
- **Description:** Whether a curator checked the term against its source text.

### nde:originalName

- **Cardinality:** Optional
- **Content:** string
- **Description:** The text in the source record the term was matched from.

### nde:curatedBy

- **Cardinality:** Optional
- **Content:** object
- **Description:** Who or what produced or checked the annotation, often software (PubTator, GPT-4o-mini, the Biothings API).

### cdifniaid:commonName

- **Cardinality:** Optional
- **Content:** string
- **Description:** The common name of a taxon, e.g. Human for Homo sapiens.

## date {#sec-date}

## terms {#sec-terms}

NIAID's annotated terms; each must be a schema:DefinedTerm.

## termsOrText {#sec-termsortext}

## sample {#sec-sample}

A sample; nde:Sample is NIAID's subclass of the Bioschemas sample.

## texts {#sec-texts}

## Concept {#sec-concept}

### @context

- **Cardinality:** Optional
- **Content:** one of: object, array of one of: string, object
- **Description:** JSON-LD context declaring the skos namespace prefix. May be a single object or an array of strings and objects.

### @id

- **Cardinality:** Optional
- **Content:** string
- **Description:** URI identifier for this concept.

### @type

- **Cardinality:** Required
- **Content:** array of string

### skos:prefLabel

- **Cardinality:** Required
- **Content:** one of: string, [object reference](#/$defs/LanguageTaggedValue), array of [object reference](#/$defs/LanguageTaggedValue)
- **Description:** Preferred lexical label for this concept. A single string, a single language-tagged value, or an array of language-tagged values. Each language should appear at most once.

### skos:notation

- **Cardinality:** Optional
- **Content:** string
- **Description:** Classification code for this concept within a scheme (a single notation string, consistent with CdifCodelistConcept).

### skos:definition

- **Cardinality:** Required
- **Content:** one of: string, [object reference](#/$defs/LanguageTaggedValue), array of one of: string, [object reference](#/$defs/LanguageTaggedValue)
- **Description:** Formal explanation of the meaning of this concept.

### skos:scopeNote

- **Cardinality:** Optional
- **Content:** one of: string, [object reference](#/$defs/LanguageTaggedValue), array of one of: string, [object reference](#/$defs/LanguageTaggedValue)
- **Description:** Note clarifying meaning and/or intended use.

### skos:note

- **Cardinality:** Optional
- **Content:** one of: string, [object reference](#/$defs/LanguageTaggedValue), array of one of: string, [object reference](#/$defs/LanguageTaggedValue)
- **Description:** General note about this concept.

### skos:historyNote

- **Cardinality:** Optional
- **Content:** one of: string, [object reference](#/$defs/LanguageTaggedValue), array of one of: string, [object reference](#/$defs/LanguageTaggedValue)
- **Description:** Note about past state or use.

### skos:changeNote

- **Cardinality:** Optional
- **Content:** one of: string, [object reference](#/$defs/LanguageTaggedValue), array of one of: string, [object reference](#/$defs/LanguageTaggedValue)
- **Description:** Note documenting a change.

### skos:editorialNote

- **Cardinality:** Optional
- **Content:** one of: string, [object reference](#/$defs/LanguageTaggedValue), array of one of: string, [object reference](#/$defs/LanguageTaggedValue)
- **Description:** Note for editors and maintainers.

### skos:inScheme

- **Cardinality:** Required
- **Content:** one of: [object reference](#/$defs/ObjectReference), array of [object reference](#/$defs/ObjectReference)
- **Description:** Concept scheme(s) this concept belongs to.

### skos:topConceptOf

- **Cardinality:** Optional
- **Content:** one of: [object reference](#/$defs/ObjectReference), array of [object reference](#/$defs/ObjectReference)
- **Description:** Concept scheme(s) for which this is a top concept.

### skos:broader

- **Cardinality:** Optional
- **Content:** array of one of: [object reference](#/$defs/ObjectReference), [object reference](#/$defs/Concept)
- **Description:** Broader (parent) concepts in the hierarchy. Items are inline concept objects or @id references.

### skos:narrower

- **Cardinality:** Optional
- **Content:** array of one of: [object reference](#/$defs/ObjectReference), [object reference](#/$defs/Concept)
- **Description:** Narrower (child) concepts in the hierarchy. Items are inline concept objects or @id references.

## BioschemasSample_termsOrText {#sec-bioschemassample-termsortext}

## work {#sec-work}

A cited or citing work. One carrying NIAID's PubMed id, DOI or journal names must be a NIAID creative work; a string or any other object is left to CDIF's own rules.

## quantity {#sec-quantity}

A schema:QuantitativeValue; a range uses minValue and maxValue.

### @type

- **Cardinality:** Optional
- **Content:** one of: string, array of string

### schema:value

- **Cardinality:** Optional
- **Content:** number or string

### schema:minValue

- **Cardinality:** Optional
- **Content:** number

### schema:maxValue

- **Cardinality:** Optional
- **Content:** number

### schema:unitText

- **Cardinality:** Optional
- **Content:** string

### schema:unitCode

- **Cardinality:** Optional
- **Content:** string

### schema:name

- **Cardinality:** Optional
- **Content:** string

## LanguageTaggedValue {#sec-languagetaggedvalue}

An RDF literal value with a language tag, serialized as a JSON-LD value object.

### @value

- **Cardinality:** Required
- **Content:** string
- **Description:** The text content.

### @language

- **Cardinality:** Required
- **Content:** string
- **Description:** BCP 47 language tag (e.g. en, fr, de).

## termOrText {#sec-termortext}
