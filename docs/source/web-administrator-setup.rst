Setup
=====

Setup is the module in which you can manage parameters of the platform.

Within setup module, you can:

- Manage associations
- Manage geographic information
- Manage people

Associations
------------

Associations are the entities who manage the collect events. Each
technical assistant have to be related in each collect activity (production event)
to one association.

Within of this module you can see the list of all associations, also you are able to add, edit or delete them.

.. image:: /_static/img/web-administrator-setup/associations.*
  :alt: Associations
  :class: device-screen-vertical side-by-side

Let's see what information is stored inside of an association.

.. csv-table:: Associations
  :header: "Field", "Description"
  :widths: 20, 80
  
  "Name","name of association"
  "Enable","it sets if the form is able (1) or disable (0)"
  "Extern Id","external identificator"
  "Date created","date when it was created"
  "Date updated","date when it was updated"

Countries
---------

Countries are geographic information about where people are located. Each person
should be associated to one country.

Let's see what information is stored inside of a country.

.. csv-table:: Countries
  :header: "Field", "Description"
  :widths: 20, 80
  
  "Name","name of country"
  "Iso 2","ISO 2 Code"
  "Extern Id","external identificator"
  "Date created","date when it was created"
  "Date updated","date when it was updated"

States
------

States are geographic information about where people are located. Each person
should be associated to one state.

Let's see what information is stored inside of a state.

.. csv-table:: States
  :header: "Field", "Description"
  :widths: 20, 80
  
  "Name","name of state"
  "Country","Country in which is located"
  "Extern Id","external identificator"
  "Date created","date when it was created"
  "Date updated","date when it was updated"

Municipalities
--------------

Municipalities are geographic information about where people are located. Each person
should be associated to one municipality.

Let's see what information is stored inside of a municipality.

.. csv-table:: Municipalities
  :header: "Field", "Description"
  :widths: 20, 80
  
  "Name","name of state"
  "State","State in which is located"
  "Extern Id","external identificator"
  "Date created","date when it was created"
  "Date updated","date when it was updated"

People
------

People is the section in which users can see contact information about technicals assistants and farmers.
This module allows to manage information of people who collect data and answer the surveys.

Let's see what information is stored inside of a person.

.. csv-table:: People
  :header: "Field", "Description"
  :widths: 20, 80
  
  "Name","Name"
  "LastName","Last Name"
  "Municipality","Municipality where person was born"
  "Kind Document","Kind of document of the person. It can be N = National, P = Passport, O = Other"
  "Gender","Gender of the person. It can be F = Female, M = Male, O = Other"
  "Document","Number of document of identification"
  "Cellphone","Number of Cellphone"
  "Address","Phisical address where person is living"
  "Email","Email"
  "Extern Id","external identificator"
  "Date created","date when it was created"
  "Date updated","date when it was updated"