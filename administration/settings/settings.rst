Appliance Settings
==================

The `Administration -> Settings` section sets global configuration parameters for the Appliance, Tenant Registration, Email, Proxy and sets which Cloud types are enabled.

Appliance Settings
------------------

Host Level Firewall Enabled
  Enables or Disables the host level firewall. This must be Enabled to use |conduit| Security Groups.
Appliance URL
  The default URL used for Agent install and Agent functionality. All Instances and Hosts must be able to resolve and reach this URL over 443 for successful agent install and communication.
.. NOTE:: Alternate Appliance URLs can be configured per Cloud in the `Edit Cloud -> Advanced Options` section.
Internal Appliance URL (PXE)
  For PXE-Boot your appliance needs to be routable directly with minimal NAT masquerading. This allows one to override the default appliance url endpoint for use by the PXE Server. If this is unset, the default appliance url will be used instead.
API Allowed Origins
  Specifies which origins are allowed to access the |conduit| API.

Tenant Management Settings
^^^^^^^^^^^^^^^^^^^^^^^^^^

Registration Enabled
  If enabled, the appliance login screen will have a "NEED AN ACCOUNT? SIGN UP HERE" link added, enabling new Tenant registration.
Default Tenant Role
  Sets the default Tenant Role applied to Tenants created from Tenant Registration.
Default User Role
  Sets the default User Role applied to the User created from a Tenant Registration.

.. Docker Privileged Mode::

Email Settings
^^^^^^^^^^^^^^

A default installation of Conduit uses a online service called postmarkapp. Conduit api requests to the postmarkapp service to send notification e-mails.

To add your own SMTP server you will need to go to the Administration and Settings of your Conduit appliance. You will then need to provide Conduit the following information, your mail server systems administrator should provide you with the below information and the preferred encryption method.

* From Address
* SMTP Server
* SMTP Port
* SSL Enabled
* TLS Encryption
* SMTP User
* SMTP Password

We recommend that you add your Conduit server to your SMTP white list as well as using user authentication as an additional security measure.

Once you have added your SMTP server information into Conduit scroll down the Administration and Settings page and press the blue save button which can be found under enabled clouds.


When you have saved your SMTP server settings in the Conduit appliance you will then need to restart the Conduit-ui. To restart the Conduit-ui connection to your Conduit server via ssh and run the below command.

``sudo conduit-ctl restart conduit-ui``

.. IMPORTANT:: If you do not restart the Conduit-ui the notifications will be sent by the original notification service postmarkapp. Please note it can take up to 3 minutes for the ui to become reachable again.
 has a built in SMTP server for email notifications and alerts. An alternate SMTP server can be specified below:

Add an alternate SMTP Server:

* From Address
* SMTP Server
* SMTP Port
* SSL Enabled
* TLS Encryption
* SMTP User
* SMTP Password

Proxy Settings
^^^^^^^^^^^^^^

The |conduit| Appliance can be configured to communicate through a Proxy server for Cloud API's and Agent communication back to the Appliance.

.. NOTE:: Additional Proxy configuration is available in the `Infrastructure -> Network -> Proxies` section. Added Proxies can be scoped to Clouds in the `Edit Cloud -> Advanced Options` section of the Cloud.

Add a Global Proxy server by entering the following:

* Proxy Host
* Proxy Port
* Proxy User
* Proxy Password
* Proxy Domain
* Proxy Workstation

Enabled Clouds
^^^^^^^^^^^^^^

Cloud types can be Enabled or Disabled in this section. When a Cloud type is disabled, it will be removed from the available options when adding new clouds in the `Infrastructure` section.

Available Cloud types:

* Conduit
* OpenStack
* Amazon
* Metacloud
* VMware vCenter
* VMware vCloud Air
* SoftLayer
* Google Cloud
* Azure (Public)
* Azure Stack (Private)
* DigitalOcean
* VirtualBox
* VMware Fusion
* VMWare ESXi
* Nutanix
* UCS
* XenServer
* Hyper-V
* MacStadium
* Oracle VM
* HP
* Supermicro
* Dell
* SCVMM
* UpCloud
* Kubernetes
* Cloud Foundry

.. include:: whitelabel.rst
.. include:: license.rst
.. include:: advanced.rst
