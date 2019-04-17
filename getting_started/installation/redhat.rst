RHEL
----

To get started installing |conduit| on RHEL 7 a few prerequisite items are required.

#. Configure firewalld to allow access from users on port 80 or 443 (Or remove firewall if not required).
#. Make sure the machine is self resolvable to its own hostname.
#. For RHEL, In order for the guacamole service (remote console) to properly install some additional optional repositories first need added.

   *  **RHEL 7.x Amazon:** ``yum-config-manager --enable rhui-REGION-rhel-server-optional``
   *  **RHEL 7.x:** ``yum-config-manager --enable rhel-7-server-optional-rpms``

   .. note:: For Amazon users a redhat subscription is not required if the appropriate yum REGION repository is added instead as demonstrated above.

.. IMPORTANT:: If the machine is unable to resolve its own hostname ``nslookup hostname`` some installation commands will be unable to verify service health during installation and fail.

The RedHat Enterprise Linux 7 server needs to be registered and activated with Redhat subscription. The server optional rpms repo needs to be enabled as well.

To check if the server has been activated please run the subscription-manager version. Subscription manager will return the version plus the python dependency version.

If the server has not been registered and activated then the subscription manager version will return the below message.

.. code-block:: bash

   sudo subscription-manager version
   server type: This system is currently not registered
   subscription management server: 0.9.51.24.-1
   subscription-manager: 1.10.14-7.el7 python-rhsm: 1.10.12-2.el7

When a server has been registered and activated with Redhat the subscription manager will return the below message.

.. code-block:: bash

  sudo subscription-manager version
  server type: Red Hat Subscription Management
  subscription management server: 0.9.51.24-1
  subscription-manager: 1.10.14-7.el7 python-rhsm: 1.10.12-2.el7

If the subscription manager re-turns the message ``This system is currently not registered`` please follow the below steps to register the server.

.. TIP:: To register the server you will need to have sudo permissions [Member of the Wheel group] or root access to the server. You will also need your Redhat registered email address and password.

subscription-manager register

.. code-block:: bash

  sudo subscription-manager register
  Username: redhat@example.com
  Password: . subscription-manager auto --attach

.. NOTE:: This can take a minute to complete

.. code-block:: bash

  sudo subscription-manager attach --auto

  Installed Product Current Status: Product Name: Red Hat Enterprise Linux
  Server Status: Subscribed

To check to see if the RHEL server has the Red Hat Enterprise Linux 7 Server - Optional (RPMs) repo enabled please run the following command to return the repo status.

.. TIP:: To check the server repos you will need to have sudo permissions [Member of the Wheel group] or root access to the server.

.. code-block:: bash

  sudo yum repolist all | grep "rhel-7-server-optional-rpms" rhel-7-server-optional-rpms/7Server/x86_64 disabled

If the repo status was returned as disabled then you will need to enable the repo using the subscription manager like below.

.. code-block:: bash

  sudo subscription-manager repos --enable rhel-7-server-optional-rpms
  Repository 'rhel-7-server-optional-rpms' is enabled for this system.

The message ``Repo 'rhel-7-server-optional-rpms' is enabled for this system.`` will appear after enabling the repo. This will confirm that the repo has been enabled.

Next simply download the relevant ``.rpm`` package for installation. This package can be acquired from your account rep or via a free trial request from |conduithub|.

.. TIP:: Use the ``wget`` command to directly download the package to your appliance server. i.e. ``wget https://downloads.conduitdata.com/path/to/package.rpm``

Next we must install the package onto the machine and configure the conduit services:

.. code-block:: bash

  sudo rpm -i conduit-appliance_x.x.x-1.amd64.rpm
  sudo conduit-ctl reconfigure

Once the installation is complete the web interface will automatically start up. By default it will be resolvable at ``https://your_machine_name`` and in many cases this may not be resolvable from your browser. The url can be changed by editing ``/etc/conduit/conduit.rb`` and changing the value of ``appliance_url``. After this has been changed simply run:

.. code-block:: bash

  sudo conduit-ctl reconfigure
  sudo conduit-ctl stop conduit-ui
  sudo conduit-ctl start conduit-ui

.. NOTE:: The ``conduit-ui`` can take 2-3 minutes to startup before it becomes available.

There are additional post install settings that can be viewed in the Advanced section of the guide.

Once the browser is pointed to the appliance a first time setup wizard will be presented. Please follow the on screen instructions by creating the master account. From there you will be presented with the license settings page where a license can be applied for use (if a license is required you may request one or purchase one by contacting your sales representative).

More details on setting up infrastructure can be found throughout this guide.

.. TIP:: If any issues occur it may be prudent to check the conduit log for details at ``/var/log/conduit/conduit-ui/current``.
