Restart a |conduit| Installation
=================================

If the initial reconfigure is stopped or your installation is damaged beyond reconfiguring again, it may be necessary to start over.

On the |conduit| appliance:

#. Run ``conduit-ctl cleanse``

#. Remove the |conduit| package

   - deb: ``dpkg --purge conduit-appliance...`` using the appropriate package name.
   - rpm: ``rpm -e (conduit-appliance...)`` using the appropriate package name.

#. Then Run

   .. code-block:: bash

    rm -rf /etc/conduit
    rm -rf /var/opt/conduit
    rm -rf /var/run/conduit
    rm -rf /var/log/conduit
    rm -rf /opt/conduit

#. Re-install |conduit|

  If the elasticsearch cluster is unhealthy and needs purged, run:

  .. code-block:: bash

    sudo conduit-ctl stop elasticsearch
    sudo rm -rf /var/opt/conduit/elasticsearch/data/conduit
    sudo conduit-ctl reconfigure

  If eleasticsearch does not restart during reconfigure:

  .. code-block:: bash

    sudo conduit-ctl start elasticsearch
