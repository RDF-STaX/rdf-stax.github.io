# Nanopublications

[Nanopublications](https://nanopub.net/) are small units of publishable knowledge. RDF-STaX provides some [helpful tools](#making-new-nanopublications) to aid you making nanopublications about RDF stream types in papers, software, on the Web, or elsewhere. You can also browse the existing nanopublications and use them in your work.

## Existing nanopublications

--8<-- "docs/includes/nanopub_links.md"

All valid nanopublications that annotate stream types using RDF-STaX can be downloaded using the links above. This dump is created automatically in the CI, and is updated whenever the ontology changes.

You can also download the nanopubs using content negotiation on URLs like: 

- `https://w3id.org/{version}/nanopubs`
- `https://w3id.org/nanopubs`

The following content types are supported: `application/trig`, `application/n-quads`.

There are also [other ways to access the nanopublications](https://nanopub.net/docs/network) – you can search for nanopubs with these parameters:

- Predicate: `http://purl.org/nanopub/x/hasNanopubType`
- Object: `https://w3id.org/stax/ontology#RdfStreamTypeUsage`

## Making new nanopublications

There are [several ways to make nanopublications](https://nanopub.net/docs/tools), but the easiest is using **[Nanodash](https://nanodash.petapico.org/)**. You only need to log in with your ORCID account, and you can start creating nanopublications right away.

To create a nanopublication about RDF stream type usage, simply use **[this template](https://nanodash.petapico.org/publish?template=https://w3id.org/np/RA91Mpsm7Ki1kdxPmxlucIyDDNv80Qp42KPpwcVSKr3n0)** – it will guide you through the process.

The published nanopublications can be later updated or retracted, if needed.

### Example nanopublication

You can see an example nanopublication using this template [here](https://w3id.org/np/RAh9bvQwkL2SDp7iqmH7G6rOrCnWtTMHgHR_St0udrRKo) and in [Nanodash](https://nanodash.petapico.org/explore?188&id=https://w3id.org/np/RAh9bvQwkL2SDp7iqmH7G6rOrCnWtTMHgHR_St0udrRKo).

## See also

- [How to use RDF-STaX](use-it.md)
- [Taxonomy overview](taxonomy.md)
- [Ontology documentation](ontology.md)
