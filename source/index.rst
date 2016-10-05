ISA Model and Serialization Specifications
==========================================

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
ISA is a metadata framework to manage an
increasingly diverse set of life science, environmental and biomedical experiments that employing one or a
combination of technologies. Built around the **Investigation** (the project context), **Study** (a unit of research)
and **Assay** (analytical measurements) abstract data model, ISA helps you to provide rich
descriptions of experimental metadata (i.e. sample characteristics, technology and measurement types, sample-to-data
relationships) so that the resulting data and discoveries are reproducible and reusable.

For a full introduction to the ISA framework, see http://www.isa-tools.org

The ISA Model and Serialization Specifications define an Abstract Model of the metadata framework. The ISA Abstract Model
has been implemented in two format specifications, ISA-Tab and ISA-JSON, both of which have supporting tools and
services associated with them. The format specifications are also available for additional tooling to take advantage
of ISA-formatted content.

.. toctree::
   :maxdepth: 2
   :numbered:

   isamodel
   isajson
   isatab
   implementations
   contributors

----------------
Revision History
----------------
+---------+----------------+------------------------------------------------------------------+
| Version | Date           | Description                                                      |
+=========+================+==================================================================+
| 1.0     | 2016-10-06     | Final release of ISA Model and Serializations specification [#]_ |
+---------+----------------+------------------------------------------------------------------+
| 1.0RC2  | 2009-01-01     | Second release candidate of ISA-Tab specification                |
+---------+----------------+------------------------------------------------------------------+
| 1.0RC1  | 2008-11-26     | First release candidate of ISA-Tab specification [#]_            |
+---------+----------------+------------------------------------------------------------------+

.. [#] http://isa-specifications.readthedocs.io
.. [#] http://isatab.sourceforge.net/docs/ISA-TAB_release-candidate-1_v1.0_24nov08.pdf