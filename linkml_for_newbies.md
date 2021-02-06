# LinkML for Newbies
This is a guide to getting started with LinkML and the ClinGen / VICC
SEPIO / VA LinkML schemas. It is intended to give a ground-up tour of the
schemas and the artifacts they generate, as well as the language and tools
surrounding their use.

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

While a YAML doesn't have a traditional header, there are a number of attributes
found throughout the LinkML and BioLink Model documentation that need to be
specified before you can get to the fun part of modeling the schema.

This section is an attempt to describe and link the salient elements of a LinkML
schema in plain english. When referencing the LinkML documentation, you will
note that LinkML is often referred to as BioLinkML, or _blml_. For the reasons
indicated [above](#the-biolinkml-package), these terms are to be treated as
synonymous with LinkML.

All of the attributes for a LinkML schema definition are summarized
[here](https://biolink.github.io/biolinkml/docs/SchemaDefinition), and we will
go into a few of the specifics on these fields below.

### id
The very first line of every LinkML schema should be the `id`, which is one of
two required fields for a LinkML schema:
```yaml
id: https://example.org/example-schema
```
The purpose of [the id field](https://biolink.github.io/biolinkml/docs/id)
is to designate the official [URI]() for the schema.

This id is for locating information about the schema document. It should direct
people to documentation on the schema (for VRS the id would be
https://vrs.ga4gh.org).

### name
The only other required field is the schema `name`. In markdown, this is
specified as `SchemaDefinition->name`, to differentiate it from the `name`
slot in other classes. In LinkML, slots are defined separate from classes and
can have [custom definitions](https://biolink.github.io/biolinkml/docs/slot_usage.html)
based on the class context in which it is used.

The name is a space separated short label for the document, such as
`example schema` or `Bob's schema for the UK`.

### prefixes
Prefixes are used to transform CURIEs into URIs. For example:
```yaml
prefixes:
  biolinkml: https://w3id.org/biolink/biolinkml/
  wgs: http://www.w3.org/2003/01/geo/wgs84_pos#
  qud: http://qudt.org/1.1/schema/qudt#
```
The CURIE `wgs:lat` will expand to http://www.w3.org/2003/01/geo/wgs84_pos#lat.

### imports
Imports are used to import other schema into the main schema document. One of
the objectives of this repository is to separate out schema components into
separate modules around their intended use, and so we will need to implement
imports. The BioLink Model repo imports `biolinkml:types` to [refer to the
LinkML types](https://github.com/biolink/biolink-model/blob/master/biolink-model.yaml#L172-L173).

```yaml
prefixes:
  biolinkml: https://w3id.org/biolink/biolinkml/

imports:
  - biolinkml:types
```

## Related reading
- [General Design of LinkML](https://github.com/biolink/biolinkml/blob/master/SPECIFICATION.md)
