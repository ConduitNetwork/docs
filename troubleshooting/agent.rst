|conduit| Agent Install Troubleshooting
========================================

When provisioning an instance, there are some network and configuration requirements to successfully install the conduit agent.  Typically when a vm instance is still in the provisioning phase long after the vm is up, the instance is unable to reach |conduit| , or depending on agent install mode, |conduit| is unable to reach the instance.

The most common reason an agent install fails is the provisioned instance cannot reach the |conduit| Appliance via the appliance_url set in Admin -> Settings over 443. When an instance is provisioned from |conduit|, it must be able to reach the |conduit| appliance via the appliance_url or the agent will not be installed.

.. image:: /images/agent-7c9a2.png

In addition to the main appliance_url in Admin -> Settings, additional appliance_urls can be set per cloud in the Advanced options of the cloud configuration pane when creating or editing a cloud. When this field is populated, it will override the main appliance url for anything provisioned into that cloud.

.. TIP:: The |conduit| UI current log, located at /var/log/conduit/conduit-ui/current, is very helpful when troubleshooting agent installations.

Agent Install Modes
-------------------

There are 3 Agent install modes:

- ssh/winrm
- VMware Tools
- cloud-init

For All Agent Install modes
^^^^^^^^^^^^^^^^^^^^^^^^^^^

When an instance is provisioned and the agent does not install, verify the following for any agent install mode:

* The |conduit| appliance_url (Admin -> Settings) is both reachable and resolvable from the provisioned node.
* The appliance_url begins with to https://, not http://.

.. NOTE:: Be sure to use https:// even when using an ip address for the appliance.

* Inbound connectivity access to the |conduit| Appliance from provisioned VM's and container hosts on port 443 (needed for agent communication)

* Private (non-conduit provided) vm images/templates must have their credentials entered. These can be entered/edited in the Provisioning - Virtual Images section but clicking the Actions dropdown of an image and selecting Edit.

.. NOTE:: Administrator user is required for Windows agent install.

* The instance does not have an IP address assigned. For scenarios without a dhcp server, static IP information must be entered by selecting the Network Type: Static in the Advanced section during provisioning. IP Pools can also be created in the Infrastructure -> Networks -> IP Pools section and added to clouds network sections for IPAM.

* DNS is not configured and the node cannot resolve the appliance. If dns cannot be configure, the ip address of the |conduit| appliance can be used as the main or cloud appliance.

SSH/Winrm
^^^^^^^^^

Linux Agent
```````````

* Port 22 is open for Linux images, and ssh is enabled
* Credentials have been entered on the image if using custom or synced image. Credentials can be entered on images in the Provisioning -> Virtual Images section.

Windows Agent
`````````````

* Port 5985 must be open and winRM enabled for Windows images.
* Credentials have been entered on the image if using custom or synced image. Credentials can be entered on images in the Provisioning -> Virtual Images section.

.. NOTE:: Administrator user is required for Windows agent install.

VMware tools (vmtools) rpc mode
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* VMware tools is installed on the template(s)
* Credentials have been entered on the image if using custom or synced image. Credentials can be entered on images in the Provisioning -> Virtual Images section.

Cloud-Init agent install mode
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Cloud-Init is configured in Admin -> Provisioning section
* Provisioned image/blueprint has Cloud-Init (linux) or Cloudbase-Init (windows) installed

Manually Installing a |conduit| Agent
--------------------------------------

While it should not be necessary to manually install an agent if the requirements are met, it is possible to manually install an agent on an instance. This can also be handy when troubleshooting an agent install.

Linux
^^^^^

#. In |conduit| , go to the VM's host detail page in Infrastructure->Hosts->Virtual Machines you will see an API Key that is unique to that host.

#. As root user, run: (replacing ${} with the relevant information)

   .. code-block:: bash

    curl -k -s "${opts.applianceUrl}api/server-script/agentInstall?apiKey=${opts.apiKey}" | bash

#. This will pull the |conduit| Agent install script from the |conduit| appliance and run it.

#. Once the agent is installed, run ``conduit-node-ctl reconfigure`` to complete the manual process.

Windows

* The windows agent setup can be downloaded at ``https://[conduit-applaince-url]/msi/conduit-agent/ConduitAgentSetup.msi``

* On the |conduit| appliance package the windows agent is located at ``/var/opt/conduit/package-repos/msi/conduit-agent``

* WinRM, VMware Tools, or Cloudbase-Init can be used to install the agent from the |conduit| appliance

* The initial windows installer is ConduitAgentSetup.msi

* Once the Windows agent is downloaded and installed with |conduit| AgentSetup.msi the agent is located and runs from ``/Program Files x86/conduit/conduit Windows Agent``

* Logs can be viewed in the Event Viewer under Applications and Services Logs  -> |conduit| Windows Agent

#. Replace the values for ``$apiKey`` and ``$applianceUrl`` in the script below.

#. Execute this script on the Windows box in Powershell.

   .. code-block:: bash

      $apiKey = "add VM apiKey here"
      $applianceUrl = "https://your_appliance_url.com/"

      $client = New-Object System.Net.WebClient
      $client.DownloadFile($applianceUrl + "/msi/conduit-agent/ConduitAgentSetup.msi", "C:\Program Files (x86)\Common Files\ConduitAgentSetup.msi")
      Start-Sleep -Seconds 10
      cd ${env:commonprogramfiles(x86)}
      $serviceName = "Conduit Windows Agent"
      if(Get-Service $serviceName -ErrorAction SilentlyContinue) {
      Stop-Service -displayname $serviceName -ErrorAction SilentlyContinue
      Stop-Process -Force -processname Conduit* -ErrorAction SilentlyContinue
      Stop-Process -Force -processname Conduit* -ErrorAction SilentlyContinue
      Start-Sleep -s 5
      $serviceId = (get-wmiobject Win32_Product -Filter "Name = 'Conduit Windows Agent'" | Format-Wide -Property IdentifyingNumber | Out-String).Trim()
      cmd.exe /c "msiexec /x $serviceId /q"
      }
      [Console]::Out.Flush()
      [gc]::collect()
      try {
      Write-VolumeCache C
      }
      Catch {
      }
      $MSIArguments= @(
      "/i"
      "ConduitAgentSetup.msi"
      "/qn"
      "/norestart"
      "/l*v"
      "conduit_install.log"
      "apiKey=$apiKey"
      "host=$applianceUrl"
      "username=`".\LocalSystem`""
      "vmMode=`"true`""
      "logLevel=`"1`""
      )
      $installResults = Start-Process msiexec.exe -Verb runAs -Wait -ArgumentList $MSIArguments
      [Console]::Out.Flush()
      [gc]::collect()
      try {
      Write-VolumeCache C
      }
      Catch {
      }
      start-sleep -s 10
      $attempts = 0
      Do {
      try {
              Get-Service $serviceName -ea silentlycontinue -ErrorVariable err
              if([string]::isNullOrEmpty($err)) {
                      Break
              } else {
                      start-sleep -s 10
                      $attempts++
              }
      }
      Catch {
              start-sleep -s 10
              $attempts++
      }
      }
      While ($attempts -ne 6)
      Set-Service $serviceName -startuptype "automatic"
      $service = Get-WmiObject -Class Win32_Service -Filter "Name='$serviceName'"
      if ($service -And $service.State -ne "Running") {Restart-Service -displayname $serviceName}
      exit $installResults.ExitCode

#. If the agent doesn't install, logs can be found in the conduit_install.log file located at ``C:\Program Files (x86)\Common Files\``

Restarting the |conduit| Agent
--------------------------------

In some situations is may necessary to restart the conduit agent on the host to re-sync communication from the agent to the |conduit| appliance.

Linux
^^^^^

On the target host, run ``sudo conduit-node-ctl restart morphd`` and the |conduit| agent will restart. ``conduit-node-ctl status`` will also show the agent status.

Windows
^^^^^^^

The |conduit| Windows Agent service can be restarted in Administrative Tools -> Services.

.. TIP:: The |conduit| Remote Console is not dependent on agent communication and can be used to install or restart the |conduit| agent on an instance.

Uninstall |conduit| Agent
^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can use the following to uninstall the linux agent:

.. code-block:: bash

  sudo rm /etc/apt/sources.list.d/conduit.list
  sudo conduit-node-ctl kill
  sudo apt-get -y purge conduit-node
  sudo apt-get -y purge conduit-vm-node
  sudo systemctl stop conduit-node-runsvdir
  sudo rm -f /etc/systemd/system/conduit-node-runsvdir.service
  sudo systemctl daemon-reload
  sudo rm -rf /var/run/conduit-node
  sudo rm -rf /opt/conduit-node
  sudo rm -rf /etc/conduit/
  sudo rm -rf /var/log/conduit-node
  sudo pkill runsv
  sudo pkill runsvdir
  sudo pkill morphd
  sudo usermod -l conduit-old conduit-node

centOS/RHEL 7 Images
--------------------

For custom centOS 7 images we highly recommend setting up cloud-init and fixing the network device names. More information for custom centOS images can be found in the centOS 7 image guide.
