Blank Dashboard
===============

Problem
  A blank dashboard or 500 error after installing conduit

.. NOTE:: A blank or 500 error on just the dashboard is different than the entire conduit-ui not loading. Please see UI note loading article for troubleshooting the ui not loading after an upgrade.

Cause
  Elasticsearch restarting prior to being fully bootstrapped during the initial install.

Solution
  To fix, purge elasticsearch by running the following on the |conduit| Appliance:

.. code-block:: bash

    curl -XDELETE http://localhost:9200/*
    conduit-ctl restart elasticsearch
    conduit-ctl restart conduit-ui

Another option is:

.. code-block:: bash

  sudo rm –rf /var/opt/|conduit| /elasticsearch/data/conduit
  conduit-ctl restart elasticsearch
  conduit-ctl restart conduit-ui

If you get a term/timeout on ui restart, run

.. code-block:: bash

  conduit-ctl kill conduit-ui
  conduit-ctl start conduit-ui


.. NOTE:: The conduit-ui may take a few minutes to load and be available after being restarted
