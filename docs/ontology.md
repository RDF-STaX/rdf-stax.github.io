--8<-- "docs/includes/links.md"

!!! note

    The documentation and the download links here are for the release version of the ontology. The ontology sources are [available on GitHub](https://github.com/RDF-STaX/rdf-stax.github.io) – see also [Contributing](contributing.md).

--8<-- "docs/includes/docs.html"

## Versioning and releases

RDF-STaX follows the [Semantic Versioning 2](https://semver.org/) scheme. The version number is stored in the `owl:versionInfo` annotation property of the ontology and is a part of the version IRI. The `dev` version corresponds to the `main` branch of the repository. The `stable` version is an alias for the latest tagged release. When you don't specify a version, the `stable` version is used.

The dropdown at the top of the page allows you to switch between different versions of the documentation. Previous releases can also be found on [GitHub](https://github.com/RDF-STaX/rdf-stax.github.io/releases).

Released versions of the ontology are available in the JSON-LD, N-Triples, RDF/XML, and Turtle formats, by appending their respective extension at the end of the ontology's URL, or with the [content negotiation mechanism](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation). Some examples of links that would work:

- `https://w3id.org/stax/ontology` (content negotiation)
- `https://w3id.org/stax/ontology.rdf` (explicitly ask for RDF/XML)
- `https://w3id.org/stax/dev/ontology` (content negotiation)
- `https://w3id.org/stax/dev/ontology.ttl` (explicitly ask for Turtle)
- `https://w3id.org/stax/1.0.0/ontology.jsonld` (explicitly ask for JSON-LD)

The released versions of the ontology include also the inferred statements, authorship information, and alignments to other ontologies. If you would like to get the raw ontology without these additions, you can find it in the [`src` directory of the main repository](https://github.com/RDF-STaX/rdf-stax.github.io/tree/main/src/stax.ttl)

!!! warning "Important"

    The RDF of the ontology can only be accessed via the ontology's PURL (`https://w3id.org/stax/...`), not via the URL you currently see in your browser.

!!! note
    
    The process for making releases is described on the [Contributing](contributing.md#releases) page.

## See also

- **[How to use it?](use-it.md)**
- [Taxonomy overview](taxonomy.md)
- [Contributing](contributing.md)
