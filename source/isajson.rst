===============
ISA JSON format
===============

:Status: ISA-JSON v1.0 specification document, September 2016.

Introduction
------------
Investigation/Study/Assay (ISA) `ISAtools website`_ is a model for the description of experimental data. It was designed
to be serialised in tabular format, given the familiarity of spreadsheets for biologists, who were the main target
audience.

Since the inception of the Tabular representation, an RDF serialisation was devised relying on the linkedISA converter
tool [linkedISA_]. This RDF representation contains all the information in the Tabular format but additionally, it makes
explicit the semantic of the different entities of the ISA model and its relationships.

This document describes another serialization of the ISA model relying on the JSON format [RFC7159_]. The JavaScript
Object Notation (JSON) [RFC7159_]is a text format for serializing structured data. Objects are rendered as an unordered
collection of name-value pairs. The JSON Schema (see [`JSON Schema`_], [`JSON Schema Core`_], and [`JSON Schema Validation`_])
defines a JSON format for describing JSON formats. Its latest specification is Draft 4.

After describing the ISA model itself, the JSON-schemas [JS-Core] and corresponding JSON representation for the ISA
model RC 1.0 [`ISA-Tab Spec RC 1.0`_] is presented.

The schemas will be made available through the ISA-API Github repository: https://github.com/ISA-tools/isa-api

.. _`ISAtools website`: http://isa-tools.org
.. _linkedISA: http://dx.doi.org/10.1186%2F1471-2105-15-S14-S4
.. _RFC7159: http://tools.ietf.org/html/rfc7159
.. _JSON Schema: http://json-schema.org/
.. _JSON Schema Core: http://tools.ietf.org/html/draft-zyp-json-schema-04
.. _JSON Schema Validation: http://tools.ietf.org/html/draft-fge-json-schema-validation-00
.. _ISA-Tab Spec RC 1.0: http://isatab.sourceforge.net/docs/ISA-TAB_release-candidate-1_v1.0_24nov08.pdf

ISA RC v1.0 JSON-Schemas
------------------------
Investigation
    The investigation represents a collection of studies. It contains high-level information (identifier, title,
    description, submission date), information about the ontology sources, related publications, people involved and
    the set of associated studies (one or more).

.. literalinclude:: ./schemas/investigation_schema.json
    :language: json
    :caption: investigation_schema.json

.. literalinclude:: ./schemas/ontology_source_reference_schema.json
    :language: json
    :caption: ontology_source_reference_schema.json

.. literalinclude:: ./schemas/publication_schema.json
    :language: json
    :caption: publication_schema.json

.. literalinclude:: ./schemas/person_schema.json
    :language: json
    :caption: person_schema.json

.. literalinclude:: ./schemas/source_schema.json
    :language: json
    :caption: source_schema.json

.. literalinclude:: ./schemas/sample_schema.json
    :language: json
    :caption: sample_schema.json

.. literalinclude:: ./schemas/material_attribute_schema.json
    :language: json
    :caption: material_attribute_schema.json

.. literalinclude:: ./schemas/factor_schema.json
    :language: json
    :caption: factor_schema.json

.. literalinclude:: ./schemas/factor_value_schema.json
    :language: json
    :caption: factor_value_schema.json