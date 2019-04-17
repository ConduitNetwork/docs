Openstack
---------

Overview
^^^^^^^^^^

Openstack is becoming a widely used on-premise infrastructure orchestration platform. It has a wide array of contributors and enterprise sponsorships. There are several variations on Openstack as well ranging from HP's Helion Cloud to Cisco's Metapod / Metacloud offering. |conduit| supports integration with all the various platform offerings and ranges in support all the way back to Openstack Icehouse. It leverages the APIs and provides full functionality as a self service portal in front of Openstack.

Features
^^^^^^^^^^

* Virtual Machine Provisioning
* Backups / Snapshots
* Security Group Management
* Disk Mode support Local/Image (via Ceph)
* Floating IP Assignment support
* Brownfield VM management and Migration
* Lifecycle Management and Resize
* Docker Host management / configuration
 
On top of all these features, |conduit| also adds additional features to Openstack that do not exist out of the box to make it easier to manage in multitenant environments as well as hybrid cloud environments:

* Image to QCOW2 Image Conversion
* QCOW2 to RAW Image Conversion
* Multitenancy resource allocation
* Virtual Image management (Blueprints)
* Auto-scaling and recovery

.. TIP:: To allow Conduit to list Hypervisor Hosts, ensure the Openstack user used for the Cloud Integration has sufficient privileges for ``"os_compute_api:os-hypervisors"`` in ``/etc/nova/policy.json`` in Openstack.

.. include:: getting_started.rst
.. include:: advanced.rst
.. include:: docker.rst
