AEPS ETL
========

AEPS :dfn:`ETL` (Extract, Transform and Load)  is the module
which allows to extract the collected data in field and save
into the central database. This module works in three steps:

1. Extracting information from raw data (those files could be
   Excel file, text file, i.e.).
2. Transforming information in the database format.
3. Loading of the data in the database. This step is splitted 
   by two steps more: insert and update of records.