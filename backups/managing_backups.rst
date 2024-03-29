Managing Backups
================

Overview
--------

Backups are automatically configured and performed on each new |conduit| -provisioned Instance. Users can edit the frequency of backups. Administrators can define destination targets where backups are stored an perform all user-based tasks.

To View Backups:
----------------

Select the Backups link in the navigation bar.

.. NOTE:: If backups are disabled, they are still created upon instance provisioning and can be executed manually. However, backups will not be executed on a schedule automatically. Scheduled backups must be enabled by an administrator to run automatically. To review how to enable/disable backups see here.

Backup View
^^^^^^^^^^^

Review information about configuration such as: schedule, target details, total amount and successfully run backups, total and average size of backups from the Backup Page.

To Display Backup
^^^^^^^^^^^^^^^^^

#. Select the Backups link in the navigation bar.
#. Select the Backups link in the sub navigation bar.
#. Clicking the backup name to review its details.

Create Instance Backup
^^^^^^^^^^^^^^^^^^^^^^

To create instance backup

#. Select the Backups link in the navigation bar.
#. Select the Backups link in the sub navigation bar.
#. Click the Add Backup button.
#. From the Create Backup Wizard select the radio button Instance, then click Next.
#. Input the following:

   Name
    Name of the backup job being created.
   Instance
    Select an instance to backup from the dropdown.

#. Click Next.
#. Depending on the instance type selected in the previous step, enter additional details such as:

   - Database Name
   - Username
   - Password
   - Container
   - etc..

#. Click the Next button.
#. Schedule the backup Days, Time, Storage Provider & Retention Count.
#. Click Complete to save.

Create Server Backup
--------------------

To create a server backup:

#. Select the Backups link in the navigation bar.
#. Select the Backups link in the sub navigation bar.
#. Click Add Backup.
#. From the Create Backup Wizard select the radio button Server, then click Next.
#. Input the following:

   - Name of the backup job being created
   - Server
   - Type of backup you wish to create.

     - File
     - Directory
     - Mongo
     - MySQL
     - Postgres

#. Click Next. Different options are presented based upon the type of backup being created.

   - File/Directory - input path for the backup.
   - Mongo/MySQL/Postgres - input 'Database IP Address/URL', 'Database Port', 'Database Username', 'Database Password', 'Database Name', and the option to select 'All Databases'.

#. Click Next.
#. Schedule the backup Days, Time, Storage Provider & Retention Count.
#. Click Complete to save.
