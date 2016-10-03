==============
ISA-Tab format
==============

:Status: ISA-Tab specification v1.0 (3 October 2016)

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in RFC 2119.

The ISA specifications are licensed under XXXXXXXXX.

------------
Introduction
------------
ISA is a metadata framework for describing experiments in biology and medicine. For a full introduction to the ISA
framework, see www.isa-tools.org

The ISA specifications define an Abstract Model of the metadata framework. The ISA Abstract Model has been implemented
in two format specifications, ISA-Tab and ISA-JSON, both of which have supporting tools and services associated with
them. The format specifications are also available for additional tooling to take advantage of ISA-formatted content.

As a pre-requisite to reading this specification, please make sure you have read and understood the ISA Abstract Model
that the ISA-Tab format is based on.

----------------
Revision History
----------------
+---------+------------+---------------------------------------------------+
| Version | Date       | Description                                       |
+=========+============+===================================================+
| 1.0     | 2016-10-03 | First release of ISA-Tab specification            |
+---------+------------+---------------------------------------------------+
| 1.0RC2  | 2009-01-01 | Second release candidate of ISA-Tab specification |
+---------+------------+---------------------------------------------------+
| 1.0RC1  | 2008-11-26 | First release candidate of ISA-Tab specification  |
+---------+------------+---------------------------------------------------+

Definitions
===========
For detail on ISA framework terminology, please read the ISA Abstract Model specification.

-------------
Specification
-------------

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

Files SHOULD be encoded using UTF-8.

Column delimiters SHOULD be the Unicode Horizontal Tab character (Unicode U+0009).

In order to facilitate identification of ISA-Tab component files, specific naming patterns SHOULD follow:

 - i_*.txt for identifying the Investigation file
 - s_*.txt for identifying Study file(s)
 - a_*.txt for identifying Assay file(s)

All labels are case-sensitive:

 - In the Investigation file, section headers MUST be completely written in upper case (e.g. STUDY), field headers MUST have the first letter of each word in upper case (e.g. Study Identifier); with the exception of the referencing label (REF).
 - In the Study or Assay files, column headers MUST also have the first letter of each word in upper case, with the exception of the referencing label (REF).

Dates SHOULD be supplied in the ISO8601 format "YYYY-MM-DD".

Rows in which the first character in the first column is Unicode U+0023 (the # character) MUST be interpreted as
comments. Reference implementation parsers SHOULD ignore those lines entirely.

All values of cells MAY be enveloped with the Unicode Quotation Mark, Unicode U+0022 (the " character).

Investigation File
==================

The Investigation file fulfils four needs:

#. to declare key entities, such as factors, protocols, which may be referenced in the other files
#. to track provevance of the terminologies (controlled vocabularies or ontologies) there are used, where applicable
#. to relate Assay files to Studies
#. to relate each Study file to an Investigation (this only becomes necessary when two or more Study files need to be grouped).

An Investigation file is structured as a table with vertical headings along the first column, and corresponding values
in the subsequent columns. The following section headings MUST appear in the Investigation file (in order).

 - ONTOLOGY SOURCE REFERENCE
 - INVESTIGATION
 - INVESTIGATION PUBLICATIONS
 - INVESTIGATION CONTACTS
 - STUDY
 - STUDY DESIGN DESCRIPTORS
 - STUDY PUBLICATIONS
 - STUDY FACTORS
 - STUDY ASSAYS
 - STUDY PROTOCOLS
 - STUDY CONTACTS

In the following sections, examples of each section block are given beside the specification of each section. For the
full example of all blocks integrated together, please see here. (TODO: add link to full example)

Ontology Source Reference section
---------------------------------
The Ontology Source section of the Investigation file is used to declare Ontology Sources used elsewhere in the ISA-Tab
files within the context of an Investigation.

Where a row labelled with Term Source REF suffixed in the Investigation
file, the value of the cell SHOULD match one of the Term Source Name value declared in this section.

Where a column labelled with Term Source REF in a Study file or Assay file associated with the Investigation, the value
of the cell SHOULD match one of the Term Source Name value declared in this section.

This section implements a list of Ontology Source from the ISA Abstract Model.

**ONTOLOGY SOURCE REFERENCE**

+-------------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Label                   | Datatype                  | Description                                                                                                                                                                     |
+=========================+===========================+=================================================================================================================================================================================+
| Term Source Name        | String                    | The name of the source of a term; i.e. the source controlled vocabulary or ontology. These names will be used in all corresponding Term Source REF fields that occur elsewhere. |
+-------------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Term Source File        | String (file name or URI) | A file name or a URI of an official resource.                                                                                                                                   |
+-------------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Term Source Version     | String                    | The version number of the Term Source to support terms tracking.                                                                                                                |
+-------------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Term Source Description | String                    | Use for disambiguating resources when homologous prefixes have been used.                                                                                                       |
+-------------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Ontology Source Reference block example:

.. code-block:: none

    ONTOLOGY SOURCE REFERENCE
    Term Source Name
    Term Source File
    Term Source Version
    Term Source Description

Investigation section
---------------------
This section is organized in several subsections, described in detail below. The Investigation section provides a
flexible mechanism for grouping two or more Study files where required. When only one Study is created, the values in
this section SHOULD be left empty and the relevant metadata values recorded in the Study section only.

**INVESTIGATION**

+-----------------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------+
| Label                             | Datatype                                    | Description                                                                                  |
+===================================+=============================================+==============================================================================================+
| Investigation Identifier          | String                                      | A identifier or an accession number provided by a repository. This SHOULD be locally unique. |
+-----------------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------+
| Investigation Title               | String                                      | A concise name given to the investigation.                                                   |
+-----------------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------+
| Investigation Description         | String                                      | A textual description of the investigation.                                                  |
+-----------------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------+
| Investigation Submission Date     | String formatted as ISO8601 date YYYY-MM-DD | The date on which the investigation was reported to the repository.                          |
+-----------------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------+
| Investigation Public Release Date | String formatted as ISO8601 date YYYY-MM-DD | The date on which the investigation was released publicly.                                   |
+-----------------------------------+---------------------------------------------+----------------------------------------------------------------------------------------------+

Investigation block example:

.. code-block:: none

    INVESTIGATION
    Investigation Identifier
    Investigation Title
    Investigation Description
    Investigation Submission Date	2016-02-25
    Investigation Public Release Date	2016-02-25

**INVESTIGATION PUBLICATIONS**

+--------------------------------------------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Label                                                  | Datatype                                                                                           | Description                                                                                                                                                                                |
+========================================================+====================================================================================================+============================================================================================================================================================================================+
| Investigation PubMed ID                                | String formatted as valid PubMed ID                                                                | The PubMed IDs of the described publication(s) associated with this investigation.                                                                                                         |
+--------------------------------------------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Publication DOI                          | String formatted as valid DOI                                                                      | A Digital Object Identifier (DOI) for that publication (where available).                                                                                                                  |
+--------------------------------------------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Publication Author List                  | String                                                                                             | The list of authors associated with that publication.                                                                                                                                      |
+--------------------------------------------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Publication Title                        | String                                                                                             | The title of publication associated with the investigation.                                                                                                                                |
+--------------------------------------------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Publication Status                       | String, or Ontology Annotation by providing accompanying Term Accession Number and Term Source REF | A term describing the status of that publication (i.e. submitted, in preparation, published).                                                                                              |
+--------------------------------------------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Publication Status Term Accession Number | String or URI                                                                                      | The accession number from the Term Source associated with the selected term.                                                                                                               |
+--------------------------------------------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Publication Status Term Source REF       | String                                                                                             | Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match one the Term Source Name declared in the in the Ontology Source Reference section. |
+--------------------------------------------------------+----------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Investigation Publications block example:

.. code-block:: none

    INVESTIGATION PUBLICATIONS
    Investigation PubMed ID
    Investigation Publication DOI
    Investigation Publication Author List
    Investigation Publication Title
    Investigation Publication Status
    Investigation Publication Status Term Accession Number
    Investigation Publication Status Term Source REF

**INVESTIGATION CONTACTS**

+--------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Label                                            | Datatype                                                                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
+==================================================+==============================================================================================+================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
| Investigation Person Last Name                   | String                                                                                       | The last name of a person associated with the investigation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
+--------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Person First Name                  | String                                                                                       | Investigation Person Name                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
+--------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Person Mid Initials                | String                                                                                       | The middle initials of a person associated with the investigation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
+--------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Person Email                       | String formatted as email                                                                    | The email address of a person associated with the investigation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
+--------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Person Phone                       | String                                                                                       | The telephone number of a person associated with the investigation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
+--------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| IInvestigation Person Fax                        | String                                                                                       | The fax number of a person associated with the investigation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
+--------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Person Address                     | String                                                                                       | The address of a person associated with the investigation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
+--------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Person Affiliation                 | String                                                                                       | The organization affiliation for a person associated with the investigation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
+--------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Person Roles                       | String or Ontology Annotation if accompanied by Term Accession Numbers and Term Source REFs  | Term to classify the role(s) performed by this person in the context of the investigation, which means that the roles reported here need not correspond to roles held withing their affiliated organization. Multiple annotations or values attached to one person can be provided by using a semicolon (";") Unicode (U0003+B) as a separator (e.g.: submitter;funder;sponsor) .The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required. |
+--------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Person Roles Term Accession Number | String                                                                                       | The accession number from the Term Source associated with the selected term.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
+--------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Investigation Person Roles Term Source REF       | String                                                                                       | Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match one of the Term Source Names declared in the Ontology Source Reference section.                                                                                                                                                                                                                                                                                                                                                                                        |
+--------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Investigation Contacts block example:

.. code-block:: none

    INVESTIGATION CONTACTS
    Investigation Person Last Name
    Investigation Person First Name
    Investigation Person Mid Initials
    Investigation Person Email
    Investigation Person Phone
    Investigation Person Fax
    Investigation Person Address
    Investigation Person Affiliation
    Investigation Person Roles
    Investigation Person Roles Term Accession Number
    Investigation Person Roles Term Source REF

This section implements an Investigation from the ISA Abstract Model.

Study section
-------------
This section is organized in several subsections, described in detail below. This section also represents a
**repeatable block**, which is replicated according to the number of Studies to report (i.e. two Studies, two Study
blocks are represented in the Investigation file). The subsections in the block are arranged vertically; the intent
being to enhance readability and presentation, and possibly to help with parsing. These subsections MUST remain within
this repeatable block, although their order MAY vary; the fields MUST remain within their subsection.

**STUDY**

:Study Identifier: A unique identifier, either a temporary identifier supplied by users or one generated by a repository or other database. For example, it could be an identifier complying with the LSID specification.
:Study Title: A concise phrase used to encapsulate the purpose and goal of the study.
:Study Description: A textual description of the study, with components such as objective or goals.
:Study Submission Date: The date on which the study is submitted to an archive.
:Study Public Release Date: The date on which the study SHOULD be released publicly.
:Study File Name: A field to specify the name of the Study Table file corresponding the definition of that Study. There can be only one file per cell.

Study block example:

.. code-block:: none

    STUDY
    Study Identifier
    Study Title
    Study Description
    Study Submission Date	2016-02-25
    Study Public Release Date	2016-02-25
    Study File Name

**STUDY DESIGN DESCRIPTORS**

:Study Design Type: A term allowing the classification of the study based on the overall experimental design, e.g cross-over design or parallel group design. The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Study Design Type Term Accession Number: The accession number from the Term Source associated with the selected term.
:Study Design Type Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Study Design Term Source REF has to match one the Term Source Name declared in the Ontology Source Reference section.

Study Design Descriptors block example:

.. code-block:: none

   STUDY DESIGN DESCRIPTORS
   Study Design Type	""
   Study Design Type Term Accession Number	""
   Study Design Type Term Source REF	""

**STUDY PUBLICATIONS**

:Study PubMed ID: The PubMed IDs of the publication(s) associated with this study (where available).
:Study Publication DOI: A Digital Object Identifier (DOI) for this publication (where available).
:Study Publication Author List: The list of authors associated with this publication.
:Study Publication Title: The title of this publication.
:Study Publication Status: A term describing the status of this publication (i.e. submitted, in preparation, published). The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Study Publication Status Term Accession Number: The accession number from the Term Source associated with the selected term.
:Study Publication Status Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match one the Term Source Name declared in the in the Ontology Source Reference section.

Study Publications block example:

.. code-block:: none

    STUDY PUBLICATIONS
    Study PubMed ID
    Study Publication DOI
    Study Publication Author List
    Study Publication Title
    Study Publication Status
    Study Publication Status Term Accession Number
    Study Publication Status Term Source REF

**STUDY FACTORS**

:Study Factor Name: The name of one factor used in the Study and/or Assay files. A factor corresponds to an independent variable manipulated by the experimentalist with the intention to affect biological systems in a way that can be measured by an assay. The value of a factor is given in the Study or Assay file, accordingly. If both Study and Assay have a Factor Value (see section 4.2.5 and 4.3.1.5, respectively), these must be different.
:Study Factor Type: A term allowing the classification of this factor into categories. The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Study Factor Type Term Accession Number: The accession number from the Term Source associated with the selected term.
:Study Factor Type Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match one of the Term Source Name declared in the Ontology Source Reference section.

Study Factors block example:

.. code-block:: none

    STUDY FACTORS
    Study Factor Name
    Study Factor Type
    Study Factor Type Term Accession Number
    Study Factor Type Term Source REF

**STUDY ASSAYS**

The Study Assay section declares and describes each of the Assay files associated with the current Study.

:Study Assay Measurement Type: A term to qualify the endpoint, or what is being measured (e.g. gene expression profiling or protein identification). The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Study Assay Measurement Type Term Accession Number: The accession number from the Term Source associated with the selected term.
:Study Assay Measurement Type Term Source REF: The Source REF has to match one of the Term Source Name declared in the Ontology Source Reference section.
:Study Assay Technology Type: Term to identify the technology used to perform the measurement, e.g. DNA microarray, mass spectrometry. The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Study Assay Technology Type Term Accession Number: The accession number from the Term Source associated with the selected term.
:Study Assay Technology Type Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match one of the Term Source Names declared in the Ontology Source Reference section.
:Study Assay Technology Platform: Manufacturer and platform name, e.g. Bruker AVANCE
:Study Assay File Name: A field to specify the name of the Assay Table file corresponding the definition of that assay. There can be only one file per cell.

.. code-block:: none

   STUDY ASSAYS
   Study Assay File Name	"a_OES2_metabolite_profiling_mass_spectrometry.txt"
   Study Assay Measurement Type	"metabolite profiling"
   Study Assay Measurement Type Term Accession Number	"http://purl.obolibrary.org/obo/OBI_0000366"
   Study Assay Measurement Type Term Source REF	"OBI"
   Study Assay Technology Type	"mass spectrometry"
   Study Assay Technology Type Term Accession Number	"http://purl.obolibrary.org/obo/OBI_0000470"
   Study Assay Technology Type Term Source REF	"OBI"
   Study Assay Technology Platform	""

**STUDY PROTOCOLS**

:Study Protocol Name: The name of the protocols used within the ISA-Tab document. The names are used as identifiers within the ISA-Tab document and will be referenced in the Study and Assay files in the Protocol REF columns. Names can be either local identifiers, unique within the ISA Archive which contains them, or fully qualified external accession numbers.
:Study Protocol Type: Term to classify the protocol. The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Study Protocol Type Term Accession Number: The accession number from the Term Source associated with the selected term.
:Study Protocol Type Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match one of the Term Source Name declared in the Ontology Source Reference section.
:Study Protocol Description: A free-text description of the protocol.
:Study Protocol URI: Pointer to protocol resources external to the ISA-Tab that can be accessed by their Uniform Resource Identifier (URI).
:Study Protocol Version: An identifier for the version to ensure protocol tracking.
:Study Protocol Parameters Name: A semicolon-delimited (";") list of parameter names, used as an identifier within the ISA-Tab document. These names are used in the Study and Assay files (in the "Parameter Value [<parameter name>]" column heading) to list the values used for each protocol parameter. Refer to section Multiple values fields in the Investigation File on how to encode multiple values in one field and match term sources
:Study Protocol Parameters Term Accession Number: The accession number from the Term Source associated with the selected term.
:Study Protocol Parameters Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match one of the Term Source Name declared in the Ontology Source Reference section.
:Study Protocol Components Name: A semicolon-delimited (";") list of a protocol’s components; e.g. instrument names, software names, and reagents names. Refer to section Multiple values fields in the Investigation File on how to encode multiple components in one field and match term sources.
:Study Protocol Components Type: Term to classify the protocol components listed for example, instrument, software, detector or reagent. The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Study Protocol Components Type Term Accession Number: The accession number from the Source associated to the selected terms.
:Study Protocol Components Type Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match a Term Source Name previously declared in the ontology section

.. code-block:: none

   STUDY PROTOCOLS
   Study Protocol Name	"Sample collection"	"Preparation"	"Mass spectrometry"	"Histology"	"Data transformation"	"Metabolite identification"
   Study Protocol Type	"Sample collection"	"Preparation"	"Mass spectrometry"	"Histology"	"Data transformation"	"Metabolite identification"
   Study Protocol Type Term Accession Number	"http://purl.bioontology.org/ontology/CSP/4009-0034"	"http://ncicb.nci.nih.gov/xml/owl/EVS/Thesaurus.owl#C25625"	"http://ncicb.nci.nih.gov/xml/owl/EVS/Thesaurus.owl#C17156"	"http://ncicb.nci.nih.gov/xml/owl/EVS/Thesaurus.owl#C16681"	"http://purl.obolibrary.org/obo/OBI_0200000"	"http://purl.obolibrary.org/obo/MI_2131"
   Study Protocol Type Term Source REF	"CSP"	"NCIT"	"NCIT"	"NCIT"	"OBI"	"MI"
   Study Protocol Description	"" "	"" "	"" "	""	""	""
   Study Protocol URI	""	""	""	""	""	""
   Study Protocol Version	""	""	""	""	""	""
   Study Protocol Parameters Name	""	"Sample mounting;Sample preservation;Sectioning instrument;Section thickness"	"Scan polarity;Mass analyzer;Ion source;Instrument;Scan m/z range;Spatial resolution;Solvent"	"Stain;High-res image;Low-res image"	"Data transformation software;Data transformation software version"	""
   Study Protocol Parameters Name Term Accession Number	""	";;;"	";;;;;;"	";;"	";"	""
   Study Protocol Parameters Name Term Source REF	""	";;;"	";;;;;;"	";;"	";"	""
   Study Protocol Components Name	""	""	""	""	""	""
   Study Protocol Components Type	""	""	""	""	""	""
   Study Protocol Components Type Term Accession Number	""	""	""	""	""	""
   Study Protocol Components Type Term Source REF	""	""	""	""	""	""

**STUDY CONTACTS**

:Study Person Last Name: The last name of a person associated with the study.
:Study Person First Name: The first name of a person associated with the study.
:Study Person Mid Initials: The middle initials of a person associated with the study.
:Study Person Email: The email address of a person associated with the study
:Study Person Phone: The telephone number of a person associated with the study.
:Study Person Fax: The fax number of a person associated with the study.
:Study Person Address: The address of a person associated with the study.
:Study Person Affiliation: The organization affiliation for a person associated with the study.
:Study Person Roles: Term to classify the role(s) performed by this person in the context of the study, which means that the roles reported here need not correspond to roles held withing their affiliated organization. Multiple annotations or values attached to one person may be provided by using a semicolon (";") as a separator, for example: "submitter;funder;sponsor” .The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Study Person Roles Term Accession Number: The accession number from the Term Source associated with the selected term.
:Study Person Roles Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match one of the Term Source Name declared in the Ontology Source Reference section.

.. code-block:: none

   STUDY CONTACTS
   Study Person Last Name
   Study Person First Name
   Study Person Mid Initials
   Study Person Email
   Study Person Phone
   Study Person Fax
   Study Person Address
   Study Person Affiliation
   Study Person Roles
   Study Person Roles Term Accession Number
   Study Person Roles Term Source REF

This section implements the metadata for a Study from the ISA Abstract Model and a list of Assays (i.e. Study and Assay without graphs; graphs are implemented in ISA-Tab as table files).

Study and Assay Table Files
===========================
Study and Assay Table files are structure with fields organized on a per-row basis. The first row MUST be used
for column headers. Generally, objects such as Materials and Processes are indicated with ``<entity> Name``, for example
``Sample Name`` to indicate a sample, or ``Assay Name`` to indicate a named instance of a process that has been applied. Object
properties MUST follow this column, where materials MAY have Characteristics and Processes have MAY have Parameter Values. Both
Characteristics and Parameters MUST be of type string, numeric, or an Ontology Annotation. ``<entity> File`` MAY be used to indicate
a data file node.

Specific types of nodes are specified in the Assay Table file section below.

Ontology Annotations
--------------------
Where a value is an Ontology Annotation in a table file, Term Accession Number and Term Source REF fields MUST
follow the column cell in which the value is entered. For example, a characteristic type Organism with a value of Homo sapiens
can be qualified with an Ontology Annotation of a term from NCBI Taxonomy as follows:

.. code-block:: none

   Characteristics[Organism]  Term Source REF   Term Accession Number
   Homo sapiens   NCBITaxon   http://purl.bioontology.org/ontology/NCBITAXON/9606

Ontology Annotations MAY be applied to any appropriate Characteristic or Parameter Value.

This implements Ontology Annotations from the ISA Abstract Model.

Unit
----
Where a value is numeric, a Unit MAY be used to qualify the quantity. In this case, following the column in which a Unit
is used, a Unit heading MUST be present, and MAY be further annotated as an Ontology Annotation.

For example, to qualify the value 300 with a Unit as an Ontology Annotation:

.. code-block:: none

   Parameter Value[Temperature]  Unit  Term Source REF   Term Accession Number
   300   Kelvin   UO http://purl.obolibrary.org/obo/UO_0000012

Processes
---------
A Process MUST be indicated with the column heading Protocol REF. The value of Protocol REF cells MUST reference
a Protocol declared in the investigation file.

Characteristics
---------------
Characteristics are used as an attribute column following Source Name, Sample Name. This column contains terms describing each material
according to the characteristics category indicated in the column header in the pattern ``Characteristics [<category term>]``.
For example, a column header "Characteristics [organism part]" would contain terms describing an organism part.
Characteristics MAY be used as an attribute column following Source Name, or Sample Name. The
value MUST be free text, numeric, or an Ontology Annotation.

For example, a characteristic type Organism with a value of Homo sapiens
can be qualified with an Ontology Annotation of a term from NCBI Taxonomy as follows:

.. code-block:: none

   Characteristics[Organism]  Term Source REF   Term Accession Number
   Homo sapiens   NCBITaxon   http://purl.bioontology.org/ontology/NCBITAXON/9606

Factor Value
------------
A factor is an independent variable manipulated by an experimentalist with the intention to affect biological systems
in a way that can be measured by an assay. This field holds the actual data for the Factor Value named between the
square brackets (as declared in the Investigation file) so MUST match; for example, Factor Value [compound]. The
value MUST be free text, numeric, or an Ontology Annotation.

.. code-block:: none

   "Factor Value[Gender]"  "Term Source REF"	"Term Accession Number"
   "Male"   "" ""


Study Table file
----------------
The Study file contains contextualizing information for one or more assays, for example; the subjects studied; their
source(s); the sampling methodology; their characteristics; and any treatments or manipulations performed to
prepare the specimens.

In Study files, there are two types of Material nodes implemented: Sources and Samples.

These are linked with a Process node that MUST be of a Protocol that is of a type ``sample collection``.

A Source MUST be indicated with the column heading Source Name.

The protocol referenced MUST be of protocol type ``sample collection``.

A Sample MUST be indicated with the column heading Sample Name.

.. code-block:: none

   "Source Name"	"Characteristics[Organism]"	"Term Source REF"	"Term Accession Number"	"Characteristics[Organism part]"	"Term Source REF"	"Term Accession Number"	"Protocol REF"	"Sample Name"	"Factor Value[Gender]"	"Term Source REF"	"Term Accession Number"	"Factor Value[Metabolic syndrome]"	"Term Source REF"	"Term Accession Number"
   "ADG10003u"	"Homo sapiens"	"NCBITAXON"	"http://purl.bioontology.org/ontology/NCBITAXON/9606"	"urine"	"BTO"	"http://purl.obolibrary.org/obo/BTO_0001419"	"Sample collection"	"ADG10003u_007"	"Male"	""	""	"diabetes mellitus"	""	""
   "ADG10003u"	"Homo sapiens"	"NCBITAXON"	"http://purl.bioontology.org/ontology/NCBITAXON/9606"	"urine"	"BTO"	"http://purl.obolibrary.org/obo/BTO_0001419"	"Sample collection"	"ADG10003u_008"	"Male"	""	""	"diabetes mellitus"	""	""


The Study Table file implements the Study graphs from the ISA Abstract Model.

Assay Table file
----------------
The Assay file represents a portion of the experimental graph (i.e., one part of the overall
structure of the workflow); each Assay file must contain assays of the same type, defined by the type of
measurement (i.e. gene expression) and the technology employed (i.e. DNA microarray). Assay-related information
includes protocols, additional information relating to the execution of those protocols and references to data
files (whether raw or derived).

A Sample MUST be provided as the first node in the experimental graph, indicated with the column heading Sample Name.

Extract Name MUST be used as an identifier for a Extract Material node within an Assay file. This column contains user-defined names
for each portion of extracted material. Extracts MAY be qualified with Characteristics, Material Type and Description.

Labeled Extract Name MUST be used as an identifier for a Labeled Extract Material node within an Assay file. Labeled Extracts
MAY be qualified with Label, Characteristics, Material Type, Description.

Assay Name MUST be used is used as an identifier for user-defined names for each assay. Assays MAY be qualified with an Assay
Name, Performer and Date.

Image File, Raw Data File or Derived Data File column heading MUST correspond to a relevant Data node to provide names or URIs of
file locations. For submission or transfer, files MAY be packed with ISA-Tab files.

Data Transformation Name MUST be used as an identifier for a user-defined name for each data transformation Process applied.

Normalization Name MUST be used as an identifier for a user-defined name for each normalization Process applied.

Assay Table files SHOULD be validated against a Configuration (see below).

.. code-block:: none

   "Sample Name"	"Protocol REF"	"Parameter Value[Extraction Method]"	"Extract Name"	"Protocol REF"	"Parameter Value[NMR tube type]"	"Term Source REF"	"Term Accession Number"	"Parameter Value[Solvent]"	"Term Source REF"	"Term Accession Number"	"Parameter Value[Sample pH]"	"Parameter Value[Temperature]"	"Unit"	"Term Source REF"	"Term Accession Number"	"Labeled Extract Name"	"Label"	"Term Source REF"	"Term Accession Number"	"Protocol REF"	"Parameter Value[Instrument]"	"Term Source REF"	"Term Accession Number"	"Parameter Value[NMR Probe]"	"Term Source REF"	"Term Accession Number"	"Parameter Value[Number of transients]"	"Parameter Value[Pulse sequence name]"	"Parameter Value[Magnetic field strength]"	"Unit"	"Term Source REF"	"Term Accession Number"	"Acquisition Parameter Data File"	"Protocol REF"	"NMR Assay Name"	"Free Induction Decay Data File"	"Protocol REF"	"Normalization Name"	"Derived Spectral Data File"	"Protocol REF"	"Data Transformation Name"	"Metabolite Assignment File"
   "ADG10003u_007"	"Extraction"	"N/A"	"N/A"	"NMR sample"	"5 mm standard"	""	""	"0.2 M phosphate buffered D2O"	""	""	"7.4"	"300"	"kelvin"	"UO"	"http://purl.obolibrary.org/obo/UO_0000012"	"N/A"	"hydrogen molecular entity"	"CHEBI"	"http://purl.obolibrary.org/obo/CHEBI_33608"	"NMR spectroscopy"	"Bruker AVANCE DRX 700 MHz spectrometer"	""	""	"5 mm TXI ATMA"	""	""	"128"	"1D NOESY with presaturation (noesypr1d)"	"16.4"	"tesla"	"UO"	"http://purl.obolibrary.org/obo/UO_0000228"	"ADG_acquisition_data.xlsx"	"NMR assay"	"ADG10003u_007"	"ADG10003u_007.zip"	"Data transformation"	"ADG_normalized_data.xlsx"	""	"Metabolite identification"	"ADG_transformed_data.xlsx"	"m_mtbls1_metabolite_profiling_NMR_spectroscopy_v2_maf.tsv"
   "ADG10003u_008"	"Extraction"	"N/A"	"N/A"	"NMR sample"	"5 mm standard"	""	""	"0.2 M phosphate buffered D2O"	""	""	"7.4"	"300"	"kelvin"	"UO"	"http://purl.obolibrary.org/obo/UO_0000012"	"N/A"	"hydrogen molecular entity"	"CHEBI"	"http://purl.obolibrary.org/obo/CHEBI_33608"	"NMR spectroscopy"	"Bruker AVANCE DRX 700 MHz spectrometer"	""	""	"5 mm TXI ATMA"	""	""	"128"	"1D NOESY with presaturation (noesypr1d)"	"16.4"	"tesla"	"UO"	"http://purl.obolibrary.org/obo/UO_0000228"	"ADG_acquisition_data.xlsx"	"NMR assay"	"ADG10003u_008"	"ADG10003u_008.zip"	"Data transformation"	"ADG_normalized_data.xlsx"	""	"Metabolite identification"	"ADG_transformed_data.xlsx"	"m_mtbls1_metabolite_profiling_NMR_spectroscopy_v2_maf.tsv"


The Assay Table file implements the Assay graphs from the ISA Abstract Model.

Configurations
--------------
Configurations for ISA-Tab content are implemented in XML files.

XML Configurations MUST declare the measurement and technology type of context, and MUST declare the valid column
names and ordering that are required. An XML schema describing the configuration format is available from
https://github.com/ISA-tools/isa-api/blob/master/isatools/schemas/isatab_configurator.xsd To view example configurations,
please see here: https://github.com/ISA-tools/isa-api/tree/master/isatools/config/xml

Data Files
----------
ISA-Tab focuses on structuring experimental metadata; raw and derived data files are considered as external files.
The Assay file can refer to one or more of these external data files. For guidelines on how to
format these data files, users should refer to the relevant standards group or reference
repository.

For submission or transfer, ISA-Tab files and associated data files MAY be packaged into an ISArchive, a zip file
containing all the files together.