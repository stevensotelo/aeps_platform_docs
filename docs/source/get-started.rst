Get started with AEPS 2.0
=========================

This project has the following repositories in Github:

* `<https://github.com/CIAT-DAPA/aeps_platform>`_: This repository has the website to configure the platform.
* `<https://github.com/CIAT-DAPA/aeps_platform_db>`_: This repository has the databases scripts of the platform.
* `<https://github.com/CIAT-DAPA/aeps_platform_forms>`_: This repository has the surveys that have been created to collect data.
* `<https://github.com/CIAT-DAPA/aeps_platform_etl>`_: This repository has the scripts to transform data from source and save records into the database.
* `<https://github.com/CIAT-DAPA/aeps_platform_docker>`_: This repository has the docker files to create the images of all components.
* `<https://github.com/CIAT-DAPA/aeps_platform_docs>`_: This repository has the documentation about all platform.

How does it work?
-----------------

The process start when farmers, technical assistants, researchers and others collect data in the field. Once they have
collected data (could be online or offline) they should send this information to central repository, this process
we called sync data. Then an administrator user should takes those data and pass them through a set of pipes,
which ones will clear data. In the process of transforming the system applies a set of filters and rules in order to 
assurance the quality data, then it will save all records into a central database. 

Once the data are stored into the database, they are ready to be anaylized with many methodologys: Bussines intelligence,
Machine Learning, Artifical intelligence, etc. When the results are ready, we can show them through interactive plots that
users can understand.

The following picture shows how the general process is:

.. image:: /_static/img/get-started/process.*
  :alt: General process
  :class: device-screen-vertical side-by-side



