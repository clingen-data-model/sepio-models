# LinkML for Newbies
This is a guide to getting started with LinkML and the ClinGen / VICC
SEPIO / VA LinkML models. It is intended to give a ground-up tour of the models
and the artifacts they generate, as well as the language and tools surrounding
their use.

## Why this guide
Many of the tools, utilities, and resources surrounding LinkML are both
feature-dense and still evolving, so this is a stripped-down version of the
documentation in those resources focused solely on what we've used and why.

## Installation
First, you will need to install some libraries and utilities to use LinkML.
We use a `Pipfile` to help with that, which is a file for specifying
dependencies and is used with the [pipenv](https://github.com/pypa/pipenv)
environment manager. Pipenv is used for a few
[VICC](http://github.com/cancervariants/) projects as well as the [LinkML
modeling language](https://github.com/biolink/biolinkml) itself.

You may install all dependencies using Pipenv. From the project root directory:
```shell
pipenv install --dev
```

### The biolinkml package
The first piece of tribal knowledge to document is that LinkML is currently
called BioLinkML. Talk to anyone involved in these projects and they will call
it LinkML–but the documentation does not reflect this (yet). The reason for this
is that BioLinkML evolved in parallel to the
[BioLink Model](https://github.com/biolink/biolink-model), but enough people
were getting confused about this that a rebranding to LinkML was deemed prudent.

As a consequence, the first dependency of this repo, `biolinkml`, is the
package corresponding the LinkML library, which provides us with much of the
functionality needed to generate artifacts (e.g. UML, JSON Schema, protobuf,
ShEx) from the LinkML models.

### Dev packages
Some dev packages are also provided. These are needed to run the analysis
notebooks. If you only wish to rebuild artifacts using the built-in tools,
you may omit the `--dev` flag from the pipenv installation.

- `jupyterlab` is for [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/),
  an IDE for Project Jupyter (and Jupyter Notebooks).
- `yamlmagic` is for [directly importing YAML]()
  to the notebook python kernel.

## Writing LinkML
LinkML is pretty cool, but can be overwhelming to users that are not familiar
with the language (or, at least it was overwhelming to me 😵).

This section is an attempt to describe and link the salient elements of a LinkML
model in plain english.

While a YAML doesn't have a traditional header, there are a number of attributes
found throughout the LinkML and BioLink Model documentation that need to be
specified before you can get to the fun part of modeling the schema.

### id
The very first line of every model should be the id:
```yaml
id: https://example.org/example-schema
```
The purpose of this id is ...

## Related reading
- [General Design of LinkML](https://github.com/biolink/biolinkml/blob/master/SPECIFICATION.md)
