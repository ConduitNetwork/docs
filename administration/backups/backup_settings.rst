Backup Settings
===============

``Administration -> Backups``

Overview
--------

The Backups Settings page allows you enable or disableScheduled Backups, and select a Default Backup Storage Provider Backups within |conduit| can always be run manually. However the scheduled backups toggle must be enabled to run jobs automatically. Configure the default storage provider to select the target location for all new backups. (This does not affect existing backups.)

|conduit| Backup Settings
--------------------------

Options:

Scheduled Backups
  Enable automatic scheduled backups for provisioned instances.

Create Backups
  When enabled, |conduit| will automatically configure instances for manual or scheduled backups.

Copy Snapshots to Store
  Copy VMware snapshots to selected Backup
Storage Provider
  Default Backups Storage Provider
Backup Appliance
  When enabled, a Backup will be created to backup the |conduit| appliance database. Select the ``Backup`` text link to edit Appliance Backup Settings and view existing Appliance Backups.

Default Backup Provider
  Enable/Disable |conduit| as the default backup provider.

Default Backup Storage Provider
  Storage Providers can be configured and managed in the Infrastructure Storage section.

Backup Retention Count
  Default maximum number of successful backups to retain.

.. include:: /administration/backups/veeam_config.rst
.. include:: /administration/backups/commvault_config.rst
