
Getting Started
^^^^^^^^^^^^^^^

Adding an Openstack cloud to |conduit| is one of the simpler cloud integrations to get started with. First go to the ``Infrastructure -> Clouds`` section and click add cloud. From here there are several options including Metapod, Helion, and general Openstack. Any of these options will actually work and for the most part the branded Openstack options are represented to make it clearer to the user as to the capabilities of |conduit| .

.. update image:: /images/openstack/add_cloud.png

.. caption="Figure 1: ", title="Add Openstack Cloud form", alt="Add Openstack Cloud form"]

Most of the information in the dialog can be acquired from the openstack dashboard. under `Project -> Access & Security -> API Access`. The API Url that is needed is the one tied to `Identity`. The Domain and Project inputs typically correlate to the multitenant domain setup within openstack (sometimes just left at default) as well as the project name given to instances. |conduit| allows multiple integrations to the same openstack cluster scopable to domains and projects as needed. The remaining options help |conduit| determine what api capabilities exist in the selected openstack environment. Hence the need for the Openstack version and image format. If a newer openstack cluster is being used then exists in the dropdown, simply select the most recent version in the dropdown and this should function sufficiently until the new version is added.

.. TIP:: Some Openstack environments do not support QCOW2 and force RAW image formats (like metapod). This is due to some network overhead in Ceph created by using QCOW2. |conduit| keeps 2 copies of openstack image templates for this exact purpose.

Saving this cloud integration should perform a verification step and close upon successful completion.

Existing Instances
^^^^^^^^^^^^^^^^^^

|conduit| provides several features regarding pulling in existing virtual machines and servers in an environment. Most cloud options contain a checkbox titled '*Inventory Existing Instances*'. When this option is selected, all VMs found within the specified scope of the cloud integration will be scanned periodically and Virtual Machines will be synced into |conduit| . By default these virtual machines are considered 'unmanaged' and do not appear in the `Provisioning -> Instances` area but rather `Infrastructure -> Hosts -> Virtual Machines`. However, a few features are provided with regards to unmanaged instances. They can be assigned to various accounts if using a multitenant master account, however it may be best suited to instead assign the 'Resource Pool' to an account and optionally move all servers with regards to that pool (more on this later).
A server can also be made into a managed server. During this process remote access is requested and an agent install is performed on the guest operating system. This allows for guest operations regarding log acquisition and stats. If the agent install fails, a server will still be marked as managed and an Instance will be created in `Provisioning`, however certain features will not function. This includes stats collection and logs.

.. NOTE:: All Cloud data is resynchronized on a 5 minute interval. This includes Datastores, Resource Pools, Networks, Blueprints, and Virtual Machines.
