## Use case 1

Test use case description. **With Markdown formatting**.

### Test CQ1.1 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc1/cq1-1.yaml))

**Question:** What are the names of all RDF stream types?

**Expectation:** there are 10 query results

??? example "SPARQL query of the test"

    ```sparql
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT * WHERE {
        ?streamType a/rdfs:subClassOf* stax:RdfStreamType ;
            skos:prefLabel ?label .
    }
    ```

### Test CQ1.2 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc1/cq1-2.yaml))

**Question:** What are the names of all RDF stream types?

**Expectation:** query results are not empty

??? example "SPARQL query of the test"

    ```sparql
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT * WHERE {
        ?streamType a/rdfs:subClassOf* stax:RdfStreamType ;
            skos:prefLabel ?label .
    }
    ```

## Use case 2

Test use case 2 description. **With Markdown formatting**.

### Test CQ2.1 ([definition](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/uc2/cq2-1.yaml))

**Question:** What are the names of all RDF stream types?

**Expectation:** there are 10 query results

??? example "SPARQL query of the test"

    ```sparql
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX stax: <https://w3id.org/stax/ontology#>

    SELECT * WHERE {
        ?streamType a/rdfs:subClassOf* stax:RdfStreamType ;
            skos:prefLabel ?label .
    }
    ```

