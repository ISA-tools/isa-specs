ISA Model and Serialization Specifications
==========================================

**Note**: The latest version of the specification and documentation can be found at:
https://isa-tools.org/isa-api/content/index.html


**Status**: ISA Model and Serialization Specifications 1.0 (28 October 2016)

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described by `RFC 2119 <http://www.ietf.org/rfc/rfc2119.txt>`_.

The ISA Model and Serialization Specifications are licensed under `CC BY-SA 4.0 <https://creativecommons.org/licenses/by-sa/4.0/>`_.

The ISA Model and Serialization Specifications are maintained by Susanna-Assunta Sansone [1]_, Philippe Rocca-Serra [1]_, Alejandra
Gonzalez-Beltran [1]_ and David Johnson [1]_ on behalf of the `ISA Community <http://www.isacommons.org>`_.

.. [1] Oxford e-Research Centre, University of Oxford, UK.

If you wish to make comments regarding these specifications, please see the page on :doc:`how to contribute </contributing>`.

------------
Introduction
------------
ISA is a metadata framework to manage an increasingly diverse set of life science, environmental and biomedical experiments that employ one or a
combination of technologies. Built around the **Investigation** (the project context), **Study** (a unit of research)
and **Assay** (analytical measurements) concepts, ISA helps you to provide rich
descriptions of experimental metadata (i.e. sample characteristics, technology and measurement types, sample-to-data
relationships) so that the resulting data and discoveries are reproducible and reusable.

.. note::
    For an introduction to ISA, please read the paper, `Towards interoperable bioscience data <http://www.nature.com/ng/journal/v44/n2/full/ng.1054.html>`_ published in *Nature Genetics*. For more details on the ISA framework and supported tools, please see https://isa-tools.org

The ISA Model and Serialization Specifications define an Abstract Model of the metadata framework. The ISA Abstract Model
has been implemented in two format specifications, ISA-Tab and ISA-JSON, both of which have supporting tools and
services associated with them. The format specifications are also available for additional tooling to take advantage
of ISA-formatted content.

These specifications are primarily aimed at software engineers to facilitate the development of automated export from
databases, or import into analytical or other tools.

.. toctree::
   :maxdepth: 2
   :numbered:

   isamodel
   isatab
   isajson
   implementations
   contributing

----------------
Revision History
----------------
+---------+--------------------+------------------------------------------------------------------+
| Version | Date               | Description                                                      |
+=========+====================+==================================================================+
| 1.0     | 2016-10-28         | Final release of ISA Model and Serialization specifications [#]_ |
+---------+--------------------+------------------------------------------------------------------+
| 1.0     | 2009-01-13         | Final release of ISA-Tab specification [#]_                      |
+---------+--------------------+------------------------------------------------------------------+
| 1.0RC1  | 2008-11-26         | First release candidate of ISA-Tab specification [#]_            |
+---------+--------------------+------------------------------------------------------------------+

.. [#] Sansone, Susanna-Assunta, Rocca-Serra, Philippe, Gonzalez-Beltran, Alejandra, Johnson, David & ISA Community. (2016, October 28). ISA Model and Serialization Specifications 1.0. Zenodo. http://doi.org/10.5281/zenodo.163640
.. [#] Rocca-Serra, Philippe, Sansone, Susanna-Assunta, & Brandizi, Marco. (2009, January 13). Specification documentation: ISA-TAB 1.0. Zenodo. http://doi.org/10.5281/zenodo.161355
.. [#] Rocca-Serra, Philippe, Sansone, Susanna-Assunta, & Brandizi, Marco. (2008, November 24). Specification documentation: release candidate 1, ISA-TAB 1.0. Zenodo. http://doi.org/10.5281/zenodo.161350
