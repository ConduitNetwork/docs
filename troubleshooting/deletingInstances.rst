Deleting Instances
==================

It is important to know the difference between deleting an Instance from the Provisioning section, and deleting a VM from the Infrastructure section.

.. IMPORTATNT:: Deleting an Instance a with Virtual Machines in it will always try to delete the actual Virtual Machines.

Instances are managed resources that may have one or multiple Virtual Machines associated. Since the vm's in the Instance are managed by |morphues|, deleting an Instance a with Virtual Machines in it will always try to delete the actual Virtual Machines.

There are scenarios where deleting, or attempting to delete the associated Virtual Machines is not desired:

- The Instance needs to be deleted, but the actual Virtual Machines need to remain.
- The actual Virtual Machines have already been deleted outside of |conduit|, so only the records in |conduit| need to be removed.

Deleting an Instance without deleting Infrastructure
----------------------------------------------------

It is not possible to delete and Instance from the Provisioning section without removing the associated Infrastructure/VM's. However this can be accomplished from the Infrastructure section by deselecting "Remove Infrastructure" when deleting the VM:

1. Navigate to the Virtual Machine record by clicking on the VM's name in the Virtual Machines section in the Instances details section, or by navigating to `Infrastructure - Hosts - Virtual Machines` and selecting the VM.

.. TIP: Global Search makes it easy to find resources in any section.

2. Click "DELETE"

3. In the delete confirmation modal:

   - Uncheck "Remove Infrastructure"
   - Check "Remove Associated Instances"

   .. image:: /images/provisioning/deleteOnlyInstance.png

   .. IMPORTANT:: Ensure "Remove Infrastructure" is NOT checked if you do not want to delete the actual Virtual Machine.

4. Select DELETE

This will delete the Virtual Machine record as well as the Instance record, but leave the Infrastructure/VM in place. If the VM is in a Cloud that is being inventoried, it will s


Deleting an Instance/VM that does not exist anymore
----------------------------------------------------

Deleting a managed resource outside of |conduit| is not recommended as it will leave stranded record in |conduit| and cause deleting the records in |conduit| to get stuck on delete when |conduit| tries to remove infrastructure that is no longer there.

To select an Instance and/or VM record in |conduit| for a Virtual Machine that no longer exists:

1. Navigate to the Virtual Machine record by clicking on the VM's name in the Virtual Machines section in the Instances details section, or by navigating to `Infrastructure - Hosts - Virtual Machines` and selecting the VM.

.. TIP: Global Search makes it easy to find resources in any section.

2. Click "DELETE"

3. In the delete confirmation modal:

   - Uncheck "Remove Infrastructure"
   - Check "Remove Associated Instances"

   .. image:: /images/provisioning/deleteOnlyInstance.png

   .. IMPORTANT:: Ensure "Remove Infrastructure" is NOT checked. If it is checked, |conduit| will try to delete the actual VM, and since it is not there anymore, the delete will not complete successfully since |conduit| will not be able to verify successful deletion of the Infrastructure.

4. Select DELETE

The key point is when deleting an Instance, or when selecting "Remove Infrastructure" when deleting a VM record, |conduit| will always try to remove the Infrastructure. If the Infrastructure/VM no longer exists, or you do not want to remove it, simply delete from the Infrastructure section and uncheck "Remove Infrastructure".

.. NOTE:: When deleting a managed VM, if that VM is the only VM inside the associated Instance, the Associated Instance must also be removed.  
