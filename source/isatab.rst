==============
ISA-Tab format
==============

.. Important:: As a pre-requisite to reading this specification, please make sure you have read and understood the :doc:`ISA Abstract Model </isamodel>` that the ISA-Tab format is based on.

For detail on ISA framework terminology, please read the :doc:`ISA Abstract Model specification </isamodel>`.

This document describes the ISA Abstract Model reference implementation specified in the ISA-Tab format. ISA-Tab files
are `tab separated value <https://en.wikipedia.org/wiki/Tab-separated_values>`_ (tsv) files, with specific labeled
column structures specified below.

Below we provide the schemas and the content rules for valid ISA-Tab documents. Full examples of ISA content as
ISA-Tab can be found in the test data package of the ISA API, here https://git.io/vPZdE We recommend that you study
these to better understand the structure of ISA-Tab documents.

Format
======
ISA-Tab uses three types of file to capture the experimental metadata:
 - Investigation file
 - Study file
 - Assay file (with associated data files)

The Investigation file contains all the information needed to understand the overall goals and means used in an
experiment; experimental steps (or sequences of events) are described in the Study and in the Assay file(s). For each
Investigation file there may be one or more Studies defined with a corresponding Study file; for each Study there may
be one or more Assays defined with corresponding Assay files.

Files SHOULD be encoded using `UTF-8 <http://www.fileformat.info/info/unicode/utf8.htm>`_.

Column delimiters SHOULD be the Unicode Horizontal Tab character (Unicode `U+0009 <http://www.fileformat.info/info/unicode/char/0009/index.htm>`_,).

In order to facilitate identification of ISA-Tab component files, specific naming patterns SHOULD follow:

 - ``i_*.txt`` for identifying the Investigation file, e.g. ``i_investigation.txt``
 - ``s_*.txt`` for identifying Study file(s), e.g. ``s_gene_survey.txt``
 - ``a_*.txt`` for identifying Assay file(s), e.g. ``a_transcription.txt``

All labels are case-sensitive:

 - In the Investigation file, section headers MUST be completely written in upper case (e.g. STUDY), field headers MUST have the first letter of each word in upper case (e.g. Study Identifier); with the exception of the referencing label (REF).
 - In the Study and Assay files, column headers MUST also have the first letter of each word in upper case, with the exception of the referencing label (REF).

Dates SHOULD be supplied in the `ISO8601 <http://www.iso.org/iso/home/standards/iso8601.htm>`_ format ``YYYY-MM-DD``.

All values of cells MAY be enveloped with the Unicode Quotation Mark, Unicode
`U+0022 <http://www.fileformat.info/info/unicode/char/0022/index.htm>`_  (the " character).

For maximal portability file names should only contain only ASCII characters not excluded
already (that is ``A-Za-z0-9._!#$%&+,;=@^(){}'[]`` - we exclude space as many utilities
do not accept spaces in file paths): non-English alphabetic characters cannot be guaranteed
to be supported in all locales. It would be good practice to avoid the shell metacharacters
``(){}'[]$."``.

Investigation File
==================

The Investigation file fulfils four needs:

#. to declare key entities, such as factors, protocols, which may be referenced in the other files
#. to track provevance of the terminologies (controlled vocabularies or ontologies) there are used, where applicable
#. to relate Assay files to Studies
#. to relate each Study file to an Investigation (this only becomes necessary when two or more Study files need to be grouped).

An Investigation file is structured as a table with vertical headings along the first column, and corresponding values
in the subsequent columns. The following section headings MUST appear in the Investigation file (in order).

 - ``ONTOLOGY SOURCE REFERENCE``
 - ``INVESTIGATION``
 - ``INVESTIGATION PUBLICATIONS``
 - ``INVESTIGATION CONTACTS``
 - ``STUDY``
 - ``STUDY DESIGN DESCRIPTORS``
 - ``STUDY PUBLICATIONS``
 - ``STUDY FACTORS``
 - ``STUDY ASSAYS``
 - ``STUDY PROTOCOLS``
 - ``STUDY CONTACTS``

In the following sections, examples of each section block are given beside the specification of each section.

For a full example of a complete Investigation File, please see https://git.io/vPZbG.

.. attention::
    Rows in which the first character in the first column is Unicode
    `U+0023 <http://www.fileformat.info/info/unicode/char/0023/index.htm>`_  (the # character) MUST be interpreted as
    comments, where reference implementation parsers SHOULD ignore those lines entirely.

    Rows where the label ``Comment[<comment name>]`` appear can also appear within any of the section blocks. Where
    these appear, the comment name must be unique within the context of a single block (e.g. you cannot have multiple
    occurences of ``Comment[external DB REF]`` within ``STUDY ASSAYS``. Also, the value cells MUST match the number of
    values indicated by the rest of the section in context.

Ontology Source Reference section
---------------------------------
The Ontology Source section of the Investigation file is used to declare Ontology Sources used elsewhere in the ISA-Tab
files within the context of an Investigation.

Where a row labelled with ``Term Source REF`` suffixed in the Investigation
file, the value of the cell SHOULD match one of the ``Term Source Name`` value declared in this section.

Where a column labelled with ``Term Source REF`` in a Study file or Assay file associated with the Investigation, the value
of the cell SHOULD match one of the ``Term Source Name`` value declared in this section.

This section implements a list of ``Ontology Source`` from the ISA Abstract Model.

This section MUST contain zero or more values.

**ONTOLOGY SOURCE REFERENCE**

This section MUST contain the following labels, with the specified datatypes for values supported:

.. csv-table::
    :file: _static/isatab/ontology_source_reference.csv
    :header-rows: 1
    :widths: 20, 20, 60

For example, the ``ONTOLOGY SOURCE REFERENCE`` section of an ISA-Tab ``i_*.txt`` file may look as follows:

.. literalinclude:: _static/isatab/i_gilbert.txt
    :lines: 1-5

Investigation section
---------------------
This section is organized in several subsections, described in detail below. The Investigation section provides a
flexible mechanism for grouping two or more Study files where required. When only one Study is created, the values in
this section SHOULD be left empty and the relevant metadata values recorded in the Study section only.

These sections implement an ``Investigation`` from the ISA Abstract Model.

**INVESTIGATION**

This section MUST contain zero or one values.

This section MUST contain the following labels, with the specified datatypes for values supported:

.. csv-table::
    :file: _static/isatab/investigation.csv
    :header-rows: 1
    :widths: 20, 20, 60

For example, the ``INVESTIGATION`` section of an ISA-Tab ``i_*.txt`` file may look as follows:

.. literalinclude:: _static/isatab/i_investigation.txt
    :lines: 6-11

**INVESTIGATION PUBLICATIONS**

This section MUST contain zero or more values.

This section MUST contain the following labels, with the specified datatypes for values supported:

.. csv-table::
    :file: _static/isatab/investigation_publications.csv
    :header-rows: 1
    :widths: 20, 20, 60

For example, the ``INVESTIGATION PUBLICATIONS`` section of an ISA-Tab ``i_*.txt`` file may look as follows:

.. literalinclude:: _static/isatab/i_investigation.txt
    :lines: 14-21

**INVESTIGATION CONTACTS**

This section MUST contain zero or more values.

This section MUST contain the following labels, with the specified datatypes for values supported:

.. csv-table::
    :file: _static/isatab/investigation_contacts.csv
    :header-rows: 1
    :widths: 20, 20, 60

For example, the ``INVESTIGATION CONTACTS`` section of an ISA-Tab ``i_*.txt`` file may look as follows:

.. literalinclude:: _static/isatab/i_investigation.txt
    :lines: 22-33

Study section
-------------
This section is organized in several subsections, described in detail below. This section also represents a
**repeatable block**, which is replicated according to the number of Studies to report (i.e. two Studies, two Study
blocks are represented in the Investigation file). The subsections in the block are arranged vertically; the intent
being to enhance readability and presentation, and possibly to help with parsing. These subsections MUST remain within
this repeatable block, although their order MAY vary; the fields MUST remain within their subsection.

These sections implement the metadata for a ``Study`` from the ISA Abstract Model and a list of ``Assay`` (i.e. ``Study`` and
``Assay`` **without** graphs; graphs are implemented in ISA-Tab as table files).

**STUDY**

This section MUST contain zero or one values.

This section MUST contain the following labels, with the specified datatypes for values supported:

.. csv-table::
    :file: _static/isatab/study.csv
    :header-rows: 1
    :widths: 20, 20, 60

For example, the ``STUDY`` section of an ISA-Tab ``i_*.txt`` file may look as follows:

.. literalinclude:: _static/isatab/i_gilbert.txt
    :lines: 35-40

**STUDY DESIGN DESCRIPTORS**

This section MUST contain zero or more values.

This section MUST contain the following labels, with the specified datatypes for values supported:

.. csv-table::
    :file: _static/isatab/study_design_descriptors.csv
    :header-rows: 1
    :widths: 20, 20, 60

For example, the ``STUDY DESIGN DESCRIPTORS`` section of an ISA-Tab ``i_*.txt`` file may look as follows:

.. literalinclude:: _static/isatab/i_gilbert.txt
    :lines: 48-51

**STUDY PUBLICATIONS**

This section MUST contain zero or more values.

This section MUST contain the following labels, with the specified datatypes for values supported:

.. csv-table::
    :file: _static/isatab/study_publications.csv
    :header-rows: 1
    :widths: 20, 20, 60

For example, the ``STUDY PUBLICATIONS`` section of an ISA-Tab ``i_*.txt`` file may look as follows:

.. literalinclude:: _static/isatab/i_gilbert.txt
    :lines: 52-59

**STUDY FACTORS**

This section MUST contain zero or more values.

This section MUST contain the following labels, with the specified datatypes for values supported:

.. csv-table::
    :file: _static/isatab/study_factors.csv
    :header-rows: 1
    :widths: 20, 20, 60

For example, the ``STUDY FACTORS`` section of an ISA-Tab ``i_*.txt`` file may look as follows:

.. literalinclude:: _static/isatab/i_gilbert.txt
    :lines: 60-64

**STUDY ASSAYS**

This section MUST contain zero or more values.

This section MUST contain the following labels, with the specified datatypes for values supported:

.. csv-table::
    :file: _static/isatab/study_assays.csv
    :header-rows: 1
    :widths: 20, 20, 60

For example, the ``STUDY ASSAYS`` section of an ISA-Tab ``i_*.txt`` file may look as follows:

.. literalinclude:: _static/isatab/i_gilbert.txt
    :lines: 65-73


**STUDY PROTOCOLS**

This section MUST contain zero or more values.

This section MUST contain the following labels, with the specified datatypes for values supported:

.. csv-table::
    :file: _static/isatab/study_protocols.csv
    :header-rows: 1
    :widths: 20, 20, 60

For example, the ``STUDY PROTOCOLS`` section of an ISA-Tab ``i_*.txt`` file may look as follows:

.. literalinclude:: _static/isatab/i_gilbert.txt
    :lines: 74-88

**STUDY CONTACTS**

This section MUST contain zero or more values.

This section MUST contain the following labels, with the specified datatypes for values supported:

.. csv-table::
    :file: _static/isatab/study_contacts.csv
    :header-rows: 1
    :widths: 20, 20, 60

For example, the ``STUDY CONTACTS`` section of an ISA-Tab ``i_*.txt`` file may look as follows:

.. literalinclude:: _static/isatab/i_gilbert.txt
    :lines: 90-100

Study and Assay files
=====================
``Study`` and ``Assay`` Table files are structure with fields organized on a per-row basis. The first row MUST be used
for column headers. Generally, objects such as Materials and Processes are indicated with ``<entity> Name``, for example
``Sample Name`` to indicate a sample, or ``Assay Name`` to indicate a named instance of a process that has been applied. Object
properties MUST follow this column, where materials MAY have Characteristics and Processes have MAY have Parameter Values. Both
``Characteristics`` and ``Parameter Values`` MUST be of type string, numeric, or an ``Ontology Annotation``. ``<entity> File`` MAY be used to indicate
a data file node.

.. attention::
    Comments are also allowed in Study and Assay files, in a similar fashion to how they are used in the Investigation
    file. Columns headed with ``Comment[<comment name>]`` MAY appear after any named node in the Study and Assay files
    (e.g. if ``Comment[ORCID ID]`` appears **after** the ``Source Name`` column, we know that the comment regarding
    ``ORCID ID`` applies to the relevant Source node based on the row.

Specific types of nodes are specified in the Assay Table file section below.

Ontology Annotations
--------------------
Where a value is an ``Ontology Annotation`` in a table file, ``Term Accession Number`` and ``Term Source REF`` fields MUST
follow the column cell in which the value is entered. For example, a characteristic type ``Organism`` with a value of ``Homo sapiens``
can be qualified with an ``Ontology Annotation`` of a term from NCBI Taxonomy as follows:

+---------------------------+-----------------+---------------------------+
| Characteristics[Organism] | Term Source REF |  Term Accession Number    |
+===========================+=================+===========================+
| Homo sapiens              | NCBITaxon       | http://.../NCBITAXON/9606 |
+---------------------------+-----------------+---------------------------+

An ``Ontology Annotation`` MAY be applied to any appropriate ``Characteristics`` or ``Parameter Value``.

This implements ``Ontology Annotation`` from the ISA Abstract Model.

Unit
----
Where a value is numeric, a ``Unit`` MAY be used to qualify the quantity. In this case, following the column in which a ``Unit``
is used, a ``Unit`` heading MUST be present, and MAY be further annotated as an ``Ontology Annotation``.

For example, to qualify the value ``300`` with a ``Unit`` ``Kelvin`` qualified as an ``Ontology Annotation`` from the Units Ontology declared
in the Ontology Sources with ``UO``:

+------------------------------+--------+-----------------+----------------------------+
| Parameter Value[Temperature] | Unit   | Term Source REF | Term Accession Number      |
+==============================+========+=================+============================+
| 300                          | Kelvin | UO              | http://.../obo/UO_0000012  |
+------------------------------+--------+-----------------+----------------------------+

Processes
---------
A ``Process`` MUST be indicated with the column heading ``Protocol REF``. The value of ``Protocol REF`` cells MUST reference
a ``Protocol`` declared in the investigation file.

Characteristics
---------------
``Characteristics`` are used as an attribute column following ``Source Name``, ``Sample Name``. This column contains terms describing each material
according to the characteristics category indicated in the column header in the pattern ``Characteristics [<category term>]``.
For example, a column header ``Characteristics [organ part]`` would contain terms describing an organ part.
``Characteristics`` SHOULD be used as an attribute column following ``Source Name``, or ``Sample Name``. The
value MUST be free text, numeric, or an ``Ontology Annotation``.

For example, a characteristic type Organism with a value of Homo sapiens
can be qualified with an Ontology Annotation of a term from NCBI Taxonomy as follows:

+-----------------------------+-----------------+---------------------------+
| Characteristics[organ part] | Term Source REF |  Term Accession Number    |
+=============================+=================+===========================+
| Liver                       | MeSH            | D008099                   |
+-----------------------------+-----------------+---------------------------+

Factor Value
------------
A factor is an independent variable manipulated by an experimentalist with the intention to affect biological systems
in a way that can be measured by an assay. This field holds the actual data for the ``Factor Value`` named between the
square brackets (as declared in the Investigation file) so MUST match; for example, ``Factor Value [compound]``. The
value MUST be free text, numeric, or an ``Ontology Annotation``.

+----------------------+-----------------+-----------------------+
| Factor Value[Gender] | Term Source REF | Term Accession Number |
+======================+=================+=======================+
| Male                 | MeSH            | D008297               |
+----------------------+-----------------+-----------------------+


Study Table file
----------------
The ``Study`` file contains contextualizing information for one or more assays, for example; the subjects studied; their
source(s); the sampling methodology; their characteristics; and any treatments or manipulations performed to
prepare the specimens.

For a full example of a complete Study Table file, please see https://git.io/vPZbF

Study Table files SHOULD have file names corresponding to the pattern ``s_*.txt``, e.g. ``s_Study01.txt``

In Study files, there are two types of ``Material`` nodes implemented: ``Source`` and ``Sample``.

These are linked with a Process node that MUST be of a Protocol that is of a type ``sample collection``.

A ``Source`` MUST be indicated with the column heading ``Source Name``.

The protocol referenced MUST be of protocol type ``sample collection``.

A ``Sample`` MUST be indicated with the column heading ``Sample Name``.

For example, a simple source to sample may be represented as:

+-------------+-------------------+-------------+
| Source Name | Protocol REF      | Sample Name |
+=============+===================+=============+
| source1     | sample collection | sample1     |
+-------------+-------------------+-------------+

Where a graph splits or pools, we use the ``Name`` column to represent the same nodes.

For example, if we split a source into two samples, we  might represent this as:

+-------------+-------------------+-------------+
| Source Name | Protocol REF      | Sample Name |
+=============+===================+=============+
| source1     | sample collection | sample1     |
+-------------+-------------------+-------------+
| source1     | sample collection | sample2     |
+-------------+-------------------+-------------+

If we pool two sources into a single sample, we might represent this as:

+-------------+-------------------+-------------+
| Source Name | Protocol REF      | Sample Name |
+=============+===================+=============+
| source1     | sample collection | sample1     |
+-------------+-------------------+-------------+
| source2     | sample collection | sample1     |
+-------------+-------------------+-------------+

Node properties, such as ``Characteristics`` (for ``Material`` nodes), ``Parameter Value`` (for ``Process`` nodes) and additional
``Name`` columns for special cases of ``Process`` node to disambiguate ``Protocol REF`` entries of MUST follow the named node of context.

For example,

.. literalinclude:: _static/isatab/s_BII-S-2.txt

The Study Table file implements the Study graphs from the ISA Abstract Model.

Assay Table file
----------------
The ``Assay`` file represents a portion of the experimental graph (i.e., one part of the overall
structure of the workflow); each ``Assay`` file must contain assays of the same type, defined by the type of
measurement (e.g. gene expression) and the technology employed (e.g. DNA microarray). Assay-related information
includes protocols, additional information relating to the execution of those protocols and references to data
files (whether raw or derived).

For a full example of a complete Assay Table file, please see https://git.io/vPZbh

Assay Table files SHOULD have file names corresponding to the pattern ``a_*.txt``, e.g. ``a_Assay01.txt``

A ``Sample`` MUST be provided as the first node in the experimental graph, indicated with the column heading ``Sample Name``.

``Extract Name`` MUST be used as an identifier for a Extract Material node within an ``Assay`` file. This column contains user-defined names
for each portion of extracted material. Extracts MAY be qualified with ``Characteristics``, ``Material Type`` and ``Description``.

``Labeled Extract`` Name MUST be used as an identifier for a Labeled Extract Material node within an ``Assay`` file. Labeled Extracts
MAY be qualified with ``Label``, ``Characteristics``, ``Material Type``, ``Description``.

``Assay Name`` MUST be used is used as an identifier for user-defined names for each assay. Assays MAY be qualified with an ``Assay
Name``, ``Performer`` and ``Date``.

``Image File``, ``Raw Data File`` or ``Derived Data File`` column heading MUST correspond to a relevant ``Data`` node to provide names or URIs of
file locations. For submission or transfer, files MAY be packed with ISA-Tab files.

``Data Transformation Name`` MUST be used as an identifier for a user-defined name for each data transformation ``Process`` applied.

``Normalization Name`` MUST be used as an identifier for a user-defined name for each normalization ``Process`` applied.

Splitting and pooling is allowed as per the examples given in Study Table file.

For example,

.. literalinclude:: _static/isatab/a_gilbert-assay-Gx.txt

The Assay Table file implements the ``Assay`` graphs from the ISA Abstract Model.

Data Files
----------
ISA-Tab focuses on structuring experimental metadata; raw and derived data files are considered as external files.
The Assay file can refer to one or more of these external data files. For guidelines on how to
format these data files, users should refer to the relevant standards group or reference
repository.

For submission or transfer, ISA-Tab files and associated data files MAY be packaged into an ISArchive, a zip file
containing all the files together.