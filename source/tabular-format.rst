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

Column delimiters should be the Unicode Horizontal Tab character (unicode codepoint 0009).

In order to facilitate identification of ISA-Tab component files in an ISArchive, specific naming patterns should follow:

 - i_*.txt for identifying the Investigation file
 - s_*.txt for identifying Study file(s)
 - a_*.txt for identifying Assay file(s)

All labels are case-sensitive:

 - In the Investigation file, section headers are completely written in upper case (e.g. STUDY), field headers have the first letter of each word in upper case (e.g. Study Identifier); with the exception of the referencing label (REF).
 - In the Study or Assay files, column headers also have the first letter of each word in upper case, with the exception of the  referencing label (REF).

Dates should be supplied in the ISO8601 format "YYYY-MM-DD".

Rows in which the first character in the first column is Unicode U+0023 (the # character) will be interpreted as
comments. ISA-Tab parsers should ignore those lines entirely.

Investigation file
==================
The Investigation file fulfils four needs:

#. to define key entities, such as factors, protocols, which may be referenced in the other files
#. to track provevance of the terminologies (controlled vocabularies or ontologies) there are used, where applicable
#. to relate Assay files to Studies
#. to relate each Study file to an Investigation (this only becomes necessary when two or more Study files need to be grouped).

An Investigation file is structured as a table with vertical headings along the first column, and corresponding values
in the subsequent columns. The following sections appear in the Investigation file (in order).

:ONTOLOGY SOURCE REFERENCE:
:Term Source Name: The name of the source of a term; i.e. the source controlled vocabulary or ontology. These names will be used in all corresponding Term Source REF fields that occur elsewhere.
:Term Source File: A file name or a URI of an official resource.
:Term Source Version: The version number of the Term Source to support terms tracking.
:Term Source Description: Use for disambiguating resources when homologous prefixes have been used.

Study file
==========
In this file, information is structured on a per-row basis with the first row being used for column headers. The
Study file contains contextualizing information for one or more assays, for example; the subjects studied; their
source(s); the sampling methodology; their characteristics; and any treatments or manipulations performed to
prepare the specimens. See also section 4.2.

Assay file
==========
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
