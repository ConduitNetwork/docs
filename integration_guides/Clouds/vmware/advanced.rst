Advanced
^^^^^^^^

There are several advanced features provided within |conduit| that can leverage some cool aspects of VMware. One of these features is Remote Console support directly to the hypervisor. To enable this feature a few prerequisites must be met. First, the |conduit| appliance must have network access to the ESXi hosts within VCenter. Secondly, firewall settings need to be adjusted on each ESXi host. This can be done in VSphere under firewall configuration on the host. Simply check the `gdbserver` option, which will open up the necessary ports (starting at 5900 range).

.. IMPORTANT:: Hypervisor Console for vCenter 6.5 requires |conduit| v3.2.0+

Now that the ESXi hosts are ready to utilize remote console, simply edit the cloud in |conduit| via ``Infrastructure -> Clouds``. Check the option that says `Use VNC`. It is important to note that currently this functionality only works for newly provisioned vm's provisioned directly via |conduit| . This should change soon however.

It is also possible to import vm snapshots for backup or conversion purposes from VCenter and also an ESXi host. However, this does require that the ESXi host license has an enterprise level license as it will not allow the appliance to download a virtual image if it is not a paid VMware license.
