==================
ISA abstract model
==================

:Status: ISA Abstract Model v1.0 specification document, September 2016.

---------------------------
Investigation, Study, Assay
---------------------------

The ISA model consists of three core object types to capture experimental metadata:
 - Investigation
 - Study
 - Assay

An Investigation contains all the information needed to understand the overall goals and means used in an
experiment; experimental steps (or sequences of events) are described in Study and Assay objects. For each
Investigation there may be one or more Studies associated with it; for each Study there may be one or more Assays.

Investigation
=============

The Investigation object is intended to:

#. to record metadata relating to a given investigation
#. to link related Study objects under an Investigation (this only becomes necessary when two or more Study objects need to be grouped)

Investigation objects record metadata relating to the description of the investigation context, such as the title and
description of the investigation as well as about related people and scholarly publications. Study and Assay objects
are grouped within Investigation objects to record other metadata within the relevant contexts.

Study
=====
A Study is a central concept containing information on the subject under study, it's characteristics and any
treatments applied.

A Study object contains contextualizing information for one or more Assays. Metadata about the study design, study
factors used, and study protocols are recorded in Study objects, as well as information similarly to the
Investigation including title and description of the study, and related people and scholarly publications.

In a Study object we record the provenance of biological samples, from source to sample materials, represented with
a directed graph.

Assay
=====
An Assay represents a test performed either on material taken from a subject or on a whole initial subject,
producing qualitative or quantitative measurements.

The Assay object groups descriptions of provenance of sample processing for related tests. Each test typically
follows the steps of one particular experimental workflow described by a particular protocol. Assay-related
metadata includes descriptions of the measurement type and technology used, and a link to what study protocol is
applied. Where an assay produces data files, links to the data are recorded here.

In an Assay object we record the provenance of biological samples, from sample through an experimental workflow,
represented with a directed graph.

The following diagram represents the ISA objects and their relationships:

(Put updated ISA diagram here)

More information about the semantic relationships presented in the ISA model is available in the ISA ontology
[`ISA ontology`_] and the linkedISA publication [linkedISA_].

Configurations
--------------
In the ISA framework, we define Configurations as a way to add constraints on the Abstract Model elements. For a given
experimental descriptor we may want to declare what minimum information should be present. Configurations can specify
what fields should be filled out and also what datatypes are valid values. In addition to this, we can also specify
the experimental workflow patterns that the Assay object should allow according to the type of measurement defined for
an assay, and the type of technology used for collecting the relevant data (e.g. sequencing or imaging technologies).

Configurations are implemented slightly differently between the ISA-Tab and ISA-JSON formats, so please refer to those
respective specifications for further information on how to use ISA configurations.

.. _ISA ontology: http://purl.org/isaterms
.. _linkedISA: http://dx.doi.org/10.1186%2F1471-2105-15-S14-S4

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