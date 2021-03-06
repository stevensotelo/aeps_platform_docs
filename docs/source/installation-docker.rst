Installation with Docker
========================

This chapter guides you through the installation and initial setup of a self-hosted 
instance of all platform from Docker containers. You can find the Dockerfiles into
the Github repository: `<https://github.com/CIAT-DAPA/aeps_platform_docker>`_. Initially you will learn 
how to install individually each component, however in the last part of this tutorial, 
it will show how to install all components together.

You should start cloning the repository from Github:

.. code-block:: console
    :linenos:

    git clone https://github.com/CIAT-DAPA/aeps_platform_docker.git

.. tip::
  The following recommendations should be followed before to execute the commands:

  - Rename the files called .env.example to .env
  - Set real values for the variables into each file .env
  - Check your current position, each container tells to you where you should be
  - Commands have to be executed in command line

AEPS Database (MySQL)
---------------------
AEPS Database is a container based on MySQL engine. 
The folder in which you should be in **cmd** is *aeps_database_mysql*.

.. warning::
  Please open the file **aeps_database_mysql/conf/01_create_db_and_user.sql** and edit the lines 2,3, 
  you have to set the **password** that you want for the **user of the database**.

  .. code-block:: sql
    :linenos:

    create database if not exists `aeps_2_0`;
    create user 'aeps_user'@'%' identified by 'your_password';
    grant all on `aeps_2_0`.* to 'aeps_user'@'%' identified by 'your_password';
    flush privileges;
  
.. code-block:: console
  :linenos:

  # Build the image
  docker build -t stevensotelo/aeps_database_mysql:latest .
  # Create a container like a deamon
  docker run -p 3306:3306 --env-file ./.env --name aeps_db -d stevensotelo/aeps_database_mysql:latest

If you want to check if the container is running correct:

.. code-block:: console
  :linenos:
  
  docker logs aeps_db
  > [Entrypoint] MySQL Docker Image 5.7.21-1.1.4
  > [Entrypoint] Initializing database
  > [Entrypoint] Database initialized
  > Warning: Unable to load '/usr/share/zoneinfo/iso3166.tab' as time zone. Skipping it.
  > Warning: Unable to load '/usr/share/zoneinfo/leapseconds' as time zone. Skipping it.
  > Warning: Unable to load '/usr/share/zoneinfo/tzdata.zi' as time zone. Skipping it.
  > Warning: Unable to load '/usr/share/zoneinfo/zone.tab' as time zone. Skipping it.
  > Warning: Unable to load '/usr/share/zoneinfo/zone1970.tab' as time zone. Skipping it.

  > [Entrypoint] running /docker-entrypoint-initdb.d/01_create_db_and_user.sql


  > [Entrypoint] running /docker-entrypoint-initdb.d/02_aeps_db.sql


  > [Entrypoint] Server shut down

  > [Entrypoint] MySQL init process done. Ready for start up.

  > [Entrypoint] Starting MySQL 5.7.21-1.1.4

.. note::
  Once you have checked that the container is running, you can try connecting from a 
  MySQL Client

AEPS Web management (Linux)
---------------------------
AEPS Web management is a container based on ASP.Net Core 2.2. 
The folder in which you should be in **cmd** is *aeps_web_management*.

.. warning::
  Please open the file **aeps_web_management/site/appsettings.json** and edit the lines 3,4, 
  with the data to connect with **AEPS Database**. The following file is just a test with default parameters, 
  **Please don't use it in productions enviroments**

  .. code-block:: c#
    :linenos:

    {
      "ConnectionStrings": {
        "AEPSDatabase": "server=172.17.0.2;port=3306;user=aeps_user;password=your_password;database=aeps_2_0",
        "AEPSUsersDatabase": "server=172.17.0.2;port=3306;user=aeps_user;password=your_password;database=aeps_2_0"
      },
      "Logging": {
        "LogLevel": {
          "Default": "Warning"
        }
      },
      "Languages": "es-CO,en-US",
      "AllowedHosts": "*",
      "Installed": "false"
    }


.. code-block:: console
  :linenos:

  # Build the image
  docker build -t stevensotelo/aeps_web_management:latest .
  # Create a container like a deamon
  docker run --name aeps_webadmin -p 8000:80 --env-file ./.env -d stevensotelo/aeps_web_management:latest

  # Once you have installed the website from a browser, you have to change the appsettings.json
  # Open command line
  docker exec -it aeps_webadmin bash
  # Opening the file appsettings.json with VIM
  vim appsettings.json

  # Change the file appsettings.json, it should be like this (remember change Connection Strings):
  {
    "ConnectionStrings": {
      "AEPSDatabase": "server=172.17.0.2;port=3306;user=aeps_user;password=your_password;database=aeps_2_0",
      "AEPSUsersDatabase": "server=172.17.0.2;port=3306;user=aeps_user;password=your_password;database=aeps_2_0"
    },
    "Logging": {
      "LogLevel": {
        "Default": "Warning"
      }
    },
    "Languages": "es-CO,en-US",
    "AllowedHosts": "*",
    "Installed": "true"
  }
  # To saved the file you should type the following command:
  # :wq!

  # Now we have to restart the container
  exit
  docker restart aeps_webadmin

.. tip::
  You should check the section Install of the AEPS WEB ADMINISTRATOR while you are trying to install the website

AEPS ETL
--------

AEPS Superset
-------------
AEPS Superset is a container based on Python 3 and Node. 
The folder in which you should be in **cmd** is *aeps_visualization_superset*.

.. warning::
  Please open the file **aeps_visualization_superset/conf/superset_config.py** and edit all lines with your custom values.
  The following file is just a test with default parameters, **Please don't use it in productions enviroments**

  .. code-block:: python
    :linenos:

    MAPBOX_API_KEY = 'your_key'
    #CACHE_CONFIG = {
    #    'CACHE_TYPE': 'redis',
    #    'CACHE_DEFAULT_TIMEOUT': 300,
    #    'CACHE_KEY_PREFIX': 'superset_',
    #    'CACHE_REDIS_HOST': 'redis',
    #    'CACHE_REDIS_PORT': 6379,
    #    'CACHE_REDIS_DB': 1,
    #    'CACHE_REDIS_URL': 'redis://redis:6379/1'}
    SQLALCHEMY_DATABASE_URI = 'mysql://aeps_user:your_password@mysql:3306/aeps_2_0'
    SQLALCHEMY_TRACK_MODIFICATIONS = True
    HTTP_HEADERS = {'X-Frame-Options': 'ALLOWALL'}

.. code-block:: console
  :linenos:

  # Build the image
  docker build -t stevensotelo/aeps_superset:latest .
  # Create a container like a deamon
  docker run -p 8088:8088 --name aeps_vz -d stevensotelo/aeps_superset:latest


