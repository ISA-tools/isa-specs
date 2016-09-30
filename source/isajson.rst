===============
ISA-JSON format
===============

:Status: ISA-JSON specification v1.0 (September 2016)

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in RFC 2119.


Definitions
===========
For detail on ISA framework terminology, please read the ISA Abstract Model specification documentation.

----------------------
ISA-JSON v1.0 overview
----------------------
This document describes the ISA model reference implementation in the JSON format [RFC7159_]. The JavaScript
Object Notation (JSON) [RFC7159_] is a text format for serializing structured data. Objects are rendered as an unordered
collection of name-value pairs. The JSON Schema (see [`JSON Schema`_], [`JSON Schema Core`_], and [`JSON Schema Validation`_])
defines a JSON format for describing JSON formats. Its latest specification is Draft 4.

The schemas are published in the ISA-API Github repository: https://github.com/ISA-tools/isa-api

.. _`ISAtools website`: http://isa-tools.org
.. _linkedISA: http://dx.doi.org/10.1186%2F1471-2105-15-S14-S4
.. _RFC7159: http://tools.ietf.org/html/rfc7159
.. _JSON Schema: http://json-schema.org/
.. _JSON Schema Core: http://tools.ietf.org/html/draft-zyp-json-schema-04
.. _JSON Schema Validation: http://tools.ietf.org/html/draft-fge-json-schema-validation-00
.. _ISA-Tab Spec RC 1.0: http://isatab.sourceforge.net/docs/ISA-TAB_release-candidate-1_v1.0_24nov08.pdf


ISA RC v1.0 JSON-Schemas
========================
The ISA-JSON schemas define the structure of the ISA-JSON objects that implement the ISA Abstract Model.

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

ISA-JSON content
================
The rules described here define the content and relationship rules that the ISA-JSON objects must adhere to to
implement ISA Abstract Model.

#. Files SHOULD be encoded using UTF-8.
#. ISA-JSON content MUST be well-formed JSON.
#. ISA-JSON content MUST validate against the ISA-JSON schemas.
#. ISA-JSON files SHOULD be suffixed with a .json extension.
#. Dates SHOULD be supplied in the ISO8601 format "YYYY-MM-DD".
#. DOIs SHOULD conform to the standard format "10.NN/xxxNNNNNN".
#. PubMed IDs SHOULD be a string of eight numbers (e.g. 12345678), optionally prefixed with PMC (e.g. PMC12345678).
#. Characteristic Categories declared SHOULD be referenced by at least one Characteristic.
#. Characteristics MUST reference a Characteristic Category declaration.
#. Unit Categories declared SHOULD be referenced by at least one Unit.
#. Units MUST reference a Unit Category declaration.
#. All Sources and Samples MUST be declared in the Study-level materials section.
#. All other materials (Extracts etc.) and DataFiles MUST be declared in the Assay-level material and data sections respectively.
#. Each Process in a Process Sequence MUST link with other Processes forwards or backwards, unless it is a starting or terminating Process (i.e. Beginning or end of the experimental graph).
#. Protocols declared SHOULD be referenced by at least one Protocol REF.
#. Protocol REFs MUST reference a Protocol declaration.
#. Study Factors declared SHOULD be referenced by at least one Factor Value.
#. Factor Values MUST reference a Study Factor declared in the Study-level factors section.
#. Protocols SHOULD have a name (in order to be referenced in ISA-Tab).
#. Protocol Parameters SHOULD have a name (in order to be referenced in ISA-Tab).
#. Study Factors SHOULD have a name (in order to be referenced in ISA-Tab).
#. Sources and Samples declared SHOULD be referenced by at least one Process at the Study-level.
#. Samples, other materials, and DataFiles declared SHOULD be used in at least one Process at the Assay-level.
#. Study and Assay filenames SHOULD be present (in order to be referenced in ISA-Tab).
#. Ontology Source References declared SHOULD be referenced by at least one Ontology Annotation.
#. Ontology Annotations MUST reference a Ontology Source Reference declaration.
#. Ontology Source References MUST contain a Term Source Name.
#. Ontology Annotations with a term and/or accession MUST provide a Term Source REF pointing to a declared Ontology Source Reference.
#. Publication metadata SHOULD match that of publication record in PubMed corresponding to the provided PubMed ID.
#. Comments MUST have a name.
