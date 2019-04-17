Upgrading
==========

|conduit| provides a very simple and convenient upgrade process. In
most cases it is simply a matter of installing the new package on top of
itself and reconfiguring the services.

.. IMPORTANT:: All services except the conduit-ui must be running during a reconfigure. The conduit-ui also must be restarted or stopped and started during an upgrade. Failure to do so will result in errors.

Debian / Ubuntu
---------------

Simply download the latest package or request the latest package from
your account service representative.

Then run the install process as follows:

.. code-block:: bash

  sudo dpkg -i conduit-appliance_x.x.x-1.amd64.deb
  sudo conduit-ctl stop conduit-ui
  sudo conduit-ctl reconfigure
  sudo conduit-ctl start conduit-ui

This typically is enough to complete a full upgrade. Databases will
automatically be migrated upon restart of the application and service
version upgrades will automatically be applied.

CentOS / RHEL
-------------

Yum based package upgrades are a little different. In this case we want
to run a ``rpm -U`` command as the package manager is slightly
different.

.. code-block:: bash

  sudo rpm -U conduit-appliance-x.x.x-1.x86_64.rpm
  sudo conduit-ctl stop conduit-ui
  sudo conduit-ctl reconfigure
  sudo conduit-ctl start conduit-ui

.. TIP:: Sometimes it may be necessary to restart all appliance services on the host. In order to do this simply type ``sudo conduit-ctl restart``. This will restart ALL services.

.. IMPORTANT If you are upgrading and have modified the java keystore you will have to do the following steps to import trusted certificates to |conduit|

.. include ssl-import.rst

Deploy WAR file
---------------

Download the war file
^^^^^^^^^^^^^^^^^^^^^

.. code-block:: text

    wget <url>

Move the file
^^^^^^^^^^^^^

.. code-block:: text

    mv <file> /opt/conduit/lib/conduit/conduit-ui.war 

Change permissions
^^^^^^^^^^^^^^^^^^

.. code-block:: text

    chown conduit-app.conduit-app /opt/conduit/lib/conduit/conduit-ui.war

Restart UI
^^^^^^^^^^

.. code-block:: text

    conduit-ctl restart conduit-ui

