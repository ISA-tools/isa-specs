==============
ISA-Tab format
==============

:Status: ISA-Tab v2.0 specification document, September 2016.

Authors
=======
Initially drafted by Philippe Rocca-Serra [1]_, Susanna-Assunta Sansone [1]_ and Marco Brandizi [1]_ (1) this
document and the work described herein incorporates input from David Hancock [2]_, Stephen Harris [3]_, Allyson
Lister [4]_, Michael Miller [5]_, Kieran O'Neill [6]_, Chris Taylor [1]_, Weida Tong [3]_ and other collaborators,
listed at the ISA-Tab project page (2) under 'Contributors'.

.. [1] EMBL-EBI The European Bioinformatics Institute, Wellcome Trust Genome Campus, Hinxton, Cambridge, UK.
.. [2] NERC Bioinformatics Center (NEBC), Centre for Ecology and Hydrology, Oxford, UK, and the University ofManchester, School of Computer Science, Manchester, UK.
.. [3] FDA's National Center for Toxicological Research (NCTR), Center for Toxicoinformatics, Jefferson, Arkansas.
.. [4] CISBAN & School of Computing Science, Newcastle University, Newcastle upon Tyne, UK.
.. [5] Rosetta Biosoftware, Seattle, Washington.
.. [6] BC Cancer Research Centre (BCCRC), Vancouver, Canada.

As a pre-requisite, please make sure you have read and understood the ISA Abstract Model that the ISA-Tab format is
based on.

---------------------
ISA-Tab v2.0 overview
---------------------
ISA-Tab uses three types of file to capture the experimental metadata:
 - Investigation file
 - Study file
 - Assay file (with associated data files)

The Investigation file contains all the information needed to understand the overall goals and means used in an
experiment; experimental steps (or sequences of events) are described in the Study and in the Assay file(s). For each
Investigation file there may be one or more Studies defined with a corresponding Study file; for each Study there may
be one or more Assays defined with corresponding Assay files.

ISA-Tab files
=============
Files should be encoded using UTF-8.

Column delimiters should be the Unicode Horizontal Tab character (Unicode U+0009).

In order to facilitate identification of ISA-Tab component files, specific naming patterns should follow:

 - i_*.txt for identifying the Investigation file
 - s_*.txt for identifying Study file(s)
 - a_*.txt for identifying Assay file(s)

All labels are case-sensitive:

 - In the Investigation file, section headers are completely written in upper case (e.g. STUDY), field headers have the first letter of each word in upper case (e.g. Study Identifier); with the exception of the referencing label (REF).
 - In the Study or Assay files, column headers also have the first letter of each word in upper case, with the exception of the  referencing label (REF).

Dates should be supplied in the ISO8601 format "YYYY-MM-DD".

Rows in which the first character in the first column is Unicode U+0023 (the # character) will be interpreted as
comments. Reference implementation parsers should ignore those lines entirely.

All values of cells may be enveloped with the Unicode Quotation Mark, Unicode U+0022 (the " character).

Investigation file
==================
The Investigation file fulfils four needs:

#. to declare key entities, such as factors, protocols, which may be referenced in the other files
#. to track provevance of the terminologies (controlled vocabularies or ontologies) there are used, where applicable
#. to relate Assay files to Studies
#. to relate each Study file to an Investigation (this only becomes necessary when two or more Study files need to be grouped).

An Investigation file is structured as a table with vertical headings along the first column, and corresponding values
in the subsequent columns. The following section headings appear in the Investigation file (in order).

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
file, the value of the cell should match one of the Term Source Name value declared in this section.

Where a column labelled with Term Source REF in a Study file or Assay file associated with the Investigation, the value
of the cell should match one of the Term Source Name value declared in this section.

**ONTOLOGY SOURCE REFERENCE**

:Term Source Name: The name of the source of a term; i.e. the source controlled vocabulary or ontology. These names will be used in all corresponding Term Source REF fields that occur elsewhere.
:Term Source File: A file name or a URI of an official resource.
:Term Source Version: The version number of the Term Source to support terms tracking.
:Term Source Description: Use for disambiguating resources when homologous prefixes have been used.

Investigation section
=====================
This section is organized in several subsections, described in detail below. The Investigation section provides a
flexible mechanism for grouping two or more Study files where required. When only one Study is created, the values in
this section should be left empty and the relevant metadata values recorded in the Study section only.

**INVESTIGATION**

:Investigation Identifier: A locally unique identifier or an accession number provided by a repository.
:Investigation Title: A concise name given to the investigation
:Investigation Description: A textual description of the investigation
:Investigation Submission: Date The date on which the investigation was reported to the repository.
:Investigation Public Release Date: The date on which the investigation should be released publicly.

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
being to enhance readability and presentation, and possibly to help with parsing. These subsections must remain within
this repeatable block, although their order may vary; the fields must remain within their subsection.

**STUDY**

:Study Identifier: A unique identifier, either a temporary identifier supplied by users or one generated by a repository or other database. For example, it could be an identifier complying with the LSID specification.
:Study Title: A concise phrase used to encapsulate the purpose and goal of the study.
:Study Description: A textual description of the study, with components such as objective or goals.
:Study Submission Date: The date on which the study is submitted to an archive.
:Study Public Release Date: The date on which the study should be released publicly.
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


Study Table file
================
In this file, information is structured on a per-row basis with the first row being used for column headers. The
Study file contains contextualizing information for one or more assays, for example; the subjects studied; their
source(s); the sampling methodology; their characteristics; and any treatments or manipulations performed to
prepare the specimens. See also section 4.2.

Assay Table file
================
In this file, as for the study files, fields are again organized on a per-row basis with the first row being used
for column headers. The Assay file represents a portion of the experimental graph (i.e., one part of the overall
structure of the workflow); each Assay file must contain assays of the same type, defined by the type of
measurement (i.e. gene expression) and the technology employed (i.e. DNA microarray). Assay-related information
includes protocols, additional information relating to the execution of those protocols and references to data
files (whether raw or derived). See also section 4.3.

Relating Study and Assay files
==============================
In a study looking at the effect of a compound inducing liver damage in rats by characterizing the metabolic
profile of urine (by NMR spectroscopy) and measuring protein and gene expression in the liver (by mass
spectrometry and DNA microarrays respectively), there will be one Study file and three Assay files, in addition
to the Investigation file.

 - The Study file will contain information on the rats (the subjects studied) their source(s) and characteristics, the description of their treatment with the compound and the steps undertaken to take urine and liver (samples) from the treated rats.
 - The Assay file for the urine metabolic profile (measurement) by NMR spectroscopy (technology) will contain the (stepwise) description of the methods by which the urine was processed for the assay, subsequent steps and protocols, and the link to the resultant raw and derived data files.
 - The Assay file for the gene expression profile (measurement) by DNA microarray (technology) will contain the (stepwise) description of how the RNA extract was prepared from the liver (or a section), how the extract was labeled, how the hybridization was performed and so on, and will also contain the links to the resultant raw and derived data files.
 - The Assay file for the protein expression profile (measurement) by mass spectrometry (technology), will contain the (stepwise) description of how the protein extract was prepared from the liver (or a section), how the extract was labeled, how the hybridization was performed and so on, and will also contain the links to the resultant raw and derived data files.

Data files and the ISArchive
============================
ISA-Tab focuses on structuring experimental metadata; raw and derived data files are considered as external files.
The Assay file can refer to one or more of these external data files, see section 4.3. For guidelines on how to
format these data files, users should refer to section 5.3 and the relevant standards group or reference
repository. In addition to raw and derived data files, the Assay file for gene
expression (measurement) by microarray (technology) will also refer to a Derived Array Data Matrix and an Array
Description File (ADF), both described in the MAGE-TAB specifications (see section 4.3.2).

For submission or transfer, ISA-Tab files and associated data files can be packaged into an ISArchive as shown:

(fig)
