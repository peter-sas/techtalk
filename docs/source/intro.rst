Introduction
============

Challenges
----------
Unlike XML or JSON, PDF document is unstructured with extensive information embedded. 
Even with plenty of Python libraries around, it's still challenging to properly extract tabular data from PDF.

Here are some challenges observed through the PDF attached below.
   * Sparse table layout
   * No separating lines or delimiters between columns
   * Multiple-level headers
   * Parsing the converted text files could be error-prone

   .. image:: images/pdf_table_example.PNG
      :alt: Tabular data in a PDF document

Dependencies
------------

The PDF table extractor module is built on the following Python libraries.
   * `pdfquery <https://github.com/jcushman/pdfquery>`_
      Used to identify page dimension and locate coordinates by keywords.
   * `tabula-py <https://github.com/chezou/tabula-py>`_
      A wrapper to tabula-java. Used to extract table from PDF directly.
   * `pandas <https://pandas.pydata.org/pandas-docs/stable/>`_
      PDF table is returned as a Pandas DataFrame.
   