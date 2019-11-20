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
      :height: 350
      :width: 700
      :alt: Tabular data in a PDF document

Background Knowledge
--------------------
Object coordinates
^^^^^^^^^^^^^^^^^^
   * The origin (0, 0) point is located in the bottom left corner.
   * Unit: point (1 inch = 72 points).

   .. image:: images/pdf_coords.png
      :height: 237
      :width: 420

Locate an object by coordinates
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
   1. Use coordinates (left, bottom, right, top).
   2. `pdfquery <https://github.com/jcushman/pdfquery>`_ follows this rule.

   .. image:: images/loc_object.png
      :height: 331
      :width: 251

Libraries for table extraction
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
   * Tabula and camelot both do a great job. 
   * But the default table detection doesn't work well.
   * They use **(top, left, bottom, right)** to locate table area, rather than (left, bottom, right, top).

Tabula-py
^^^^^^^^^
   * Core function::
   
      read_pdf(pdf_path, pages=page, area=[tbl_area_blue], 
	           pandas_options=ath_headers, guess=False)
   * Again, coordinates has to be **(top, left, bottom, right)**.
   * Extraction method: *stream* or *lattice*?
   * Returns the table as pandas DataFrame.
   * Top and bottom are calculated in another direction around.

      * top = page height – coordinate top
      * bottom = page height – coordinate bottom

      .. image:: images/tabula_coords.png
         :height: 384
         :width: 674

Artifacts
---------
Generic modules/ functions
^^^^^^^^^^^^^^^^^^^^^^^^^^

   * Return coordinates (left, bottom, right, top) of LTTextBox by keyword::
   
      get_textbox_coords(pdf_path, page, keyword="")

   * Return page dimensions (width, height)::

      get_page_dims(pdf_path, page)

Dependencies
------------

The PDF table extractor module is built on the following Python libraries.
   * `pdfquery <https://github.com/jcushman/pdfquery>`_
      Used to identify page dimension and locate coordinates by keywords.
   * `tabula-py <https://github.com/chezou/tabula-py>`_
      A wrapper of tabula-java. Used to extract table from PDF directly.
   * `pandas <https://pandas.pydata.org/pandas-docs/stable/>`_
      PDF table is returned as a Pandas DataFrame.

Comparison
----------
* Advantage
   * Accurate results as along as the table area is specified properly
   * Possible to automate

References
----------

* `PDF Page Coordinates <https://www.pdfscripting.com/public/PDF-Page-Coordinates.cfm>`_
