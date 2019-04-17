CentOS
------

To get started installing |conduit| on CentOS a few preparatory items should be addressed first.

#. Configure firewalld to allow access from users on port 80 or 443 (Or remove firewall if not required).
#. Make sure the machine is self resolvable to its own hostname.

   .. IMPORTANT:: If the machine is unable to resolve its own hostname ``nslookup hostname`` some installation commands will be unable to verify service health during installation and fail.

#. Next simply download the relevant ``.rpm`` package for installation. This package can be acquired from your account rep or via a free trial request from |conduithub|.

   .. TIP:: Use the ``wget`` command to directly download the package to your appliance server. i.e. ``wget https://downloads.goconduit.com/path/to/package.rpm`` THIS IS NOT THE PACKAGE URL. The package URL can be acquired from your account rep or via a free trial request from |conduithub|

#. Next we must install the package onto the machine and configure the conduit services:

   .. code-block:: bash

    sudo rpm -i conduit-appliance-x.x.x-1.x86_64.rpm
    sudo conduit-ctl reconfigure

#. Once the installation is complete the web interface will automatically start up. By default it will be resolvable at ``https://your_machine_name`` and in many cases this may not be resolvable from your browser. The url can be changed by editing ``/etc/conduit/conduit.rb`` and changing the value of ``appliance_url``. After this has been changed simply run :

   .. code-block:: bash

     sudo conduit-ctl reconfigure
     sudo conduit-ctl stop conduit-ui
     sudo conduit-ctl start conduit-ui

   .. note:: The conduit-ui can take 2-3 minutes to startup before it becomes available.

There are additional post install settings that can be viewed in the Advanced section of the guide.

Once the browser is pointed to the appliance a first time setup wizard will be presented. Please follow the on screen instructions by creating the master account. From there you will be presented with the license settings page where a license can be applied for use (if a license is required you may request one or purchase one by contacting your sales representative).

More details on setting up infrastructure can be found throughout this guide.

.. TIP:: If any issues occur it may be prudent to check the conduit log for details at ``/var/log/conduit/conduit-ui/current``.
