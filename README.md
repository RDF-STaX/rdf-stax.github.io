# RDF Stream Taxonomy (RDF-STaX)

This is the main repository of the RDF Stream Taxonomy. Here you will find the ontology itself (`src`) and the documentation sources (`docs`).

**Read more about RDF-STaX on the [official website](https://w3id.org/stax/).**

Please file any feature requests, bugs, or other issues on **[issue tracker](https://github.com/RDF-STaX/rdf-stax.github.io/issues)**.

## Editing the ontology

- The main ontology file is `src/stax.ttl`. It should be edited with Protégé.
    - Do not add information about the authors/contributors there. This is done in the `src/authors.ttl` file (see below).
    - Do not set the ontology's version IRI or version – this is done automatically in CI during release.
- The `src/authors.ttl` file contains information about the authors/contributors of the ontology. It should be edited manually with a text editor.

## Editing documentation

Documentation is stored in the [`docs` directory](https://github.com/RDF-STaX/rdf-stax.github.io/tree/main/docs). You can open a pull request for any of the files there, except the ones in the `includes` subdirectory. These files are generated automatically in the CI pipeline.

## License

The RDF-STaX ontology and its documentation is licensed under the [Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/) license.
