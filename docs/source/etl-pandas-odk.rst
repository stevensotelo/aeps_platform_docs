Pandas (ODK)
============

It is a implementation of an ETL in Pandas (Python enviroment).
Currently, **it is just working to process files from ODK in Excel format**.
It has a set of scripts which are available at: https://github.com/CIAT-DAPA/aeps_platform_etl/tree/dev/src/python

Translation
-----------

It is the process which takes the raw data and transforms them in files with
the database estructure. Overall, it loads the parameters, then
get raw data and set the configurations values, then it stablishes
connection with the database. Once it is ready, starts to process
the form (*you can see more information forward*), in order to do that,
it checks the tables related about the general information, once
it has processed the form, starts to process the survey. Those steps
are repeated for all datasources. The following picture show the general 
process followed by this ETL:

.. image:: /_static/img/etl-pandas/translation.*
  :alt: Translation process
  :class: device-screen-vertical side-by-side

- **Process form**: 
- **Process survey**: