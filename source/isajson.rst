===============
ISA-JSON format
===============

:Status: ISA Model and Serialization Specifications 1.0 (6 October 2016)

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described by `RFC 2119 <http://www.ietf.org/rfc/rfc2119.txt>`_.

The ISA Model and Serialization Specifications are licensed under `CC BY-SA 4.0 <https://creativecommons.org/licenses/by-sa/4.0/>`_.

The ISA Model and Serialization Specifications are maintained by Susanna-Assunta Sansone [1]_, Philippe Rocca-Serra [1]_, Alejandra
Gonzalez-Beltran [1]_ and David Johnson [1]_ on behalf of the `ISA Community <http://www.isacommons.org>`_.

.. [1] Oxford e-Research Centre, University of Oxford, UK.

If you wish to make comments regarding this specification, please report using the
`ISA Specifications issue tracker <https://github.com/ISA-tools/isa-specifications/issues>`_ or send them to
isatools@googlegroups.com. All comments are welcome.

------------
Introduction
------------
ISA is a metadata framework for describing experiments in biology and medicine. For a full introduction to the ISA
framework, see http://www.isa-tools.org

The ISA specifications define an Abstract Model of the metadata framework. The ISA Abstract Model has been implemented
in two format specifications, ISA-Tab and ISA-JSON, both of which have supporting tools and services associated with
them. The format specifications are also available for additional tooling to take advantage of ISA-formatted content.

.. Important:: As a pre-requisite to reading this specification, please make sure you have read and understood the :doc:`ISA Abstract Model </isamodel>` that the ISA-Tab format is based on.

-----------
Definitions
-----------
For detail on ISA framework terminology, please read the :doc:`ISA Abstract Model specification </isamodel>`.

-------------
Specification
-------------
This document describes the ISA Abstract Model reference implementation specified in the JSON format [RFC7159_]. The JavaScript
Object Notation (JSON) [RFC7159_] is a text format for serializing structured data. Objects are rendered as an unordered
collection of name-value pairs. The JSON Schema (see [`JSON Schema`_], [`JSON Schema Core`_], and [`JSON Schema Validation`_])
defines a JSON format for describing JSON formats.

.. _RFC7159: http://tools.ietf.org/html/rfc7159
.. _JSON Schema: http://json-schema.org/
.. _JSON Schema Core: http://tools.ietf.org/html/draft-zyp-json-schema-04
.. _JSON Schema Validation: http://tools.ietf.org/html/draft-fge-json-schema-validation-00

Below we provide the schemas and the content rules for valid ISA-JSON documents. Full examples of ISA content as
ISA-JSON can be found in the sample data package of the ISA API, here https://git.io/vPZ2e We recommend that you study
these to better understand the structure of ISA-JSON documents.

Schemas
=======
The ISA-JSON schemas define the structure of the ISA-JSON objects that implement the ISA Abstract Model. Here we
list the JSON schemas with their corresponding model entity, and provide show the schema implemented.

You can also find these schemas in Github at https://git.io/vPZgD

assay_schema.json
-----------------
This schema implements Assay from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/assay_schema.json
    :language: json

comment_schema.json
-------------------
This schema implements Comment from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/comment_schema.json
    :language: json

data_schema.json
----------------
This schema implements Data from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/data_schema.json
    :language: json

factor_schema.json
------------------
This schema implements Factor from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/factor_schema.json
    :language: json

factor_value_schema.json
------------------------
This schema implements Factor from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/factor_value_schema.json
    :language: json

investigation_schema.json
-------------------------
This schema implements Investigation from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/investigation_schema.json
    :language: json

material_attribute_schema.json
------------------------------
This schema implements Material from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/material_attribute_schema.json
    :language: json

material_attribute_value_schema.json
------------------------------------
This schema implements Material from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/material_attribute_value_schema.json
    :language: json

material_schema.json
--------------------
This schema implements Material from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/material_schema.json
    :language: json

ontology_annotation_schema.json
-------------------------------
This schema implements Ontology from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/ontology_annotation_schema.json
    :language: json

ontology_source_reference_schema.json
-------------------------------------
This schema implements Ontology from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/ontology_source_reference_schema.json
    :language: json

person_schema.json
------------------
This schema implements Person from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/person_schema.json
    :language: json

process_parameter_value_schema.json
-----------------------------------
This schema implements Process from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/process_parameter_value_schema.json
    :language: json

process_schema.json
-------------------
This schema implements Process from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/process_schema.json
    :language: json

protocol_parameter_schema.json
------------------------------
This schema implements Protocol from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/protocol_parameter_schema.json
    :language: json

protocol_schema.json
--------------------
This schema implements Protocol from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/protocol_schema.json
    :language: json

publication_schema.json
-----------------------
This schema implements Publication from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/publication_schema.json
    :language: json

sample_schema.json
------------------
This schema implements Sample from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/sample_schema.json
    :language: json

source_schema.json
------------------
This schema implements Source from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/source_schema.json
    :language: json

study_schema.json
-----------------
This schema implements Study from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/study_schema.json
    :language: json


Content rules
=============
The rules described here define the content and relationship rules that the ISA-JSON objects must adhere to to
implement ISA Abstract Model.

#. Files SHOULD be encoded using `UTF-8 <http://www.fileformat.info/info/unicode/utf8.htm>`_.
#. ISA-JSON content MUST be well-formed `JSON <http://tools.ietf.org/html/rfc7159>`_.
#. ISA-JSON content MUST validate against the ISA-JSON schemas.
#. ISA-JSON files SHOULD be suffixed with a ``.json`` extension.
#. Dates SHOULD be supplied in the `ISO8601 <http://www.iso.org/iso/home/standards/iso8601.htm>`_ format "YYYY-MM-DD".
#. DOIs SHOULD conform to the standard format `ISO 26324 <http://www.iso.org/iso/catalogue_detail?csnumber=43506>`_ DOI format "10.NN/xxxNNNNNN".
#. `PubMed IDs <https://www.nlm.nih.gov/bsd/disted/pubmedtutorial/020_830.html>`_ SHOULD be a string of eight numbers (e.g. 12345678), optionally prefixed with PMC (e.g. PMC12345678).
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