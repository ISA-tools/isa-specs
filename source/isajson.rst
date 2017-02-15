===============
ISA-JSON format
===============

.. Important:: As a pre-requisite to reading this specification, please make sure you have read and understood the :doc:`ISA Abstract Model </isamodel>` that the ISA-Json format is based on.

For detail on ISA framework terminology, please read the :doc:`ISA Abstract Model specification </isamodel>`.

This document describes the ISA Abstract Model reference implementation specified in the JSON format [RFC7159_]. The JavaScript
Object Notation (JSON) [RFC7159_] is a text format for serializing structured data. Objects are rendered as an unordered
collection of name-value pairs. The JSON Schema (see [`JSON Schema`_], [`JSON Schema Core`_], and [`JSON Schema Validation`_])
defines a JSON format for describing JSON formats.

.. _RFC7159: http://tools.ietf.org/html/rfc7159
.. _JSON Schema: http://json-schema.org/
.. _JSON Schema Core: http://tools.ietf.org/html/draft-zyp-json-schema-04
.. _JSON Schema Validation: http://tools.ietf.org/html/draft-fge-json-schema-validation-00

Below we provide the `schemas`_ and the `content rules`_ for valid ISA-JSON documents. Full examples of ISA content as
ISA-JSON can be found in the ISA datasets repository, here https://git.io/vD1vx.

We recommend that you study these to better understand the structure of ISA-JSON documents.

Format
======
Files SHOULD be encoded using `UTF-8 <http://www.fileformat.info/info/unicode/utf8.htm>`_.

All ISA-JSON content regarding multiple ``Study`` and ``Assay`` should fall under one ``Investigation`` JSON structure,
therefore should be recorded in a single JSON file. The JSON file SHOULD have a ``.json`` extension.

Dates SHOULD be supplied in the `ISO8601 <http://www.iso.org/iso/home/standards/iso8601.htm>`_ format ``YYYY-MM-DD``.

For maximal portability file names should only contain only ASCII characters not excluded
already (that is ``A-Za-z0-9._!#$%&+,;=@^(){}'[]`` - we exclude space as many utilities
do not accept spaces in file paths): non-English alphabetic characters cannot be guaranteed
to be supported in all locales. It would be good practice to avoid the shell metacharacters
``(){}'[]$."``.

Schemas
=======
The ISA-JSON schemas define the structure of the ISA-JSON objects that implement the ISA Abstract Model. Here we
list the JSON schemas with their corresponding model entity, and provide show the schema implemented.

You can also find these schemas in Github at https://git.io/vPZgD

investigation_schema.json
-------------------------
This schema implements Investigation from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/investigation_schema.json
    :language: json

study_schema.json
-----------------
This schema implements Study from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/study_schema.json
    :language: json

assay_schema.json
-----------------
This schema implements Assay from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/assay_schema.json
    :language: json

comment_schema.json
-------------------
This schema implements the ability to annotate objects with user-defined comments.

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
This schema implements Study factor from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/factor_schema.json
    :language: json

factor_value_schema.json
------------------------
This schema implements Factor value given to a node corresponding to a declared Factor.

Schema:

.. literalinclude:: _static/isajson/factor_value_schema.json
    :language: json

material_attribute_schema.json
------------------------------
This schema is used in a Material node to declare an attribute (Characteristic).

Schema:

.. literalinclude:: _static/isajson/material_attribute_schema.json
    :language: json

material_attribute_value_schema.json
------------------------------------
This schema is used in a Material node to hold an attribute value (value of a Characteristic).

Schema:

.. literalinclude:: _static/isajson/material_attribute_value_schema.json
    :language: json

material_schema.json
--------------------
This schema implements Material nodes from the ISA Abstract Model.

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
This schema implements Contact from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/person_schema.json
    :language: json

process_parameter_value_schema.json
-----------------------------------
This schema is used in a Process node to hold a parameter value (value of a Protocol parameter).

Schema:

.. literalinclude:: _static/isajson/process_parameter_value_schema.json
    :language: json

process_schema.json
-------------------
This schema implements Process nodes from the ISA Abstract Model.

Schema:

.. literalinclude:: _static/isajson/process_schema.json
    :language: json

protocol_parameter_schema.json
------------------------------
This schema is used in a Protocol to describe a protocol parameter.

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