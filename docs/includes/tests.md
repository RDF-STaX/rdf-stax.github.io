## Use case 1

**Annotating published datasets and streams.** In this use case, RDF-STaX's stream types are used as metadata of published RDF datasets or streams, for example on the Internet. This published metadata is intended for the various users to understand the content of the stream. The [usage manual](../use-it.md) has several examples for this type of usage.

### Test CQ1.1 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc1/cq1-1.yaml))

**Question:** What are the names and descriptions of all RDF stream types?

**Expectation:** there are 10 query results

??? example "SPARQL query of the test"

    ```sparql
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT * WHERE {
        ?streamType a/rdfs:subClassOf* stax:RdfStreamType ;
            skos:prefLabel ?label ;
            skos:note ?note .
    }
    ```

### Test CQ1.2 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc1/cq1-2.yaml))

**Question:** What is the definition for each stream type?

**Expectation:** there are 10 query results

??? example "SPARQL query of the test"

    ```sparql
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT * WHERE {
        ?streamType a/rdfs:subClassOf* stax:RdfStreamType ;
            skos:definition ?definition .
    }
    ```

### Test CQ1.3 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc1/cq1-3.yaml))

**Question:** What is the type of element of each concrete stream type? Provide additional references to external sources for each element type, if available.

**Expectation:** there are 7 query results

??? example "SPARQL query of the test"

    ```sparql
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT * WHERE {
        ?streamType a stax:ConcreteRdfStreamType ;
            stax:hasElementType ?elementType .

        OPTIONAL {
            ?elementType skos:relatedMatch ?reference .
        }
    }
    ```

### Test CQ1.4 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc1/cq1-4.yaml))

**Question:** How can each of the concrete stream types be used? Provide a link to one example for each.

**Expectation:** there are 7 query results

??? example "SPARQL query of the test"

    ```sparql
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT ?streamType (SAMPLE(?example) as ?anyExample) WHERE {
        ?streamType a stax:ConcreteRdfStreamType ;
            skos:example ?example .
    }
    GROUP BY ?streamType
    ```

## Use case 2

**Embedding metadata in RDF streams.** This use case is similar to use case 1, but more focused on embedding the stream type metadata *within* the stream itself, with the goal of enabling streaming tool interoperability. For example, a consumer of the stream can check the type of the stream and decide whether it can consume it or not (and if any additional conversions are required).

### Test CQ2.1 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc2/cq2-1.yaml))

**Question:** Which concrete stream types can be viewed as generalizations of other stream types?

**Expectation:** there are 4 query results

??? example "SPARQL query of the test"

    ```sparql
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT * WHERE {
        ?broaderStreamType a stax:ConcreteRdfStreamType ;
      		skos:narrower+ ?narrowerStreamType .
    }
    ```

### Test CQ2.2 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc2/cq2-2.yaml))

**Question:** Which concrete stream types can be trivially extended (by assuming the default graph) into other stream types?

**Expectation:** there are 3 query results

??? example "SPARQL query of the test"

    ```sparql
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT * WHERE {
        ?baseStreamType a stax:ConcreteRdfStreamType ;
      		skos:broader*/stax:canBeTriviallyExtendedInto ?extendedStreamType .
    }
    ```

### Test CQ2.3 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc2/cq2-3.yaml))

**Question:** Which concrete stream types can be flattened into other stream types?

**Expectation:** there are 9 query results

??? example "SPARQL query of the test"

    ```sparql
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT * WHERE {
        ?baseStreamType a stax:ConcreteRdfStreamType ;
      		skos:broader*/stax:canBeFlattenedInto ?flattenedStreamType .
    }
    ```

### Test CQ2.4 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc2/cq2-4.yaml))

**Question:** Which concrete stream types can be grouped to obtain other stream types?

**Expectation:** there are 2 query results

??? example "SPARQL query of the test"

    ```sparql
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT * WHERE {
        ?baseStreamType a stax:ConcreteRdfStreamType ;
      		skos:broader*/stax:canBeGroupedInto ?groupedStreamType .
    }
    ```

## Use case 3

**Analyzing the state of the art of RDF streaming.** This use case is realized with [RDF-STaX's Nanopublication mechanism](../nanopubs.md), which allows anyone to publish statements like "paper/software X uses stream type Y". The collection of such published nanopublications can then be later used to derive insights about the state of the art (SOTA) of RDF streaming. RDF-STaX can also be used in SOTA investigations outside the context of Nanopublications.

### Test CQ3.1 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc3/cq3-1.yaml))

**Question:** What are the taxonomical parents of each stream type, listed in order?

**Expectation:** there are 10 query results

??? example "SPARQL query of the test"

    ```sparql
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT ?label (GROUP_CONCAT(?broader; SEPARATOR=", ") as ?parents) WHERE {
        ?streamType a/rdfs:subClassOf* stax:RdfStreamType ;
            skos:prefLabel ?label .

        OPTIONAL {
            ?streamType skos:broader+ [ skos:prefLabel ?broader ] .
        }
    }
    GROUP BY ?streamType ?label
    ```

### Test CQ3.2 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc3/cq3-2.yaml))

**Question:** Is there any stream type that is a taxonomical parent or child of itself?

**Expectation:** query results are empty

??? example "SPARQL query of the test"

    ```sparql
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT * WHERE {
        {
            ?streamType skos:broader+ ?streamType .
        }
        UNION
        {
            ?streamType skos:narrower+ ?streamType .
        }
    }
    ```

### Test CQ3.3 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc3/cq3-3.yaml))

**Question:** Which conversions between concrete stream types cannot be done in any trivial way (grouping, flattening, extending)? Allow for multiple trivial transformations in series and take into account the taxonomical structure.

**Expectation:** there are 25 query results

??? example "SPARQL query of the test"

    ```sparql
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT ?fromStreamType ?toStreamType WHERE {
        ?toStreamType a stax:ConcreteRdfStreamType .
        ?fromStreamType a stax:ConcreteRdfStreamType

        MINUS {
            ?fromStreamType
                (skos:broader*/(stax:canBeFlattenedInto|stax:canBeGroupedInto|stax:canBeTriviallyExtendedInto)?)+
                ?toStreamType .
        }
    }
    ```

