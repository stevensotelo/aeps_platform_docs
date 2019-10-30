Administrator guide
===================

This document describes how to set the configuration with **ODK Tools** 
in order to be able for collecting information of production events 
with a site-specific agriculture approach. 
This guide was designed for people who have the **administrator role**. 
An *administrator* is the person who is in charge of distributing the surveys 
and centralizing the data collected by the collectors users.

Preparing surveys
-----------------
The administrator should prepare the surveys before to share with users.
Preparing files is a process that allows to administrators configure and customize
the parameters of the surveys. The file in which is easy to make those changes
are in Excel files (*[my_survey].xlsx* or *[my_survey].xls*), however administrator
can make the changes in [my_survey].xml. We will focus in Excel files.

- **Set the url for submission answers**:

.. seealso::
  You can see a list of surveys in :doc:`collect-odk-v1`

Sharing surveys
---------------

Currently, we have different ways to share the form to these users such as: 
Implement an Aggregate ODK server, use Google Drive, distribution through a file, etc.
We have documented the following methods to spread forms:

- :doc:`collect-odk-v1-administrator-googledrive`
- :doc:`collect-odk-v1-administrator-file`