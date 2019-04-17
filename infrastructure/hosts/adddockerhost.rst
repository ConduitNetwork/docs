Docker Hosts
------------

Overview
^^^^^^^^

Conduit can provision Docker Hosts into any cloud, convert existing Hosts to Docker Hosts, or even make itself a Docker Host.

.. image:: /images/infrastructure/add_docker.gif

To add a Docker Host to any cloud:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Navigate to Infrastructure -> Hosts
2. Click the :guilabel:`+CONTAINER HOST` button
3. Select a container host type

.. image:: /images/infrastructure/add_docker.png

4. Select a Group

.. image:: /images/infrastructure/select_group.png

.. [caption="Figure 3: ", title="Select Group", alt="Select Group"]

5. Enter the following:
  * Name
  * Description
  * Visibility
  * Select a Cloud
  * Enter tags (optional)

Then click NEXT.

.. image:: /images/infrastructure/create_host.png

.. [caption="Figure 4: ", title="Create Host", alt="Create Host"]

6. Configure the host options

Select a Service Plan (Volume, Memory and CPU count fields may not be shown if selected service plan does not have custom options enabled).
  * Add and set size the volumes
  * Set memory size
  * Set the CPU count
  * Select a network

Optionally configure the following:
  * OS username
  * OS password
  * Domain name
  * Hostname (default is the name previously provided for the container host)

 Then click the NEXT button


.. image:: /images/infrastructure/create_host_2.png

.. [caption="Figure 5: ", title="Create Host", alt="Create Host"]

7. Optionally add any Automation Workflows and configure for Backups.

.. image:: /images/infrastructure/docker_host_automation.png

.. [caption="Figure 6: ", title="Docker Host Automation", alt="Automation"]

8. Review and click Complete to save

.. image:: /images/infrastructure/save_docker_host.png

.. [caption="Figure 7: ", title="Save Docker Host", alt="Save"]

Your new container host will begin provisioning, and soon be running and ready for containers.

Add an existing Docker Host
^^^^^^^^^^^^^^^^^^^^^^^^^^^

|conduit| can manage and inventory existing/brownfield Docker Hosts by using the `Manual Docker Host` option.

.. NOTE:: Adding a Docker Host that was previously managed by another |conduit| Appliance will disable management of the host on that Appliance as the |conduit| Agent settings will be reconfigured.

.. NOTE:: `Container Mode` on the Cloud settings where the Host is being added must be set to |conduit| for non-Kubernetes/Swarm hosts.

1. Navigate to Infrastructure -> Hosts
2. Select :guilabel:`+CONTAINER HOST` button
3. Select `Manual Docker Host`
4. In the CREATE HOST Wizard, enter the following:

   GROUP

   GROUP
    Select the Group this Host will be available for

   Select :guilabel:`NEXT`

   NAME

   CLOUD
    Select the Cloud the Host will be assigned to
   NAME
    Enter name for the Docker Host in |conduit|
   DESCRIPTION
    Enter optional description for the Docker Host
   VISIBILITY
    Select Tenant Visibility
   TAGS
    Add optional Conduit tags (these are not meta-data tags)

   Select :guilabel:`NEXT`

   CONFIGURE

   SSH HOST
    Enter IP or resolvable hostname of the target host
   SSH USER
    Enter existing username on the target host
   SSH PASSWORD
    Enter password for SSH User
   PUBLIC KEY
    For key auth (recommended), copy and add the displayed Public Key to the ``authorized_keys`` file on the target host.
   PLAN
    Default Manual
   LVM ENABLED?
    Deselect if target host is not LVM enabled (required when using |conduit| provided docker images)
   DATA VOLUME
    Enter path of the target data volume on the target host
   SOFTWARE RAID?
    Enable for software RAID (disabled by default)
   NET INTERFACE
    Enter network interface name of target host's target network

   Select :guilabel:`NEXT`

   AUTOMATION

   POST PROVISION
     Select a workflow to execute after Host is added (optional).

   Select :guilabel:`NEXT`

   REVIEW
    Review settings and select :guilabel:`COMPLETE` to add the Manual Docker Host.

Your new container host will begin provisioning, and soon be running and ready for containers.

.. NOTE:: Existing containers will be inventoried after the Hosts is successfully added.
