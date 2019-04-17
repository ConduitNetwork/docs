Database Tier
---------------


Conduit needs a database to connect to.  Out of the box Conduit uses MySQL but Conduit supports any mySQL compliant database.  There are many ways to set up a highly available, MySQL dialect based database.  One which has found favor with many of our customers is Percona's XtraDB Cluster.  Percona's product is based off of Galera's WSREP Clustering, which is also supported.

If you're not as familiar with WSREP and prefer replication, some of our customers prefer to configure a failover connection to a MariaDB or MySQL based Master/Master Replication cluster.  Less often used, though still a viable option, is MySQL based NDB Clustering.  Wonderful guides for each of these HA and DR based database management strategies can be found here: https://www.percona.com/doc/percona-xtradb-cluster/LATEST/index.html


Requirements
^^^^^^^^^^^^

.. NOTE:: Conduit idiomatically connects to database nodes over 3306

Once you have your database installed and configured:


#. Create the Database you will be using with conduit.

   .. code-block:: bash

    mysql> CREATE DATABASE conduitdb;

    mysql> show databases;


#. Next create your conduit database user. The user needs to be either at the IP address of the conduit application server or use ``@'%'`` within the user name to allow the user to login from anywhere.

   .. code-block:: bash

    mysql> CREATE USER '$conduit_db_user_name'@'$source_ip' IDENTIFIED BY '$conduit_db_user_pw';

#. Next Grant your new conduit user permissions to the database.

   .. code-block:: bash

    mysql> GRANT ALL PRIVILEGES ON *.* TO '$conduit_db_user_name'@'$source_ip' IDENTIFIED BY '$conduit_db_user_pw' with grant option;

    mysql>  GRANT SELECT, PROCESS, SHOW DATABASES, SUPER ON *.* TO 'conduitdbuser'@'$source_ip' IDENTIFED BY PASSWORD 'secretpasshere';

    mysql> FLUSH PRIVILEGES;

#. Checking Permissions for your user.

   .. code-block:: bash

    SHOW GRANTS FOR '$conduit_db_user_name'@'$source_ip';
