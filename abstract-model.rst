ISA abstract model
==================
The ISA model uses three core object types to capture the    experimental metadata:
 - Investigation
 - Study
 - Assay

The Investigation contains all the information needed to understand the overall goals and means used in an
experiment; experimental steps (or sequences of events) are described in a Study and in an Assay. For each
Investigation there may be one or more Studies associated with it; for each Study there may be one or more Assays.

Investigation
    The Investigation object is intended to meet four needs:
    1.	to define key entities, such as factors, protocols, which may be referenced in the other objects;
    2. to track provenance of the terminologies (controlled vocabularies or ontologies) that are used, where
    applicable;
    3.to relate Assay objects to Study objects; and optionally
    4. to relate each Study to an Investigation (this only becomes necessary when two or more Study objects need to
    be grouped).

An investigation contains the following properties:

Study
    The Study object contains contextualizing information for one or more assays, for example; the subjects studied;
    their source(s); the sampling methodology; their characteristics; and any treatments or manipulations performed to
    prepare the specimens.

Assay
    The Assay object represents a portion of the experimental graph (i.e., one part of the overall structure of the
    workflow); each Assay must contain assays of the same type, defined by the type of measurement (i.e. gene
    expression) and the technology employed (i.e. DNA microarray). Assay-related information includes protocols,
    additional information relating to the execution of those protocols and references to data files (whether raw or
    derived).

The following diagram represents the entities and their relationships as per ISA Model Release Candidate version 1.0.

.. image:: res/isa_model_1.png

More information about the semantic relationships presented in the ISA model is available in the ISA ontology
[`ISA ontology`_] and the linkedISA publication [linkedISA_].

ISA Infrastructure - Configurations
-----------------------------------
TODO

.. _ISA ontology: http://purl.org/isaterms
.. _linkedISA: http://dx.doi.org/10.1186%2F1471-2105-15-S14-S4