
Reference Implementations
=========================

:Status: ISA Model and Serialization Specifications 1.0 (6 October 2016)

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described by `RFC 2119 <http://www.ietf.org/rfc/rfc2119.txt>`_.

The ISA Model and Serialization Specifications are licensed under `CC BY-SA 4.0 <https://creativecommons.org/licenses/by-sa/4.0/>`_.

The ISA Model and Serialization Specifications are maintained by Susanna-Assunta Sansone [1]_, Philippe Rocca-Serra [1]_, Alejandra
Gonzalez-Beltran [1]_ and David Johnson [1]_ on behalf of the `ISA Community <http://www.isacommons.org>`_.

If you wish to make comments regarding this specification, please report using the
`ISA Specifications issue tracker <https://github.com/ISA-tools/isa-specifications/issues>`_ or send them to
isatools@googlegroups.com. All comments are welcome.

The ISA Model and Serialization Specifications have several Reference Implementations as data formats (ISA-Tab and
ISA JSON) with supporting software tools. Below is a brief list of tools and supported formats.

+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| Tool                          | Description                                                                                                                                                | Format            | Development Status   | Platform                   |
+===============================+============================================================================================================================================================+===================+======================+============================+
| ISA API                       | Python API for ISA conversions, validation and content creation                                                                                            | ISA-Tab, ISA-JSON | Active (pre-release) | Python 3+                  |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| linkedISA                     | Convert ISA-Tab to OWL                                                                                                                                     | ISA-Tab           | Active               | Java 1.6                   |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| OntoMaton                     | Annotation of ISA-Tab spreadsheets                                                                                                                         | ISA-Tab           | Active               | Google Spreadsheets Add-on |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| rISA                          | Parse ISA-Tab into R data structures                                                                                                                       | ISA-Tab           | Active               | R/Bioconductor             |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| biopy-isatab                  | Python Parser for ISA-Tab                                                                                                                                  | ISA-Tab           | Active               | Python 2.7+                |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| ISA creator                   | Used for creating ISA-Tab files                                                                                                                            | ISA-Tab           | Maintenance mode     | Java 1.6                   |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| ISA-Tab Viewer                | Visualizer for ISA-Tabs (browser)                                                                                                                          | ISA-Tab           | Maintenance mode     | JavaScript / HTML / CSS    |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| ISA configurator              | Used with ISAcreator to develop ISA-Tab XML Configurations that are used as ISA-Tab templates and used for validating against domain-specific requirements | ISA-Tab           | Maintenance mode     | Java 1.6                   |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| ISA validator                 | Used with ISA XML Configurations to validate ISA-Tab files against domain-specific requirements                                                            | ISA-Tab           | Maintenance mode     | Java 1.6                   |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| ISA converter                 | Convert ISA-Tab files into other formats                                                                                                                   | ISA-Tab           | Maintenance mode     | Java 1.6                   |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| ISA to RDF                    | Convert from ISA-Tab to RDF                                                                                                                                | ISA-Tab           | Maintenance mode     | Java 1.6                   |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| MAGE to ISA converter         | Converter which can pull from ArrayExpress (by an accession number) or read local files and convert them to ISAtab.                                        | ISA-Tab           | Maintenance mode     | Java 1.6                   |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| BII (Bio Investigation Index) | Web application and DB                                                                                                                                     | ISA-Tab           | Maintenance mode     | Java 1.6                   |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+
| Bio-Parser-ISATab             | PERL Parser for ISA-Tab                                                                                                                                    | ISA-Tab           | Unsupported          | PERL                       |
+-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+----------------------+----------------------------+

For further information on the software tools supporting ISA, please visit www.isa-tools.org and www.github.com/ISA-tools

.. [1] Oxford e-Research Centre, University of Oxford, UK.