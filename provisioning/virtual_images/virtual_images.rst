Virtual Images
==============

`Provisioning -> Virtual Images`

Overview
--------

The Virtual Image section displays a list of all images, local and synced, that are available to deploy. |conduit| includes a rich catalog of pre-configured System Images available for every cloud type. User Images are automatically synced from Cloud Integrations and added to the Virtual Images section. Images can also be uploaded directly into |conduit| via local file or url. Amazon and Azure Marketplace images can also be added to the Virtual Images Section.

.. IMPORTANT:: Invalid Image Settings cause provisioning failures. |conduit| syncs in as much meta-data as possible for synced images, they still need to be properly configure to ensure successful provisioning.

.. WARNING:: Cloud-init is enabled by default for all Linux Images. If your Linux image does not have Cloud-init installed, `Cloud-init Enabled` must be unchecked before provisioning the image or it will fail immediately.

Image Types
-----------

|conduit| provides a vast *System Image* repo with pre-configured images for every Cloud. All other images are *User Images*. User images can be added directly to |conduit| , or automatically synced from integrated clouds. It is important to configure synced User Images for metadata, including specifying the Platform and User Credentials, prior to provisioning. Provisioning a User Image that has not been configured may result in failed provisioning.

.. IMPORTANT:: Synced User Images need to be configured prior to provisioning.

Configuring Virtual Images
--------------------------

System Images
^^^^^^^^^^^^^

System Images are pre-configured with metadata and have Cloud-Init or Cloudbase-Init installed. These images are ready to be provisioned with no configuration necessary. It is highly recommended to populate the ``Administration -> Provisioning -> Cloud-Init`` section with user data prior to provisioning, as the user and password/key will be added to all Instances provisioned from System Images. Users can also be added during provisioning in the `Add User` provisioning wizard section.

.. NOTE:: System Images settings are not editable.

User Images
^^^^^^^^^^^

Typically |conduit| does not have sufficient metatdata to successfully provision synced User Images. After integrating clouds and User Images have synced, it is highly recommended to configure the images prior to provisioning.

**To edit and configure an existing Virtual Image:**

1. Select `Actions - Edit` in the Virtual Images list, or `Edit` on a Virtual Image detail page.
2. Configure the following on the Image:

   Name
     Name of the Virtual Image in |conduit| . This can be changed from the name of the Image, but editing will not change the name of the actual Image.
   Operating System
     Specifies the Platform and OS of the image. All Windows images will need to have Operating System specified on the  Virtual Image, as |conduit| will assign Linux as the Platform for all Images without Operating System specified.
   Minimum Memory
    The Minimum Memory setting will filter available Service Plans options during provisioning. Service Plans that do not meet the Minimum Memory value set on the Virtual Image will not be provided as Service Plan choices.
   Cloud Init Enabled?
     On by default, uncheck for any Image that does not have Cloud-Init or Cloudbase-Init installed.
   Install Agent
     On by default, uncheck to skip Agent install. Note this will result in the loss of utilization statistics, logs, script execution, and monitoring. (Some utilization stats are collected for agent-less hosts and vm's from VMware and AWS clouds).
   Username
     Existing Username on the Image. This is required for authentication, unless |conduit| is able to add user data, Cloud-Init, Cloudbase-Init or Guest Customizations. If Cloud-Init, Cloudbase-Init or Guest Customizations are used, credentials are defined in `Administration -> Provisioning` and `User Settings `. If credentials are defined on the Image and Cloud-Init is enabled, |conduit| will add that user during provisioning, so ensure that user does not already exist n the image (aka ``root``). For Windows Guest Customizations, |conduit| will set the Administrator password to what is defined on the image if Administrator user is defined. Do not define any other user than Administrator for Windows Images unless using Cloudbase-init. |conduit| recommends running Guest Customizations for all Windows Images, which is required when joining Domains as the SID will change.
   Password
     Password for the Existing User on the image if Username is populated.
   Storage Provider
    Location where the Virtual Image will be stored. Default Virtual Image Storage location is /var/opt/conduit/conduit-ui/vms. Additional Storage Providers can be configured in `Infrastructure -> Storage`.
   Cloud-Init User Data
     Accepts what would go in runcmd and can assume bash syntax. Example use: Script to configure satellite registration at provision time.
   Create Image
    Select FILE to select or drag and drop image file, or URL to download the image from an accessible URL. It is recommend to configure the rest of the settings below prior to uploading the source Image File(s).
   Permissions
    Set Tenant permissions in a multi-tenant |conduit| environment. No impact on single-tenant environments.
   Auto Join Domain?
    Enable to have instances provisioned with this image auto-join configured domains (Windows only, domain controller must be configure in `Infrastructure -> Network` and the configured domain set on the provisioned to Cloud or Network).
   VirtIO Drivers Loaded?
    Enable if VirtIO Drivers are installed on the image for provisioning to KVM based Hypervisors.
   VM Tools Installed?
    On by default, uncheck if VMware Tools (including OpenVMTools) are not installed on the Virtual Image. |conduit| will skip network wait during provisioning when deselected.
   Force Guest Customization?
    VMware only, forces guest customizations to run during provisioning, typically when provisioning to a DHCP network where guest customizations would not run by default.
   Trial Version
    Enable to automatically re-arm the expiration on Windows Trial Images during provisioning.
   Enabled Sysprep?
    Applicable to Nutanix Only. Enable of the Windows Image has been sys-prepped. If enabled Conduit will inject Unattend.xml through the Nutanix API (v3+ only)

3. Save Changes

.. NOTE:: Cloud-Init is enabled by default on all Images. Images without Cloud-Init or Cloudbase-Init installed must have the `cloud-init` flag disabled on the Virtual Image setting or Provisioning may fail.

Provisioning Images
-------------------

When provisioning a System Image for the first time, |conduit| will download and stream the image from S3 to the source Cloud if the image is not local to the Cloud. The Image will also be cached on the |conduit| Appliance under ``/var/opt/conduit/vm/vmcache``. Subsequent provisions of the image will use the created template in the Cloud or the cached local Image if the images does not exist in the selected Cloud, in which case the cached Image will be copied to the Cloud.

When using Images that already exist in the destination cloud, such as synced, marketplace, or previously copied images, no image transfer between the |conduit| Appliance and destination cloud will take place.

.. NOTE:: The |conduit| Appliance must be able to download from Amazon S3 when provisioning System Images for the first time.

.. NOTE:: The |conduit| Appliance must be able reach and resolve the destination Host when provisioning System Images or uploaded Images for the first time. This included being able to resolve ESXi host names in VMware vCenter clouds, and reach the destination ESXi host over port 443.

Add Virtual Image
-----------------

Virtual Images can be upload to |conduit| from local files or URL's. Amazon and Azure Marketplace metadata can also be added to the Virtual Images library, enabling the creation of custom catalog Instance Type from Marketplace images (no image is transferred to |conduit| when adding Marketplace images).

.. WARNING:: Be conscious of your Storage Provider selection. The default Storage Provider is the |conduit| Appliance at ``/var/opt/conduit/conduit-ui/vms``. Uploading large images to the |conduit| Appliance when there is inadequate space will cause upload failures and impact Appliance functionality. Ensure there is adequate space on your selected Storage Provider. Additional Storage Provider can be added at `Infrastructure -> Storage`, which can be configured as the default Virtual Image Store or selected when uploading Images.

To Add Virtual Image:

1. Select :guilabel:`+ Add` in the Virtual Images page.
2. Select Image format:

   * Alibaba
   * Amazon AMI
   * Azure Marketplace
   * Digital Ocean
   * ISO
   * PXE Boot
   * QCOW2
   * RAW
   * VHD
   * VirtualBox
   * VirtualBox (vdi)
   * VMware (vmdk/ovf/ova)

3. Configure the following on the Virtual Image:

   Name
    Name of the Virtual Image in |conduit| . This can be changed from the name of the Image, but editing will not change the name of the actual Image.
   Operating System
    Specifies the Platform and OS of the image. All Windows images will need to have Operating System specified on the Virtual Image, as |conduit| will assign Linux as the Platform for all Images without Operating System specified.
   Minimum Memory
    The Minimum Memory setting will filter available Service Plans options during provisioning. Service Plans that do not meet the Minimum Memory value set on the Virtual Image will not be provided as Service Plan choices.
   Cloud Init Enabled?
    On by default, uncheck for any Image that does not have Cloud-Init or Cloudbase-Init installed.
   Install Agent
    On by default, uncheck to skip Agent install. Note this will result in the loss of utilization statistics, logs, script execution, and monitoring. (Some utilization stats are collected for agent-less hosts and vm's from VMware and AWS clouds).
   Username
    Existing Username on the Image. This is required for authentication, unless |conduit| is able to add user data, Cloud-Init, Cloudbase-Init or Guest Customizations. If Cloud-Init, Cloudbase-Init or Guest Customizations are used, credentials are defined in `Administration -> Provisioning` and `User Settings `. If credentials are defined on the Image and Cloud-Init is enabled, |conduit| will add that user during provisioning, so ensure that user does not already exist n the image (aka ``root``). For Windows Guest Customizations, |conduit| will set the Administrator password to what is defined on the image if Administrator user is defined. Do not define any other user than Administrator for Windows Images unless using Cloudbase-init. |conduit| recommends running Guest Customizations for all Windows Images, which is required when joining Domains as the SID will change.
   Password
    Password for the Existing User on the image if Username is populated.
   Storage Provider
    Location where the Virtual Image will be stored. Default Virtual Image Storage location is /var/opt/conduit/conduit-ui/vms. Additional Storage Providers can be configured in `Infrastructure -> Storage`.
   Cloud-Init User Data
    Accepts what would go in runcmd and can assume bash syntax. Example use: Script to configure satellite registration at provision time.
   Create Image
    Select FILE to select or drag and drop image file, or URL to download the image from an accessible URL. It is recommend to configure the rest of the settings below prior to uploading the source Image File(s).
   Permissions
    Set Tenant permissions in a multi-tenant |conduit| environment. No impact on single-tenant environments.
   Auto Join Domain?
    Enable to have instances provisioned with this image auto-join configured domains (Windows only, domain controller must be configure in `Infrastructure -> Network` and the configured domain set on the provisioned to Cloud or Network).
   VirtIO Drivers Loaded?
    Enable if VirtIO Drivers are installed on the image for provisioning to KVM based Hypervisors.
   VM Tools Installed?
    On by default, uncheck if VMware Tools (including OpenVMTools) are not installed on the Virtual Image. |conduit| will skip network wait during provisioning when deselected.
   Force Guest Customization?
    VMware only, forces guest customizations to run during provisioning, typically when provisioning to a DHCP network where guest customizations would not run by default.
   Trial Version
    Enable to automatically re-arm the expiration on Windows Trial Images during provisioning.
   Enabled Sysprep?
    Applicable to Nutanix Only. Enable of the Windows Image has been sys-prepped. If enabled Conduit will inject Unattend.xml through the Nutanix API (v3+ only)

.. NOTE:: Default Storage location is ``/var/opt/conduit/conduit-ui/vms``. Additional Storage Providers can be configured in `Infrastructure -> Storage`. Ensure local folders are owned by conduit-app.conduit-app if used.

.. WARNING:: Provisioning will fail if `Cloud init Enabled` is checked and Cloud-Init is not installed on the Image.

.. NOTE:: Existing Image credentials are required for Linux Images that are not Cloud-Init enabled and for Windows Images when Guest Customizations are not used. Cloud-Init and Windows user settings need to be configured in `Administration -> Provisioning` when using Cloud-Init or Guest Customizations and new credentials are not set on the Virtual Image.

4. Upload Image
    Images can be uploaded by File or URL:
      *File*
       Drag and Drop the image file, or select :guilabel:`Add File` to select the image file.
      *Url*
       Select the URL radio button, and enter URL of the Image.

    .. NOTE:: The Virtual Image configuration can be saved when using a URL and the upload will finish in the background. When selecting/drag and dropping a file, the image files must upload completely before saving the Virtual Image record or the Image will not be valid.

5. Save Changes.
