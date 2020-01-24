Install
=======

In this chapter you will learn how to install the website.
The installation is the process in which you have to create the first
user, he will be the administrator of all platform.

.. tip::
  You should check the variable's value **Installed** inside of **appsettings.json**, 
  if it is **true**, it means that the website was configured, however if it is equals to **false**,
  you have to create the admin user.

.. image:: /_static/img/web-administrator-install/install.*
  :alt: Installation
  :class: device-screen-vertical side-by-side

The instructions to install the website are the following:

1. Check the *appsettings.json* file and the value of the variable *Installed*, it should be with value *false*
2. Check the *Connection Strings* of the database and setup them
3. Start the website
4. Create the administrator user
5. Change the value of the variable *Installed* to *true*
6. Restart the website
7. Log in into the website with that administrator user

The final status of the *appsettings.json* should be like that:

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
      "Installed": "true"
  }