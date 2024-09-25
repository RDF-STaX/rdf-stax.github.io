# Nanopublications

[Nanopublications](https://nanopub.net/) are small units of publishable knowledge. RDF-STaX provides some [helpful tools](#making-new-nanopublications) to aid you making nanopublications about RDF stream types in papers, software, on the Web, or elsewhere. You can also browse the existing nanopublications and use them in your work.

These Nanopublications essentially serve as a **collaborative, living literature review** of RDF streaming. You can query them to find out how RDF stream types are used in practice, and you can also contribute your own findings.

## Existing nanopublications

--8<-- "docs/includes/nanopub_links.md"

!!! example "Experimental: SPARQL endpoint"

    You can query the dataset through the experimental SPARQL endpoint: **[query GUI](https://query.np.trustyuri.net/tools/type/aabe9436b877b6a91acaa9741b3e1e5c1f47e1069ff2c0cb2bf0ceac25176629/yasgui.html)**.

    Endpoint URL: `https://query.np.trustyuri.net/repo/type/aabe9436b877b6a91acaa9741b3e1e5c1f47e1069ff2c0cb2bf0ceac25176629`

    *This endpoint may change or stop working in the future without prior notice.*
    

All valid nanopublications that annotate stream types using RDF-STaX can be downloaded using the links above. This dump is created automatically in the CI, and is updated whenever the ontology changes.

You can also download the nanopubs using content negotiation on URLs like: 

- `https://w3id.org/stax/{version}/nanopubs`
- `https://w3id.org/stax/nanopubs`

The following content types are supported: `application/trig`, `application/n-quads`.

There are also [other ways to access the nanopublications](https://nanopub.net/docs/network) – you can search for nanopubs with these parameters:

- Predicate: `http://purl.org/nanopub/x/hasNanopubType`
- Object: `https://w3id.org/stax/ontology#RdfStreamTypeUsage`

## Making new nanopublications

There are [several ways to make nanopublications](https://nanopub.net/docs/tools), but the easiest is using **[Nanodash](https://nanodash.petapico.org/)**. You only need to log in with your ORCID account, and you can start creating nanopublications right away.

To create a nanopublication about RDF stream type usage, simply use **[this template](https://nanodash.petapico.org/publish?template=https://w3id.org/np/RAxdT1PPKv4bzQkAwVf_0m3-Hv7NeK9dLcL3snD_TsURE)** – it will guide you through the process.

The published nanopublications can be later updated or retracted, if needed.

Your nanopublications will automatically appear on this page after at most a day or two. The SPARQL endpoint listed above is updated much faster, usually within a few minutes.

### Example nanopublication

You can see an example nanopublication using this template [here](https://w3id.org/np/RAh9bvQwkL2SDp7iqmH7G6rOrCnWtTMHgHR_St0udrRKo) and in [Nanodash](https://nanodash.petapico.org/explore?188&id=https://w3id.org/np/RAh9bvQwkL2SDp7iqmH7G6rOrCnWtTMHgHR_St0udrRKo).

## See also

- [How to use RDF-STaX](use-it.md)
- [Taxonomy overview](taxonomy.md)
- [Ontology documentation](ontology.md)
