[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/RDF-STaX/rdf-stax.github.io?sort=semver)](https://w3id.org/stax/stable) [![Website](https://img.shields.io/website?down_color=red&down_message=offline&up_color=green&up_message=up&url=https%3A%2F%2Fw3id.org%2Fstax)](https://w3id.org/stax) [![.github/workflows/validate.yml](https://github.com/RDF-STaX/rdf-stax.github.io/actions/workflows/validate.yml/badge.svg)](https://github.com/RDF-STaX/rdf-stax.github.io/actions/workflows/validate.yml) [![GitHub License](https://img.shields.io/github/license/RDF-STaX/rdf-stax.github.io)](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/LICENSE) [![GitHub issues](https://img.shields.io/github/issues/RDF-STaX/rdf-stax.github.io)](https://github.com/RDF-STaX/rdf-stax.github.io/issues)

# RDF Stream Taxonomy (RDF-STaX)

This is the main repository of the RDF Stream Taxonomy. Here you will find the ontology itself (`src`) and the documentation sources (`docs`).

**Read more about RDF-STaX on the [official website](https://w3id.org/stax/).**

Please file any feature requests, bugs, or other issues in the **[issue tracker](https://github.com/RDF-STaX/rdf-stax.github.io/issues)**.

## Editing the ontology

- The main ontology file is `src/stax.ttl`. It should be edited with Protégé.
    - Do not add information about the authors/contributors there. This is done in the `src/authors.ttl` file (see below).
    - Do not set the ontology's version IRI or version – this is done automatically in CI during release.
- The `src/authors.ttl` file contains information about the authors/contributors of the ontology. It should be edited manually with a text editor.
- The `tests` directory contains competency question tests that are ran automatically. Implementing new tests is [documented on the RDF-STaX website](https://w3id.org/stax/dev/contributing#competency-question-tests).

## Editing documentation

Documentation is stored in the [`docs` directory](https://github.com/RDF-STaX/rdf-stax.github.io/tree/main/docs). You can open a pull request for any of the files there, except the ones in the `includes` subdirectory. These files are generated automatically in the CI pipeline.

## Citation

If you use RDF-STaX in your research, please cite [the paper introducing it](https://arxiv.org/abs/2311.14540) ([PDF](https://arxiv.org/pdf/2311.14540.pdf)):

Sowinski, P., Szmeja, P. Ganzha, M., & Paprzycki, M. (2023). RDF Stream Taxonomy: Systematizing RDF Stream Types in Research and Practice. _[arXiv preprint arXiv:2311.14540](https://arxiv.org/abs/2311.14540)_.

Or use this BibTeX entry:

```bibtex
@article{sowinski2023rdfstax,
  title={RDF Stream Taxonomy: Systematizing RDF Stream Types in Research and Practice}, 
  author={Piotr Sowinski and Pawel Szmeja and Maria Ganzha and Marcin Paprzycki},
  journal={arXiv preprint arXiv:2311.14540},
  year={2023},
  url={https://doi.org/10.48550/arXiv.2311.14540},
  doi={10.48550/arXiv.2311.14540}
}
```

## License

The RDF-STaX ontology and its documentation is licensed under the [Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/) license.
