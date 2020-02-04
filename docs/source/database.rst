Introduction
============

It is the database component, which was designed for Transactional SQL systems and built in My SQL. 
This schema was designed for offering a dynamic structure to manage complex surveys for agriculture.
We have 3 potential databases:

* AEPS Database: That database stores all information about agronomy practices of the platform.
* AEPS Users: It has information about the Users. They are generate from ASP.NET Core Identity.
* Superset management: It has all tables that are used in **Superset** application.

.. tip::
  All databases can be stored in the same engine, even within the same database.