.. _snow:

ServiceNow
------------





Add Service Now Integration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Navigate to ``Administration -> Integrations``
#. Select ``+ NEW INTEGRATION``
#. Select ``ServiceNow`` from the TYPE dropdown.
#. Add the following:

   NAME
    Name of the Integration in Conduit.
   ENABLED
    Leave checked to enable the Integration.
   HOST
    Url of the ServiceNow Instance ex: https://your.instance.service-now.com
   USER
    A user in ServiceNow that is able to access the REST interface and create/update/delete incidents, requests, requested items, item options, catalog items, workflows, etc.
   PASSWORD
    Above ServiceNow user's password

#. Save Changes

.. IMPORTANT:: When using ServiceNow version London, the following steps must also be performed.  An administrator needs to modify the access permissions on the 'catalog_script_client' and 'io_set_item' tables.  This is performed by ensuring the 'Can create', 'Can update', and 'Can Delete' are checked under Application Access for 'All application scopes' for these tables.

ServiceNow Approval Policies
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Add ServiceNow Provision Approval Policy to a Cloud
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. NOTE:: Any Instance provisioned into a Cloud with an Approval Policy enabled will require approval.

To add a ServiceNow Approval policy to a Cloud:

#. Navigate to ``Infrastructure -> Clouds``
#. Select a Cloud by clicking on the Cloud Name link
#. Select the POLICIES tab
#. Select + ADD POLICY
#. Select ``Provision Approval``
#. Optionally enter a description for the Policy
#. Configure the following:

   APPROVAL INTEGRATION
    Select the ServiceNow Integration already configured in ``Administration -> Integrations`` to use for the Approval Policy.

   WORKFLOW
    Select the ServiceNow workflow for the Approval workflow in ServiceNow. Note these workflows are configured and synced in from the ServiceNow Integration.

   TENANTS (if applicable)
     Only required for multi-tenant permission scoping. For the policy to apply to a sub-tenant, type the name of the tenant(s) and select the Tenant(s) from the list.

#. Save Changes

Add ServiceNow Provision Approval Policy to a Group
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. NOTE:: Any Instance provisioned into a Group with an Approval Policy enabled will require approval.

To add a ServiceNow Approval policy to a Group:

#. Navigate to ``Infrastructure -> Groups``
#. Select a Group by clicking on the Group Name link
#. Select the POLICIES tab
#. Select + ADD POLICY
#. Select ``Provision Approval``
#. Optionally enter a description for the Policy
#. Configure the following:

   APPROVAL INTEGRATION
    Select the ServiceNow Integration already configured in ``Administration -> Integrations`` to use for the Approval Policy.

   WORKFLOW
    Select the ServiceNow workflow for the Approval workflow in ServiceNow. Note these workflows are configured and synced in from the ServiceNow Integration.

   TENANTS (if applicable)
     Only required for multi-tenant permission scoping. For the policy to apply to a sub-tenant, type the name of the tenant(s) and select the Tenant(s) from the list.

#. Save Changes

Using ServiceNow Approval Policies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Any Instance provisioned into a Cloud or Group with an Approval Policy enabled will be in a PENDING state until the request in Approved.

Instances pending a ServiceNow approval will show "Waiting for Approval" with the Requested Item number and Request number, ex: ``Waiting for Approval [RITM0010002 - REQ0010002]``.

ServiceNow Approval requests are displayed in ``Operations -> Approvals``.
Instances pending a ServiceNow approval must be Approved in ServiceNow for provisioning to initiate. Approval requests from a ServiceNow Approval Policy cannot be approved in Conduit, only Internal Approvals.

ServiceNow Approval requests are displayed in Conduit under ``Operations -> Approvals``. Pending ServiceNow Approval requests can be cancelled in Conduit by selecting the request and then selecting ``ACTIONS -> Cancel``.

Once a pending ServiceNow Approval request is Approved in ServiceNow, the Instance(s) will begin to provision in Conduit within 5 minutes of being approved in ServiceNow.

ServiceNow Service Catalog Integration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following is a guide to installing the Conduit ServiceNow application.

.. IMPORTANT:: A valid SSL Certificate is required on the |conduit| Appliance for the ServiceNow plugin to be able to communicate with the appliance.

ServiceNow Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~

#. Install the Conduit Application from the ServiceNow store
#. Navigate to Conduit Catalog -> Properties
#. Set the following properties:

   Conduit Appliance Endpoint
    The full url to your Conduit appliance
   Password
    Password of the Conduit Administrator
   Username
    Username of the Conduit Administrator

#. Create a new User
#. Assign the following roles to the user:

   - x_moda_conduit_ca.integration
   - catalog_admin
   - itil
   - rest_service


  .. IMPORTANT:: When using ServiceNow version London, the following steps must also be performed.  An administrator needs to modify the access permissions on the 'catalog_script_client' and 'io_set_item' tables.  This is performed by ensuring the 'Can create', 'Can update', and 'Can Delete' are checked under Application Access for 'All application scopes' for these tables.

Conduit Configuration
~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to ``Administration -> Integrations``
#. Click :guilabel:`+ NEW INTEGRATION`
#. Select ‘ServiceNow’ in the Type field
#. Fill in the Host, User and Password fields (using the User and Password created in the previous section)

.. ServiceNow Monitoring Notifications


ServiceNow Monitoring Integration Settings
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. NOTE:: A ServiceNow Integration must be already configured in `Administration -> Integrations` to enable the ServiceNow Monitoring Integration.

Enabled
  Enables the ServiceNow Monitoring Integration
Integration
  Select from a ServiceNow Integration added in `Administration -> Integrations`
New Incident Action
  The Service Now action to take when a Conduit incident is created.
Close Incident Action
  The Service Now action to take when a Conduit incident is closed.

Incident Severity Mapping

.. [width="40%",frame="topbot",options="header"]

=================== =================
|conduit| Severity ServiceNow Impact
------------------- -----------------
Info                Low/Medium/High
Warning             Low/Medium/High
Critical	          Low/Medium/High
=================== =================
