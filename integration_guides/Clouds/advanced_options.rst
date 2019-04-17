Advanced Options
^^^^^^^^^^^^^^^^

DOMAIN
  Specify a default domain for instances provisioned to this Cloud.
SCALE PRIORITY
  Specifies the priority with which an instance will scale into the cloud. A lower priority number means this cloud integration will take scale precedence over other cloud integrations in the group.
APPLIANCE URL
  Alternate Appliance url for scenarios when the default Appliance URL (configured in `admin -> settings`) is not reachable or resolvable for Instances provisioned in this cloud. The Appliance URL is used for Agent install and reporting.
TIME ZONE
  Configures the time zone on provisioned VM's if necessary.
DATACENTER ID
  Used for differentiating pricing among multiple datacenters. Leave blank unless prices are properly configured.
NETWORK MODE
  Unmanaged or Managed
SECURITY MODE
  Defines if Conduit will control local firewall of provisioned servers and hosts.

  .. IMPORTANT:: When local firewall management is enabled, Conduit will automatically set an IP table rule to allow incoming connections on tcp port 22 from the Conduit Appliance.

STORAGE MODE
  Single Disk, LVM or Clustered
GUIDANCE
  Enable Guidance recommendations on cloud resources.
DNS INTEGRATION
  Records for instances provisioned in this cloud will be added to selected DNS integration.
SERVICE REGISTRY
  Services for instances provisioned in this cloud will be added to selected Service Registry integration.
CONFIG MANAGEMENT
  Select a Chef, Salt, Ansible or Puppet integration to be used with this Cloud.
CMDB
  Select CMDB Integration to automatically update selected CMDB.
AGENT INSTALL MODE
  * SSH / WINRM: |conduit| will use SSH or WINRM for Agent install.
  * Cloud-Init (when available): |conduit| will utilize Cloud-Init or Cloudbase-Init for agent install when provisioning images with Cloud-Init/Cloudbase-Init installed. |conduit| will fall back on SSH or WINRM if cloud-init is not installed on the provisioned image.
API PROXY
  Required when a Proxy Server blocks communication between the |conduit| Appliance and the Cloud. Proxies can be added in the `Infrastructure -> Networks -> Proxies` tab.

Provisioning Options
^^^^^^^^^^^^^^^^^^^^

PROXY
  Required when a Proxy Server blocks communication between an Instance and the |conduit| Appliance. Proxies can be added in the `Infrastructure -> Networks -> Proxies` tab.
Bypass Proxy for Appliance URL
  Enable to bypass proxy settings (if added) for Instance Agent communication to the Appliance URL.
USER DATA (LINUX)
  Add cloud-init user data or scripts. Assumes bash syntax.
