Power DNS
---------

Overview
^^^^^^^^

|conduit| integrates directly with Power DNS to automatically create DNS entries for Instances provisioned to a configured Cloud or Group. |conduit| also syncs in Power DNS Domains for easy selection while provisioning, or setting as the default Domain on a Cloud or Network.

Add Power DNS Integration
^^^^^^^^^^^^^^^^^^^^^^^^^

Power DNS can be added in the `Administration` or `Infrastructure` sections:

#. In ``Administration -> Integrations``, select :guilabel:`+ New Integration`
#. In ``Infrastructure -> Networks -> Services``, select :guilabel:`Add Service`
#. Provide the following:

   TYPE
    Power DNS
   NAME
    Name for the Integration in |conduit|
   API HOST
    URL of Power DNS API. Example: ``http://10.30.20.10:8081``
   Token
    Power DNS API Token
   Version
    Power DNS API Version

#. Once saved the Integration will be added and visible in both ``Administration -> Integrations`` and ``Infrastructure -> Networks -> Services``

.. NOTE:: All fields can be edited after saving.

Domains
^^^^^^^

Once the integration is added, Power DNS Domains will sync and listed under ``Infrastructure -> Networks -> Domains``.

.. NOTE:: Default Domains can be set on Networks and Clouds, and can be selected when provisioning. Additional configuration options are available by editing a domain in `Networks -> Domains`

Configuring Power DNS with Clouds and Groups
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

DNS Integrations are available in the `DNS Integration` dropdown in Cloud and Group settings.

|conduit| will register Instances with the DNS provider when provisioned into a Cloud or Group with a DNS Integration added.

Add DNS Integration to a Cloud
..............................

#. In ``Infrastructure -> Clouds`` edit the target Cloud.
#. Expand the `Advanced Options` section.
#. In the `DNS Integration` dropdown, select an available DNS Integration.
#. Save Changes

Add DNS Integration to a Group
..............................

#. In ``Infrastructure -> Groups`` select the target Group.
#. Select the `Edit` button for the Group
#. Expand the `Advanced Options` section.
#. In the `DNS Integration` dropdown, select an available DNS Integration.
#. Save Changes

.. NOTE:: Instances provisioned into a Cloud or Group with a DNS Integration added will be registered as instancename.domain with the DNS Provider during provisioning, and de-registered at teardown.
