Docker
^^^^^^

So far this document has covered how to add the Openstack cloud integration and has enabled users the ability to provision virtual machine based instances via the `Add Instance` catalog in `Provisioning`. Another great feature provided by |conduit| out of the box is the ability to use Docker containers and even support multiple containers per Docker host. To do this a Docker Host must first be provisioned into Openstack (multiple are needed when dealing with horizontal scaling scenarios).

To provision a Docker Host simply navigate to the Cloud detail page or `Infrastructure->Hosts` section. From there click the `+ Container Host` button to add a Openstack Docker Host. This host will show up in the Hosts tab. |conduit| views a Docker host just like any other Hypervisor with the caveat being that it is used for running containerized images instead of virtualized ones. Once a Docker Host is successfully provisioned a green checkmark will appear to the right of the host marking it as available for use. In the event of a failure click into the relevant host that failed and an error explaining the failure will be displayed in red at the top.

Some common error scenarios include network connectivity. For a Docker Host to function properly, it must be able to resolve the |conduit| appliance url which can be configured in ``Admin -> Settings``. If it is unable to resolve and negotiate with the appliance than the agent installation will fail and provisioning instructions will not be able to be issued to the host.
