# Contributing to RDF-STaX

Do you have an idea for how to improve RDF-STaX? Or maybe you found a bug? **Any contributions are welcome!**

## Filing issues

Feature requests, bug reports, and other issues can be filed in the [issue tracker on GitHub](https://github.com/RDF-STaX/rdf-stax.github.io/issues).

## Communication

You can join the **[Discord chat](https://discord.gg/e4TaZgsYNQ)** to discuss RDF-STaX with the community.

## Editing the ontology

The ontology is stored in the [`src` directory of the main repository](https://github.com/RDF-STaX/rdf-stax.github.io/tree/main/src). It is split into two files:

- The main ontology file is `src/stax.ttl`. It should be edited with Protégé.
    - Do not add information about the authors/contributors there. This is done in the `src/authors.ttl` file (see below).
    - Do not set the ontology's version IRI or version – this is done automatically in CI during release.
    - You must keep this file valid OWL 2 DL. The CI will check it when you open a pull request.
- The `src/authors.ttl` file contains information about the authors/contributors of the ontology. It should be edited manually with a text editor.
- The `src/alignments.ttl` file contains alignments to other vocabularies. It should be edited manually with a text editor.

**Pull requests are welcome.**

### Competency question tests

The competency question tests are stored in the [`tests` directory](https://github.com/RDF-STaX/rdf-stax.github.io/tree/main/tests), divided into subdirectories by use cases – `uc{X}`. Each test is defined as a pair of files: a YAML file named `cq{X}-{Y}.yaml`, and SPARQL file named `cq{X}-{Y}.rq`, where `{X}` is the use case number and `{Y}` is the test number. The YAML file contains the metadata of the test, and the SPARQL file contains the query to be executed against the ontology.

The YAML file must adhere to the JSON Schema defined in the [`tests/test-schema.json` file](https://github.com/RDF-STaX/rdf-stax.github.io/blob/main/tests/test-schema.json). The CI will check if the tests are valid when you open a pull request.

In each use case directory there is also an `index.md` file that describes the use case. This file is used to generate the documentation on the website.

A list of all implemented competency question tests can be found in the [documentation](uses/cq.md).

### CI pipeline

The CI automatically publishes the ontology (see [the releases section below](#releases)) and pushes it to the website. The CI does the following:

- Check if the ontology is valid and matches the OWL 2 DL profile (with [ROBOT](https://robot.obolibrary.org/)).
- Validate the competency question tests and run them agains the ontology.
- Set the ontology's version IRI and version.
- Save an OWL 2 DL version of the ontology in all supported formats.
    - For [Jelly](https://w3id.org/jelly), the CI uses the [Apache Jena RIOT utility](https://jena.apache.org/documentation/tools/index.html) with the [Jelly-JVM plugin for Jena](https://w3id.org/jelly/jelly-jvm/dev/getting-started-plugins/).
- Infer additional statements with [ROBOT](https://robot.obolibrary.org/reason).
- Merge in the author information from `src/authors.ttl`.
- Merge in the alignments to other vocabularies from `src/alignments.ttl`.
- Serialize the ontology in all supported formats.

The CI code can be found in the [`ci-worker` repository](https://github.com/RDF-STaX/ci-worker). The code there is licensed under Apache 2.0.

## Editing documentation

Documentation is also stored in the main repository, in the [`docs` directory](https://github.com/RDF-STaX/rdf-stax.github.io/tree/main/docs). You can open a pull request for any of the files there, except the ones in the `includes` subdirectory. These files are generated automatically in the CI pipeline.

You can also use the *Edit this page* link in the top right corner of each page on the website to edit the page directly on GitHub.

## Releases

The `dev` (development) version corresponds to the `main` branch of the repository. A new development release is made automatically every time a commit is pushed to the `main` branch.

The stable versions (e.g., 1.0.0) are created manually by the maintainer. To create a new tagged release:

1. Check out the main branch of the [main repo](https://github.com/RDF-STaX/rdf-stax.github.io) on your local machine.
2. Update the main branch by running git pull. Make sure the pull was successful.
3. Create a new tag with the version number: `git tag vX.Y.Z`.
4. Push the tag to GitHub: `git push origin --tag vX.Y.Z`.

The rest of the process is automatic. Make sure to prepend `v` before the version tag, e.g., `v1.0.0`. Otherwise, the release will not be created.

## See also

- [How to use RDF-STaX?](use-it.md)
- [Licensing and citation](licensing.md)
