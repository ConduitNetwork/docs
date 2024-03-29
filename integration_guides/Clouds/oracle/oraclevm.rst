Oracle VM
---------

Add an Oracle VM Cloud
^^^^^^^^^^^^^^^^^^^^^^

Name
  Name of the Cloud in |conduit|
Location
  Description field for adding notes on the cloud, such as location.
Visibility
  For setting cloud permissions in a multi-tenant environment. Not applicable in single tenant environments.
API URL
  Oracle VM API URL. ex: https://10.20.30.40:7002/ovm/core/wsapi/rest
USERNAME
  Oracle VM User
PASSWORD
  Oracle VM User Password
REPOSITORY
  Available repositories will auto-populate upon successful authentication with the above credentials. Select appropriate repository for this Cloud.
SERVER POOL
  Available server pools will auto-populate upon successful authentication with the above credentials. Select appropriate server pool for this Cloud.
Inventory Existing Instances
  If enabled, existing Virtual Machines will be inventoried and appear as unmanaged Virtual Machines in |conduit| .

The Cloud can now be added to a Group or configured with additional Advanced options.

.. .. include:: /integration_guides/advanced_options.rst
