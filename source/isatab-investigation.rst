==================
Investigation file
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

Ontology Source Reference section
=================================
The Ontology Source section of the Investigation file is used to declare Ontology Sources used elsewhere in the ISA-Tab
files within the context of an Investigation.

Where a row labelled with Term Source REF suffixed in the Investigation
file, the value of the cell SHOULD match one of the Term Source Name value declared in this section.

Where a column labelled with Term Source REF in a Study file or Assay file associated with the Investigation, the value
of the cell SHOULD match one of the Term Source Name value declared in this section.

**ONTOLOGY SOURCE REFERENCE**

:Term Source Name: The name of the source of a term; i.e. the source controlled vocabulary or ontology. These names will be used in all corresponding Term Source REF fields that occur elsewhere.
:Term Source File: A file name or a URI of an official resource.
:Term Source Version: The version number of the Term Source to support terms tracking.
:Term Source Description: Use for disambiguating resources when homologous prefixes have been used.

Investigation section
=====================
This section is organized in several subsections, described in detail below. The Investigation section provides a
flexible mechanism for grouping two or more Study files where required. When only one Study is created, the values in
this section SHOULD be left empty and the relevant metadata values recorded in the Study section only.

**INVESTIGATION**

:Investigation Identifier: A identifier or an accession number provided by a repository. This SHOULD be locally unique.
:Investigation Title: A concise name given to the investigation.
:Investigation Description: A textual description of the investigation.
:Investigation Submission Date: The date on which the investigation was reported to the repository.
:Investigation Public Release Date: The date on which the investigation was released publicly.

**INVESTIGATION PUBLICATIONS**

:Investigation PubMed ID: The PubMed IDs of the described publication(s) associated with this investigation.
:Investigation Publication DOI: A Digital Object Identifier (DOI) for that publication (where available).
:Investigation Publication Author List: The list of authors associated with that publication.
:Investigation Publication Title: The title of publication associated with the investigation.
:Investigation Publication Status: A term describing the status of that publication (i.e. submitted, in preparation, published).
:Investigation Publication Status Term Accession Number: The accession number from the Term Source associated with the selected term.
:Investigation Publication Status Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match one the Term Source Name declared in the in the Ontology Source Reference section.

**INVESTIGATION CONTACTS**

:Investigation Person Last Name: The last name of a person associated with the investigation.
:Investigation Person First Name: The first name of a person associated with the investigation.
:Investigation Person Mid Initials: The middle initials of a person associated with the investigation.
:Investigation Person Email: The email address of a person associated with the investigation.
:Investigation Person Phone: The telephone number of a person associated with the investigation.
:Investigation Person Fax: The fax number of a person associated with the investigation.
:Investigation Person Address: The address of a person associated with the investigation.
:Investigation Person Affiliation: The organization affiliation for a person associated with the investigation.
:Investigation Person Roles: Term to classify the role(s) performed by this person in the context of the investigation, which means that the roles reported here need not correspond to roles held withing their affiliated organization. Multiple annotations or values attached to one person can be provided by using a semicolon (";") Unicode (U0003+B) as a separator (e.g.: submitter;funder;sponsor) .The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Investigation Person Roles Term Accession Number: The accession number from the Term Source associated with the selected term.
:Investigation Person Roles Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match one of the Term Source Names declared in the Ontology Source Reference section.

Study section
=============
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

**STUDY DESIGN DESCRIPTORS**

:Study Design Type: A term allowing the classification of the study based on the overall experimental design, e.g cross-over design or parallel group design. The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Study Design Type Term Accession Number: The accession number from the Term Source associated with the selected term.
:Study Design Type Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Study Design Term Source REF has to match one the Term Source Name declared in the Ontology Source Reference section.

**STUDY PUBLICATIONS**

:Study PubMed ID: The PubMed IDs of the publication(s) associated with this study (where available).
:Study Publication DOI: A Digital Object Identifier (DOI) for this publication (where available).
:Study Publication Author List: The list of authors associated with this publication.
:Study Publication Title: The title of this publication.
:Study Publication Status: A term describing the status of this publication (i.e. submitted, in preparation, published). The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Study Publication Status Term Accession Number: The accession number from the Term Source associated with the selected term.
:Study Publication Status Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match one the Term Source Name declared in the in the Ontology Source Reference section.

**STUDY FACTORS**

:Study Factor Name: The name of one factor used in the Study and/or Assay files. A factor corresponds to an independent variable manipulated by the experimentalist with the intention to affect biological systems in a way that can be measured by an assay. The value of a factor is given in the Study or Assay file, accordingly. If both Study and Assay have a Factor Value (see section 4.2.5 and 4.3.1.5, respectively), these must be different.
:Study Factor Type: A term allowing the classification of this factor into categories. The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Study Factor Type Term Accession Number: The accession number from the Term Source associated with the selected term.
:Study Factor Type Term Source REF: Identifies the controlled vocabulary or ontology that this term comes from. The Source REF has to match one of the Term Source Name declared in the Ontology Source Reference section.

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

Several ISA-Tab example files are available from the project page www.isa-tools.org. The example below shows an
Investigation File
with one Study and two Assays. The column A holds headers for sections (e.g., INVESTIGATION PUBLICATIONS) and
fields (e.g., Investigation Pubmed ID); while subsequent columns hold the value(s) for the fields named. In this
example, where only one Study has been created, the Investigation section is left empty. It is important to note
that each section is independent of any other, therefore the values in a column are related only within each
section (i.e., between headings), never between sections. For example, the values in column B in the STUDY FACTORS
section are not necessarily connected to the values in the same column in the STUDY ASSAYS section.

.. csv-table::
   :header: "A", "B", "C"
   :widths: 30, 30, 30
   :delim: U+0009
   :file: _static/i_investigation.txt