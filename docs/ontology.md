# RDF-STaX ontology documentation

--8<-- "docs/includes/links.md"

!!! info

    You can also download other versions of the ontology or an OWL 2 DL version. See the [versioning and releases](#versioning-and-releases) section below for more information.

!!! note

    The documentation and the download links here are for the release version of the ontology. The ontology sources are [available on GitHub](https://github.com/RDF-STaX/rdf-stax.github.io) – see also [Contributing](contributing.md).

--8<-- "docs/includes/docs.html"

## OWL 2 Profiles

The ontology is written in OWL 2 DL. It is checked for compliance with the profile in the CI pipeline.

RDF-STaX imports [SKOS](https://www.w3.org/TR/skos-reference/), which is OWL 2 Full by default. There is however [a subset of SKOS that is OWL 2 DL](https://www.w3.org/TR/skos-reference/#rdf-schema-owl-dl), and this is the version of SKOS that is used in RDF-STaX.

The released version of the ontology includes additional assertions (inferred, authorship, alignments) that are not part of the ontology itself. These assertions may be in OWL 2 Full. To get the OWL 2 DL version of the ontology, see the notes on [versioning and releases](#versioning-and-releases) below.

## Versioning and releases

RDF-STaX follows the [Semantic Versioning 2](https://semver.org/) scheme. The version number is stored in the `owl:versionInfo` annotation property of the ontology and is a part of the version IRI. The `dev` version corresponds to the `main` branch of the repository. When you don't specify a version, the `dev` version is used.

The dropdown at the top of the page allows you to switch between different versions of the documentation. Previous releases can also be found on [GitHub](https://github.com/RDF-STaX/rdf-stax.github.io/releases).

The released versions of the ontology include also the inferred statements, authorship information, and alignments to other ontologies. If you would like to get the raw ontology without these additions (OWL 2 DL), append `/dl` to the URL, e.g., `https://w3id.org/stax/ontology/dl`.

Released versions of the ontology are available in the JSON-LD, N-Triples, RDF/XML, and Turtle formats, by appending their respective extension at the end of the ontology's URL, or with the [content negotiation mechanism](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation). Some examples of links that would work:

- `https://w3id.org/stax/ontology` (content negotiation)
- `https://w3id.org/stax/ontology.rdf` (explicitly ask for RDF/XML)
- `https://w3id.org/stax/ontology/dl.rdf` (OWL 2 DL version, explicitly ask for RDF/XML)
- `https://w3id.org/stax/dev/ontology` (content negotiation)
- `https://w3id.org/stax/dev/ontology/dl` (OWL 2 DL version, content negotiation)
- `https://w3id.org/stax/dev/ontology.ttl` (explicitly ask for Turtle)
- `https://w3id.org/stax/1.0.0/ontology` (content negotiation)
- `https://w3id.org/stax/1.0.0/ontology.jsonld` (explicitly ask for JSON-LD)

!!! warning "Important"

    The RDF of the ontology can only be accessed via the ontology's PURL (`https://w3id.org/stax/...`), not via the URL you currently see in your browser.

!!! note
    
    The process for making releases is described on the [Contributing](contributing.md#releases) page.

### Archival in Zenodo

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10072907.svg)](https://zenodo.org/doi/10.5281/zenodo.10072907)

Each RDF-STaX release is archived in Zenodo under this DOI: [10.5281/zenodo.10072907](https://zenodo.org/doi/10.5281/zenodo.10072907).

## See also

- **[How to use it?](use-it.md)**
- [Taxonomy overview](taxonomy.md)
- [Contributing](contributing.md)
