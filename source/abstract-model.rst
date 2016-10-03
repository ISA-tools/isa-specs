================================
ISA Abstract Model Specification
================================

:Status: ISA Abstract Model specification  v1.0 (3 October 2016)

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in RFC 2119.

The ISA specifications are licensed under XXXXXXXXX.

------------
Introduction
------------
ISA is a metadata framework for describing experiments in biology and medicine. For a full introduction to the ISA
framework, see www.isa-tools.org

The ISA specifications define an Abstract Model of the metadata framework. The ISA Abstract Model has been implemented
in two format specifications, ISA-Tab and ISA-JSON, both of which have supporting tools and services associated with
them. The format specifications are also available for additional tooling to take advantage of ISA-formatted content.

----------------
Revision History
----------------
+---------+------------+---------------------------------------------------+
| Version | Date       | Description                                       |
+=========+============+===================================================+
| 1.0     | 2016-10-03 | First release of ISA Abstract Model specification |
+---------+------------+---------------------------------------------------+

-------------
Specification
-------------

Ontology Annotation
===================
For a given value, an Ontology Annotation SHOULD qualify this value with an accession number taken from an Ontology
Source.

An Ontology Annotation SHOULD record the following:

:Accession Number: The accession number from the Ontology Source associated with the selected term.

Ontology Source
===============
An Ontology Source describes the resource from which the value of an Ontology Annotation is derived from. Ontology
Sources SHOULD be referenced by Ontology Annotations. An Ontology Source should contain enough information on which to
be able to ascertain the Ontology Source's provenance.

An Ontology Source SHOULD record the following:

:Name: The name of the source of a term; i.e. the source controlled vocabulary or ontology. These names will be used to reference the Ontology Source from an Ontology Annotation.
:File: A file name or a URI of an official resource.
:Version: The version number of the Term Source to support terms tracking.
:Description: Use for disambiguating resources when homologous prefixes have been used.

Unit
====
Units are used to classify dimensional data, and used accordingly with relevant values. A Unit SHOULD be implemented as an Ontology Annotation.

Publication
===========
A Publication SHOULD record the following:

:PubMed ID: The PubMed IDs of the described publication(s) associated with this investigation.
:DOI: A Digital Object Identifier (DOI) for that publication (where available).
:Author List: The list of authors associated with that publication.
:Title: The title of publication associated with the investigation.
:Status: An Ontology Annotation describing the status of that publication (i.e. submitted, in preparation, published).

Contact
=======
A Contact SHOULD record the following:

:Name: The name of a person.
:Email: The email address of a person.
:Phone: The telephone number of a person.
:Address: The address of a person.
:Affiliation: The organization affiliation for a person.
:Roles: Ontology Annotations to classify the roles performed by this person in the context of an Investigation or Study.

---------------------------
Investigation, Study, Assay
---------------------------

The ISA model consists of three core entities to capture experimental metadata:
 - Investigation
 - Study
 - Assay

An Investigation contains all the information needed to understand the overall goals and means used in an
experiment; experimental steps (or sequences of events) are described in a Study and Assay . For each
Investigation there may be one or more Study associated with it; for each Study there may be one or more
Assays.

Investigation
=============

An Investigation is intended to:

#. to record metadata relating to a given investigation
#. to link related Study objects under an Investigation (this only becomes necessary when two or more Study objects need to be grouped)

Investigations record metadata relating to the description of the investigation context, such as the title and
description of the investigation as well as about related people and scholarly publications. Studys and Assays
are grouped within Investigations to record other metadata within the relevant contexts.

An Investigation SHOULD record the following:

:Identifier: A identifier or an accession number provided by a repository. This SHOULD be locally unique.
:Title: A concise name given to the investigation.
:Description: A textual description of the investigation.
:Submission Date: The date on which the investigation was reported to the repository.
:Public Release Date: The date on which the investigation was released publicly.
:Publications: A list of Publications relating to the investigation.
:Contacts: A list of Contacts relating to the investigation.

Study
=====
A Study is a central concept containing information on the subject under study, it's characteristics and any
treatments applied.

A Study contains contextualizing information for one or more Assays. Metadata about the study design, study
factors used, and study protocols are recorded in Study objects, as well as information similarly to the
Investigation including title and description of the study, and related people and scholarly publications.

A Study SHOULD record the following:

:Identifier: A identifier or an accession number provided by a repository. This SHOULD be locally unique.
:Title: A concise name given to the investigation.
:Description: A textual description of the investigation.
:Submission Date: The date on which the study was reported to the repository.
:Public Release Date: The date on which the study was released publicly.
:Publications: A list of Publications relating to the study.
:Contacts: A list of Contacts relating to the study.
:Design Type: An Ontology Annotation classifying the study based on the overall experimental design, e.g cross-over design or parallel group design.
:Factor Name: The name of one factor used in the Study and/or Assay files. A factor corresponds to an independent variable manipulated by the experimentalist with the intention to affect biological systems in a way that can be measured by an assay. The value of a factor is given in the Study or Assay file, accordingly.
:Factor Type: An Ontology Annotation allowing the classification of this factor into categories.

In a Study object we record the provenance of biological samples, from source material through a collection process to sample material, represented with directed acyclic graphs (direct graphs with no loops/cycles). The pattern of nodes is usually formed of a source material node, followed by a sample collection process node, followed by a sample material node.

For example:

.. code-block:: none

  (source material)->(sample collection)->(sample material)

These study graphs can split and pool depending on how the samples are collected.

In a splitting example, multiple samples might be derived from the same source:

.. code-block:: none

  (source material 1)->(sample collection)->(sample material 1)
  (source material 1)->(sample collection)->(sample material 2)

In a pooling example, multiple sources may be used to create a single sample:

.. code-block:: none

  (source material 1)->(sample collection)->(sample material 1)
  (source material 2)->(sample collection)->(sample material 1)


Assay
=====
An Assay represents a test performed either on material taken from a subject or on a whole initial subject,
producing qualitative or quantitative measurements.

An Assay groups descriptions of provenance of sample processing for related tests. Each test typically
follows the steps of one particular experimental workflow described by a particular protocol.

Assay-related metadata includes descriptions of the measurement type and technology used, and a link to what study
protocol is applied. Where an assay produces data files, links to the data are recorded here.

An Assay SHOULD record the following:

:Measurement Type: An Ontology Annotation to qualify the endpoint, or what is being measured (e.g. gene expression profiling or protein identification). The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Technology Type: An Ontology Annotation to identify the technology used to perform the measurement, e.g. DNA microarray, mass spectrometry. The term can be free text or from, for example, a controlled vocabulary or an ontology. If the latter source is used the Term Accession Number and Term Source REF fields below are required.
:Technology Platform: The manufacturer and platform name, e.g. Bruker AVANCE, of the technology used.

In an Assay we record the provenance of biological samples, from sample material through an experimental workflow, represented with directed acyclic graphs. Assay graphs usually follow the pattern of a sample material, followed by a series of process and material/data nodes.

For example, to show a sample that goes through some extraction process (e.g. nucleic acid extraction) through to producing some sequenced data, we might produce something like:

.. code-block:: none

  (sample material)->(extraction process)->(extract)->(sequencing process)->(raw data file)

Like with the study graphs, splitting and pooling can occur where appropriate in assay graphs.

Study and Assay graphs
======================
Experimental graphs described in Studies and Assays are made up of specific types of nodes.

Experimental graphs MUST be directed and acyclic (i.e. MUST NOT contain loops/cycles).

All nodes in Study and Assay graphs MUST be uniquely identifiable.

Material nodes:

Material nodes can also be used as a generic structure to describe materials consumed or produced during an experimental workflow. Materials SHOULD record the following:

:Characteristics: A list of material characteristics that may be qualitative or quantitative in description. Qualitative values MAY be Ontology Annotations, while quantitative values MAY be qualified with a Unit definition.
:Material Type: An Ontology Annotation describing the material.

Sources are a special kind of Material node and are considered as the starting biological material used in a study.
Source nodes SHOULD be followed by a Process node describing a sample collection process, and SHOULD only appear in
Study graphs.

Samples are a special kind of Material node and represent major outputs resulting from a protocol application.
Sample nodes in the Study graphs SHOULD be preceded by a Process node describing a sample collection process. Sample nodes in the Assay graphs SHOULD be followed by a Process node and SHOULD NOT be preceded by any node.

Data nodes:

Data nodes represent outputs resulting from a protocol application that corresponds to some process that produces data, typically in the form of data files. Data nodes SHOULD record the following:

:File name: A file name or full path referencing a data file produced by the related process that MAY be packaged with, or is accessible via, the ISA reference implementation content.

Data nodes SHOULD be preceded by a Process node describing a data-producing process, such as NMR scanning or DNA sequencing.

Process nodes:

Processes represent the application of a protocol to some input material (e.g. a Source) to produce some output (e.g.a Sample).

Processes SHOULD record the following:

:Parameter Values: Reporting on the values taken by parameters when applying a protocol. A protocol description in the Study SHOULD declare the required parameters, where here the values applied are recorded.
:Performer: Name of the operator who carried out the protocol. This allows account to be taken of operator effects and can be part of a quality control data tracking.
:Date: The date on which a protocol is performed. This allows account to be taken of day effects and can be part of a quality control data tracking.

Process nodes SHOULD be preceded by zero or more material or data nodes, and followed by zero or more material or data nodes.


Configurations
--------------
In the ISA framework, we define Configurations as a way to add constraints on the Abstract Model elements. For a given
experimental descriptor we may want to declare what minimum information should be present. Configurations can specify
what fields should be present and also what datatypes are valid values. In addition to this, we can also specify
the experimental workflow patterns that the Assay object should allow according to the type of measurement defined for
an assay, and the type of technology used for collecting the relevant data (e.g. sequencing or imaging technologies).

For example, we may create a configuration that mandates that Investigation metadata MUST record the title, author list,
and description. The Abstract Model specification only specifies that these SHOULD be present. Therefore the
configuration specifies additional constraints on a reference implementation of ISA that can be provided by users
beyond the reference implementation developers, e.g. Users, curators, publishers, etc.

For example, we mandate that the Study graphs MUST follow the (source)->(sample collection->(sample) pattern. A
reference implementation could specify this as a configuration if it is not hard-coded in the reference implementation.

Where the power of configurations becomes more apparent is where we want to describe Assay graphs. A data publisher
might provide a configuration specification that mandates that valid submissions to the data publisher from
researchers must follow something like

.. code-block:: none

  (sample)->(nucleic acid extraction)->(extract)->(nucleic acid sequencing)->(raw data)

for a technology/measurement type combination of genome sequencing/nucleotide sequencing. A configuration for a
different technology/measurement type combination of SNP analysis/DNA microarray might specify

.. code-block:: none

  (sample)->(DNA extraction)->(extract)->(nucleic acid hybridization)->(data collection)->(raw data)

Configurations MUST add constraints to the reference implementation of the Abstract Model.

How configurations are implemented is left open to reference implementation developers, but the point is to allow users
of reference implementations of the ISA Abstract Model to add constraints to ISA content in a flexible manner.
Configurations are implemented differently between the ISA-Tab and ISA-JSON formats, so please refer to those
respective specifications for further information on how to use them, or to see examples of how they are implemented.
