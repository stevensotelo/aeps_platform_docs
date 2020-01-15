Configuration
=============

The ETL module has many standard configuration files,
which are the main parameters to execute all process of transforming data.
In this chapter, we will describe which are those parameters.
It was designed for working with *datasources* in Excel format.

.. tip::
  **Form**: refers to the overview. The questions about farmers, technical assistants 
  and farms are in the head of the form.

  **Survey**: refers to the questions that are related with the production events.


Parameters
----------

The parameters are in the file **configuration.xlsx**.
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
  :header: "Column","Description"

  "parent_table","It is the name of the table which is the parent table"
  "parent_field","It is the field which will be used to find the id of the parent record"
  "child_table","It is the name of current table which is being processed"
  "child_field","It is the field which is the foreign key in the current table"

.. note::
  We have to do this because in most of the cases we don’t have the id of each table directly, 
  so it is a method to relate tables without lose information.

.. warning::
  You have to take into account what you configured in this section, because you have set the same
  fields like keys in the **form** section (*you will see forward*). The foreign keys that you set here,
  should be setted in the form section. It is because the ETL will use those fields to connect them
  across the tables, if they wouldn't match, it won't import nothing to the database.

- **additional**: This sheet set for which tables the ETL has to add default information.

.. csv-table:: Additional
  :header: "Column", "Description"
  :widths: 20, 80

  "table","This column has the list of the database tables"
  "register_date","This column set if for the records imported for the table, it should add information about *created* and *updated* fields. It will take the current date from the system. The values can be **0** (not add) or **1** (add)"
  "has_enable","This column set by default *enable* to tables with have this flag. This flag just should be enable for the tables which has the field enable. The values can be **0** (not add) or **1** (add)"

ETL Configuration
-----------------

The ETL configuration is in the file **form.xlsx**.
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

- **survey**: This sheet has the configuration of the survey. It relates the blocks and 
  questions, which are required in the survey with the questions in the database, they
  are related through identifiers of each side.

.. csv-table:: Survey
  :header: "Column", "Type", "Description"
  :widths: 20, 10, 70

  "block","string","This field refers to blocks of questions. It has the **machine name** of the block. The value should be the same in the field *name* of the table *frm_blocks*"
  "repeat","int","This field is required to know of the block repeat inside of the survey. If value is **0**, it means the the block of questions won't repeat again, otherwise this field should have the value **1**."
  "id","int","It is the id of the question inside of the database (*frm_questions*)."
  "question","string","This field refers to blocks of questions. It has the **machine name** of the question. The value should be the same in the field *name* of the table *frm_questions*"
  "type","string","It is the value type from source. The value can be: **unique, string, int, double, date, multiple, key**"

- **transformations**: This sheet has the rules to transform raw data in new data.
  It allows to change the final value of the surveys questions, with a set of functions 
  available. Those transformation will be applied in the **translate** process. 

.. csv-table:: Transformations
  :header: "Column", "Type", "Description"
  :widths: 20, 10, 70

  "table","string","it is the table's name. When table is parted of the *form* the value is the name of the table, however when table is parted of *survey* it should has the value **survey**"
  "field","string","it is the column's name in which you will apply the transformation. For the *form* fields, it will take the column's name into the database, however when table is parted of *survey* it should has the **machine name (value of the field name inside of the table frm_questions)**."
  "type","string","it is the name of the function which will be applied to the field. See the following table to know which are available."
  "value","","it will take a different behavior depending of the **type**"
  "transform","","it will take a different behavior depending of the **type**"
  "conditions","","it will take a different behavior depending of the **type**"
  "units","","it will take a different behavior depending of the **type**"

.. csv-table:: List of type of the transformations
  :header: "Value", "Description"
  :widths: 20, 80

  "replace","it will replace a the value in the column **value** for the column **transform**"
  "split","it will split the value of the column in two. The pattern to split will be taken of the **value** and the second value will be set in the column of **transform**."
  "add","it will add a new column. It will creates a new column (the column name will be taken from **field**) and set value **transform**."
  "unit","it will set the units for the columns. It will take the value from the column **transform** and set to the unit to the column in **field**"
  "multiply","it will multiply the column by a number. It will take the value in **field** and multiply time **transform**, then it will set the value **final_value**. It will take some consideration according to field **condition**, if the value is **unit**, it will apply the multiply depending of the value in the column **units**."

- **validations**: This sheet has the rules which the ETL will check before to approve some record.
  This verification will be checked in the **translate** process. 

.. csv-table:: Validations
  :header: "Column", "Type", "Description"
  :widths: 20, 10, 70

  "table","string","it is the table's name. When table is parted of the *form* the value is the name of the table, however when table is parted of *survey* it should has the value **survey**"
  "field","string","it is the column's name in which you will be checked. For the *form* fields, it will take the column's name into the database, however when table is parted of *survey* it should has the **machine name (value of the field name inside of the table frm_questions)**."
  "type","string","it is the name of the type of validation which will be checked in the field. See the following table to know which are available."
  "condition","",""
  "condition_field","",""
  "condition_value","",""
  "expression","string","It is a regular expression which will be validated for the field."
  "message","string","It is the message that will be showed to user when the record fail the validation process."

.. csv-table:: List of type of validations
  :header: "Value", "Description"
  :widths: 20, 80

  "required","It will check that the value is not null or empty."
  "reg_exp","It will check that the value accomplish the format. The regular expression will be taken from **expression**"
