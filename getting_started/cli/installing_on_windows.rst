Installing on Windows
---------------------------------------

The conduit cli is capable of running on many platforms due to its ruby runtime. This includes windows based platforms. To get started, we must first ensure ruby is running on the windows machine in question. To do this please visit :ref:`ruby-prerequisite` and download at least Ruby version 2.2.0 (2.3.3 recommended).

  .. note::
      When installing ruby on windows, make sure the options are selected for adding the ruby binaries to your PATH.

Now that ruby is installed, simply open a PowerShell window and run

    .. code-block:: text

      gem install conduit-cli --no-ri --no-rdoc

A list of installed dependencies should start sliding by the screen. Once this has completed the CLI setup is complete. Now all that must be done is configuring the cli to point to an appliance for use.

    .. code-block:: text

      conduit remote add myapp https://applianceUrl
      conduit remote use myapp
      conduit login

Credentials are used to acquire an access token which is then stored in the users home directory in a folder called .conduit. Now all commands provided by the CLI are available for use just as if running in a *nix based environment.
