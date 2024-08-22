# RDF-STaX uses and publications

**Are you using RDF-STaX in your project or paper?** We would be glad to list it here! **Please [open an issue](https://github.com/RDF-STaX/rdf-stax.github.io/issues/new)** with a link or a brief explanation of how you use RDF-STaX.

## Papers using RDF-STaX

- Sowiński, P.; Szmeja, P.; Ganzha, M.; Paprzycki, M. (2024). RDF Stream Taxonomy: Systematizing RDF Stream Types in Research and Practice. _Electronics_, _13_(13), 2558. [https://doi.org/10.3390/electronics13132558](https://doi.org/10.3390/electronics13132558)
- Sowiński, P., Ganzha, M., & Paprzycki, M. (2023). RiverBench: an Open RDF Streaming Benchmark Suite. _[arXiv preprint arXiv:2305.06226](https://arxiv.org/abs/2305.06226)_.

## Projects using RDF-STaX

### RiverBench

[RiverBench](https://w3id.org/riverbench/) is an open, community-driven RDF streaming benchmark suite. It uses RDF-STaX for annotating the stream types of the benchmark datasets. The [RDF-STaX annotation system](../use-it.md) is integrated into the [RiverBench metadata ontology](https://w3id.org/riverbench/schema/metadata).

Each dataset is assigned two stream type usages – one grouped RDF stream type and one flat RDF stream type. This is because in RiverBench each dataset can be viewed as either *streaming* or *flat*. Each dataset also has multiple distributions (flat or streaming) which are annotated with the corresponding stream type usage. The annotations are validated using SHACL, to make sure that the annotation is not contradictory ([see the rules](https://github.com/RiverBench/schema/blob/3d03cb01764d3c36cefb6f982e5e8bad55aa41d7/src/shacl/dataset.ttl#L175)). For this, the `#!turtle stax:canBeFlattenedInto` and `#!turtle stax:canBeGroupedInto` properties are used, along with the taxonomical structure from SKOS.

??? example "Example usage (click to expand)"

    From dataset [digital-agenda-indicators](https://w3id.org/riverbench/datasets/digital-agenda-indicators/dev/) ([source](https://github.com/RiverBench/dataset-digital-agenda-indicators/blob/01c1beb18fd38011373d6e4faf422de8f1c325cc/metadata.ttl)):

    ```turtle
    :dataset stax:hasStreamTypeUsage [
        a stax:RdfStreamTypeUsage ;
        rdfs:comment "The dataset can be viewed as a stream of graphs corresponding to statistical observations. Each graph is uniquely identified by its subject IRI."@en ;
        stax:hasStreamType stax:subjectGraphStream
    ] , [
        a stax:RdfStreamTypeUsage ;
        rdfs:comment "The dataset can be viewed as a flattened stream of triples."@en ;
        stax:hasStreamType stax:flatTripleStream
    ] .
    ```

    The distribution annotations are generated automatically by the CI. You can find the complete generated metadata [here](https://w3id.org/riverbench/datasets/digital-agenda-indicators/dev.ttl).

**Links:**

- Benchmark profiles group datasets by stream type and other technical characteristics:
    - [Profiles in the `stream` benchmark category](https://w3id.org/riverbench/v/dev/categories/stream#benchmark-profiles)
    - [SHACL fragment used to filter datasets by stream type](https://github.com/RiverBench/schema/blob/3d03cb01764d3c36cefb6f982e5e8bad55aa41d7/src/lib/profiles/propGraphStream.ttl) (in this example, only RDF graph streams or subtypes are allowed)
- Datasets ([example](https://w3id.org/riverbench/datasets/assist-iot-weather-graphs/dev/#technical-metadata)) include `stax:hasStreamTypeUsage` annotations. This can be seen in:
    - [Dataset documentation pages](https://w3id.org/riverbench/datasets/)
    - Dataset [RDF metadata](https://w3id.org/riverbench/datasets/assist-iot-weather-graphs/dev.ttl)
- [Complete metadata dump](https://w3id.org/riverbench/dumps/dev.ttl.gz)


### Jelly

[Jelly](https://w3id.org/jelly) is a high-performance binary RDF serialization format and streaming protocol. It [uses RDF-STaX stream types](https://w3id.org/jelly/dev/user-guide/#stream-types) in its stream metadata to specify how the RDF stream should be interpreted at the receiving end.
For performance reasons, Jelly's stream metadata specifies the stream type not in RDF (like RiverBench, for example), but as an [integer identifier](https://w3id.org/jelly/dev/specification/reference/#logicalstreamtype).

Jelly is implemented in [Jelly-JVM](https://w3id.org/jelly/jelly-jvm/dev/), which works with Apache Jena and RDF4J. This implementation uses RDF-STaX in the parser/consumer to check if the consumed stream is of the expected type or its subtype. It also checks if the consumed stream's physical (binary) layout is compatible with the expected stream type and can be interpreted as such.

??? example "Jelly-JVM consumer example (click to expand)"

    Example of using Jelly-JVM in Scala to decode a flat RDF quad stream either as such, or as an RDF dataset stream.
    Adapted from [Jelly-JVM usage examples](https://github.com/Jelly-RDF/jelly-jvm/blob/485b01e0c994db5aaad80c53547ff6a5dd7f1caa/examples/src/main/scala/eu/ostrzyciel/jelly/examples/PekkoStreamsDecoderFlow.scala).

    ```scala
    val decodedQuads: Future[Seq[Quad]] = Source(bytes)
      .via(JellyIo.fromBytes)
      // We use "decodeQuads" because the physical stream type is QUADS.
      // And then we want to treat it as a flat RDF quad stream, so we call "asFlatQuadStreamStrict".
      // We use the "Strict" method to tell the decoder to check if the incoming logical stream type
      // is the same as we are expecting: flat RDF quad stream.
      .via(DecoderFlow.decodeQuads.asFlatQuadStreamStrict)
      .runWith(Sink.seq)

    // We can also treat each stream frame as a separate dataset. This way we would get an
    // RDF dataset stream.
    val decodedDatasets: Future[Seq[DatasetGraph]] = Source(bytes)
      .via(JellyIo.fromBytes)
      // Note that we cannot use the strict variant (asDatasetStreamOfQuadsStrict) here,
      // because the stream says its logical type is flat RDF quad stream.
      .via(DecoderFlow.decodeQuads.asDatasetStreamOfQuads)
      .runWith(Sink.seq)
    ```

Similarly, the producer in Jelly-JVM has an API based on RDF-STaX types to specify the RDF-STaX type of the produced stream. These streams are type-safe, so their compatibility with a given RDF-STaX type is checked at compile time.

??? example "Jelly-JVM producer example (click to expand)"

    Example of using Jelly-JVM in Scala to encode a sequence of RDF graphs either as an RDF graph stream or as a flat RDF triple stream. Adapted from [Jelly-JVM usage examples](https://github.com/Jelly-RDF/jelly-jvm/blob/485b01e0c994db5aaad80c53547ff6a5dd7f1caa/examples/src/main/scala/eu/ostrzyciel/jelly/examples/PekkoStreamsEncoderFlow.scala).

    ```scala
    // A sequence of RDF graphs -- we skip the initialization for brevity.
    val graphs: Seq[Set[Triple]]
    val graphStream = Source(graphs)
      // Make an RDF graph stream out of the sequence of RDF graphs.
      .via(EncoderFlow.graphStream(
        // Do not use a size limiter here – we want exactly one graph in each frame
        None,
        JellyOptions.smallStrict,
      ))

    // We can also treat this as a flat RDF triple stream, with each Seq[Triple]
    // being simply treated as a batch of triples (Jelly jargon: a "frame").
    val flatTripleStream = Source(graphs)
      .via(EncoderFlow.flatTripleStreamGrouped(None, JellyOptions.smallStrict))
    ```

**Links:**

- [Jelly documentation](https://w3id.org/jelly/dev/)
    - [Stream type handling – user guide](https://w3id.org/jelly/dev/user-guide/#stream-types)
    - [Definition of binary stream type encoding](https://w3id.org/jelly/dev/specification/reference/#logicalstreamtype)
    - [Specification defining how Jelly implementations should handle RDF-STaX types](https://w3id.org/jelly/dev/specification/serialization/#logical-stream-types)
- [Jelly-JVM documentation](https://w3id.org/jelly/jelly-jvm/dev/)

### Nanopublications

RDF-STaX is used in [nanopublications](../nanopubs.md) to annotate stream types in research works or software. You can find more information on the [dedicated page about nanopublications](../nanopubs.md).

## Use case-based competency question tests

Based on the above use cases, a number of competency question tests were created. The tests are implemented as SPARQL queries and are used in Continuous Integration (CI) to test the RDF-STaX ontology. You can find a list of all the tests on **[this subpage](cq.md)**. The documentation for creating new tests is available [here](../contributing.md#competency-question-tests).

## See also

- [Competency question tests](cq.md)
- [Contributing](../contributing.md)
- [Licensing and citation](../licensing.md)
