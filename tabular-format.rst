==============
ISA tab format
==============

:Status:
    Release candidate 1, ISA-TAB v1.0 specification document, version November 2009.

Authors
-------
Initially drafted by Philippe Rocca-Serra [1]_, Susanna-Assunta Sansone [1]_ and Marco Brandizi [1]_ (1) this
document and the work described herein incorporates input from David Hancock [2]_, Stephen Harris [3]_, Allyson
Lister [4]_, Michael Miller [5]_, Kieran O'Neill [6]_, Chris Taylor [1]_, Weida Tong [3]_ and other collaborators,
listed at the ISA-TAB project page (2) under 'Contributors'.

.. [1] EMBL-EBI The European Bioinformatics Institute, Wellcome Trust Genome Campus, Hinxton, Cambridge, UK.
.. [2] NERC Bioinformatics Center (NEBC), Centre for Ecology and Hydrology, Oxford, UK, and the University ofManchester, School of Computer Science, Manchester, UK.
.. [3] FDA's National Center for Toxicological Research (NCTR), Center for Toxicoinformatics, Jefferson, Arkansas.
.. [4] CISBAN & School of Computing Science, Newcastle University, Newcastle upon Tyne, UK.
.. [5] Rosetta Biosoftware, Seattle, Washington.
.. [6] BC Cancer Research Centre (BCCRC), Vancouver, Canada.

Documents and contacts
----------------------
The current document and several example files are available from the ISA-TAB project page (2). This documentation
is primarily aimed at software engineers, to facilitate the development of automated export from databases, or
import into analytical or other tools. A mailing list (isatab-devel@lists.sourceforge.net) has been set up to
facilitate discussion. Comments and suggestions on this document should be addressed to Philippe Rocca-Serra
(rocca@ebi.ac.uk) and the mailing list.

Abstract
--------
This document describes ISA-TAB, a general purpose framework with which to capture and communicate the complex metadata
required to interpret experiments employing combinations of technologies, and the associated data files. Sections 1 to
3 introduce the ISA-TAB proposal, describe the rationale behind its development, provide an overview of its structure
and relate it to other formats. Section 4 describes the specification in detail; section 5 provides examples of design
patterns.

ISA-TAB builds on the existing paradigm that is MAGE-TAB - a tab-delimited format to exchange microarray data. ISA-TAB
necessarily maintains backward compatibility with existing MAGE-TAB files to facilitate adoption; conserving the
simplicity of MAGE-TAB for simple experimental designs, while incorporating new features to capture the full complexity
of experiments employing a combination of technologies. Like MAGE-TAB before it, **ISA-TAB is simply a format**; the
decision on how to regulate its use (i.e. enforcing completion of mandatory fields or use of a controlled terminology)
is a matter for those communities, which will implement the format in their systems and for which submission and
exchange of minimal information is critical. In this case, an additional layer or of constraints should be agreed
and required on top of the ISA-TAB specification.

Prerequisites
-------------
Familiarity with the syntax and grammar defined in the MAGE-TAB specifications (3) is required, as the authors assume
knowledge of the MAGE-TAB format when describing the structure of ISA-TAB in this document.

ISA-TAB introduction
--------------------
Rationale
---------

The Investigation / Study / Assay (ISA) tab-delimited (TAB) format is a general purpose framework with which to collect
and communicate complex metadata (i.e. sample characteristics, technologies used, type of measurements made) from
experiments employing a combination of technologies. In particular, ISA-TAB has been developed for — but not limited
to — experiments using genomics, transcriptomics, proteomics or metabol/nomics techniques (hereafter referred as
'omics-based' experiments). For example, consider an investigation into the effect of a compound that induces liver
damage, which looks at changes both in (i) the metabolite profile of urine and (ii) gene expression in the liver
(by mass spectrometry and microarray technologies, respectively). The general motivation for this work is the
fulfillment of the needs of two groups:

The BioInvestigation Index project (4) to create a common structured representation of the metadata —  required to
interpret an experiment — with which to facilitate combined submission to ArrayExpress (5), Pride (6), and in the
near future, a metabolomics repository;

Collaborative systems (2, 7, 8) committed to pipelining omics-based experiments into EBI public repositories, or
willing to exchange data among themselves, or planning to enable their users to import data from public repositories
into their local systems.

ISA-TAB has been developed in synergy with other existing efforts, complementing and extending where necessary, as
follows:
 - it builds on the existing MicroArray Gene Expression (MAGE)-TAB paradigm (9);
 - it includes metadata as required by the Pride repository, supporting the Proteomics Standards Initiative (PSI, 10);
 - it places its concepts in line with the Functional Genomics Experiment (FuGE) objects (11, 12);
 - it complements the Study Data Tabulation Model (SDTM) (14, 15);
 - it introduces a generic structure to accommodate experiment employing a combination of technologies.

As stated, ISA-TAB could be viewed as an extended version of MAGE-TAB, a format that supports the management, exchange
and submission of microarray-based experiment data and metadata. This format was designed for use by laboratories
with little or no bioinformatics support, which cannot therefore deal with the complexity of the MAGE Markup Language
(ML) format (13). ISA-TAB builds on the MAGE-TAB paradigm, and shares its motivation for the use of tab-delimited text
files; i.e., that they can easily be created, viewed and edited by researchers using spreadsheet software such as
Microsoft Excel. ISA-TAB also employs MAGE-TAB syntax as far as possible to ensure backward compatibility with existing
 MAGE-TAB files (as described further in section 3.1). ISA-TAB contains all the fields in MAGE-TAB; however, it has a
 number of additional features that make it a more general framework, able to accommodate experiments employing a
 combination of technologies. Concepts in ISA-TAB have also been aligned with some of the objects in the FuGE model,
 for several reasons: First, because FuGE is a formal published model intended for functional genomics. Second,
 because the FuGE model is integral to the development of MAGE-ML v2, which will be related to the MAGE-TAB format.
 Finally because ISA-TAB is an effective way to render to FuGE -based documents in user-friendly readable format (as
 described further in section 3.2). The relation to SDTM biomedical tabular format in described in section 3.3.

The ISA-TAB format is described in detail in section 4.

Definitions
-----------
Investigation, Study and Assay are the three key entities (8) around which the ISA-TAB framework is built. They assist
in structuring and classifying information relevant to the subject under study and the different technologies employed.
Note that ‘subject’ as used above could to refer inter alia to an organism, or tissue, or an environmental sample.
Study is the central unit, containing information on the subject under study, its characteristics and any treatments
applied.

A Study has associated Assays; these are measurements performed either on the whole initial subject or on sample taken
from the subject, which produce qualitative or quantitative data. Assays can be characterized as the smallest complete
unit of experimentation producing data associated to a subject; i.e. one hybridization is treated as one assay; each
technical replicate represents an additional assay; one LC-MS run equals one assay; a multiplexed microarray with n a
layouts of the same design corresponds to n hybridizations; and a MALDI MS chip with n spots could perform up to n
assays (i.e. all spots analyzed). Investigation is a higher-order object, whose primary rolel is to group related
Studies.

It should be noted that the word 'experiment' has been deliberately avoided. A comparison of ArrayExpress and Pride
revealed that ‘experiment’ is used to refer to objects at different levels of granularity in each; i.e. to refer to a
set of related hybridizations in ArrayExpress, but only a single gel-based separation run in Pride. Following the
abstractions proposed here, an experiment in ArrayExpress would be equivalent to a Study.

The choice of Study as the central unit of the ISA-TAB proposal is supported by its use in existing biomedical formats,
such as the SDTM, which encompasses both the Standard for Exchange of Nonclinical Data (SEND, 14) and the Clinical
Data Interchange Standards Consortium (CDISC, 15). SDTM has been endorsed by the US Food and Drug Administration (FDA)
as the preferred way to organize, structure and format both clinical and non-clinical (toxicological) data submissions
(16, 17). See also sections 3.3 and 5.3.

ISA-TAB development process
---------------------------
Created to fulfill the need of the BioInvestigation Index project (4), the first straw-man proposal, ISA-TAB v0.1,
was presented and discussed in a workshop held at the European Bioinformatics Institute (EBI), Cambridge, UK, on 6-8
December, 2007, funded by the UK Biotechnology and Biological Sciences Research Council (BBSRC BB/E025080/1) (1). The
goal of this first workshop was the creation of an ‘exchange network test bed’ for a heterogeneous set of resources
(e.g.,  public and proprietary repositories, public and commercial software tools), variously run by academic,
industrial and governmental groups. The participants represented a range of groups interested in leveraging common
standards to report omics-based experiments, bringing with them experience of building standards gained through their
involvement in, or leadership of relevant efforts. The workshop report (8) is available from the ISA-TAB website (2).
The workshop produced a general consensus on the important role for ISA-TAB in addressing the immediate need for a
communications framework for multi-omics experiments. A series of technical challenges were also identified, the
majority of which have been resolved in the ISA-TAB v0.3 release.

A second workshop was held at EBI on 16-18 June, 2008. On this occasion, the ISA-TAB v0.3 proposal was revised in the
light of a series of real-life case examples - produced by the participating communities. These modifications were
agreed on, resulting in the current ISA-TAB v1.0 version. Participants also discussed examples of tools that need to be
developed to assist the users in the creation of ISA-TAB files and finalized the work plan to release the XSL
templates described in section 3.2. A short summary of this second workshop is available as a powerpoint presentation
from the ISA-TAB website (2).

It is foreseen that, following the publication this 'Release candidate 1, ISA-TAB v1.0 specification' document on the
ISA-TAB website, other workshops will be held to bring together those communities, which will implement the format in
their systems. Based on their feedback the initial design patterns documentation (see section 5) will be expanded and
eventually form an implementation guideline document.

ISA-TAB v1.0 structure overview
-------------------------------
ISA-TAB uses three types of file to capture the experimental metadata:
 - Investigation file
 - Study file
 - Assay file (with associated data files)

The Investigation file contains all the information needed to understand the overall goals and means used in an
experiment; experimental steps (or sequences of events) are described in the Study and in the Assay file(s). For each
Investigation file there may be one or more Study files; for each Study file there may be one or more Assay files.

Each file has a defined structure, with fields being organized on a per-column or per-row basis; each file is described
briefly in the subsections below and more fully in section 4.

Investigation file
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
    In this file, information is structured on a per-row basis with the first row being used for column headers. The
    Study file contains contextualizing information for one or more assays, for example; the subjects studied; their
    source(s); the sampling methodology; their characteristics; and any treatments or manipulations performed to
    prepare the specimens. See also section 4.2.

Assay file
    In this file, as for the study files, fields are again organized on a per-row basis with the first row being used
    for column headers. The Assay file represents a portion of the experimental graph (i.e., one part of the overall
    structure of the workflow); each Assay file must contain assays of the same type, defined by the type of
    measurement (i.e. gene expression) and the technology employed (i.e. DNA microarray). Assay-related information
    includes protocols, additional information relating to the execution of those protocols and references to data
    files (whether raw or derived). See also section 4.3.

Relating Study and Assay files
    In a study looking at the effect of a compound inducing liver damage in rats by characterizing the metabolic
    profile of urine (by NMR spectroscopy) and measuring protein and gene expression in the liver (by mass
    spectrometry and DNA microarrays respectively), there will be one Study file and three Assay files, in addition
    to the Investigation file.

     - The Study file will contain information on the rats (the subjects studied) their source(s) and characteristics, the description of their treatment with the compound and the steps undertaken to take urine and liver (samples) from the treated rats.
     - The Assay file for the urine metabolic profile (measurement) by NMR spectroscopy (technology) will contain the (stepwise) description of the methods by which the urine was processed for the assay, subsequent steps and protocols, and the link to the resultant raw and derived data files.
     - The Assay file for the gene expression profile (measurement) by DNA microarray (technology) will contain the (stepwise) description of how the RNA extract was prepared from the liver (or a section), how the extract was labeled, how the hybridization was performed and so on, and will also contain the links to the resultant raw and derived data files.
     - The Assay file for the protein expression profile (measurement) by mass spectrometry (technology), will contain the (stepwise) description of how the protein extract was prepared from the liver (or a section), how the extract was labeled, how the hybridization was performed and so on, and will also contain the links to the resultant raw and derived data files.

Data files and the ISArchive
    ISA-TAB focuses on structuring experimental metadata; raw and derived data files are considered as external files.
    The Assay file can refer to one or more of these external data files, see section 4.3. For guidelines on how to
    format these data files, users should refer to section 5.3 and the relevant standards group or reference
    repository (i.e. 5, 6, 10, 11, 12, 18, 19, 20). In addition to raw and derived data files, the Assay file for gene
    expression (measurement) by microarray (technology) will also refer to a Derived Array Data Matrix and an Array
    Description File (ADF), both described in the MAGE-TAB specifications (see section 4.3.2).

    For submission or transfer, ISA-TAB files and associated data files can be packaged into an ISArchive as shown in
    Figure 1.
