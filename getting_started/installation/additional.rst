Additional Options
------------------

There are several additional configuration options during installation that may be performed. For example, |conduit| provides convenient options for uploading your own SSL certificates as well as externalizing several dependent services.

System Defaults
^^^^^^^^^^^^^^^

|conduit| follows several install location conventions. Below is a list of system defaults for convenient management:

* Installation Location: ``/opt/conduit``
* Log Location: ``/var/log/conduit``

  * Conduit-UI: ``/var/log/conduit/conduit-ui``
  * MySQL: ``/var/log/conduit/mysql``
  * NginX: ``/var/log/conduit/nginx``
  * Check Server: ``/var/log/conduit/check-server``
  * Elastic Search: ``/var/log/conduit/elsticsearch``
  * RabbitMQ: ``/var/log/conduit/rabbitmq``
  * Redis: ``/var/log/conduit/redis``

*  User-defined install/config: ``/etc/conduit/conduit.rb``

SSL Certificates
^^^^^^^^^^^^^^^^

The default installation generates a self-signed SSL certificate. To implement a third-party certificate:

#. Copy the private key and certificate to ``/etc/conduit/ssl/your_fqdn_name.key`` and ``/etc/conduit/ssl/your_fqdn_name.crt`` respectively.

#. Edit the configuration file ``/etc/conduit/conduit.rb`` and add the following entries:

   .. code-block:: bash

    nginx['ssl_certificate'] = 'path to the certificate file'
    nginx['ssl_server_key'] = 'path to the server key file'

   .. NOTE:: Both files should be owned by root and only readable by root, also if the server certificate is signed by an intermediate then you should include the signing chain inside the certificate file.

#. Next simply reconfigure the appliance and restart nginx:

   .. code-block:: bash

    sudo conduit-ctl reconfigure
    sudo conduit-ctl restart nginx

Additional Configuration Options
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

There are several other options available to the ``/etc/conduit/conduit.rb`` file that can be useful when setting up external service integrations or high availability:

.. code-block:: bash

  mysql['enable'] = false
  mysql['host'] = '52.53.240.28'
  mysql['port'] = 10004
  mysql['conduit_db'] = 'conduitdb01'
  mysql['conduit_db_user'] = 'merovingian'
  mysql['conduit_password'] = 'Wm5n5gXqXCe9v52'
  rabbitmq['enable'] = false
  rabbitmq['vhost'] = 'zion'
  rabbitmq['queue_user'] = 'dujour'
  rabbitmq['queue_user_password'] = '5tfg9n2iBifzW5c'
  rabbitmq['host'] = '54.183.196.152'
  rabbitmq['port'] = '10008'
  rabbitmq['stomp_port'] = '10010'
  redis['enable'] = false
  redis['host'] = '52.53.240.28'
  redis['port'] = 10009
  elasticsearch['enable'] = false
  elasticsearch['cluster'] = 'nebuchadnezzar'
  elasticsearch['es_hosts'] = {'52.53.214.68' => 10003}

These settings allow one to externally configure and scale mysql, elasticsearch, redis, and rabbitmq which is critical for a high availability setup.
