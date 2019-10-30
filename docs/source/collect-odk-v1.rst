AEPS Collect data - ODK (version 1)
===================================

The forms are created using the `XLSForm standard <https://xlsform.org/en/>`_, then are 
transformed with the `ODK XLSForm tool <https://opendatakit.org/xlsform/>`_
for the generation of XML files.

.. tip::
  The form that is distributed to users who collect the information is **[my_survey].xml**. 
  This file is interpreted by ODK Collect to deploy the controls and allow users to collect data.
  The form structure is found in the document **[my_survey].xlsx**.   

We have developed a list of forms which are available at: https://github.com/CIAT-DAPA/aeps_platform_forms/tree/develop/odk

.. csv-table:: Forms
  :header: "Category", "Name", "File name", "Developed by", "Description"
  :widths: 20, 20, 10, 20, 40

  "Crops","Rice production events","aeps_production_event", "CIAT", ""

The forms can be edited according to the needs of each implementation
following the rules of `XLS Form <http://xlsform.org/en/>`_. 
Files are transformed into XML using the online tool https://opendatakit.org/xlsform/.
For more information about Open Data Kit (ODK) you can consult the official documentation 
at: https://docs.opendatakit.org/.

.. toctree::
  :hidden:
  :maxdepth: 1

  collect-odk-v1-administrator
  collect-odk-v1-administrator-googledrive
  collect-odk-v1-administrator-file