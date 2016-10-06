==================
ISA Abstract Model
==================

This ISA specification defines an Abstract Model of the metadata framework. The ISA Abstract Model has been implemented
in two format specifications, :doc:`ISA-Tab </isatab>` and :doc:`ISA-JSON </isajson>`, both of which have supporting
tools and services associated with them. The format specifications are also available for additional tooling to take
advantage of ISA-formatted content.

The concept map below shows the ISA objects/entities and their relation to one another:

.. image:: _static/isa_model_1.png
   :align: center
   :alt: Concept map showing ISA objects/entities and their relation to one another.

Ontology Annotation
===================
For a given value, an ``Ontology Annotation`` SHOULD qualify this value with an accession number taken from an ``Ontology
Source``.

An ``Ontology Annotation`` SHOULD record the following:

.. csv-table::
    :file: _static/model/ontology_annotation.csv
    :header-rows: 1
    :widths: 10, 10, 80


Ontology Source
===============
An ``Ontology Source`` describes the resource from which the value of an ``Ontology Annotation`` is derived from.
An ``Ontology Source`` SHOULD be referenced by an ``Ontology Annotation``. An ``Ontology Source`` should contain enough information on which to
be able to ascertain the provenance of an ``Ontology Source``.

An ``Ontology Source`` SHOULD record the following:

.. csv-table::
    :file: _static/model/ontology_source.csv
    :header-rows: 1
    :widths: 10, 10, 80

Unit
====
A ``Unit`` is used to classify dimensional data, and used accordingly with relevant values.

A ``Unit`` SHOULD be implemented as an ``Ontology Annotation``.

Publication
===========
A ``Publication`` SHOULD record the following:

.. csv-table::
    :file: _static/model/publication.csv
    :header-rows: 1
    :widths: 10, 10, 80

Contact
=======
A ``Contact`` SHOULD record the following:

.. csv-table::
    :file: _static/model/contact.csv
    :header-rows: 1
    :widths: 10, 10, 80

Investigation, Study, Assay
===========================

The ISA model consists of three core entities to capture experimental metadata:
 - ``Investigation``
 - ``Study``
 - ``Assay``

An ``Investigation`` contains all the information needed to understand the overall goals and means used in an
experiment; experimental steps (or sequences of events) are described in a ``Study`` and ``Assay`` . For each
``Investigation`` there may be one or more ``Study`` associated with it; for each ``Study`` there may be one or more
``Assay``.

Investigation
-------------

An ``Investigation`` is intended to:

#. to record metadata relating to a given investigation
#. to link related ``Study`` objects under an ``Investigation`` (this only becomes necessary when two or more ``Study`` objects need to be grouped)

An ``Investigation`` is used to record metadata relating to the description of the investigation context, such as the title and
description of the investigation as well as about related people and scholarly publications. ``Study`` and ``Assay`` objects
are grouped within an ``Investigation`` to record other metadata within the relevant contexts.

An ``Investigation`` SHOULD record the following:

.. csv-table::
    :file: _static/model/investigation.csv
    :header-rows: 1
    :widths: 10, 10, 80

Study
-----
A ``Study`` is a central concept containing information on the subject under study, its characteristics and any
treatments applied.

A ``Study`` contains contextualising information for one or more ``Assay``s. Metadata about the study design, study
factors used, and study protocols are recorded in ``Study`` objects, as well as information similarly to the
``Investigation`` including title and description of the study, and related people and scholarly publications.

A ``Study`` SHOULD record the following:

.. csv-table::
    :file: _static/model/study.csv
    :header-rows: 1
    :widths: 10, 10, 80

In a ``Study`` object we record the provenance of biological samples, from source material through a collection process to sample material, represented with directed acyclic graphs (direct graphs with no loops/cycles). The pattern of nodes is usually formed of a source material node, followed by a sample collection process node, followed by a sample material node.

For example:

.. code-block:: none

  (source material)->(sample collection)->(sample material)

These study graphs MAY split and pool depending on how the samples are collected.

In a splitting example, multiple samples might be derived from the same source:

.. code-block:: none

  (source material 1)->(sample collection)->(sample material 1)
  (source material 1)->(sample collection)->(sample material 2)

In a pooling example, multiple sources may be used to create a single sample:

.. code-block:: none

  (source material 1)->(sample collection)->(sample material 1)
  (source material 2)->(sample collection)->(sample material 1)

Assay
-----
An ``Assay`` represents a test performed either on material taken from a subject or on a whole initial subject,
producing qualitative or quantitative measurements.

An ``Assay`` groups descriptions of provenance of sample processing for related tests. Each test typically
follows the steps of one particular experimental workflow described by a particular protocol.

``Assay``-related metadata includes descriptions of the measurement type and technology used, and a link to what study
protocol is applied. Where an assay produces data files, links to the data are recorded here.

An ``Assay`` SHOULD record the following:

.. csv-table::
    :file: _static/model/assay.csv
    :header-rows: 1
    :widths: 10, 10, 80

In an ``Assay`` we record the provenance of biological samples, from sample material through an experimental workflow, represented with directed acyclic graphs. ``Assay`` graphs usually follow the pattern of a sample material, followed by a series of process and material/data nodes.

For example, to show a sample that goes through some extraction process (e.g. nucleic acid extraction) through to producing some sequenced data, we might produce something like:

.. code-block:: none

  (sample material)->(extraction process)->(extract)->(sequencing process)->(raw data file)

Like with the study graphs, splitting and pooling can occur where appropriate in assay graphs.

Study and Assay graphs
----------------------
Experimental graphs relating to ``Study`` and ``Assay`` objects are made up of specific types of nodes.

Experimental graphs MUST be `directed and acyclic <https://en.wikipedia.org/wiki/Directed_acyclic_graph>`_ (i.e. MUST NOT contain loops/cycles).

All nodes in ``Study`` and ``Assay`` graphs MUST be uniquely identifiable. User-defined identifiers MAY also be used.

Experimental graphs MUST be composed of the following node types

**Material nodes**

``Material`` nodes can also be used as a generic structure to describe materials consumed or produced during an experimental workflow.
``Material`` nodes SHOULD record the following:

.. csv-table::
    :file: _static/model/material_node.csv
    :header-rows: 1
    :widths: 10, 10, 80

``Source`` nodes are a special kind of ``Material`` node and are considered as the starting biological material used in a study.
``Source`` nodes SHOULD be followed by a ``Process`` node describing a sample collection process, and SHOULD only appear in
``Study`` graphs.

``Sample`` nodes are a special kind of ``Material`` node and represent major outputs resulting from a protocol application.
``Sample`` nodes in the ``Study`` graphs SHOULD be preceded by a ``Process`` node describing a sample collection process. ``Sample`` nodes in the ``Assay`` graphs SHOULD be followed by a ``Process`` node and SHOULD NOT be preceded by any node.

**Data nodes**

``Data`` nodes represent outputs resulting from a protocol application that corresponds to some process that produces data, typically in the form of data files. ``Data`` nodes SHOULD record the following:

.. csv-table::
    :file: _static/model/data_node.csv
    :header-rows: 1
    :widths: 10, 10, 80

``Data`` nodes SHOULD be preceded by a ``Process`` node describing a data-producing process, such as NMR scanning or DNA sequencing.

**Process nodes**

``Process`` nodes represent the application of a protocol to some input material (e.g. a ``Source``) to produce some output (e.g.a ``Sample``).

``Process`` nodes SHOULD record the following:

.. csv-table::
    :file: _static/model/process_node.csv
    :header-rows: 1
    :widths: 10, 10, 80

``Process`` nodes SHOULD be preceded by zero or more ``Material`` or ``Data`` nodes, and followed by zero or more ``Material`` or ``Data`` nodes.

