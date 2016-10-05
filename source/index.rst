ISA Model and Serialization Specifications
==========================================

:Status: ISA Model and Serialization Specifications 1.0 (6 October 2016)

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in RFC 2119.

The ISA Model and Serialization Specifications are licensed under CC BY-SA 4.0.

The ISA Model and Serialization Specifications are maintained by Susanna-Assunta Sansone, Philippe Rocca-Sera, Alejandra
Gonzalez-Beltran and David Johnson on behalf of the ISA Community.

If you wish to make comments regarding this specification, please report using the ISA Specifications issue tracker or
send them to isatools@googlegroups.com. All comments are welcome.

------------
Introduction
------------
ISA is a metadata framework to manage an
increasingly diverse set of life science, environmental and biomedical experiments that employing one or a
combination of technologies. Built around the 'Investigation' (the project context), 'Study' (a unit of research)
and 'Assay' (analytical measurements) abstract data model, ISA helps you to provide rich
descriptions of experimental metadata (i.e. sample characteristics, technology and measurement types, sample-to-data
relationships) so that the resulting data and discoveries are reproducible and reusable. For a full introduction to the ISA
framework, see www.isa-tools.org

The ISA specifications define an Abstract Model of the metadata framework. The ISA Abstract Model has been implemented
in two format specifications, ISA-Tab and ISA-JSON, both of which have supporting tools and services associated with
them. The format specifications are also available for additional tooling to take advantage of ISA-formatted content.


.. _ISA-tools.org: http://www.isa-tools.org
.. _ISA metadata framework: http://www.isa-tools.org

----------------
Revision History
----------------
+---------+----------------+-------------------------------------------------------------+
| Version | Date           | Description                                                 |
+=========+================+=============================================================+
| 1.0     | 2016-10-06     | Final release of ISA Model and Serializations specification |
+---------+----------------+-------------------------------------------------------------+
| 1.0RC2  | 2009-01-01     | Second release candidate of ISA-Tab specification           |
+---------+----------------+-------------------------------------------------------------+
| 1.0RC1  | 2008-11-26     | First release candidate of ISA-Tab specification            |
+---------+----------------+-------------------------------------------------------------+

.. toctree::
   :maxdepth: 2
   :titlesonly:

   ISA Abstract Model <isamodel>
   ISA JSON format <isajson>
   ISA-Tab format <isatab>
   Reference Implementations <implementations>
   Contributors <contributors>

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

