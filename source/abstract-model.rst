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

The Investigation object is intended to meet 3 needs:

#. to track provenance of the terminologies (controlled vocabularies or ontologies) that are used, where applicable
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

ISA Infrastructure - Configurations
-----------------------------------
TODO

.. _ISA ontology: http://purl.org/isaterms
.. _linkedISA: http://dx.doi.org/10.1186%2F1471-2105-15-S14-S4