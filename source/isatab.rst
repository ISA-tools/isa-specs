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

.. toctree::
   :maxdepth: 2
   :titlesonly:

   Investigation file <isatab-investigation>
   Study Table file <isatab-tables>
   Assay Table file <isatab-tables>
   Data files <isatab-data>