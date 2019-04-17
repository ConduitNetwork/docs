|conduit| UI not loading after upgrade or reconfigure
======================================================

Problem:
  The |conduit| ui does not load after performing an upgrade.

Common Causes:
   #. The conduit-ui has not finished loading
   #. The conduit-ui was not fully stopped before reconfigure, or not started after reconfigure
   #. |conduit| was forced to restart or shut down while the database schema was being migrated during an upgrade

Solutions:
  #. The conduit-ui has not finished loading.

      An easy way to see when the ui is finished loading and running is to tail the ui current file and look for the conduit logo with version and start time

      .. code-block:: bash

        conduit-ctl tail conduit-ui

  .. NOTE:: After running `conduit-ctl start conduit-ui`, the |conduit| ui takes around 3 minutes to run depending on hardware.

  #. The conduit-ui was not fully stopped before reconfigure, or not started after reconfigure

      The conduit ui must be stopped prior to running conduit-ctl reconfigure when upgrading. Sometimes running conduit-ctl stop conduit-ui will timeout and the ui is not actually stopped. If stopping the ui does timeout, run conduit-ctl kill conduit-ui prior to reconfigure, and be sure to run conduit-ctl start conduit-ui after reconfigure is completed.


      If you ran a reconfigure before stopping the ui, run:

      .. code-block:: bash

        sudo conduit-ctl kill conduit-ui
        sudo conduit-ctl reconfigure
        sudo conduit-ctl start conduit-ui

      Wait for the ui to come up.

  #. |conduit| was forced to restart or shut down while the database schema was being migrated during an upgrade

      If the ui fails to start and you see the error ``Invocation of init method failed; nested exception is liquibase.exception.LockException: Could not acquire change log lock.  Currently locked by conduit`` it likely means conduit was forced to restart or shut down while the database schema was being migrated during an upgrade, and the lock was not released.

      To release the lock, you will need to run a mysql query. You will need to install mysql-client on the conduit appliance, and grab the password for conduit mysql. The username and db name are both conduit. The password to login to mysql can be found in the application.yml file located at ``/opt/conduit/conf/application.yml``

      Then run the following:

      .. code-block:: bash

        mysql -u conduit -p -h 127.0.0.1 conduit

      At the prompt, enter the mysql password from the application.yml

      Then run:

      .. code-block:: bash

        DELETE FROM DATABASECHANGELOGLOCK;

      Then restart conduit-ui:

      .. code-block:: bash

        sudo conduit-ctl restart conduit-ui

      If the restart timesout, run:

      .. code-block:: bash

        sudo conduit-ctl kill conduit-ui
        sudo conduit-ctl start conduit-ui
