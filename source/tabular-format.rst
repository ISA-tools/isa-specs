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

Definitions
===========
Investigation, Study and Assay are the three key entities around which the ISA-Tab framework is built. They assist
in structuring and classifying information relevant to the subject under study and the different technologies employed.
Note that 'subject' as used above could to refer inter alia to an organism, or tissue, or an environmental sample.
Study is the central unit, containing information on the subject under study, its characteristics and any treatments
applied.

A Study has associated Assays; these are measurements performed either on the whole initial subject or on sample taken
from the subject, which produce qualitative or quantitative data. Assays can be characterized as the smallest complete
unit of experimentation producing data associated to a subject; i.e. one hybridization is treated as one assay; each
technical replicate represents an additional assay; one LC-MS run equals one assay; a multiplexed microarray with n a
layouts of the same design corresponds to n hybridizations; and a MALDI MS chip with n spots could perform up to n
assays (i.e. all spots analyzed). Investigation is a higher-order object, whose primary role is to group related
Studies.

-------------------------------
ISA-Tab v1.0 structure overview
-------------------------------
ISA-Tab uses three types of file to capture the experimental metadata:
 - Investigation file
 - Study file
 - Assay file (with associated data files)

The Investigation file contains all the information needed to understand the overall goals and means used in an
experiment; experimental steps (or sequences of events) are described in the Study and in the Assay file(s). For each
Investigation file there may be one or more Study files; for each Study file there may be one or more Assay files.

Each file has a defined structure, with fields being organized on a per-column or per-row basis; each file is described
briefly in the subsections below and more fully in section 4.

Investigation file
==================
The Investigation file is intended to meet four needs: (i) to define key entities, such as factors, protocols,
which may be referenced in the other files; (ii) to track provevance of the terminologies (controlled vocabularies
or ontologies) there are used, where applicable; (iii) to relate Assay files to Study files; and optionally, (iv)
to relate each Study file to an Investigation (this only becomes necessary when two or more Study files need to
be grouped).

The optional Investigation section of an Investigation file is a flexible solution to group two or more Study files,
as required by several use cases. In the toxicogenomics domain, for example, acute toxicity studies are followed by
long term toxicity studies and in vitro toxicity studies. For clarity, the users would link these Study files by
filling the Investigation section. Another example comes from the environmental genomics domain, where several studies
carried out in the same area can be usefully related under the same Investigation. See also section 4.1.

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
