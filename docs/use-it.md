# How to use RDF-STaX?

RDF stream type usage is often a subjective matter, so RDF-STaX provides [facilities](ontology.md) for making *subjective* assertions about RDF stream types. For example: *I see this resource as an RDF graph stream, because (...)*, as opposed to strict, universal classification. The types in RDF-STaX are semantically related, [allowing you to reason about them](#using-semantic-relations-from-the-ontology).

**The assertions can be made by anyone, anywhere. You can use RDF-STaX to annotate published streams, datasets, research papers, software, and more.**

## Annotating RDF stream types

Making a statement about something's RDF stream type is very straightforward. For example, to say that `#!turtle <https://example.org/some-resource>` is an RDF graph stream, you would use the `#!turtle stax:RdfStreamTypeUsage` class:

```turtle
@prefix stax: <https://w3id.org/stax/ontology#> .

_:usage a stax:RdfStreamTypeUsage ;
    stax:hasStreamType stax:graphStream ;
    stax:isUsageOf <https://example.org/some-resource> .
```

It is recommended (but not required) to have one `#!turtle stax:RdfStreamTypeUsage` instance per annotated resource and per RDF stream type. This makes it easier to find all the annotations for a given resource or stream type.

You can also make the statement in reverse, by annotating the resource itself. This can be especially useful when annotating RDF streams on the Web or in a dataset. The following three examples illustrate combining RDF-STaX with other vocabularies for describing datasets and streams ([VoCaLS](http://w3id.org/rsp/vocals), [VoID](https://www.w3.org/TR/void/), [DCAT](https://www.w3.org/TR/vocab-dcat-3/), [LDES](https://w3id.org/ldes/specification)). RDF-STaX here plays the role of a **bridge between the different ontologies**, providing a way to describe stream types in a universal manner.

??? example "Example: VoCaLS `RDFStream` (click to expand)"

    To annotate a `#!turtle vocals:RDFStream` from the [VoCaLS Vocabulary](http://w3id.org/rsp/vocals):

    ```turtle
    @prefix stax: <https://w3id.org/stax/ontology#> .
    @prefix vocals: <http://w3id.org/rsp/vocals#> .

    _:stream a vocals:RDFStream ;
        # ... other properties of the stream ...
        stax:hasStreamTypeUsage [
            a stax:RdfStreamTypeUsage ;
            stax:hasStreamType stax:graphStream
        ] .
    ```

    VoCaLS defines `#!turtle vocals:RDFStream` as "a stream composed of RDF data elements, i.e. RDF graphs and/or triples". Instances of this class can be thus annotated as [RDF graph stream](taxonomy.md#rdf-graph-stream) or [flat RDF triple streams](taxonomy.md#flat-rdf-triple-stream).


??? example "Example: VoID `Dataset` (click to expand)"

    To annotate a `#!turtle void:Dataset` from the [VoID Vocabulary](https://www.w3.org/TR/void/):

    ```turtle
    @prefix stax: <https://w3id.org/stax/ontology#> .
    @prefix void: <http://rdfs.org/ns/void#> .

    _:dataset a void:Dataset ;
        # ... other properties of the dataset ...
        stax:hasStreamTypeUsage [
            a stax:RdfStreamTypeUsage ;
            stax:hasStreamType stax:flatTripleStream
        ] .
    ```

    In VoID, `#!turtle void:Dataset` refers to a set of triples, which can be viewed as a [flat RDF triple stream](taxonomy.md#flat-rdf-triple-stream).


??? example "Example: DCAT `Distribution` (click to expand)"

    In [DCAT](https://www.w3.org/TR/vocab-dcat-3/), a dataset may have multiple representations (`#!turtle dcat:Distribution`). Thus, tou may want to annotate the distribution, not the dataset itself:

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
                stax:hasStreamType stax:datasetStream
            ]
        ] .
    ```

    Of course, annotating the dataset itself also makes sense, if you want to make a statement about the dataset as a whole.

    In DCAT, all RDF stream types from RDF-STaX are applicable, depending on the content of the dataset.


??? example "Example: LDES `EventStream` (click to expand)"

    In [Linked Data Event Streams](https://w3id.org/ldes/specification) (LDES) the `#!turtle ldes:EventStream` is a collection of stream elements – sets of RDF triples. Each element is identified with its subject node. Therefore, instances of this class can be annotated in RDF-STaX as [RDF subject graph streams](taxonomy.md#rdf-subject-graph-stream).

    ```turtle
    @prefix ldes: <https://w3id.org/ldes/specification#> .
    @prefix stax: <https://w3id.org/stax/ontology#> .

    _:stream a ldes:EventStream ;
        # ... other properties of the stream ...
        stax:hasStreamTypeUsage [
            a stax:RdfStreamTypeUsage ;
            stax:hasStreamType stax:subjectGraphStream
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
    rdfs:comment "The authors state that for their proposed system, 'the streaming element (i.e. a single message) (...) is a set of triples'. Therefore, internally it uses an RDF graph stream."@en ;
    stax:hasStreamType stax:graphStream ;
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

These rich annotations are used in [RDF-STaX nanopublications](nanopubs.md).

## Making RDF stream type usage nanopublications

This *subjective* style of RDF-STaX meshes very well with the idea of [nanopublications](https://nanopub.net/), small snippets of scientific knowledge. **See the [documentation page on nanopublications](nanopubs.md)** for more information on how to find, use, and create them.

## Using semantic relations from the ontology

The ontology includes several semantic relations between the RDF stream types. You can use them to reason about the types – for example can stream of type X be flattened into type Y?

- `#!turtle skos:broader` and `#!turtle skos:narrower` – properties indicating sub- and super-types of streams.
- `#!turtle stax:canBeFlattenedInto` – property indicating that a stream of type X can be flattened into a stream of type Y. For example, a `#!turtle stax:graphStream` can be flattened into a `#!turtle stax:flatTripleStream`.
- `#!turtle stax:canBeGroupedInto` – property indicating that a stream of type X can be grouped into a stream of type Y. For example, a `#!turtle stax:flatQuadStream` can be grouped into a `#!turtle stax:datasetStream`.
- `#!turtle stax:canBeTriviallyExtendedInto` – property indicating that a stream of type X can be trivially turned into a stream of type Y, by explicitly adding the graph component (default graph). For example, a `#!turtle stax:flatTripleStream` can be trivially extended into a `#!turtle stax:flatQuadStream`.

These semantic relations are used in [RiverBench](uses/index.md#riverbench) to validate the stream type annotations.

## Example SPARQL queries

The **[competency question tests](uses/cq.md)** provide examples of SPARQL queries that can be used with the RDF-STaX ontology.

## See also

- [Licensing and citation](licensing.md)
- [Taxonomy overview](taxonomy.md)
- [Ontology documentation](ontology.md)
- [Nanopublications](nanopubs.md)
- [Existing use cases](uses/index.md)
