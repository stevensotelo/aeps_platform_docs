Configuration
=============

The ETL module has many standard configuration files,
which are the main parameters to execute all process of transforming data.
In this chapter, we will describe which are those parameters.
It was designed for working with *datasources* in Excel format.

Main configuration
------------------

The main configurataion is in the file **configuration.xlsx**.
This file has the global parameters to execute the transforming process.
It has information about how to connect with database, how are the relation
between tables into database and some additional specific conditions for each
table. Let's see what each sheet has:

- **global**: This sheet has the global parameters for the ETL. It has the parameters
  to connect directly with database and the type of process to execute.

.. csv-table:: Variables
  :header: "Parameter", "type", "Description"
  :widths: 20, 10, 70
  
  "database_user","string","Name of user to connect with database"
  "database_pwd","string","Password of the user to connect with database"
  "database_host","string","IP or hostname of the server in which is the database"
  "database_port","int", "Port in which is available the database in the server"
  "database_schema","string", "Name of the database. By default is: aeps_2_0"
  "type_process","string", "It sets the kind of process to execute. The values can be: **full**: It execute the three steps"

- **dependencies**: This sheet has the relationship between tables of the database. 
  The first row has the tables names, the first column has also the tables names.
  The values, which instersect tables, are the references about how the *ETL* should connect
  data from the source. The values are composed in the following way:
  the first value is the *column name* of the top table (it is the name of the 
  foreign key for the table that we are relating both tables), the second value
  is the *column name* of the table in the row, which the ETL has to search the 
  id. The following is an example of this sheet:

.. csv-table:: Dependencies
  :header: "Table","soc_associations","con_countries","con_states","con_municipalities","soc_people","soc_technical_assistants","far_farms","far_plots","far_production_events","far_responses_bool","far_responses_date","far_responses_numeric","far_responses_options","far_responses_text"

  "soc_associations","","","","","","association-ext_id","","","","","","","",""
  "con_countries","","","country-ext_id","","","","","","","","","","",""
  "con_states","","","","state-ext_id","","","","","","","","","",""
  "con_municipalities","","","","","municipality-ext_id","","","","","","","","",""
  "soc_people","","","","","","person-document","farmer-document","","technical-document","","","","",""
  "soc_technical_assistants","","","","","","","","","technical-person","","","","",""
  "far_farms","","","","","","","","farm-ext_id","","","","","",""
  "far_plots","","","","","","","","","plot-ext_id","event-ext_id","event-ext_id","event-ext_id","event-ext_id","event-ext_id"
  "far_production_events","","","","","","","","","","event-plot","event-plot","event-plot","event-plot","event-plot"
  "far_responses_bool","","","","","","","","","","","","","",""
  "far_responses_date","","","","","","","","","","","","","",""
  "far_responses_numeric","","","","","","","","","","","","","",""
  "far_responses_options","","","","","","","","","","","","","",""
  "far_responses_text","","","","","","","","","","","","","",""

.. note::
  We have to do this because in most of the cases we don’t have the id of each table directly, 
  so it is a method to relate tables without lose information

- **additional**: This sheet set for which tables the ETL has to add default information.

.. csv-table:: Additional
  :header: "Column", "Description"
  :widths: 20, 80

  "table","This column has the list of the database tables"
  "register_date","This column set if for the records imported for the table, it should add information about *created* and *updated* fields. It will take the current date from the system. The values can be **0** (not add) or **1** (add)"
  "has_enable","This column set by default *enable* to tables with have this flag. This flag just should be enable for the tables which has the field enable. The values can be **0** (not add) or **1** (add)"

Survey configuration
--------------------

The survay configuration is in the file **form.xlsx**.
This file has the configuration about how to extract information from the source,
how transform the raw data into database tables. Let's see what each sheet has:

- **form**: This sheet has the relationship between datasource and database.
  It sets how each field from source is related with the tables columns.  
  Like you will see, this configuration is just for main tables, *it doesn't 
  take into account a configuration for the surveys*.

.. csv-table:: Form
  :header: "Column", "Description"
  :widths: 20, 80

  "form_sheet","This column has the sheet's name in which is data in the source"
  "form_field","This column has the name of column in the source"
  "form_key","It sets if the column is key in the source"
  "soc_associations","This column is to set a relationship from source and table *soc_associations*. The values in this column are the columns names of the table"
  "con_countries_1","This data is for identifying **technical assistants**. This column is to set a relationship from source and table *con_countries*. The values in this column are the columns names of the table"
  "con_countries_2","This data is for identifying **farmers**. This column is to set a relationship from source and table *con_countries*. The values in this column are the columns names of the table"
  "con_states_1","This data is for identifying **technical assistants**. This column is to set a relationship from source and table *con_states*. The values in this column are the columns names of the table"
  "con_states_2","This data is for identifying **farmers**. This column is to set a relationship from source and table *con_states*. The values in this column are the columns names of the table"
  "con_municipalities_1","This data is for identifying **technical assistants**. This column is to set a relationship from source and table *con_municipalities*. The values in this column are the columns names of the table"
  "con_municipalities_2","This data is for identifying **farmers**. This column is to set a relationship from source and table *con_municipalities*. The values in this column are the columns names of the table"
  "soc_people_1","This data is for identifying **technical assistants**. This column is to set a relationship from source and table *soc_people*. The values in this column are the columns names of the table"
  "soc_people_2","This data is for identifying **farmers**. This column is to set a relationship from source and table *soc_people*. The values in this column are the columns names of the table"
  "soc_technical_assistants","This column is to set a relationship from source and table *soc_technical_assistants*. The values in this column are the columns names of the table"
  "far_farms","This column is to set a relationship from source and table *far_farms*. The values in this column are the columns names of the table"
  "far_plots","This column is to set a relationship from source and table *far_plots*. The values in this column are the columns names of the table"
  "far_production_events","This column is to set a relationship from source and table *far_production_events*. The values in this column are the columns names of the table"
