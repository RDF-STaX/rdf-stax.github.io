# RDF-STaX uses and publications

Are you using RDF-STaX in your project or paper? We would be glad to list it here! **Please [open an issue](https://github.com/RDF-STaX/rdf-stax.github.io/issues/new)** with a link or a brief explanation of how you use RDF-STaX.

## Papers using RDF-STaX

- Sowinski, P., Szmeja, P. Ganzha, M., & Paprzycki, M. (2023). RDF Stream Taxonomy: Systematizing RDF Stream Types in Research and Practice. _[arXiv preprint arXiv:2311.14540](https://arxiv.org/abs/2311.14540)_.
- Sowinski, P., Ganzha, M., & Paprzycki, M. (2023). RiverBench: an Open RDF Streaming Benchmark Suite. _[arXiv preprint arXiv:2305.06226](https://arxiv.org/abs/2305.06226)_.

## Projects using RDF-STaX

### RiverBench

[RiverBench](https://w3id.org/riverbench/) is an open, community-driven RDF streaming benchmark suite. It uses RDF-STaX for annotating the stream types of the benchmark datasets. The [RDF-STaX annotation system](use-it.md) is integrated into the [RiverBench metadata ontology](https://w3id.org/riverbench/schema/metadata).

Each dataset is assigned two stream type usages – one grouped RDF stream type and one flat RDF stream type. This is because in RiverBench each dataset can be viewed as either *streaming* or *flat*. Each dataset also has multiple distributions (flat or streaming) which are annotated with the corresponding stream type usage. The annotations are validated using SHACL, to make sure that the annotation is not contradictory ([see the rules](https://github.com/RiverBench/schema/blob/c38e2a8fb1d8d9e0dd019ff2d0515651c3b6b7da/src/dataset-shacl.ttl)). For this, the `#!turtle stax:canBeFlattenedInto` and `#!turtle stax:canBeGroupedInto` properties are used, along with the taxonomical structure from SKOS.

??? example "Example usage (click to expand)"

    From dataset [digital-agenda-indicators](https://w3id.org/riverbench/datasets/digital-agenda-indicators/dev/) ([source](https://github.com/RiverBench/dataset-digital-agenda-indicators/blob/1557f93529d38602e07ddedfb2513d42189ff7e9/metadata.ttl)):

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

    The distribution annotations are generated automatically by the CI. You find the complete generated metadata [here](https://w3id.org/riverbench/datasets/digital-agenda-indicators/dev.ttl).

**Links:**

- [Profiles](https://w3id.org/riverbench/profiles) group datasets by stream type
- Datasets ([example](https://w3id.org/riverbench/datasets/assist-iot-weather-graphs/dev/#technical-metadata)) include `stax:hasStreamTypeUsage` annotations. This can be seen in:
    - [Dataset documentation pages](https://w3id.org/riverbench/datasets/)
    - Dataset [RDF metadata](https://w3id.org/riverbench/datasets/assist-iot-weather-graphs/dev.ttl)
- [Complete metadata dump](https://w3id.org/riverbench/dumps/dev.ttl.gz)


### Nanopublications

RDF-STaX is used in [nanopublications](nanopubs.md) to annotate stream types in research works or software. You can find more information on the [dedicated page about nanopublications](nanopubs.md).

## See also

- [Contributing](contributing.md)
- [Licensing and citation](licensing.md)
