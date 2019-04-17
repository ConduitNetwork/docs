VMware Fusion
-------------

Add a VMware Fusion Cloud
^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Navigate to ``Infrastructure -> Clouds``
#. Select :guilabel:`+ CREATE CLOUD`, select VMware Fusion, and then click :guilabel:`Next`.
#. Enter the following into the Create Cloud modal:

   Name
      Name of the Cloud in |conduit|
   Location
      Description field for adding notes on the cloud, such as location.
   Visibility
      For setting cloud permissions in a multi-tenant environment. Not applicable in single tenant environments.
   VMWARE FUSION HOST
      IP or URL of VMware Fusion Host
   WORKING PATH
      Existing folder |conduit| will write to on Host
   USERNAME
      Host Username
   PASSWORD
      Host Password
   BRIDGE NAME
      Will auto-populate upon successful authentication with the Fusion Host (E.X. 'EN0: ETHERNET')

#. The Cloud can now be added to a Group or configured with additional Advanced options.

.. include:: /integration_guides/Clouds/advanced_options.rst
