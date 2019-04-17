Conduit DB Migration
---------------------

If your new installation is part of a migration or you need to move the data from your original Conduit database, this is easily accomplished by using a stateful dump.

To begin this, stop the Conduit UI on your original Conduit server:

.. code-block:: bash

 [root@app-server-old ~] conduit-ctl stop conduit-ui

Once this is done you can safely export. To access the MySQL shell we will need the password for the Conduit DB user. We can find this in the conduit-secrets file:

.. code-block:: bash

  [root@app-server-old ~] cat /etc/conduit/conduit-secrets.json | grep conduit_password
  "conduit_password": "451e122cr5d122asw3de5e1b", <---------------this one
  "conduit_password": "9b5vdj4de5awf87d",

Take note of the first ``conduit_password`` as it will be used to invoke a dump. Conduit provides embedded binaries for this task. Invoke it via the embedded path and specify the host. In this example we are using the conduit database on the MySQL listening on localhost. Enter the password copied from the previous step when prompted:

.. code-block:: bash

  [root@app-server-old ~] /opt/conduit/embedded/mysql/bin/mysqldump -u conduit -h 127.0.0.1 conduit -p > /tmp/conduit_backup.sql
  Enter password:


This file needs to be pushed to the new Conduit Installation's backend. Depending on the GRANTS in the new MySQL backend, this will likely require moving this file to one of the new Conduit frontend servers.

Once the file is in place it can be imported into the backend. Begin by ensuring the Conduit UI service is stopped on all of the application servers:

.. code-block:: bash

 [root@app-server-new ~] conduit-ctl stop conduit-ui

Then you can import the MySQL dump into the target database using the embedded MySQL binaries, specifying the database host, and entering the password for the conduit user when prompted:

.. code-block:: bash

  [root@app-server-new ~] /opt/conduit/embedded/mysql/bin/mysql -u conduit -h 10.1.2.2 conduit -p < /tmp/conduit_backup.sql
  Enter password:

The data form the old appliance is now replicated on the new appliance. Simply start the UI to complete the process:

.. code-block:: bash

  [root@app-server-new ~] conduit-ctl start conduit-ui
