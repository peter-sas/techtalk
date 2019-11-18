User Guide
==========

Get the codebase
----------------
Clone the git reposotory at `COC Gitlab Repo <https://gitlab.sas.com/coc/code.git>`_.

Usage
-----
Below is sample code to demonstrate the usage.::

   from coc.modules.pdfFile import get_textbox_coords, get_page_dims
   from tabula import read_pdf
   
   col_cos_name = get_textbox_coords(pdf_path, page, keyword="Name")
   col_cos_totals = get_textbox_coords(pdf_path, page, keyword="Totals")
   pg_dims = get_page_dims(pdf_path, page)
   tbl_top = pg_dims['height'] - col_cos_name[0][3]
   tbl_bottom = pg_dims['height'] - col_cos_totals[0][1]
   tbl_right = pg_dims['width']
   tbl_area = [tbl_top, 0, tbl_bottom, tbl_right]
   ath_white_df = read_pdf(pdf_path, pages=page, area=[tbl_area_white],
                  pandas_options={"dtype": str}, guess=False, stream=True)
