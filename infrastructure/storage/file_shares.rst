File Shares
-----------

File Shares are for Backup, Archives, Deployment and Virtual Images storage targets. File Shares can be browsed and files and folders can be uploaded, downloaded or deleted from the File Shares section. Retention Policies can be set on Storage File Shares for files to be deleted or backed up to another File Share after a set amount of time.

Supported File Share Types
^^^^^^^^^^^^^^^^^^^^^^^^^^

* CIFS (Samba Windows File Sharing)
* Dell EMC ECS Share
* Dell EMC Isilon Share
* Local Storage
* NFSv3

CIFS File Shares
^^^^^^^^^^^^^^^^

To Add a CIFS File Share:

#. Select the Infrastructure link in the navigation bar.
#. Select the Storage link in the sub navigation bar.
#. In the FILE SHARES tab, Click the :guilabel:`+ ADD` button.
#. Select `CIFS (Samba Windows File Sharing)` from the dropdown list
#. From the NEW FILE SHARE Wizard input the following:

   NAME
     Name of the File Share in |conduit|.
   HOST
     Enter host IP or resolvable hostname
      Example: ``192.168.200.210``
   USERNAME
    CIFS Share Username
   PASSWORD
    CIFS Share User Password
   SHARE PATH
    Enter CIFS Share Path
      Example: ``cifs``
   Default Backup Target
    Sets this File Share as the default backup target when creating Backups. If selected the option to update existing Backup configuration to use this File Share will be presented.
   Archive Snapshots
    Enabled to export VM snapshots to this File Share when creating VMware Backups, after which the snapshot will be removed from the source Cloud.
   Default Deployment Archive Target
    Sets this File Share as the default storage target when uploading Deployment files in the `Deployments` section.
   Default Virtual Image Store
    Sets this File Share as the default storage target when uploading Virtual Images from the `Virtual Images` section, importing Images from Instance Actions, creating Images with the `Image Builder` and when creating new images from `Migrations`.

   RETENTION POLICY
    None
      Files in the File Share will not be automatically deleted or backed up.
    Backup Old Files
      This option will backup files after a set amount if time and remove them from the File Share.
        DAYS OLD
          Files older than the set number of days will be automatically backed up to the selected Backup File Share.
        BACKUP File Share
          Search for and select the File Share the files will be backed up to.
    DELETE OLD FILES
      This option will delete files from this File Share after a set amount of days.
        DAYS OLD
          Files older than the set number of days will be automatically deleted from the File Share.

#. Select :guilabel:`SAVE CHANGES`

The File Share will be created and displayed in the File Shares tab.

- To browse, upload, download, or delete files from this File Share, select the name of the File Share.

- To edit the File Share, select the edit icon or select the name of the File Share and select :guilabel:`ACTIONS - EDIT`.

  .. WARNING:: Repointing a File Share that is in use may cause loss of file references. Ensure data is mirrored first.

- To delete a File Share, select the trash icon or select the name of the File Share and select :guilabel:`DELETE`.

  .. WARNING:: When deleting a File Share, all Deployment Versions and Backups associated with the File Share will be deleted.


Dell EMC ECS File Shares
^^^^^^^^^^^^^^^^^^^^^^^^

To Add a Dell EMC ECS File Share:

#. Select the Infrastructure link in the navigation bar.
#. Select the Storage link in the sub navigation bar.
#. In the FILE SHARES tab, Click the :guilabel:`+ ADD` button.
#. Select `Dell EMC ECS Share` from the dropdown list
#. From the NEW FILE SHARE Wizard input the following:

   NAME
     Name of the File Share in |conduit|.
   STORAGE SERVICE
     Select existing Dell EMC ECS Storage Server (configured in `Infrastructure - Storage - Servers`)
   SHARE PATH
     Enter Dell EMC ECS Share Path
      Example: ``ecs-file-share-1``
   USER
    Dell EMC ECS User
   SECRET KEY
    Dell EMC ECS Secret key
   Volume Size
    Specify volume size for the File Share (in MB)
   Allowed IP's
    Specify IP Addresses to limit accessibility to the File Share
      Leave blank for open access
        Click the ``+`` symbol to the right of the first ALLOWED IPS field to add multiple IP's
   NAMESPACE
     Select Dell EMC ECS Namespace (synced)
   STORAGE GROUP
    Select Dell EMC ECS Storage Group (synced)
   Default Backup Target
    Sets this File Share as the default backup target when creating Backups. If selected the option to update existing Backup configuration to use this File Share will be presented.
   Archive Snapshots
    Enabled to export VM snapshots to this File Share when creating VMware Backups, after which the snapshot will be removed from the source Cloud.
   Default Deployment Archive Target
    Sets this File Share as the default storage target when uploading Deployment files in the `Deployments` section.
   Default Virtual Image Store
    Sets this File Share as the default storage target when uploading Virtual Images from the `Virtual Images` section, importing Images from Instance Actions, creating Images with the `Image Builder` and when creating new images from `Migrations`.

   RETENTION POLICY
    None
      Files in the File Share will not be automatically deleted or backed up.
    Backup Old Files
      This option will backup files after a set amount if time and remove them from the File Share.
        DAYS OLD
          Files older than the set number of days will be automatically backed up to the selected Backup File Share.
        BACKUP File Share
          Search for and select the File Share the files will be backed up to.
    DELETE OLD FILES
      This option will delete files from this File Share after a set amount of days.
        DAYS OLD
          Files older than the set number of days will be automatically deleted from the File Share.

#. Select :guilabel:`SAVE CHANGES`

The File Share will be created and displayed in the File Shares tab.

- To browse, upload, download, or delete files from this File Share, select the name of the File Share.

- To edit the File Share, select the edit icon or select the name of the File Share and select :guilabel:`ACTIONS - EDIT`.

  .. WARNING:: Repointing a File Share that is in use may cause loss of file references. Ensure data is mirrored first.

- To delete a File Share, select the trash icon or select the name of the File Share and select :guilabel:`DELETE`.

  .. WARNING:: When deleting a File Share, all Deployment Versions and Backups associated with the File Share will be deleted.


Dell EMC Isilon File Shares
^^^^^^^^^^^^^^^^^^^^^^^^^^^

To Add a Dell EMC Isilon File Share:

#. Select the Infrastructure link in the navigation bar.
#. Select the Storage link in the sub navigation bar.
#. In the FILE SHARES tab, Click the :guilabel:`+ ADD` button.
#. Select `Dell EMC Isilon Share` from the dropdown list
#. From the NEW FILE SHARE Wizard input the following:

   NAME
     Name of the File Share in |conduit|.
   STORAGE SERVICE
     Select existing Dell EMC Isilon Storage Server (configured in `Infrastructure - Storage - Servers`)
   SHARE PATH
     Enter Dell EMC Isilon Share Path
      Example: ``ecs-file-share-1``
   Volume Size
    Specify volume size for the File Share (in MB)
   Allowed IP's
    Specify IP Addresses to limit accessibility to the File Share
      Leave blank for open access
        Click the ``+`` symbol to the right of the first ALLOWED IPS field to add multiple IP's
   NAMESPACE
     Select Dell EMC Isilon Namespace (synced)
   STORAGE GROUP
    Select Dell EMC Isilon Storage Group (synced)
   Default Backup Target
    Sets this File Share as the default backup target when creating Backups. If selected the option to update existing Backup configuration to use this File Share will be presented.
   Archive Snapshots
    Enabled to export VM snapshots to this File Share when creating VMware Backups, after which the snapshot will be removed from the source Cloud.
   Default Deployment Archive Target
    Sets this File Share as the default storage target when uploading Deployment files in the `Deployments` section.
   Default Virtual Image Store
    Sets this File Share as the default storage target when uploading Virtual Images from the `Virtual Images` section, importing Images from Instance Actions, creating Images with the `Image Builder` and when creating new images from `Migrations`.

   RETENTION POLICY
    None
      Files in the File Share will not be automatically deleted or backed up.
    Backup Old Files
      This option will backup files after a set amount if time and remove them from the File Share.
        DAYS OLD
          Files older than the set number of days will be automatically backed up to the selected Backup File Share.
        BACKUP File Share
          Search for and select the File Share the files will be backed up to.
    DELETE OLD FILES
      This option will delete files from this File Share after a set amount of days.
        DAYS OLD
          Files older than the set number of days will be automatically deleted from the File Share.

#. Select :guilabel:`SAVE CHANGES`

The File Share will be created and displayed in the File Shares tab.

- To browse, upload, download, or delete files from this File Share, select the name of the File Share.

- To edit the File Share, select the edit icon or select the name of the File Share and select :guilabel:`ACTIONS - EDIT`.

  .. WARNING:: Repointing a File Share that is in use may cause loss of file references. Ensure data is mirrored first.

- To delete a File Share, select the trash icon or select the name of the File Share and select :guilabel:`DELETE`.

  .. WARNING:: When deleting a File Share, all Deployment Versions and Backups associated with the File Share will be deleted.


Local Storage File Shares
^^^^^^^^^^^^^^^^^^^^^^^^^

.. IMPORTANT:: Local Storage refers to local to the |conduit| Appliance and the path must be owned by `conduit-app`. Please be conscious of storage space. High Availability configurations require Local Storage File Shares paths to be shared storage paths between the font end |conduit| Appliances.

.. NOTE:: To change the owner of a file path to be used as a Local Storage File Share, run ``chown conduit-app.conduit-app /path`` on the |conduit| Appliance.

.. NOTE:: |conduit| will validate path and ownership of the File Share Path.

To Add a Local Storage File Share:

#. Select the Infrastructure link in the navigation bar.
#. Select the Storage link in the sub navigation bar.
#. In the FILE SHARES tab, Click the :guilabel:`+ ADD` button.
#. Select `Local Storage Share` from the dropdown list
#. From the NEW FILE SHARE Wizard input the following:

   NAME
     Name of the File Share in |conduit|.
   STORAGE PATH
     Enter the File Share path on the local |conduit| Appliance.
      Example: ``/var/opt/conduit/conduit-ui/vms/virtual-images``

      .. IMPORTANT:: High Availability configurations require Local Storage File Shares paths to be shared storage paths between the font end |conduit| Appliances.
   Default Backup Target
    Sets this File Share as the default backup target when creating Backups. If selected the option to update existing Backup configuration to use this File Share will be presented.
   Archive Snapshots
    Enabled to export VM snapshots to this File Share when creating VMware Backups, after which the snapshot will be removed from the source Cloud.
   Default Deployment Archive Target
    Sets this File Share as the default storage target when uploading Deployment files in the `Deployments` section.
   Default Virtual Image Store
    Sets this File Share as the default storage target when uploading Virtual Images from the `Virtual Images` section, importing Images from Instance Actions, creating Images with the `Image Builder` and when creating new images from `Migrations`.

   RETENTION POLICY
    None
      Files in the File Share will not be automatically deleted or backed up.
    Backup Old Files
      This option will backup files after a set amount if time and remove them from the File Share.
        DAYS OLD
          Files older than the set number of days will be automatically backed up to the selected Backup File Share.
        BACKUP File Share
          Search for and select the File Share the files will be backed up to.
    DELETE OLD FILES
      This option will delete files from this File Share after a set amount of days.
        DAYS OLD
          Files older than the set number of days will be automatically deleted from the File Share.

#. Select :guilabel:`SAVE CHANGES`

The File Share will be created and displayed in the File Shares tab.

- To browse, upload, download, or delete files from this File Share, select the name of the File Share.

- To edit the File Share, select the edit icon or select the name of the File Share and select :guilabel:`ACTIONS - EDIT`.

  .. WARNING:: Repointing a File Share that is in use may cause loss of file references. Ensure data is mirrored first.

- To delete a File Share, select the trash icon or select the name of the File Share and select :guilabel:`DELETE`.

  .. WARNING:: When deleting a File Share, all Deployment Versions and Backups associated with the File Share will be deleted.

NFSv3 File Shares
^^^^^^^^^^^^^^^^^

.. NOTE:: Configure access to the NFS folder on the NFS Provider prior to adding the NFSv3 File Share.

.. NOTE:: Upon save |conduit| will create a persistent mount owned by ``conduit-app.conduit-app`` on the |conduit| Appliance for the NFSv3 File Share.

To Add a NFSv3 File Share:

#. Select the Infrastructure link in the navigation bar.
#. Select the Storage link in the sub navigation bar.
#. In the FILE SHARES tab, Click the :guilabel:`+ ADD` button.
#. Select `NFSv3` from the dropdown list
#. From the NEW FILE SHARE Wizard input the following:

   NAME
     Name of the File Share in |conduit|.
   HOST
     Enter the File Share path on the local |conduit| Appliance.
   EXPORT FOLDER
     Enter the NFSv3 Folder
   Default Backup Target
    Sets this File Share as the default backup target when creating Backups. If selected the option to update existing Backup configuration to use this File Share will be presented.
   Archive Snapshots
    Enabled to export VM snapshots to this File Share when creating VMware Backups, after which the snapshot will be removed from the source Cloud.
   Default Deployment Archive Target
    Sets this File Share as the default storage target when uploading Deployment files in the `Deployments` section.
   Default Virtual Image Store
    Sets this File Share as the default storage target when uploading Virtual Images from the `Virtual Images` section, importing Images from Instance Actions, creating Images with the `Image Builder` and when creating new images from `Migrations`.

   RETENTION POLICY
    None
      Files in the File Share will not be automatically deleted or backed up.
    Backup Old Files
      This option will backup files after a set amount if time and remove them from the File Share.
        DAYS OLD
          Files older than the set number of days will be automatically backed up to the selected Backup File Share.
        BACKUP File Share
          Search for and select the File Share the files will be backed up to.
    DELETE OLD FILES
      This option will delete files from this File Share after a set amount of days.
        DAYS OLD
          Files older than the set number of days will be automatically deleted from the File Share.

#. Select :guilabel:`SAVE CHANGES`

The File Share will be created and displayed in the File Shares tab.

- To browse, upload, download, or delete files from this File Share, select the name of the File Share.

- To edit the File Share, select the edit icon or select the name of the File Share and select :guilabel:`ACTIONS - EDIT`.

  .. WARNING:: Repointing a File Share that is in use may cause loss of file references. Ensure data is mirrored first.

- To delete a File Share, select the trash icon or select the name of the File Share and select :guilabel:`DELETE`.

  .. WARNING:: When deleting a File Share, all Deployment Versions and Backups associated with the File Share will be deleted.
