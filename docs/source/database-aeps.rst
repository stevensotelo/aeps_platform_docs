AEPS Database
=============

Relational model
----------------

The following picture shows how the database was built and the relation between tables:

.. image:: /_static/img/database/erm.*
  :alt: AEPS Database
  :class: device-screen-vertical side-by-side

Table dictionary
----------------

In the following table you can see the list of all tables:

.. csv-table:: AEPS Tables
  :header: "Table name", "Engine", "Comment"
  :widths: 30, 10, 60
  
  "con_countries","InnoDB","This table has the list of countries"
  "con_municipalities","InnoDB","This table has the list of municipalities - administrative level 3"
  "con_states","InnoDB","This table has the list of states - administrative level 2"
  "far_answers","InnoDB","This table has the forms answers of each production event"
  "far_farms","InnoDB","This table has the information about farms"
  "far_plots","InnoDB","This table has the information about farms plots"
  "far_production_events","InnoDB","This table has the history about production events in"
  "far_responses_bool","InnoDB","This table has the forms answers of each production event for question with the boolean values"
  "far_responses_date","InnoDB","This table has the forms answers of each production event for question with the date values"
  "far_responses_numeric","InnoDB","This table has the forms answers of each production event for question with the numeric values"
  "far_responses_options","InnoDB","This table has the forms answers of each production event for question with the unique or multiple type"
  "far_responses_text","InnoDB","This table has the forms answers of each production event for question with the text values"
  "frm_blocks","InnoDB","This table has the list of blocks or sections to add to the forms"
  "frm_blocks_forms","InnoDB","This table has the relationship between forms and blocks"
  "frm_forms","InnoDB","This table has the list of forms"
  "frm_forms_settings","InnoDB","This table has the list of settings for forms"
  "frm_options","InnoDB","This table has the list of options for questions, the questions have to be unique or multiple"
  "frm_questions","InnoDB","This table has the list of questions for the forms"
  "frm_questions_rules","InnoDB","This table has the list of rules for each question. A rule depends of the application in where is gonna be validated"
  "soc_associations","InnoDB","This table has the information about associations"
  "soc_people","InnoDB","This table has the information about people. It has personal information about farmers and technical assistans"
  "soc_technical_assistants","InnoDB","This table has the information about who people are technical assistants"

Views dictionary
----------------

In the following table you can see the list of all views to extract data from the database:

.. csv-table:: AEPS Views
  :header: "Views name", "Comment"
  :widths: 30, 70
  
  "vw_answers", "This view has information about all answers of the surveys. The answers are separated according of data type."
  "vw_production_events", "This view has information about all production events stored in the database. It has information about farmers, technical assistants, farms and plots."
  "vw_forms", "This view has information about how the surveys are built."
  "vw_answers_ta", "This view is a mix of vw_answers and vw_production_events."