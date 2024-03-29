Veeam Settings
--------------

Enabled
  Enable the Veeam integration
Default Backup Provider
  Sets Veeam as the Default Backup Provider in |conduit| . Backup Providers can also be configured per Backup.
Visibility
  Sets visibility in multi-tenant |conduit| environments:

  * Public: Accessible by all Tenants
  * Private: Accessible only to the Tenant the Veeam integration is added.

Host
  Host name or the IP address of the Veeam Backup Enterprise Manager. This is the same host that you use to access the Veeam Backup Enterprise Manager browser-based user interface.
Port
  The HTTP(S) port of the Veeam Backup Enterprise Manager API. The default is 9399.
Username
  The username used to authenticate with the Veeam Backup Enterprise Manager.
Password
  The password used to authenticate with the Veeam Backup Enterprise Manager.
Backup Repositories
  Once credentials are authenticated, search will populate available Veeam Repositories to select from.
Backup Job Templates
  The backup jobs configured in the Veeam Backup and Replication Console that can be cloned when creating new backup jobs.
Refresh Available Jobs
  Use to sync newly created Jobs in Veeam.

.. IMPORTANT:: Once a Veeam Integration has been enabled, a ``VEEAM SERVER`` setting will be available in VMware and Hyper-V cloud settings (``Infrastructure -> Clouds -> Edit a Cloud``). To enabled backups on a Cloud, a Veeam Server must be selected in the ``VEEAM SERVER`` dropdown in the Cloud settings and saved. Failure to do so will result in blank ``Backup Repositories`` and ``Backup Job Templates`` options when configuring Veeam Backups during provisioning´´.
