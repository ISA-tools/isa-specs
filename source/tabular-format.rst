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
