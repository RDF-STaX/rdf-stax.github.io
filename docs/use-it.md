# How to use RDF-STaX?

RDF stream type usage is often a subjective matter, so RDF-STaX provides [facilities](ontology.md) for making *subjective* assertions about RDF stream types. For example: *I see this resource as an RDF graph stream, because (...)*, as opposed to strict, universal classification.

The assertions can be made by anyone, anywhere – be it in the metadata of your resource, when discussing research works and software, or elsewhere.

## Annotating RDF stream types

Making a statement about something's RDF stream type is very straightforward. For example, to say that `#!turtle <https://example.org/some-resource>` is an RDF graph stream, you would use the following RDF:

```turtle
@prefix stax: <https://w3id.org/stax/ontology#> .

_:usage a stax:RdfStreamTypeUsage ;
    stax:hasStreamType stax:rdfGraphStream ;
    stax:isUsageOf <https://example.org/some-resource> .
```

It is recommended (but not required) to have one `#!turtle stax:RdfStreamTypeUsage` instance per annotated resource and per RDF stream type. This makes it easier to find all the annotations for a given resource or stream type.

You can also make the statement in reverse, by annotating the resource itself. This can be especially useful when annotating RDF streams on the Web or in a dataset. The following three examples illustrate combining RDF-STaX with other vocabularies for describing datasets and streams ([VoCaLS](http://w3id.org/rsp/vocals), [VoID](https://www.w3.org/TR/void/), [DCAT](https://www.w3.org/TR/vocab-dcat-3/)).

??? example "Example: VoCaLS `RDFStream` (click to expand)"

    To annotate a `#!turtle vocals:RDFStream` from the [VoCaLS Vocabulary](http://w3id.org/rsp/vocals):

    ```turtle
    @prefix stax: <https://w3id.org/stax/ontology#> .
    @prefix vocals: <http://w3id.org/rsp/vocals#> .

    _:stream a vocals:RDFStream ;
        # ... other properties of the stream ...
        stax:hasStreamTypeUsage [
            a stax:RdfStreamTypeUsage ;
            stax:hasStreamType stax:rdfGraphStream
        ] .
    ```


??? example "Example: VoID `Dataset` (click to expand)"

    To annotate a `#!turtle void:Dataset` from the [VoID Vocabulary](https://www.w3.org/TR/void/):

    ```turtle
    @prefix stax: <https://w3id.org/stax/ontology#> .
    @prefix void: <http://rdfs.org/ns/void#> .

    _:dataset a void:Dataset ;
        # ... other properties of the dataset ...
        stax:hasStreamTypeUsage [
            a stax:RdfStreamTypeUsage ;
            stax:hasStreamType stax:flatRdfTripleStream
        ] .
    ```

    In VoID, `#!turtle void:Dataset` refers to a set of triples, which can be viewed as a flat RDF triple stream.


??? example "Example: DCAT `Distribution` (click to expand)"

    In [DCAT](https://www.w3.org/TR/vocab-dcat-3/), a dataset may have multiple representations (`#!turtle dcat:Distribution`). Thus, here we will want to annotate the distribution, not the dataset itself:

    ```turtle
    @prefix dcat: <http://www.w3.org/ns/dcat#> .
    @prefix stax: <https://w3id.org/stax/ontology#> .

    _:dataset a dcat:Dataset ;
        # ... other properties of the dataset ...
        dcat:distribution [
            a dcat:Distribution ;
            # ... other properties of the distribution ...
            stax:hasStreamTypeUsage [
                a stax:RdfStreamTypeUsage ;
                stax:hasStreamType stax:rdfDatasetStream
            ]
        ] .
    ```


### Adding more information

The `#!turtle stax:RdfStreamTypeUsage` instance is a good place to put additional information about the usage, such as a textual explanation, the source of the information, or the author of the statement. For example:

```turtle
@prefix cito: <http://purl.org/spar/cito/> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix stax: <https://w3id.org/stax/ontology#> .

_:usage a stax:RdfStreamTypeUsage ;
    rdfs:comment "The authors state that for their proposed system, 'the streaming element (i.e. a single message) (...) is a set of triples'. Therefore, it uses an RDF graph stream."@en ;
    stax:hasStreamType stax:rdfGraphStream ;
    stax:isUsageOf <https://doi.org/10.1109/ICSTCC.2017.8107003> ;
    cito:citesAsEvidence <https://doi.org/10.1109/ICSTCC.2017.8107003> ;
    dcterms:creator <https://orcid.org/0000-0002-2543-9461> .
```

You can use whatever properties you like, however, the following are recommended:

- [CiTO ontology](http://purl.org/spar/cito) for typing the citations.
- [DCMI Metadata Terms](http://purl.org/dc/terms/) for the statement author information.
- `#!turtle rdfs:comment` for the textual explanation.
- For statement creators, we recommend using [ORCID](https://orcid.org/).
- For research works, we recommend using [DOI](https://www.doi.org/).

## Making RDF stream type usage nanopublications

This *subjective* style of RDF-STaX meshes very well with the idea of [nanopublications](https://nanopub.net/), small snippets of scientific knowledge. See the [documentation page on nanopublications](nanopubs.md) for more information on how to find, use, and create them.

## See also

- [Licensing and citation](licensing.md)
- [Taxonomy overview](taxonomy.md)
- [Ontology documentation](ontology.md)
- [Nanopublications](nanopubs.md)
