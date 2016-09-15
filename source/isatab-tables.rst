===========================
Study and Assay Table files
===========================

Study Table file
================

In this file, information is structured on a per-row basis with the first row being used for column headers. The
Study file contains contextualizing information for one or more assays, for example; the subjects studied; their
source(s); the sampling methodology; their characteristics; and any treatments or manipulations performed to
prepare the specimens.

Assay Table file
================
In this file, as for the study files, fields are again organized on a per-row basis with the first row being used
for column headers. The Assay file represents a portion of the experimental graph (i.e., one part of the overall
structure of the workflow); each Assay file must contain assays of the same type, defined by the type of
measurement (i.e. gene expression) and the technology employed (i.e. DNA microarray). Assay-related information
includes protocols, additional information relating to the execution of those protocols and references to data
files (whether raw or derived).

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
