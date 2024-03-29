Setup
----------------
The first thing that needs to be done after installing the cli is pointing the cli to the appliance. The CLI can be pointed at many appliances and uses the RESTful OAUTH public developer apis to perform tasks. To set this up simply add a remote appliance with the conduit remote add command.

  .. code-block:: text

      conduit remote add myappliance https://applianceUrl
      conduit remote use myappliance
      conduit login

There are several commands available when dealing with configuration of remote appliances. To see what commands are available just type

  .. code-block:: text

      conduit remote


Getting Started
^^^^^^^^^^^^^^^^
To get started with the conduit CLI its helpful to use conduit shell. The shell provides a handy shell with history and some autocomplete features for learning to use it. All commands mentioned prefixed with conduit can be omitted since we are in shell mode.

To confirm that we are hooked into the appliance properly lets check our authentication information:

.. code-block:: text

    conduit> whoami
    Current User
    ==================

    ID: 1
    Account: Labs (Master Account)
    First Name: Demo
    Last Name: Environment
    Username: david
    Email: david@conduitdata.com
    Role: System Admin

    Remote Appliance
    ==================

    Name: demo
    Url: https://demo.conduitdata.com
    Build Version: 2.10.0

Fantastic! We are now ready to start our adventure in the Conduit CLI. If this command fails please be sure to verify the appliance url entered previously is correct, and also verify the provided credentials are correctly entered.

While the CLI is relatively young there are a ton of features provided with it that can make it very convenient for working with conduit. There are several base commands with subcommands within for example. Lets look at what happens when we simply type ``conduit`` on the command line:


.. code-block:: text

    Usage: conduit [command] [options]

    Commands:
    	remote
    	login
    	logout
    	whoami
    	groups
    	clouds
    	hosts
    	load-balancers
    	shell
    	tasks
    	workflows
    	deployments
    	instances
    	apps
    	app-templates
    	deploy
    	license
    	instance-types
    	security-groups
    	security-group-rules
    	accounts
    	users
    	roles
    	key-pairs
    	virtual-images
    	library
    	version

As you can see the cli is split into sections. Each of. these sections has subcommands available for performing certain actions. For example lets look at `conduit instances`

.. code-block:: text

    conduit> instances
    Usage: conduit instances [list,add,remove,stop,start,restart,backup,run-workflow,stop-service,start-service,restart-service,resize,upgrade,clone,envs,setenv,delenv] [name]

These commands typically make it easier to figure out what command subsets are available and the CLI documentation can provide helpful information in more depth on each command option.

Provisioning
^^^^^^^^^^^^^^^^^

To get started provisioning instances from the CLI a few prerequisite commands must be setup in the CLI. First we must decide what Group we want to provision into. We can first get a list of available groups to use by running conduit groups list

    .. code-block:: text

      conduit> groups list

      Conduit Groups
      ==================


      =  Automation - denver
      => Demo - Multi
      =  Conduit AWS - US-West
      =  Conduit Azure - US West
      =  Conduit Google - Auto
      =  conduit-approvals -
      =  NIck-Demo - Chicago
      =  San Mateo Hyper-V - San Mateo, CA
      =  San Mateo Nutanix - San Mateo, CA
      =  San Mateo Openstack - San Mateo, CA
      =  San Mateo Servers - San Mateo, CA
      =  San Mateo UCS - San Mateo, CA
      =  San Mateo Vmware - San Mateo, CA
      =  San Mateo Xen - San Mateo, CA
      =  snow-approvals -
      =  SoftLayer - Dallas-9

In the above example the currently active group is Demo as can be seen by the => symbol to the left of the group name. To switch groups simply run:

    .. code-block:: text

      conduit groups use "San Mateo Xen"

This now becomes the active group we would like to provision into. Another thing to know before provisioning is we do have to also specify the cloud we want to provision into . This does require the cloud be in the group that is currently active. To see a list of clouds in the relevant group simply run:

    .. code-block:: text

      conduit clouds list -g [groupName]

This will scope the clouds command to list only clouds in the group specified.

Conduit makes it very easy to get started provisioning via the CLI. It provides a list of instance-types that can be provisioned via the ``instance-types`` list command. Lets get started by provisioning an ubuntu virtual machine.

  .. code-block:: text

      conduit> instances add

      Usage: conduit instances add TYPE NAME
        -g, --group GROUP                Group
        -c, --cloud CLOUD                Cloud
        -O, --option OPTION              Option
        -N, --no-prompt                  Skip prompts. Use default values for all optional fields.
        -j, --json                       JSON Output
        -d, --dry-run                    Dry Run, print json without making the actual request.
        -r, --remote REMOTE              Remote Appliance
        -U, --url REMOTE                 API Url
        -u, --username USERNAME          Username
        -p, --password PASSWORD          Password
        -T, --token ACCESS_TOKEN         Access Token
        -C, --nocolor                    ANSI
        -V, --debug                      Print extra output for debugging.
        -h, --help                       Prints this help

  .. code-block:: text

      conduit> instances add ubuntu MyInstanceName -c "San Mateo Vmware"

      conduit> instances add ubuntu -c "San Mateo Vmware" dre-test
      Layout ['?' for options]: ?
      * Layout [-O layout=] - Select which configuration of the instance type to be provisioned.

      Options
      ===============
      * Docker Ubuntu Container [104]
      * VMware VM [105]
      * Existing Ubuntu [497]


      Layout ['?' for options]: VMware VM
      Plan ['?' for options]: ?
      * Plan [-O servicePlan=] - Choose the appropriately sized plan for this instance

      Options
      ===============
      * Memory: 512MB Storage: 10GB [10]
      * Memory: 1GB Storage: 10GB [11]
      * Memory: 2GB Storage: 20GB [12]
      * Memory: 4GB Storage: 40GB [13]
      * Memory: 8GB Storage: 80GB [14]
      * Memory: 16GB Storage: 160GB [15]
      * Memory: 24GB Storage: 240GB [16]
      * Memory: 32GB Storage: 320GB [17]


      Plan ['?' for options]: 10
      Root Volume Label [root]:
      Root Volume Size (GB) [10]:
      Root Datastore ['?' for options]: ?
      * Root Datastore [-O rootVolume.datastoreId=] - Choose a datastore.

      Options
      ===============
      * Auto - Cluster [autoCluster]
      * Auto - Datastore [auto]
      * cluster: labs-ds-cluster - 2.9TB Free [19]
      * store: ds-130-root - 178.5GB Free [5]
      * store: ds-130-vm - 699.0GB Free [6]
      * store: ds-131-root - 191.3GB Free [1]
      * store: ds-131-vm - 798.9GB Free [9]
      * store: ds-132-root - 191.2GB Free [4]
      * store: ds-132-vm - 799.4GB Free [10]
      * store: ds-177-root - 399.4GB Free [3]
      * store: labs-vm - 2.9TB Free [18]
      * store: VeeamBackup_WIN-0JNJSO32KI4 - 5.1GB Free [8]
      * store: VeeamBackup_WIN-QGARB6FA1GQ - 2.7GB Free [17]


      Root Datastore ['?' for options]: Auto - Cluster
      Add data volume? (yes/no): no
      Network ['?' for options]: VM Network
      Network Interface Type ['?' for options]: E1000
      IP Address: Using DHCP
      Add another network interface? (yes/no): no
      Public Key (optional) ['?' for options]:
      Resource Pool ['?' for options]: ?
      * Resource Pool [-O config.vmwareResourcePoolId=] -

      Options
      ===============
      * Resources [resgroup-56]
      * Resources / Brian [resgroup-2301]
      * Resources / Brian / Macbook [resgroup-2302]
      * Resources / David [resgroup-2158]
      * Resources / David / Macbook [resgroup-2160]

      Resource Pool ['?' for options]: resgroup-2160



As can be seen in the example above, the CLI nicely prompts the user for input on required options for provisioning this particular instance type within this particular cloud. It provides capabilities of adding multiple disks and multiple networks in this scenario. It is also posslbe to skip these prompts and provision everything via one command line syntax by using the ``-O optionName=value syntax:``

  .. code-block:: text

       conduit> instances add ubuntu MyInstanceName -c "San Mateo Vmware"  -O layout=105 -O servicePlan=10 -O rootVolume.datastoreId=autoCluster

This will cause conduit cli to skip prompting for input on these prompts. All inputs have an equivalent -O option that can be passed. To see what that option argument is simply enter ? on the input prompt to get specifics.


Now your VM should be provisioning and status can be checked by simply typing ``conduit instances list``.



List Arguments
^^^^^^^^^^^^^^^^^

Most of the list command types can be queried or paged via the cli. To do this simply look at the help information for the relevant list command

.. code-block:: text

    conduit> instances list -h
    Usage: conduit [options]
    -g, --group GROUP                Group Name
    -m, --max MAX                    Max Results
    -o, --offset OFFSET              Offset Results
    -s, --search PHRASE              Search Phrase
    -S, --sort ORDER                 Sort Order
    -D, --desc                       Reverse Sort Order
    -j, --json                       JSON Output
    -r, --remote REMOTE              Remote Appliance
    -U, --url REMOTE                 API Url
    -u, --username USERNAME          Username
    -p, --password PASSWORD          Password
    -T, --token ACCESS_TOKEN         Access Token
    -C, --nocolor                    ANSI
    -V, --debug                      Print extra output for debugging.
    -h, --help                       Prints this help
