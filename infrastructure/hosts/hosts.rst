Hosts
=====

Overview
--------

The `Infrastructure -> Hosts` section provides a universal stage for viewing and managing Hosts and Virtual Machines from all of your Clouds.

In this section you can:

* View & Manage all Hosts, Virtual Machines & Bare Metal
* Provision Docker & KVM Hosts
* Convert existing hosts to Docker & KVM Hosts
* Add Hypervisors
* Convert Hosts, Virtual Machines and Bare Metal to Managed

  .. IMPORTANT:: When local firewall management is enabled, Conduit will automatically set an IP table rule to allow incoming connections on tcp port 22 from the Conduit Appliance.

Hosts
-----

Hosts in |conduit| are Hypervisors and Docker Hosts that your VM's and Container are hosted on, such as ESXi, Hyper-V and Docker Hosts. These Hosts are populated from integrated clouds, hosts provisioned from Conduit, or manually added Hosts.

.. //==== Adding Hosts
.. //==== Managing Hosts
.. //==== Removing Hosts


Virtual Machines
----------------

The Virtual Machines tab lists all Managed and Unmanaged VM's across |conduit| . Managed VM's are either provisioned by Conduit, or inventoried VM's that were converted to managed. Unmanaged VM's are from Cloud integrations with "Inventory Existing Instances" enabled in the Cloud settings.

.. //==== Managing Virtual Machines
.. //==== Removing Virtual Machines

Bare Metal
----------

Bare Metal hosts are from PXE Boot or manually added in this section. Bare Metal hosts that are also Hypervisors will be listed in both the Bare Metal and Hypervisor sections.

.. //==== Managing Bare Metal
.. //==== Removing Bare Metal

.. include:: adddockerhost.rst
